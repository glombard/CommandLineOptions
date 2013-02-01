Below is the original text from the page on [SourceForge](http://clop.sourceforge.net/)...

**History**

I originally wrote this C# code for a small contest (and even won a consolation prize - 2 O'Reilly .NET books!).

Kohsuke K. actually found a use for this code in a GPL-licensed project of his and suggested I host it on SourceForge and encouraged me to decide on a license for it.

So that's how I got here.

**Command-Line Options Parsing using Reflection**

This is my entry for Chris Sells's .NET contest. Written in about 3 hours on Aug 30, 2002. Download it here.

It's not a flashy UI app, but only a class of a few hundred lines. However, it was a good learning experience for me and I believe it demonstrates good use of attributes and reflection.

Please don't just judge the program by its output. :-) It's about the code (specifically the CommandLineOptions class) and how it makes command-line option handling easier.

**Relection**

When I first heard about .NET's reflection and attributes, I thought it sounded cool in theory, but kind of useless in real life. Recently it hit me: reflection could be used to dynamically populate class fields from another source, such as an .ini file or command-line options. (Then it hit me, that's what XML serialization does too, but that's another story).

**Command-Line Options**

This class will be useful for me because I'm tired of writing command-line parsing code - those big switch statements - in every utility I write. From now on, I can just inherit my options class from CommandLineOptions and the parsing happens automatically!

It even generates the text for the "usage" section in the help text! I no longer have to manually sync up the fields in the options class, the parsing code and the help text. I just add a new field to the options class, and everything else "just works".

I define 3 types of command-line options:

* boolean options/flags (yes/no only), e.g. "/s" means recurse subdirectories
* value options (e.g. /loglevel=3)
* parameters (e.g. filenames not associated with an /option)

Please see CommandLineOptions.cs for the class, and MyApp.cs for a sample program that uses it.

**Example**

The options syntax is quite flexible. Here is a silly example of the type of options the class can recognize:

`myapp param1 --input=file.txt /pi 3.1416 -debug /loglevel:3 -secretoption=gert param2`

I.e. options can start with "/", "-" or "--" and the option name and its value can be separated with a space, ":" or "=".

Run the batch file test.cmd to test the program with the parameters listed above.

**What I've learned**

I've used some cool .NET techniques like:

* Learning about member fields with reflection
* Implementing custom attributes
* Dynamically changing run-time objects with field.SetValue
* Copying an object to another object of any other type with Convert.ChangeType - this is so cool! For example:
field.SetValue(this, Convert.ChangeType(someValue, field.FieldType))
* As a .NET novice, I'm quite proud of what I learned by making this work.

**Thanks for looking!**

Download clop.zip here.

**Update:**

I won the "Best technical insight" category in Chris's contest! Woohoo! :-)

Mail me! gert at codeblast dot com
