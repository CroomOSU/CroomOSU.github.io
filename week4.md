## Eric Croom’s CS 373 Weekly Write Ups

## Week 4 Write Up
This week we are exploring vulnerabilities and exploits.  This was presented from the perspective of the attacker and the process behind different types of exploits.  We were introduced to WinDBG for debugging files and gathering information.  There were several labs as well as a walkthrough of a stack exploit.

### WinDBG
This program can be attached to processes so that you can begin to debug that process.  The ability to disassemble the code and see the assembly code if very useful.  The main feature of debugging allows you to set break points and evaluate the environment and data after stopping the program.  Once stopped you can examine memory addresses as well step through the execution.  This program also displays register values and allows you to investigate the stack.

### Lab
#### Part 1
The first part of the lab was to introduce us to the functionality of WinDBG and learning some of the commands to evaluate the operations being performed.  A set of steps are provided to guide us through the process of examining an exploit.  Though for this lab we are aware of the exploit and what it’s doing.  In real world scenarios we will most likely not have the same amount of information.
Some of concepts covered were:
-	Setting break points: bp <address>
-	Continuing executions:  g
-	Loading modules to understand start and end of the address space:  lm m Symbol
-	PEB and TEB for getting process and thread information
-	.formats for converting data
-	Address displays information about the target provided
Below is a screen shot of a formatted register to get the return value of the function.

![Format Register](/images/register.PNG)

#### Part 2
The next section of the lab has us going over how to investigate the stack and track what the attack is doing.  By setting break points at functions we are able to step into the code and evaluate the registers for the data contained within.  
One of the main takeaways from this part of the lab was to understand how to trace the data within the program execution to find the where the malicious code is being placed.  And while this was important to understanding where the code is being placed within the stack the last section shows how javascript is used to generate the large buffer and determine the location needed to ensure the exploit is successful.  Following the instructions and the lectures I was able to launch the calculator app from the browser using the exploit.

![calc](/images/calc.png)

#### Part 3
The last part of the lab is to investigate a use after free vulnerability and an examination of the heap.  Here we examined where a freed block of code is called using HeapFree.  We then determined the size of this element.  In javascript we create a variable that is of the same size and fill an array with this value.  Now we have a repeating condition that allows us to exploit with shell code.  Using this method I was able to get the calc to execute by overwriting the freed space with a heap spray of the shell code.  

![ week4labP3](/images/week4labP3.png)

### Conclusion
This week I found a bit challenging as I felt that while the information was covered to do the labs it was not fully explained.  It seemed as if important details were mentioned in passing.  After having watched the lectures a few times I was able properly digest the information.  Once I was able to comprehend some of the lower level details and remember Assembly the labs became easier to accomplish.
After the concepts became clearer this week’s activities and presentation became much more enjoyable.  Learning about vulnerabilities and exploits will be very useful in helping to defend against such attacks.

### References
The information above was obtained from the following asset.

Antoniewicz, Brad - Defense Against The Dark Arts


<a href="../">Back to Home</a>
