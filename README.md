# CSCI 306 Grading Tool

A tool for the ages.  To view more detail about the project and schedule, view the files inside the "public" folder.

### Purpose 

This tool is meant to aid in grading the CSCI 306 Software Engineering class taught at the Colorado School of Mines.  Hence this tool has a very focused and limited scope for that class and that class only.  Further extensions to the tool for other classes may be considered in the future.

This tool will help in automating a lot of the grading for a class.  It allows the grader to avoid navigating the slower Eclipse and Canvas interfaces, and instead give just the information the grader cares about, cleanly and efficiently.

### Requirements

To run the scripts in this tool, you will need a system with a Bash shell.  Furthermore, you need to make sure you have the following tools: wget, sed, jq, java, javac, subl.  To install them, run the following commands: 

    sudo apt-get install jq
    sudo apt-get install java
    sudo apt-get install javac
	sudo add-apt-repository ppa:webupd8team/sublime-text-3
	sudo apt-get update
	sudo apt-get install sublime-text-installer

I'm not sure if these are the correct commands, I'm just making a guess.  As you can see, there are a lot of dependencies.  This tool also uses `sed` and `wget`, but I think most Linux distributions already have those tools by default. 

Additionally, the grader must grant OAuth 2.0 access or whatever to this tool.  Currently, this hasn't been implemented.  I have just inserted the access token directly into the script.  Technically, creating your own token for your account and pasting it into the script is against Canvas' user policies, so don't do that.

### Usage

To use this tool, simply run the `jgrader.sh` script inside the directory of the tool.  The tool will then ask for the section and assignment that the grader wants to grade.

From there, the tool will go through each ungraded submission, compile it, then for each of these open a new window and display results:

- the output of the program (if the assignment has a Swing GUI, it will display that; otherwise, console output will just be printed in a new terminal window)
- the results of junit tests, if any
- a text editor (default sublime) will display the source code for the grader to review
- the original window will display the user's submission comment

From there, a bunch of prompts appear sequentially in the original window.  First, there is a prompt for inputting a comment, and after that for inputting a grade.  After that is a prompt for inputting the partner's name (which should be in the comment).  The tool will make sure this person exists before accepting the input.  His/her grade will automatically be updated as well.

If you want to skip grading the submission, leave the grade and comment prompts blank and just press enter.  Then, jgrader will list all of the submissions (as user ids) that weren't graded.  The grader can then go to those directories inside the `submissions` folder and grade them manually.

After all this, the tool will close all the opened windows, and move on to the next ungraded submission.

Note: running jgrader will delete whatever's currently in the submissions folder, so make sure you don't want that stuff anymore.

### Upgrading

This tool uses set versions for JUnit and Hamcrest (currently, JUnit 4.12 and Hamcrest 1.3).  These are jar files found in the <code>jars/</code> directory.  To update them, or use a different version, go to [this website](https://github.com/junit-team/junit4/wiki/Download-and-Install), download the jars you want to use, and put them in the <code>jars/</code> directory.

### Future considerations

This tool really works best when you want to hammer out the bulk of your grading.  If a student has a personal complaint about a grade or some other special case like that, you should probably just go to Canvas and resolve the issue through that.  In the future, this tool might be expanded to be useful for special cases like this.  For now, no.

This tool also definitely needs to support adding multiple partners.  Currently, only one additional partner may be written in per submission.

Another possible consideration is expanding the tool to work beyond just Java programs.  This should be a relatively simple upgrade to make if wanted.

I also think it would be pretty cool if the tool could make an educated guess for the partner based on the submission comment.

Also, if the prompy page found on the CSCI 306 web page could somehow be integrated (maybe even just opening on firefox), that would be pretty useful too.

Jgrader could possibly be extended to be useful for classes beyond the computer science department; however, this is unlikely, considering Canvas has a "SpeedGrader" tool that looks way better than mine.  Jgrader is really only helpful for submissions that need to be compiled or whatever outside of the Canvas website and can't just be viewed with a document previewer or something.

Read the documents inside the `public` folder to try and get a better idea of how this project is structure if you want to make changes.  I don't claim I'm a master of making script tools (quite the opposite), so if something makes no sense and those admittedly poorly-written documents are don't clarify anything, please email me at psobolew@mines.edu with questions as well.