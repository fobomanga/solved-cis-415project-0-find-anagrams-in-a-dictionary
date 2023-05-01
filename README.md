Download Link: https://assignmentchef.com/product/solved-cis-415project-0-find-anagrams-in-a-dictionary
<br>
A dictionary file contains a list of words with out duplicates. There are however capitalized and non-capitalized words, such as “A” and “a”. Anagrams are words that can be spelled using the same set of letters, such as “restful” and “fluster”. An anagram family is a sorted set of letters such as “eflrsu” for the previous anagram. The goal is to find all anagrams in the dictionary. Every word that can be spelled using the same set of letters will be grouped together in the output file.

Specification

Anagrams are case-insensitive, thus “Salem” and “meals” are the members of the same anagram family “aelms”. The capitalization of the word must be preserved for output, so “salem” is not acceptable. Duplicate words such as “A” and “a” are both words in the same anagram family “a”. An anagram family size is the number of words that can be spelled with the set of letters.

The program shall do the following:

<ul>

 <li>Open a file specified on the command line.</li>

 <li>Read each line as a word and add it to an existing anagram family or create a new one.</li>

 <li>Enumerate the anagram families printing to a file: print the sorted set followed by ‘:’ print the number of anagrams followed by ‘<em>r</em>’</li>

</ul>

print a tab ‘<em>t</em>’ before each anagram, then anagram, followed by ‘<em>r</em>’

<ul>

 <li>Do not print out anagram families whose size is 1.</li>

 <li>Clean up all memory data structures and close all files.</li>

 <li>Detect and handle erroneous command line input.</li>

</ul>

Here is an example of expected output in a file:

aefrst : 3 afters faster strafe

Design

A header specification for two data structures and functions will be provided, all functions need to be implemented appropriately. StringList is a structure to store a list of strings, AnagramList is a structure to store an anagram family and the associated words in a StringList.

<table width="355">

 <tbody>

  <tr>

   <td width="62">/∗ List</td>

   <td width="234">of      strings        structure ∗/struct StringList {</td>

   <td width="58"> </td>

  </tr>

  <tr>

   <td width="62"> </td>

   <td width="234">                         struct                StringListchar ∗Word;};</td>

   <td width="58">∗ Next ;</td>

  </tr>

  <tr>

   <td width="62">/∗ List</td>

   <td width="234">of anagrams structure ∗/struct AnagramList{</td>

   <td width="58"> </td>

  </tr>

  <tr>

   <td width="62"> </td>

   <td width="234">                         struct                StringList</td>

   <td width="58">∗Words;</td>

  </tr>

  <tr>

   <td width="62"> </td>

   <td width="234">struct AnagramListchar ∗Anagram;};</td>

   <td width="58">∗Next ;</td>

  </tr>

 </tbody>

</table>

/∗Create a new string   l i s t       node∗/ struct       StringList ∗MallocSList ( char ∗word );

/∗Free a string list , including all children ∗/ void FreeSList ( struct StringList ∗∗node );

/∗Append a string l i s t node to the end/ tail of a string l i s t ∗/ void AppendSList( struct StringList ∗∗head , struct StringList ∗node );

/∗Format output to a f i l e according to specification .∗/ void PrintSList (FILE ∗ file , struct StringList ∗node );

/∗Return the number of strings in the string l i s t .∗/ int SListCount ( struct StringList ∗node );

/∗Create a new anagram node ,              including           the        string    l i s t      node with the word.∗/ struct AnagramList∗ MallocAList ( char ∗word );

/∗Free an anagram list , including anagram children and string l i s t words .∗/ void FreeAList ( struct AnagramList ∗∗node)

/∗Format output to a file , print anagram l i s t with words , according to spec∗/ void PrintAList (FILE ∗ file , struct AnagramList ∗node );

/∗Add a new word to the anagram l i s t ∗/ void AddWordAList( struct AnagramList ∗∗node , char ∗word );

The provided header file may not be changed. AddWordAList will create an AnagramList if (*node) is null, the first time it will be. You need to make sure that the anagram is stored in sorted lower case. You need to make sure that AddWordAList compares a lower case version of word, it should be easier for comparison if the word is also sorted. Make sure that SList stores the word with proper case and does not sort the word. You will need to make a copy the string and free it after usage to do this correctly. Note: you will need to implement a function to un-capitalize a character array and a function to sort the character array. Quick sort is recommended, please cite your source.

A compiled working test version of the main driver program will be provided to test with. The program reads from input and writes to output adding each word to the anagram list, then prints the anagram list, and cleans up. The main program file consists of the following sudo code:

open input f i l e or stdin open output f i l e or stdout

exit i f either f i l e is invalid while getline from input f i l e add word to a l i s t

print a     l i s t free a     l i s t close input and output     f i l e .

Usage is as follows:

<ul>

 <li>./anagram // read from stdin, write stdout</li>

 <li>./anagram file1 // read from file1, write stdout</li>

 <li>./anagram file1 file2 // read from file1, write file2.</li>

</ul>

This can be tested with such commands as:

<ul>

 <li>./anagram <em>&lt;</em>file1 <em>&gt;</em>file2 //test for reading from stdin/ write stdout.</li>

 <li>./anagram file1 <em>&gt;</em>file2 // test for reading from file1 / write stdout.</li>

 <li>./anagram file1 file2 // test for reading from file1 / write file2.</li>

</ul>

Several dictionaries will be provided: A, A-B, A-B-C, and A-Z. Output files for A,A-B,A-B-C will be provided.

Implementation

You need to implement all of the functions in the header file along with the main driver program. Sample input/output files will be provided, the output file should match exactly. You can use the command line “diff file1 file2” to verify that two files are identical.

Note you will be penalized heavily if valgrind reports any memory errors. After you have a working version of the program, you need to test it using valgrind to make sure it has no memory errors. If valgrind indicates any problems with your codes use of heap memory, it is usually an indication that you are doing something very wrong that will bite you eventually; you must fix your code to remove all such problem reports.

A gzipped tar archive containing source files, a makefile, and test input and output files is available on Canvas. In addition to anagram.h and makefile there is also an object file with a working version of the main driver program. This will allow you to test your implementation of SList and Alist before implementing your own driver program.

<h1>5           Approach: Building and debugging anagram</h1>

You should first study the anagram.h structures and functions to understand what they provide, then analyze the sudo code to see how it uses the functions. First construct anagram.c by copy pasting anagram.h and deleting the # statements and structure declarations. You will then need to implement each function, some functions will call other functions, such as MallocAList will call MallocSList. Once you have all the functions implemented you can run the following for verification: ./ anagramtest <em>&lt;</em>A. dict  |              diff − A. out

./ anagramtest <em>&lt;</em>A−B. dict                |        diff − A−B. out

Once you have this working then implement your own main.c and call the functions in anagram.h. The make file will build the two file anagram and anagramtest