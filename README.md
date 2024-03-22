# Yara-Rule-for-Dark-Comet-Strain
**Introduction**

Since I want to learn reverse engineering and work in the field, a close friend of mine recommended I learn how to use YARA. So I cleared my weekend plans and got down to business. 

YARA is  known to be the pattern matching swiss army knife created by VirusTotal. In essence it is a rule enginer that supports a human readable language. It's main objective is detection, but its subobjectives can be used for identification, classification, hunting, or triaging. In a comparative sense, YARA is grep on steroids. 


**Rule Syntax**

<img width="564" alt="Screenshot 2024-03-21 at 15 44 42" src="https://github.com/CaptainIndy/Yara-Rule-for-Dark-Comet-Strain/assets/142528700/dc7a0c20-01bb-49b7-873f-9e9abbb26355">

In the following example above, there is an example rule showing rule syntax. Every rule starts with a rule name enclosed by a pair of curly brackets. Inside you have three different sections:
- meta: your description section where you would put the following:
    - your name as the author
    - the description of the rule
    - a hash so that others can validate your work
    - a date since it is important to know how old a YARA rule is.
- strings: the section  where the rule engine is going to search for the strings we specify and want to match upon.
  Types of strings
    - Ascii strings
    - Wide unicode strings specified by the "wide" variable
    - Regex (which start with a forward slash and end with a forward slash) contains regular expression pattern that that defines the string to match
    - hex or bytes: enclosed by curles braces and consist of hexadecimal values representing bytes of the string
- Condition: the section that specifies the Boolean expression that determines whether the rule should be considered a match. This section allows you to combine the strings from the "strings" section using logical operators to create a complex criteria. In this section we use various logical operators to create complex conditions.
  - Some common operators include:
      - and: Both operands must be true for the condition to be true.
      - or: At least one of the operands must be true for the condition to be true.
      - not: Negates the result of the operand.
      - all of: synonym for 'and'
      - any of: synonym for 'or'
      - for all: Quantifier that specifies that a condition must be true for all elements in a set.
   
Downloading Yara:
- Before going any further, make sure you download YARA for your system. Here is the link with the documentation and the instructions depending on what type of machine you are running. I recommend downloading YARA in your VM since that is where you will be working.
  https://yara.readthedocs.io/en/stable/gettingstarted.html
  
**Steps I took to Analyze my first piece of Malware**

Step 1: The first thing I did was go into a VM and downloaded Yara. You can use any Linux, Windows, or any system you choose. Just make sure you can download YARA onto your machine. 

Step 2: I went to Malware Bazaar and found an old strain of Malware. I wanted something that was a few years old and not as advanced and recent. I stumbled upon the Dark Comet malware family after asking ChatGPT what YARA rule I should write my first rule for. After searching for the Dark Comet family in the search box and finding a random strain a few years old, I downloaded it onto my VM. It downloads as a zip file that is password protected (the password being "infected"). 

<img width="375" alt="Screenshot 2024-03-21 at 16 13 50" src="https://github.com/CaptainIndy/Yara-Rule-for-Dark-Comet-Strain/assets/142528700/f0119e73-250b-41cc-9017-db9b0e516a17">

<img width="436" alt="Screenshot 2024-03-21 at 16 14 06" src="https://github.com/CaptainIndy/Yara-Rule-for-Dark-Comet-Strain/assets/142528700/e55e7739-4a64-48b0-8f98-01fdcf9701ce">

On Malware Bazaar, you can see the the strain has a specific SHA-256 hash that makes the malware easily identifiable for later reference. In the second photo you can see that there is more information like when was it first seen, the file type (executable), other specific hash identifiers, other similar malware samples, and the reporter Abuse_ch who is well known in the cybersecurity community for providing malware analyzing services. 

Step 3: Further Analysis on Virus Total and Anyrun
I decided to dive a bit deeper and look on Virus Total for more information. I dropped the malware onto the website and received more specific information. 

<img width="493" alt="Screenshot 2024-03-21 at 16 24 25" src="https://github.com/CaptainIndy/Yara-Rule-for-Dark-Comet-Strain/assets/142528700/877a8336-25ba-4207-95c5-a1ff9715801b">

Here we can see it is a Windows32 Portable Executable. Also we can see that our malware has been protected or obfuscated using the Themida Software protection tool. Themida is a commercial software protection and licensing tool used by developers to protect their application against reverse engineering, cracking, and unauthorized use. When a file is protected with Themida, it undergoes various transformations and obfuscations to make it more difficult for attackers to analyze or modify protected code. This is done through encryption, added anti-debugging and anti-reverse engineering techniques, and modifying the structure of the executable to thwart analysis. This obviously raises some flags in our case and will require the use or reverse engineering tools such as Ghidra, Binary Ninja, or Cuttr to dissect this malware. But for the scope and practice of simply creating a rule for my first time, I will keep it simple and save that for a later date. 

Furthermore, I decided to upload the malware to Anyrun, a malware analysis platform that allows users to execute and analyze malware samples in a controlled environment. It provides a sandboxed environment where malware can be run safely to observe its behavior such as file modifications, network activity, and process interactions. 
