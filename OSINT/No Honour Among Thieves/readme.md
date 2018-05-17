# No Honour Among Thieves

Format: UHCTF{...}

We found out that one of our competitors has been stealing source code from a couple of our projects. What better way to return the favour than by stealing one of his secrets? Maybe if we could find a way to login using his credentials...
The website of our competitor is: http://185.206.146.26:3377/index.html

Note: port scanning and brute-force attacks are not required and should not be used!

JustUseYourHead™: ✅


## Points

50

## Solution

1. Malict Solutions is a company website created by 'Roberto Fortunitas' (see Contact page of website). The intranet page 'login.php' is directly accessible through the Malict Solutions website. We can extract the email address from Roberto using the Contact page of the main website.

2. The login page also contains a 'reset password' feature. This feature allows you to reset the password when some security questions are answered. The security questions are the following:

- Email  (we have already found this).
- My favorite artist.
- My date of birth.
- My favorite city.

2. Now that we have the email address, we still have to find the answer on the last 3 security questions in order to reset the password. If we hover over the picture in the Contact page of the main website, we will see that the Facebook and Soundcloud page of Roberto is showing up. Both social media pages contain the necessary information to infer the answers to the security questions.

3. First, we start with the Soundcloud page. There is only one uploaded soundtrack and no likes or reposts. If we click on the title of the soundtrack, we get the page 'https://soundcloud.com/robertofortunitas/ioh'. Now, there are 2 possible options: You could either Soundhoud/Shazam the music track to identify the artist (which has proven to be difficult in the noisy environment, sorry for that!) or you can read the description of the track that says 'Best artist of all time together with Fuzzylogixx! Such a good track!'. The description shows us that this track is composed together with another artist called 'Fuzzylogixx'. If we look up 'Fuzzylogixx' on Google, we find that there are only 2 artists that have composed a track together with 'Fuzzylogixx'. This is 'Garnomala' and 'Mariano Di Martino'. We can listen to both songs on platforms such as Beatport or Spotify to identify which track is the correct one. As a result, we will find out that the track is called 'Intentions Of Harmony' and therefore the favorite artist of Roberto Fortunitas is 'Mariano Di Martino'.

4. So far, we have found the email and favorite artist. To get the date of birth and favorite city, we have to use the Facebook page of Roberto Fortunitas. Let's start with the 'favorite city'. Roberto has visited several cities, all of which are named directly in either a Facebook post or as a description on a photo. There is one exception: the pictures from April 19th contain the description 'Most amazing trip so far! What a city!'. Note the 'Most amazing' -> favorite city. All pictures from that post are from 'Los Angeles'. We can infer this in many ways:
- Picture 1: Not much to infer from, unless you recognize it. This is the Santa Monica Pier located in Santa Monica, Los Angeles.
- Picture 2: Set from the Big Bang Theory, recorded in Burbank, Los Angeles.
- Picture 3: The chairs in front of the coffee place are from the set of the movie 'La La Land' recorded in Burbank, Los Angeles.
- Picture 4: Santa Monica Pier again. If you watch closely, you will see the text '#pacificpark' which you can then Google.
- Picture 5,6,7,8: Random pictures from Los Angeles, not much to infer from.
- Picture 9: Looking up 'City Loft' and 'Bubba Gump' will show you that this picture is from the Universal City Walk located in Hollywood, Los Angeles.

5. Next, we have to find the date of birth. The year in which he is born (1962) is publicly shown in the About section ('Over' in Dutch).
Then, we can infer the month and day from a Facebook picture with the description 'A gift from my girlfriend! On my birthday! So sweet!'. The date of this picture is set to September 16th.

6. Finally, we have all the answers. If we correctly provide those answers on the login page, we will get the password of Roberto (PasWorD12345).

7. When we login with the provided email address and password, we will see the internal inbox of Roberto. A lot of messages are shown, but only part of it is visible. If we go to the Sent email page, we see that Roberto has sent an email to himself with the text '
Own log Login: roberto.fortunitas password: U H C TF{please_hire_me_nsa_supercalifragilisti ...'. The text 'supercalifragilisti' is part of the larger word 'supercalifragilisticexpialidocious' from a Mary Poppins song. So the final flag is `UHCTF{please_hire_me_nsa_supercalifragilisticexpialidocious}`.



## Authors

* **Mariano Di Martino** and **Robin Quetin**: Challenge concept
* **Mariano Di Martino**: Write-up.



