# Leaky

Format: UHCTF{...}

My friend recently made a fan website that is terribly insecure. Unfortunately he is being stubborn and doesn't believe me. He told me he has hidden a file on his server and wants me to retrieve the content as proof.

Website: http://172.16.1.148 (Offline now)

JustUseYourHead: ✓


## Challenge Files

None


## Points

40

## Solution

1. The core of this challenge was how the index.php worked. If you looked at the URL of your browser when visiting any link provided on the index.php page the link turns into http://domain/index.php?page=TWICE.php this indicated that the index page fetched the other pages, and this can be abused! 

2. The ls.php page was provided to let you browse the folders of the server itself. If you visited this page you should have seen "Error no 'input' argument given." This indicated that ls.php is expecting another argument when called named 'input'. This could be used to craft links like http://domain/ls.php?input=/home/ubuntu/ to use the page as a file browser.

3. At this point you could have done 2 things, either you make a brute force script that starts at http://domain/ls.php?input=/ and checks every directory for a file that matches something like "flag/key/uhctf/...", or you JustUseYourHead and deduct that the home folder is the most common place to store data on linux systems and start looking there. Both ways would have worked but it's always useful to check the most common things first, don't make a challenge harder than it actually is. ;) If you looked at the home folder you should have seen a folder called "warm", this should have given you a clue that you were looking at the correct folder. 

4. If you found the "warm" folder you probably went a bit further and ended up with the flag which was at /home/ubuntu/warm/warmer/hot/flag.txt

5. Now that you know the location of the flag you just need a way to read its content out. This could be done with the index.php page. As said in step 1, the index.php fetches pages dynamically. These pages are not limited to the ones in the same folder or limited to php files, so it can be used as a file reader. This means that we can take the path of the flag and insert it as a "page": http://domain/index.php?page=/home/ubuntu/warm/warmer/hot/flag.txt and retrieve the flag.

The flag is: `UHCTF{THIS_SITE_IS_BAD_AND_I_SHOULD_FEEL_BAD}`

## Notes

The pattern "index.php?page=..." is actually fairly common yet it is a serious security risk. Depending on file permissions this pattern would allow you to read ssh keys, passwords, certificates, private keys, config files, log files (which can be abused to create an exploit), the content of the php scripts themselves (which often contain credentials), etc. This is actually the purpose of this challenge, to make you realize this pattern is in fact a security risk.

## Authors

* **Brent Berghmans**





