# Week 4 - HackerOne CTF 

Sasha Thomas

April 27th 2020

## Introduction and Materials

This week, I did some of the challenges through the HackerOne CTF, which ended up giving me an invitation to a private bug bounty program!

As with the other labs, I just used Chrome and Firefox. The mock website for this challenge is called "Postbook," and let's users make an account, update some settings, and post things to a global timeline. It's similar to JuiceShop in a way, but much, much simpler. 

## Steps to Reproduce (Flag0)

1. It's mentioned that users of the website might have insecure passwords. When I made my own account, I noticed "user" posted to the timeline. I tried logging into his account with the password "password," which worked and gave me my first flag.

## Steps to Reproduce (Flag1)

1. Each post that is created has an ID associated with it. You can change the ID multiple ways;
   1. By altering the ID sent in the POST request created when submitting a new post, or...
   2. An input box, which is hidden using the `visibility` CSS attribute, but clearly visible in the source code.
2. Altering this number gave me the second flag.

## Steps to Reproduce (Flag2)

1. The third flag was "hidden" in one of the headers.

## Steps to Reproduce (Flag3)

1. The 4th flag is recieved by editing a different users post. Each post is associated with a unique ID, which isn't hidden. By sending a POST request with an exisiting post ID, the previous post is rewritten with whatever you write. 

## Steps to Reproduce (Flag4)

1. Flag4 and Flag5 took me the longest. Flag4 asks you to sign into a user with ID 1, or the admin. I tried SQLi, but it didn't work and I figured it was beyond the scope of this. I eventually looked at the cookie for logging in, which seemed a little off. For example, one of the fake accounts I made had the cookie set to `id=eccbc87e4b5ce2fe28308fd9f2a7baf3`. I found a website which guessed what type of hash a string was, and inputting this resulted in "likely MD5 or MD4." Throwing the same string into an MD5 "decoder" resulted in... "3". So, I assumed it was just taking the user ID and hashing it for the cookie. Knowing this, I hashed "1" and replaced my cookie with the result, which logged me in and gave me the flag.

## Steps to Reproduce (Flag5)

1. The last flag asked you to delete a post which had been posted to the timeline (by another user). Looking at this behavior when I deleted my own post, I noticed it was hitting a page called `delete.php` with a variable ID set to a random string. Random, until I did the same thing I did for Flag4, and found that, yet again, the ID of the post was being hashed using MD5. Following the same steps as I did with Flag4, except this time replacing the post ID, I was successfully able to delete another user's post and retrieve the last flag.

## Results and Discussion

This was a nice break, especially from last week, where much of what I did was completely new to me. It's nice to know that I'm not at the very bottom; this challenge was labeled "easy," and even though I didn't breeze through it, each flag took me about 5-10 minutes. It felt Juice Shop-esque, but a little easier.

## Conclusion

In conclusion, I think this gave me confidence that I have in fact learned. There is so much I don't know, and so much I'd like to learn, it can be overwhelming at times. In the fall, these flags would have taken me much longer to find, but now I can follow the basic clues and use the right tools. As far as the security principles violated for this, it's pretty much everything, so I don't have too much to say. Whereas Juice Shop is set up to be a little more realistic, this is set up more like a CTF (because it is one). 
