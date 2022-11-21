# RE-Jython

### Authors:
Samuel Gassman, Yanwei Ding, Yaznitha Sai Nalajala, Sobha Tejaswi Garapati, Bhavya Naga Sai Tadikonda

--------------------

### WARNING:
#### This repository contains code that cannot be guaranteed to be benign. 
#### No warranty of any form is associated with any aspect of this repository, and downloading any or all of the files from this repository implies you agree to release the authors from any and all liability regarding issues that occur whether intentional or unintentional from the use or posession of these programs. 
----------------------

### Description:
This project is an academic research project to partially automate the process of reverse engineering C and C++ binaries. It has three primary functions:
* To iterate over all user defined functions and inspect them for irregularities in their calling convention that may impact the generation of their parameter lists, and to propose suggestions for more reasonable parameter lists if the irregularities cause issues for Ghidra. ("Calling Convention Cleaning")
* To remove any code that unnecessarily increases the complexity of the binary (say for example, code inserted by the compiler like stack canaries)
* To detect where the main method is inside the executable ("Entry Point Detection").

When treating the Jython file as a script, it will first find the main method of the executable, iterate over all of the user defined functions in the code, and then demonstrate fixing their parameter lists (if issues are found) as well as removing unnecessary code. The ghidra project itself will remain unchanged, but this script will write out individual files for each of the functions it recommends changing.


### Contents:
This project contains:
* a script called "obfuscationcleaner.jy"
* a ghidra project containing the nested subdirectories:
	* CallingConventionCleaning
	* DeadCodeCleaning
	* EntryPointDetection
	
#### Note that the programs located in the EntryPointDetection directory are not created by the authors, and have been obtained through fair use from the reverse engineering practice website crackmes.one.
#### Credit is given to the authors of those programs:
* License Checker 0x03 (license_checker_3): NomanProdhan
* Gugus the first (gugus.out): bueb810
* My First Easy Crackme (Easy_CrackMe.exe): Lobeshnik
* Beginner Crack Me (Crack Me.exe): RedXen
* First-Crackme (First-Crackme.exe): sweety
* World Useless CrackMe (crackme): AzarAbdulla
* CrackMe-0x1 (CrackMe-0x1.exe): ixp-s

-----------------------------

### Usage Instructions:
1. Download [Ghidra here](ghidra-sre.org)
2. Clone this github repository (in a safe location where you accept any possible risk associated with having the programs on your system)
3. Open the "obfuscationcleaner.jy" file. At the top there is a line of code you can paste into the Jython Interpreter to execute the script. You will need to modify the path to the script based on the directory you cloned the repository to.
4. Start ghidra, open up this project (the reverseEngineeringScriptTests.gpr file)
5. Under "Window", 
    1. Click "Python Interpreter"
    2. While Ghidra calls it their "Python Interpeter", it is capable of accepting jython code, and directly integrates into Ghidra's Java libraries.
    3. Paste the "exec(...." line that you have modified to use your path instead of the default path.
    
    
    
### Additional Features:
* You can change the output location for where this script writes its files to by modifying the WINPATH or UNIXPATH global variables in the script
* You can also modify the level of strictness the script runs with with regards to how strictly or leniently it should consider a variable a parameter based on:
    * the number of push instructions in the assembly of the function
    * the number of variables with a "positive stack offset" (above RBP)
    * the number of variables that are never written to


