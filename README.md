Download Link: https://assignmentchef.com/product/solved-comp2150-assignment-4-hash-table-data-structure
<br>



The assignment has two parts. Each part is worth half of the total marks for the assignment. The entire assignment is in javascript.

Part 1: Hash Table Data Structure

Create a javascript class called HashTable that implements a hash table. When initialized, the HashTable should be given a size as a parameter. The HashTable will create an array of that size as a field. When adding or searching for an element in the HashTable, the position of the element in the table will be its hashVal modulo the length of the array (see below for hashVal information).

The HashTable should use separate chaining. If there is a collision between two elements based on their hash code, the HashTable should place both elements in a linked list of elements at the array position. The order of elements in the linked list at a position is not important.

The HashTable should implement the following methods:

<ul>

 <li>add(x):​ takes a Hashable object x and adds it to the HashTable in the appropriate position (see below for information on the Hashable class). There is no return value for the method.</li>

 <li>get(x):​ takes a Hashable object x and returns the first occurrence <strong>equal to</strong>​ x in the​ hash table. If the element does not exist, the method should throw an error.</li>

 <li>remove(x):​ takes a Hashable object x and deletes one occurrence of an object equal to x in the hash table. If the element does not exist, the method should leave the table unchanged. If several elements are equal to x, the method can delete any of them. The method should return a boolean that indicates whether an element was removed or not.</li>

 <li>contains(x):​ takes a Hashable object x and determines if it is in the hash table. Returns a boolean value.</li>

 <li>isEmpty():​ returns a boolean value determining whether the hash table is empty or not.</li>

</ul>

For each of the first four methods, the method should ensure that the parameter has type Hashable (<strong>or</strong>​ has a hashVal() method, and an equals() method, as appropriate), and it should​   throw an error if the condition does not hold.​

A note on the get() method: you may ask “why does it return the same thing as it’s searching for?” Answer: <strong>it’s not. </strong>​ It’s searching for the first object that’s ​           <strong>equal to</strong>​ the parameter, which​ depends on the definition of equality for the method.  It is possible that they are not the same objects, or even have the same contents (see KeyValueHash below).

<h1>Hashable</h1>

You should also implement a hierarchy of Hashable classes that can be stored in the

HashTable.  The Hashable class should be abstract (using the techniques shown in class) with an abstract hashVal() and an abstract equals(x) method. You should implement three Hashable subclasses:

<ul>

 <li>IntHash, whose hash function is the value of the integer. Two IntHash objects are equal if they contain the same integer value.</li>

 <li>StringHash, whose hash function is the following expression:</li>

</ul>

s[0]*p^(n-1) + s[1]*p^(n-2) + … s[n-2]*p + s[n-1]

where s[i] is the ASCII value of the i-th character of the string, n is the length of the string, and p is a prime (use a prime number less than 1000 of your choice). You can assume that all characters in the strings are ASCII characters. Two StringHash objects are equal if they contain the same strings.

<ul>

 <li>KeyValueHash, which stores two values, a key and a value. The hashVal for a key-value pair is the hashVal of the key, which must be a Hashable type. Two KeyValueHash objects should be considered equal if they have the same ​</li>

</ul>

The subclasses can have additional methods if you need them, including getters.

<h1>Unit Testing</h1>

Construct a set of at least <strong>five </strong>​ different unit tests for your HashTable. To do unit testing in​                javascript, you should simply write a separate file of tests that can be run (i.e., you should not need to use a testing framework like jest or mocha — do not assume the markers will have either installed on their system.)

<ol>

 <li>Create a test file with “let assert = require(‘assert’);​ ” near the top of the​</li>

 <li>Write a file with a series of tests in whatever format you would like. Each test should be its own function.</li>

 <li>Write a main function that calls all of the test methods.</li>

 <li>Have a single executable line that calls the main function.</li>

 <li>In your tests, say assert([something]); to give assertions. You need at least one assertion per test method.</li>

</ol>

At least two of your tests should test boundary conditions: an empty HashTable, and a

HashTable with one element. You will be graded on your tests, so write useful tests for all four unit tests.

Save all of your unit tests as part of a single file and submit them with your code. The markers will be running your tests, so ensure that they pass. <strong>Give instructions on how to run them in</strong>​     <strong> your readme file. </strong>You are strongly advised to complete the unit tests before starting Part 2.​

<strong> </strong>

<strong>Part 2: Dictionary and LZW Encoding </strong>

<strong> </strong>

<h1>Dictionary</h1>

Using your HashTable data structure from Part 1, create a dictionary type called Dictionary. The dictionary type must use containment (not inheritance) when using the HashTable.

In the Dictionary, each entry is a Key-Value pair, and there can’t be two Key-Value pairs in a dictionary with the same Key (that is, keys are unique in a dictionary). The dictionary should have the following operations:

<ol>

 <li>put(k,v):​ takes a Hashable key k and a value v and adds it to the dictionary, if it does not exist. If a key-value pair with k as the key already exists, the current value is replaced with v. The method does not have a return value.</li>

 <li>get(k):​ takes a Hashable key k and returns the value v associated with it, if it appears in the dictionary. Throws​ an error if the key k is not in the dictionary.​</li>

 <li>contains(x):​ takes a Hashable key x and determines if it is a key in the dictionary. Returns a boolean value.</li>

 <li>isEmpty():​ returns a boolean depending on whether the dictionary is empty or not.</li>

</ol>

When created, your dictionary should create a HashTable of a fixed size (1000). You do not need to provide unit testing for your dictionary, but of course you are encouraged to do so.

<h1>LZW Encoding</h1>

Compression is the process of taking a file and using information about the file (“what letters and phrases are more common?”) to create a smaller file with the same information. The smaller file (the compressed file) can be decompressed to recover the original file. zip files are created by compression.

Using your Dictionary, you will implement LZW encoding, a compression algorithm. LZW encoding compresses text files by replacing portions of the text with a single integer. As the LZW encoder runs on more and more text, the portions of text replaced with a single integer grow longer and longer.

Before encoding any text, create a dictionary that associates numerical values with each single character. For this assignment, you will be encoding printable ASCII characters in your dictionary as follows:




<table width="0">

 <tbody>

  <tr>

   <td width="283">Character</td>

   <td width="283">LZW Encoding value</td>

  </tr>

  <tr>

   <td width="283">[space]</td>

   <td width="283">0</td>

  </tr>

  <tr>

   <td width="283">!</td>

   <td width="283">1</td>

  </tr>

  <tr>

   <td width="283">“</td>

   <td width="283">2</td>

  </tr>

  <tr>

   <td width="283">…</td>

   <td width="283">…</td>

  </tr>

  <tr>

   <td width="283">A</td>

   <td width="283">33</td>

  </tr>

  <tr>

   <td width="283">B</td>

   <td width="283">34</td>

  </tr>

  <tr>

   <td width="283">…</td>

   <td width="283">…</td>

  </tr>

  <tr>

   <td width="283">Z</td>

   <td width="283">58</td>

  </tr>

  <tr>

   <td width="283">…</td>

   <td width="283">…</td>

  </tr>

  <tr>

   <td width="283">a</td>

   <td width="283">65</td>

  </tr>

  <tr>

   <td width="283">…</td>

   <td width="283">…</td>

  </tr>

  <tr>

   <td width="283">z</td>

   <td width="283">90</td>

  </tr>

  <tr>

   <td width="283">…</td>

   <td width="283">…</td>

  </tr>

  <tr>

   <td width="283">~</td>

   <td width="283">94</td>

  </tr>

 </tbody>

</table>




That is, all ASCII characters with values from 32 to 126 should be encoded as <strong>their ASCII</strong>​<strong> value minus 32</strong>. To convert from an integer to a character representation in javascript, use the​          String.fromCharCode() method, which converts an ASCII value to a character (e.g.,

String.fromCharCode(33) is a string ‘!’). <strong>Note</strong>​ that the newline character (
) is ​        <strong>NOT</strong>​ in the list of​ characters above, so there will be no newlines in the input for this algorithm.

Next, the LZW algorithm looks at the text file and encodes successive portions of the file into an integer according to this pseudocode:

<ol>

 <li>curr_key = next unseen char from the file</li>

 <li>while curr_key is in the dictionary:</li>

 <li>last_key = curr_key</li>

 <li>curr_key += the next char from the file</li>

 <li>add curr_key to the dictionary with a new LZW encoding value</li>

 <li>output the value in the dictionary for last_key</li>

 <li>set the last character of curr_key as the next starting point for encoding (i.e., the last character of curr_key is the new curr_key next time the pseudocode is run)</li>

</ol>

Repeat this code until all of the characters in the file have been considered. Finally, output a stop code (in our case, the stop code will be -1) after all input has been processed.  See an example run of the LZW encoding below. (To run this pseudocode multiple times, you can manage your position in the input file with an integer index.)

Your Encoder class should have a constructor and one method called encode(). The constructor should take the name of the file that should be encoded. The encode() method should open a

new output file (by adding the “.lzw” extension to the original file name), open the input file, and write the codes for the LZW algorithm to the output file. (You should write the values as <strong>integers and separated by a space</strong>. Do not output any newline symbols. Yes, the output file​          will be larger than the input file in this implementation.)

You should read the filename from the command-line arguments. Use process.argv (an array) to get the command-line arguments when running node.js.

You do not need to implement a decoder. A LZW decoder will be provided for you shortly before the assignment due date.

<h1>Example LZW encoding</h1>

Consider the string “TOBEORNOTTOBETHATISTHEBANANA”. The LZW algorithm finds the following values of curr_key and last_key at each step. The output (an integer) and the modifications to the dictionary are also shown.

<table width="0">

 <tbody>

  <tr>

   <td width="168">1. curr_key = “TO”,</td>

   <td width="144">last_key = “T”.</td>

   <td width="96">Output = 52,</td>

   <td width="180">Add to dictionary: TO:95</td>

  </tr>

  <tr>

   <td width="168">2. curr_key = “OB”,</td>

   <td width="144">last_key = “O”.</td>

   <td width="96">Output = 47,</td>

   <td width="180">Add to dictionary: OB:96</td>

  </tr>

  <tr>

   <td width="168">3. curr_key = “BE”,</td>

   <td width="144">last_key = “B”,</td>

   <td width="96">Output = 34,</td>

   <td width="180">Add to dictionary: BE:97</td>

  </tr>

  <tr>

   <td width="168">4. curr_key= “EO”,</td>

   <td width="144">last_key = “E”,</td>

   <td width="96">Output = 37,</td>

   <td width="180">Add to dictionary: EO:98</td>

  </tr>

  <tr>

   <td width="168">5. curr_key=”OR”,</td>

   <td width="144">last_key = “O”,</td>

   <td width="96">Output = 47,</td>

   <td width="180">Add to dictionary: OR:99</td>

  </tr>

  <tr>

   <td width="168">6. curr_key=”RN”,</td>

   <td width="144">last_key = “R”,</td>

   <td width="96">Output = 50,</td>

   <td width="180">Add to dictionary: RN:100</td>

  </tr>

  <tr>

   <td width="168">7. curr_key=”NO”,</td>

   <td width="144">last_key = “N” ,</td>

   <td width="96">Output = 46,</td>

   <td width="180">Add to dictionary: NO:101</td>

  </tr>

  <tr>

   <td width="168">8. curr_key=”OT”,</td>

   <td width="144">last_key = “O” ,</td>

   <td width="96">Output = 47,</td>

   <td width="180">Add to dictionary: OT:102</td>

  </tr>

  <tr>

   <td width="168">9. curr_key=”TT”,</td>

   <td width="144">last_key = “T” ,</td>

   <td width="96">Output = 52,</td>

   <td width="180">Add to dictionary: TT:103</td>

  </tr>

  <tr>

   <td width="168">10. curr_key=”TOB”,</td>

   <td width="144">last_key = “TO” ,</td>

   <td width="96">Output = 95,</td>

   <td width="180">Add to dictionary: TOB:104</td>

  </tr>

  <tr>

   <td width="168">11. curr_key=”BET”,</td>

   <td width="144">last_key = “BE” ,</td>

   <td width="96">Output = 97,</td>

   <td width="180">Add to dictionary: BET:105</td>

  </tr>

  <tr>

   <td width="168">12. curr_key=”TH”,</td>

   <td width="144">last_key = “T” ,</td>

   <td width="96">Output = 52,</td>

   <td width="180">Add to dictionary: TH:106</td>

  </tr>

  <tr>

   <td width="168">13. curr_key=”HA”,<sub>​</sub></td>

   <td width="144">last_key = “H” ,</td>

   <td width="96">Output = 40,</td>

   <td width="180">Add to dictionary: HA:107</td>

  </tr>

  <tr>

   <td width="168">14. curr_key=”AT”,<sub>​</sub></td>

   <td width="144">last_key = “A” ,</td>

   <td colspan="2" width="276">Output = 33, Add to dictionary: AT:108</td>

  </tr>

  <tr>

   <td width="168">15. curr_key=”TI”,</td>

   <td width="144">last_key = “T” ,</td>

   <td colspan="2" width="276">Output = 52, Add to dictionary: TI:109</td>

  </tr>

  <tr>

   <td width="168">16. curr_key=”IS”,</td>

   <td width="144">last_key = “I” ,</td>

   <td colspan="2" width="276">Output = 41, Add to dictionary: IS:110</td>

  </tr>

  <tr>

   <td width="168">17. curr_key=”ST”,</td>

   <td width="144">last_key = “S” ,</td>

   <td colspan="2" width="276">Output = 51, Add to dictionary: ST:111</td>

  </tr>

  <tr>

   <td width="168">18. curr_key=”THE”,</td>

   <td width="144">last_key = “TH” ,</td>

   <td colspan="2" width="276">Output = 106, Add to dictionary: THE:112</td>

  </tr>

  <tr>

   <td width="168">19. curr_key=”EB”,</td>

   <td width="144">last_key = “E” ,</td>

   <td colspan="2" width="276">Output = 37, Add to dictionary: EB:113</td>

  </tr>

  <tr>

   <td width="168">20. curr_key=”BA”,</td>

   <td width="144">last_key = “B” ,</td>

   <td colspan="2" width="276">Output = 34, Add to dictionary: BA:114</td>

  </tr>

  <tr>

   <td width="168">21. curr_key=”AN”,</td>

   <td width="144">last_key = “A” ,</td>

   <td colspan="2" width="276">Output = 33,    Add to dictionary: AN:115</td>

  </tr>

  <tr>

   <td width="168">22. curr_key=”NA”,</td>

   <td width="144">last_key = “N” ,</td>

   <td colspan="2" width="276">Output = 46, Add to dictionary: NA:116</td>

  </tr>

  <tr>

   <td width="168">23. curr_key=”ANA”,</td>

   <td width="144">last_key = “AN” ,</td>

   <td colspan="2" width="276">Output = 115, Add to dictionary: ANA:117</td>

  </tr>

  <tr>

   <td width="168">24. curr_key=”A​<strong>[EOF]</strong>​”,</td>

   <td width="144">last_key = “A”,</td>

   <td colspan="2" rowspan="2" width="276">Output = 33,</td>

  </tr>

  <tr>

   <td colspan="2" width="312">25. output stop code (-1).</td>

  </tr>

 </tbody>

</table>

<h1>Javascript Notes and Hints</h1>

<ol>

 <li>You must “use strict” in all of your files.</li>

 <li>You are not required to use #private fields in the assignment, but all fields should be <strong>treated as private.</strong> This means using the tools we have used throughout the term: e.g.,​ proper encapsulation, implementation independent data structures, getters, setters if necessary, and operations on data structures rather than releasing a whole data structure.</li>

 <li>Use fs.writeFileSync, fs.appendFileSync and fs.readFileSync for file manipulation.</li>

 <li>Use the substring method on strings to extract a portion of a string, like in Java.</li>

 <li>Use process.argv (an array) to get command line parameters in javascript.</li>

</ol>

<strong> </strong>