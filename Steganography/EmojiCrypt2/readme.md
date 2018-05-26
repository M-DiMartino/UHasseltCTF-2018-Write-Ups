# EmojiCrypt V2

Format: `UHCTF{...}`

We intercepted another top secret message! However, this one seems more complex than the last one. Can you help us extracting the data again?

The website they used to encode this message was: [http://172.16.1.149/v2](http://172.16.1.149/v2) (Offline)

## Challenge Files

[captured.txt](challenge/captured.txt)

## Points

60

## Solution

1. This challenge was an excercise in your ability to see data patterns and extract them. The website was given as a tool to help you achieve this goal. 

2. If you played around on the website you should have noticed that one character would now transform into 3 emojis. However this is not entirely correct. If we put in values outside of the ASCII range they transform into more emojis. For instance '🚤' would transform into 6 emojis. This should be an indication that the amount of emojis is variable. If it's variable it needs to be indicated somewhere, otherwise the decoder doesn't know how to decode it either. 

3. If you solved the previous challenge you should have known that the last hex digit was used in the previous challenge, this was again the case in this challenge and it would have been a good place to start with. If we use 'T' again from the last challenge it becomes: `1F562 1F695 1F004` and we see the ASCII value of 'T' agains in the last hex digits. Which leaves out the first emoji which ends with '2'. Let us now try something non-ASCII like '🚤' this becomes: `1F455 1F331 1F56F 1F6B6 1F4EA 1F694`. The unicode value of '🚤' is `1F6A4` and again, the last hex digits form this value. Which leaves out the first emoji again, this time it ends with '5'. 

4. Before we can write a decoder we need to figure out what this first emoji is used for. This required some experimenting with all sorts of unicode values. 

| Character | Unicode Value (Hex) | Emojis       | Emojis Hex                             |
| --------- | -------------------:| ------------:| -------------------------------------- |
| T         | 54                  | ♂➕⛔         |  2642  2795  26D4                      |
| Σ         | 3A3                 | ⏳🚳👊👓       |  23F3 1F6B3 1F44A 1F453                |
| Ⴆ         | 10A6                | 🌴💱🔰📪👦      | 1F334 1F4B1 1F530 1F4EA 1F466          |
| 😌         | 1F60C               | ✅🏑💯🌶⭐🏜    |  2705 1F3D1 1F4AF 1F336  2B50 1F3DC    |

5. There are a couple of ways you could use to figure out what the first emoji meant. 
   * We can see that a character with 3 emojis has a 2 in the first emoji 
   * A character with 4 emojis has a 3
   * A character with 5 has a 4
   * A character with 6 has a 5 
 
   Or you could use the hex values of the characters to figure it out:
   * A character which uses 2 hex values has a 2 in the first emoji.
   * A character which uses 3 hex values has 3 in the first emoji.
   * ... 

6. Now we know that the first emoji is used to tell the decoder how many emojis are used to encode the next character. Knowing all of this we can write a script. The script should work as follows: 
   1. Read in 1 emoji
   2. Extract the last hex digit and determine it's value, we'll call this `emojiAmount`
   3. Read in `emojiAmount` of emojis and concatenate their last hex digits, we'll call this `emojiValue`. 
   4. Convert `emojiValue` from a string to an unicode character and print out this character. 
   5. If we are not at the end our string, go back to step 1.

The flag is: `UHCTF{EMOJIS ARE FUN}`

## Notes

We have heard your feedback and recognize that this challenge was too difficult for the amount of points given. We will take this into consideration for the challenges of next year. 

## Hints

1. Each emoji seems to have some trailing bits of information... 
This hint was given to make you look at last couple of bits in the hopes that it would lead you to find the pattern in either hex or in binary. The category name "Steganography" could have been used to deduct this as well. In steganography it is common to hide data in the least significant bits. This hint was also given in EmojiCrypt V1.

2. There is more to the world than ASCII. 
This hint was given to make you try out non-ASCII values on the website. It was given to help you figure out that this version used a variable amount of emojis. And with this, figure out that the first emoji represented the amount of emojis used. 

3. We made a breakthrough! It seems like they use a variable amount of emojis per character!
Same as 2 but more bluntly.  

## Authors

* **Brent Berghmans**





