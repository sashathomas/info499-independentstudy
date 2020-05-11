# Week 7 - SmashTheStack (Level 1...) 

Sasha Thomas

May 11th 2020

## Introduction and Materials

This week I started to learn a little about C and buffer overflows using SmashTheStack.

I haven't done much work being this close to the binary, so many of these concepts are super new to me. I'm still wrapping my head around stacks, heaps, buffers, and a bunch of other things, so I was only able to get through the first level (which wasn't even related to exploits, just a PHP challenge). 

## Steps to Reproduce

1. The first challenge is accessed through the web. You are given a very simple webpage which allows you to upload a file:

   ![start](C:\Users\turtl\Documents\week6\images\start.png)

   I started out by looking at the source code and network tab for any hints. It was uninteresting apart from a hidden input which defines the max file size you can upload, which was 100kb. 

2. Just to see what would happen, I uploaded a picture of a cat to see if I could find it in `/uploads` as the page says. While I couldn't access the directory, I was able to access individual files:

   ![uploadedcatto](C:\Users\turtl\Documents\week6\images\uploadedcatto.PNG)

3. Since this was the first challenge, I assumed that it was likely there were no mitigations for the types of files I could upload. I also noticed that when I uploaded a file, I was taken to `/send_clearence.php`, so my next idea was to upload a PHP script and try to interact with the machine running the site. 

4. Crafting this PHP file took me the longest, especially because my knowledge of PHP is limited. My first attempt was solely to see if I could get the page to work with what I gave it:

   ```php
   <?php
       echo "Hello World!"
   ?>
   ```

   Uploading this did exactly what I wanted it to:

   ![helloworld](C:\Users\turtl\Documents\week6\images\helloworld.PNG)

5. With this information, it was mostly trial and error. Researching led me to the `shell_exec` command, and this super basic PHP let me pass in commands through the browser:

   ```php
   <?php
       $cmd = $_GET['cmd'];
       echo shell_exec($cmd);
   ?>
   ```

   ![phpscriptworks](C:\Users\turtl\Documents\week6\images\phpscriptworks.PNG)

6. The first page instructs you to poke around the user directories when you "gain clearance." The only user directory I had access to was level1's, which initially I thought was a dead end:

   ![userdirectory](C:\Users\turtl\Documents\week6\images\userdirectory.PNG)

   Horrible formatting which could be fixed by a couple lines of code aside, I decided to check `.bash_history`, mostly because the initial page told me to look around here. I found an interesting string that looked like it could represent a password:

   ![plaintext](C:\Users\turtl\Documents\week6\images\plaintext.PNG)

   And lucky enough, this string is the SSH password for level2, which I'm still working on...

## Conclusion

Having access to the actual buffer overflow challenge, I've been working through it on my own. I think I should be able to get it within this week. I'm sure the solution is relatively simple, but I'm more concerned with understanding the "why" at this point, so hopefully part II of this will come next week. 



