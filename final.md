## Eric Croom’s CS 373 Weekly Write Ups

## Final Write Up
The final write up for CS 373 consists of completing three challenges from Hack the Box.  Additionally, there was a challenge just to get an invite to sign up to the site.  The three challenges needed to add up to 50 points or more.  I decided to do some of the reversing challenges as I have some experience reverse engineering applications and thought these might be a good way introduce myself to Hack the Box as well as to investigating some of these types of issues.
Evidence of signing up is listed in the image below.  By the fact that I can access my profile / dashboard it is pretty clear that I was successful.  The image also shows the completed tasks.  One of the challenges has since been retired, but it was completed when it was active.

![final0](/images/final0.png)

### Signing Up
When I began, I was presented with a screen to enter an invite code.  Since I didn’t have one I had two options.  Google the answer or press F12.  I chose to investigate with web browser tools.  Note that the images below will show not my real attempt, but a second walkthrough as I did not record my original attempt.  
I noticed that there was a JavaScript file called inviteapi.min.js.  I decided to investigate and though it would have been easier if it wasn’t minified, I found what looked to be function names.  

![final1](/images/final1.png)

Attempting to call of one of the function names was successful.  This allowed me to return a data object that appeared to be encoded.  This also had an encode type of ROT13.  I had no idea what this was so google to the rescue.  This is a cypher that has decoders online.  Decoding it gave me the following text: “In order to generate the invite code, make a POST request to /api/invite/generate”.

![final2](/images/final2.png)

I had to get a rest client for chrome and send out this post request.

![final3](/images/final3.png)

To be honest I got a bit stuck here.  I tried this code and failed since it was obviously encoded.  After a long time of googling and trial and error I was able to determine that this was base 64 and decoded it using an online converter.
This “QlVEU1ItWExLQVYtRkRPQUgtSUpUUkItS01DS0c=” became “BUDSR-XLKAV-FDOAH-IJTRB-KMCKG”.  Honestly, this was a lot more work than I thought it was going to be and I got stuck in several places.  I am glad I started early on these challenges.


### Snake [10 points]
The first challenge I took on was the Snake Reversing Challenge.  Initially this looked fairly easy as it was just a python script:

![final4](/images/final4.png)

Getting the user name was pretty easy.  On line 42 there is a comparison with the user input to a variable called slither.  Just printing out the variable slither by altering the .py file allowed me to get the username, anaconda.  

![final5](/images/final5.png)

Finding the password was a bit more difficult.  At first, I thought this would be easy since there is a loop to check password characters against a list of chars.  Based on the comparison it appeared that str(chr(char)) in a for loop of char in chars would return me the password.  So, my first inclination was to print all of these out and use it as the password.  This worked for the script but failed in the hack the box site.  
Further investigation found that the loop is breaking after the first character is validated.  So, I started working my way up the script to determine where chars I being populated.  Chars is being appended in two places.  The first is using the lock and key variables and the second is using the chains variable.  Since the final product uses the chains I moved up above this entry and printed the characters in char prior to chains being added.  This gave me the correct password:  udvvrjwa$$

![final6](/images/final6.png)

There was a lot of misdirection and useless variable in this challenge.  It was rather confusing at first and I guess that is what some malware designers want.  The more confusing the code the less likely there are methods deployed to prevent it from functioning.
### Tear or Dear [20 points]
The next challenge “Tear or Dear” is probably my favorite of the three.  I have worked with windows applications and Visual Studio for several years, so I felt right at home working this issue.  
The first step I do when examining any file, and in this case an exe is to open it in notepad++ to see what I can find without running it.  As it was a complied binary there wasn’t a whole lot of information to work with until the very end of the file.

![final7](/images/final7.png)

Here we can see the manifest and assembly information that is generally associated with files created by Visual Studio and use the Microsoft JIT complier.  This gave me the right scent on how to proceed.  I downloaded dotPeek from Jetbrains to decompile the .NET code. 

![final8](/images/final8.png)

This is useful in discovering information, however, I needed to debug the application to determine the locations and values needed to pass the challenge.  Luckily this tool has the ability to export it to a visual studio project.  
Once I had a project available to debug in visual studio, I could really begin to work this issue.  We are presented with a username and password windows form.  I set a break point inside the button click event.  They weren’t very imaginative and just when with the default event handler button1_Click.  Here there are a few stets of data conversion and then a comparison for username.  One thing I found that really narrows down you time searching things is to make sure the input you are testing (username and password) is different.  This help you figure out what’s going on.  
Using “test” as the username and “pass” as the password I began working through the code.  Setting a breakpoint, I was able to deduce that the username is being changed to the password and then there is another check before a success criteria is reached.  Realistically, this is not the username I entered but just a variable called username.  The actual username comes from a textbox called textbox_user.  Evaluating the variable “this.o” which is compared to the username (or really the password now it is being changed somewhere else in code) we find that the password is in plain text as “roiw!@#”
Now I needed to investigate what the second half of the criteria does.  It is a series of embedded functions:  check1 -> check2 -> check3 -> check4 -> check.  This last function is the one that does the actual work.  And by actual work I mean doesn’t do anything but compare the username textbox text to a predefined variable.  The value of this variable “this.aa” is “piph”.  

![final9](/images/final9.png)

![final10](/images/final10.png)

![final11](/images/final11.png)

### Find the Easy Pass [20 points]
This was another reversing challenge that I was hoping to be disassembled by dotPeek.  Opening the application in dotPeek reveals that it isn’t compatible.  So, I open the file with notepad++.  Scanning through didn’t reveal much until I scrolled back up to the top.  The first three characters are MZP.  This rung some bells from a lecture, and I started to google this being in a header of a file.  Stack overflow revealed that this is most likely a Delphi file and the P is for pascal.  This is what I was remembering from class.  

![final12](/images/final12.png)

Now I had to do some more research on how to debug files like this.  From the lectures I remembered that IDA Pro is the industry standard tool.  I looked up some free alternatives that support debugging and came across OllyDbg.  This is a disassembler / debugger that should work for most executables.  
I loaded the tool with the easypass.exe and set about analyzing.  The first thing I found was that there is an ability to extract strings.  Doing this as the module is running landed me on a page that happened to have the following text on screen:

![final13](/images/final13.png)

Double clicking on the “Good Job” takes me to the part in the module that will be executing that code.  The line above this is a jump instruction.  So logically the call before it might have something to do this with this comparison.  I placed a break point here ran the code and entered a password to test:

![final14](/images/final14.png)

Stepping through the code I can see a CMP or comparison call to two registers, EAX, EDX.  Here EAX contains my password “test”.  This is being compared against the value in EDX “fortran!”.  This leads me to believe that this will be the correct password.
Starting over I ran the exe through the OllyDbg tool using the password “fortran!”.  This led me to the correct response.

![final15](/images/final15.png)

### Summary
This exercise was much more challenging than I originally anticipated.  I had to research and google a lot of information just to get me started on some of these challenges.  I did not add each and every search I performed throughout the descriptions above as it would exhausting and pretty tedious to read.  An example would be that I probably don’t need to illustrate how I had to google a walkthrough of using OllyDbg to debug an application.  As I’m used to visual studio this one was a bit different to use.  
While difficult it was a very interesting experience and is representative of some of the topics presented in this class.  It would take way too long to find challenges that would span the entirety of the knowledge presented in this class.  I decided to stick with the topic I had some knowledge of and apply the concepts of the class to complete the challenges.


<a href="../">Back to Home</a>
