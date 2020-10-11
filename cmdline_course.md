---
layout: default
---

## Introduction
<img src="https://imgs.xkcd.com/comics/regular_expressions.png" alt="Photo" hspace="20" width="40%" align="right"/>

My name is Dean Rahman.
In fall of 2019 (period II), I studied the course titled "Command Line Tools for Linguists" at University of Helsinki.
It was taught by fantastic lecturers [Hande Celikkanat](https://www.linkedin.com/in/hande-celikkanat-08664423/) and [Miikka Silfverberg](https://www.linkedin.com/in/miikka-silfverberg-78146019).
Here is the [description of the course](https://courses.helsinki.fi/en/kik-lg219/129824412) by the course organizers.
Below is a summary of my experience with the course which I have a written as a part of the final project for the course.

Like all 5-credit single-period courses at U of Hel (which constitute the great majority of courses here), the Command Line course was 7 weeks of action-packed compressed learning fun, each week with a new module of concepts.
Hence the week by week structure of the summary.
(The redundant numbering with each of the week numbers is to highlight the use of a markdown list discussed after week 7 :)
Enjoy!            

## Experience (List)

1. Week 1

   Introduction to Command Line Environments

   We familiarized ourselves with Command Line Environments.
   Even though the majority of us had already gotten at least a peak at command line environments before (e.g. in the prerequisite course Introduction to Linguistics), this is the spot for me to express what each of us felt the first time we really comprehended what command lines were about: Holy Cow!
   We were culture shocked and delighted at the simultaneous self-service orientation and simplicity of  command lines after growing up with graphical user interfaces (GUIs) such as Windows, Macs and smartphones.
   The most cliché but effective explanation to a newbie is something along the lines of..imagine, instead of clicking and highlighting a file icon inside a folder and dragging it into another folder, you type in a highly specific sentence to the computer so it does the same thing.
   (This is of course because the folders thing is a just an analogy for our human brains for the construct that computers use in an array of memory..blah blah blah..).
   As you will see if you read the rest of the course summary, moving a file is the tip of the visible tip of the hidden iceberg, but for this week, it's enough to say the other simple things we learned which were mind blowing.

   Typing in the simple two character command

   `<ls>`

   (abbreviation for list), lists out all the visible files and folders in a folder (called "directory" in non-iconic speak).

   We can move out of a directory (folder) to go one folder up by typing

   `<cd ..>`.

   Using some pre-specified few characters or the folder path allows us to see the list of files in any directory or change to any directory, e.g.

   `<cd ~/KIK-LG219/final/`>.

   The command

   `<wget https//somewebsite.com/somefile.jpg>`

   lets us download a file from a website without opening up a GUI browser.
   Holy cow!
   One of the students remembers a reference to this in either the movie The Social Network or the show Silicon Valley, both about programmers.  

2. Week 2

   Navigating a UNIX System

   Stuff we were doing in Week 1 to files (copying, moving, deleting) we started doing to entire directories in Week 2!
   We also learned how to move files *between* computers.
   Holy guacamole!
   (The other computer, not the one we're physically typing on, is called a "remote server" through a remote connection command named

   `<scp>`).

   Besides all the wowing, this is the week that the necessary mindset became extra clear for me.
   It was in the context of zipping and unzipping files, but it applies to everything command line.
   Should we sit around memorizing

   `<tar -czvf name-of-archive.tar.gz /path/to/directory-or-file>`

   to zip files? Or

   `<tar -xf name-of-archive.tar.gz>`

   to unzip files? Of course not.
   Either we acquire these or any commands because we use these every day or we always have the internet for reference.
   While learning by Googling is becoming the modus operandi for most practitioners, especially in a domain as powerful as command line, it is essential to become aware of what is possible and expand the problem solving mindset and look up exact commands (syntax) by reference.    

3. Week 3

   Basic Corpus Processing

   The simple command
   `<wc text_file.txt>`:

   That's how we can find out the number of lines, words and characters in a file.
   What about getting rid of all capital letters in a file? We also learned how to do that and every other cool thing we thought was only ever possible in Microsoft Word.
   What about text processing in Microsoft Excel?
   Well, we can cut and paste columns in formatted text files right at the command line.

   It's one thing to be able to use these functions in an out-of-the-box software.
   It's another thing to be able to program them right from a (free) operating system.
   And forget about Word and Excel; they're nothing.
   We even learned the command line sequences that allowed us to do something we could only do using AntConc previously.
   That's right, we learned all the steps to compute descending word frequencies in a file as well!
   (I knew you were wondering why we would want to change all upper cases to lower :)

4. Week 4

   Advanced Corpus Processing

   Regex, `grep` and `sed`. In Week 4, we started getting into the hardcore stuff.
   Regular expressions are a way of expressing different but related words or character strings using a single expression.
   Using the command

   `grep`,

   we learned how to display on the screen and output to a file all of the sentences or lines with words that satisfy a regular expression.
   Using the command

   `sed`,

   we learned how to replace all instances of strings satisfying a regular expression with a different expression.

   As with Week 3, it became clear not only how softwares implement word processing features such as find-and-replace which we used as laypersons, but also how to execute a slew of processes which would now be available to us as aspiring language technologists.
   Each week's lessons were underscored with a quiz and this week's quiz was my favorite because every question felt as if I were solving a puzzle for fun.

5. Week 5

   Scripting and Configuration Files

   Just when I thought I was on top of the world, knowing how to do anything to a poor text file with the use of regular expressions, grep and sed, my mind was blown again.
   (Yes, my mind was in pieces by this point.)
   So what we could do anything to *a* file?
   What about mass production?
   What about doing that same sequence of things to many, many files?

   In Week 5, it was time to learn how to write scripts (short programs in shell syntax) which would process any file with our sequence to repeatably produce the same type of output.
   Because I had done data analysis in Python, many students looked to me to already know what was going on.
   But this was a very challeging week for me.
   Not only was applying sequences to text files somehow different, setting enviroment variables and doing so en masse via configuration files were both very new to me and I am still reviewing these concepts to fully grasp them.

   E.g. `export PATH=$PATH:$HOME/KIK-LG219/week5` is an easy example: it sets my week5 folder as `PATH`.

   Because of the challenging nature of this week, another student and I camped out one night in the hallway outside of Hande's office and got dirty looks from most of the Language Tech faculty and staff who were passing through.
   Our hope of course was to catch Hande and ambush her with questions which we did several times.
   Finally, partly to help us with look-over-our-shoulder-coaching, partly for her own fun (I hope), partly to make us sweat and, you know, to get rid of us, she had us solve a few problems real-time with her watching.
   That was a lot of fun and brought back the feeling from my Deloitte days.

6. Week 6

   Installing and Running Programs

   Week 6 was another challenging week. We had previously covered installation package managers which help ensure that prerequisite installations are in place before attempting the target installation.
   However, we learned in Week 6 that diligence is still required whenever installing a target program.
   Even after searching

   `apt-get`

   for how to install target programs or applications, we might encounter errors because every computer is different (somehow especially Windows computers).

   For python, it is possible to set up different environments with different versions of the same software when such is necessitated by different target softwares having conflicting version-dependencies on prerequisite software.
   It is also otherwise convenient to set up different environments for different types of work (or perhaps for different people to use the same computer?).

   We also learned about programming Makefiles to run

   `make`

   syntax to generate a set of target files based on a group of source files.
   We covered this concept in Week 5, but Makefiles allow us to refresh the target files when there is an update to one or more of the source files.
   For large processes this is handy in cutting down rebuild times (as in, nothing happens if no changes occurred and we can just use the stored target files from the prior build). 


7. Week 7

   Version control on GitHub  

   I had been familiar with the concept of version control from design for complex (multi-component) manufacturing, but it was good to see how the concept applies to software and multi-file management.
   We learned how to use git to execute version control and GitHub to store repositories for version control in a collaborative context.
   We learned how to add files to tracking (and remove them) and also how to commit changes and push these to the remote repositories for collaborative development.
   We exercised rolling back versions, doing segregated feature development and merging different branches (segregated sequences) of development.
   After the exercises, we moved directly on to actually applying the principles of version control to our final projects.

   `git add -A` adds all files changed so far to git tracking.

   `git commit -m"A comment string to distinguish this commit from prior commits"` commits all added files.

   `git push` pushes all commited files.

+ Final Project

   The final project consisted of building three webpages linking to one another.
   The first introduces myself and is created from a markdown file.
   The second is a similarly created webpage introducing this course.
   (You are in fact looking at this very page.)
   The third is a webpage created in Latex using Overleaf of my CV.
   What are markdown files?
   They are simple text files in a specific format (i.e. using very simple syntax) with links to websites, references to pictures and some cool text-based tricks such as tables and lists.
   Based on these simple files, Jeckyll can build static webpages.
   We hosted these on github.io having built them using the principles of version control learned during Week 7!

## A Summary of the Summary (Table)

**Week** | **Theme** | **Example/Scenario**
--- | --- | ---
1 | Command Line Enviroment | `<ls>` shows all files and subdirectories in a directory
2 | Navigating Unix Systems | `<mv -r subdirectory/ ~/someDirectory/>` moves subdirectory from the current directory to someDirectory 
3 | Corpus Processing | Replace all instances of a word with another word
4 | Corpus Processing continued | Descending word frequencies
5 | Scripting and Configuration Files | A script which computes descending word frequencies of any file provided as an argument
6 | Installing and Running Programs | A Makefile gets rid of headers/footers on a group of source files and makes frequency files from each, rerunning only when a source file changes
7 | Version Control | Team member 1 makes changes to files a and b on master branch; member 2 changes file c on experimental branch
Final | Markdown-based Static Websites | Two markdown files A.md and B.md respectively drive A.html and B.html that link to one another

## Concluding Thoughts
<img src="https://imgs.xkcd.com/comics/git_commit.png" alt="Photo" hspace="20" width="35%" align="right"/>
If you have read this far, I hope you have gotten the sense that I learned a lot in this course and had a lot of fun at the same time. 
I do feel able to operate in a linux environment and I know how to do some hardcore corpus processing because, you know, it's ***language*** technology.
And if I get stuck, I have a sense of where to go. This is a *tremendous* amount to get out of one 5-credit course.
Moreover, it really sunk in because of the multi-modal teaching (online demo videos by the lecturers themselves, on-point readings and in-person/over-Slack guidance through practical exercises).
It has been one of the best courses, from some of the best lecturers anywhere and I am grateful..and each week had a hilarious comic about the week's topic.
My favorite comic overall is at the top of the webpage and my favorite with a detailed inside joke is down here on the right.














