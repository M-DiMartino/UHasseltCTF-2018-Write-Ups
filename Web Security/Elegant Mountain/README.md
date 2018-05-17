# Elegant Mountain

Format: UHCTF{...}

The government agency has been looking for this mysterious person for years! They thought he was dead. But very recently, he opened up a scamming website to sell useless overpriced products.

Can you try to find the admin panel and his credentials to shutdown this stupid website?

    The website: http://185.206.146.26:1250

Note: port scanning and brute-force attacks are not required and should not be used!


## Challenge Files

None


## Points

60

## Solution

This challenge teaches you that security through obscurity is generally not an effective defense. And that guessing passwords is often still practical.

1. The website has a 'hidden' admin webpage on the location http://185.206.146.26:1250/admin.php. This page could have been found using tools such as 'dirb' or you could have guessed it yourself manually. The fact that there is an administrator page is suggested by the Facebook page of 'Elegant Mountain' (accessible through the Contact page of the website).

2. An email and password is requested to login to the admin panel. You can find the email (testadmin@elegantmountain.com) in the HTML plaintext of the admin.php page. However, the password is 'testadmin'. Unfortunately, it is still common practice for beta/alpha webpages to have very easy passwords, usually the same as the username or email. The image on the Elegant Mountain Facebook page also showed that the text 'testadmin' was selected and the password shown also suggested the actual length.

3. When logged in with the correct email and password, an beta admin panel will be shown. Several pages show dummy data. The only page that we can exploit is 'settings.php' (Can be accessed by opening the menu in the top right corner). This page allows you to reset the password. However, when we try to click on the 'Reset password' button, a message will be shown saying that we cannot reset passwords of test accounts.

4. To exploit this 'password' functionality, we simply have to change the POST parameter 'email_id' to the number '2' (Use Burp or any HTTP proxy for this. Even Firefox Developer tools should work). This is the only number that is linked to a valid email address, this could have been easily bruteforce-able. This vulnerability is called an 'Indirect Object Reference' (OWASP). A similar vulnerability has been found on Facebook 'http://www.anandpraka.sh/2016/03/how-i-could-have-hacked-your-facebook.html' (pardon us for the bad grammar in the provided link).

5. When we have sent a POST request with email_id=2, we get a message saying that the password has been succesfully reset. Next to that message, we see the text 'DEBUG: a175ca42134b1c45984455f4143c6d55' (the admin page is still in beta, that's why we see the debug message ;) ). This is a MD5 hash. Databases online exist that contain this hash and the corresponding plaintext value. For instance: 'https://hashkiller.co.uk/md5-decrypter.aspx' will show us that this hash corresponds to 'iamtom'.

6. Now that we have the password, we are left to find the corresponding email address. On the main website of Elegant Mountain, we can see on several places that a person with the name 'Tom Keen' is the owner/creator of the website. Since we already know the domain '@elegantmountain.com', we can simply put 'tomkeen' in front of it (so we get 'tomkeen@elegantmountain.com'). This step might look far fetched, but it is still actively being done in real-life phishing scenarios.

7. When logging in with email 'tomkeen@elegantmountain.com' and password 'iamtom', the flag will given.

The flag is: `UHCTF{now_i_can_do_bug_bounties}`


## Authors

* **Mariano Di Martino**





