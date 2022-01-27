# Sean Hoerl CS3700 Project 1 (Wordle Client)

## Language
I chose to implement the Wordle client in Python 3

## High Level Approach
My high level approach was to leverage regex and the word list we were given to filter out all words it could not possibly be. Since there are only 26 letters, the process of elimination allows us to find the right word pretty quickly.

## Guessing strategy
For my first guess, I choose a random word out of a list I have of vowel heavy words. I found this list online by researching the best first guesses for wordle. The article can be found [here](https://ftw.usatoday.com/lists/wordle-best-first-words-list). I did have to ensure that those words were all in the word list we were given. Since all of the possible words the first guess could be are vowel heavy, it is likely that we will get some 1 and 2's, and if not, than we can essentially ignore a lot of words in our word list as most words have vowels. I then build a regex to help me search for the word.

The regex would start out as '\w\w\w\w\w' as it could be any five letters. Once we make our first guess, if we have any 2's, we can replace the \w with that character, since we know the character has to exist there. Then we will look at our excluded list and see what is there, and replace every instance of \w with the appropriate regex for ignoring those characters. If we know a, b, and c are ignored, the regex expression for that \[^abc\]. So if we that 'z' is the third letter, and a, b, and c are not included, the regex would look like: "\[^abc\]\[^abc\]z\[^abc\]\[^abc\]".

## Challenges
Doing it this way, I had to account for the instance where you guess 'aabbb' and you get 1, 0, 0, 0, 0. If adding items to your included and excluded list just based off of the marks we get back, we would have 'a' in both the included and excluded list. In this case, since we would always see the 1 before the 0, we can just check if a letter is in the included list before adding it to the excluded list. This was not immediately apparent to me, and I only realized after a bit of testing, so this was the most challenging aspect of this project for me.

## Overview of Testing

I did all of my development on the Khoury Linux machine, so while developing I was able to run my client and make sure I was headed in the right direction. This also means I didn't have to account for any disconnect in packages installed in my local environment versus the Khoury linux environment. While building my guessing strategy, I would run the client to see how it performed. I ran each iteration of my strategy about ~10 times to make sure that works reliably. I also tried hard coding some errors in to make sure my client handled it properly (like guessing a 6 letter word). Once I was confident in my final strategy, I ran it about another 10 times to make sure it worked consistently. 

