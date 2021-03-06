Mturk Qualification Generator
==========================

This program is intended to simplify the process of uploading any qualification to MTurk. In the past we've had to use either Amazon's clunky system of self-generating bash files or a small hacky script written in haste to for a deadline. Both involved creating the XML for qualification content manually. Here we try to make life a little simpler by parsing a regular text file with some simple formatting easily readable and formattable by humans into XML and then uploading that to the Amazon server.


Prerequisites
----------------
**Warning:** some familiarity with the command line required!

Here's what you need before you in order for this script to work:

1. Latest version of [Python](https://www.python.org/download/). This will *not* work with 2.X, 3.X is required!
4. Your versions of the files found in the example folder. See the **Formatting** section for details.


Running
--------
Once all is set up, simply open your terminal, navigate to the folder where you saved the python script and run:

``python mturk_manager.py TESTDIR``

Where ``TESTDIR`` is the path to the folder containing your qualification question and properties files. This path can be relative (e.g. just the name of the folder if it's in the same folder as the script) or the full absolute path.



Formatting
------------------------
The purpose of this program is to make creating MTurk qualification tests easy for *humans*. Thus its contribution is in defining a simple and intuitive syntax for qualification definitions.

We need two files to set up a qualification test. One defines the qualification's properties, gives it a name and a short description. This file's name should end in ".properties". The properties file is extremely easy to set up, just looking at the one in the **example** folder should be enough to understand how to create it.
The second file you'll need defines the actual questions that your qualification poses to the workers. This file's name should end in ".questions". Its syntax has a couple of quirks that will be covered in detail below. At this point you might find it useful to have the example.question file open so that you can look at what's being described below.

The syntax may be easier to understand and learn if we first establish what MTurk needs to define a list of questions. Each question must contain some content (the question itself) and a list of answers to display. MTurk would also need to know whether several answers can be selected with checkboxes or just one with a radio button. Finally, we should specify how many points the question is worth. Each of the answers to the question must contain a) some text and b) some indication whether it's the correct answer.

With this in mind, let's look at one entry in example.questions. It starts with **Question XX**, where **XX** indicates what kind of question it is. The types currently supported by boto are listed below. With the exception of the last two, all the names are self-explanatory.

- radiobutton
- dropdown
- checkbox
- list
- combobox
- multichooser

The next line or lines are taken up by the content of the question. This is what the test taker will actually see. This content can be as many lines as you want it to and is followed by a list of possible answers to the question. Those will be covered below. The question entry ends with a **Score** field. The way file parsing is currently set up, you must end a question entry with a **Score** label even if the score is 0. Now let's look at how answer definitions are formatted.

Each answer has text delimited by **Answer** and **correct** labels. For readability it's a good idea to place these things on separate lines, but any whitespace between the labels and the text will do. The **correct** label is followed by a digit indicating whether the answer is correct or not. "1" here signals that the answer is correct, any other number means the opposite. Marking answers as correct is only useful if we want the test to be evaluated automatically by MTurk. Thus it is possible to indicate **no** correct answers to one question or *some* of them or *even all*.

That is it for syntax, I hope it made sense!
Once you have properties and question files that adhere to these guidelines ready, you can run the script.


Admin Stuff
-----------
This project is open source, you can fork and modify the code to your heart's content. See LICENSE for legal information. The program is minimally maintained by the Cognitive Neuroscience Lab at University of Maryland College Park.
