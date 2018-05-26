# EmojiCrypt

Format: `UHCTF{...}`

We intercepted a top secret message but when we reviewed the data we just found some random emojis! We wonder if there's some data hiding in these emojis. 

The website they used to encode this message was: [http://172.16.1.149](http://172.16.1.149) (Offline)

*JustUseYourHead™: ✅*

## Challenge Files

[captured.txt](challenge/captured.txt)

## Points

50

## Solution

1. This challenge was an excercise in your ability to see data patterns and extract them. The website was given as a tool to help you achieve this goal. 

2. If you played around on the website you should have noticed that one character would transform into 2 emojis and that these emojis were chosen randomly. This should give you a hint that the pattern is hidden on a lower level. For instance, if I convert `Test` I get:
   * 🚕✴🕶😕👧🕣🎷🌔
   * 🌥↔📶⬅🏧🕓🎧🏔 

3. Now there are multiple representations this could have worked with but in this write-up we're going to use hexadecimal. If we look at these emoji strings in hex we get this:
   * `1F695 2734 1F576 1F615 1F467 1F563 1F3B7 1F314`
   * `1F325 2194 1F4F6  2B05 1F3E7 1F553 1F3A7 1F3D4`

4. From this hex representation we can conclude that the last hex digit of each emoji always stays the same. If we look at the hex value of 'T' we get 54. If we look at the last hex-digits of the emojis, we see that the first two emojis end in 5 and 4. If we try this for next value "e" which is 65 in hex, we can see that this pattern holds up. 

5. Now that we figured out how the data is represented we can either write a script to decode the captured message or we can decode it manually. 

The flag is: `UHCTF{I WANTED A CHALLENGE WITH EMOJIS}`

## Hints

1. Each emoji seems to have some trailing bits of information... 
This hint was given to make you look at last couple of bits in the hopes that it would lead you to find the pattern in either hex or in binary. The category name "Steganography" could have been used to deduct this as well. In steganography it is common to hide data in the least significant bits. 

## Authors

* **Brent Berghmans**





