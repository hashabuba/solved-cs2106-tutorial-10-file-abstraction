Download Link: https://assignmentchef.com/product/solved-cs2106-tutorial-10-file-abstraction
<br>
<ol>

 <li>Explain the following concepts in your own words clearly; the shorter, the better! Your explanation should be easily understandable for non-CS2106 students.</li>

</ol>




<ol>

 <li>What is a file?</li>

 <li>Name and describe some classifications of files.</li>

 <li>Distinguish between a file type and a file extension.</li>

 <li>What does it mean to open and close a file?</li>

 <li>What does it mean to truncate a file?</li>

</ol>




<ol start="2">

 <li>(Understanding directory permission) In *nix system, a directory has the same set of permission settings as a file. For example:</li>

</ol>










You can see that directory <strong>Directory </strong>has the read, write, execute permission for owner, but only execution permission for group and others. It is easy to understand the permission bits for a regular file (read = can only access, write = can modify, execute = can execute this file). However, the same cannot be said for the directory permission bits.




Let’s perform a few experiments to understand the permission bits for a directory.

<strong> </strong>

<strong>Setup: </strong>

<ul>

 <li>Unzip <strong>zip</strong> on any *nix platform (Solaris, Mac OS X included).</li>

 <li>Change directory to the <strong>DirExp/</strong> directory, there are 4 subdirectories with the same set of files. Let’s set their permission as follows:</li>

</ul>

<table width="573">

 <tbody>

  <tr>

   <td width="212">chmod 700 NormDir</td>

   <td width="361">NormDir is a normal directory with read, write and execute permissions.</td>

  </tr>

  <tr>

   <td width="212">chmod 500 ReadExeDir</td>

   <td width="361">ReadExeDir has read and execute permission.</td>

  </tr>

  <tr>

   <td width="212">chmod 300 WriteExeDir</td>

   <td width="361">WriteExeDir has write and execute permission.</td>

  </tr>

  <tr>

   <td width="212">chmod 100 ExeOnlyDir</td>

   <td width="361">ExeOnlyDir has only execute permission.</td>

  </tr>

 </tbody>

</table>




Perform the following operations on each of the directory and note down the result. Make sure you are at the <strong>DirExp/</strong> directory at the beginning. DDDD is one of the subdirectories.




<ol>

 <li>Perform “<strong>ls –l DDDD</strong>“.</li>

 <li>Change into the directory using “<strong>cd DDDD</strong>“.</li>

 <li>Perform “<strong>ls –l</strong>“.</li>

 <li>Perform “<strong>cat file.txt</strong>” to read the file content.</li>

 <li>Perform “<strong>touch file.txt</strong>” to modify the file.</li>

 <li>Perform “<strong>touch newfile.txt</strong>” to create a new file.</li>

</ol>




Can you deduce the meaning of the permission bits for directory after the above? Can you use the “directory entry” idea to explain the behavior?







<ol start="3">

 <li>(Adapted from [SGG]) Why do many operating systems have a system call to “open” a file, rather than just passing a path to the read or write system calls each time?</li>

</ol>




<strong> </strong>

<ol start="4">

 <li>(Wrapping File Operations) File operations are very expensive in terms of time. There are several reasons:</li>

 <li>a) As we learned in the lecture, each file operation is a system call, which requires an execution mode change (user kernel); b) Secondary storage mediums have high access latencies.</li>

</ol>




This leads to a strange phenomenon: it is generally true that the total time to perform 100 file operations for 1 item each is <strong>much longer </strong>than performing a single file operation for 100 items instead. e.g. writing one byte 100 times takes longer than writing 100 bytes in one go.




Most high-level programming languages therefore provide <strong>buffered file operations </strong>that wrap around primitive file operations. The buffered version maintains an internal intermediate storage in memory (i.e. buffer) to store values read from/written to the file by the user. For example, a <strong>buffered write operation </strong>will wait until the internal memory buffer is full before doing a large one-time file write operation to <strong><em>flush</em> </strong>the buffer content into file.




<ol>

 <li>(Generalization) Give one or two examples of buffered file operations found in your favorite programming language(s). Other than the “chunky” read/write benefit, are there any other additional features provided by these high-level buffered file operations?</li>

</ol>

<em> </em>

<ol>

 <li>(Application) Take a look at the given “<strong>c</strong>” source code. Compile and perform the following experiments: Change the trigger value from 100, 200, … until you see values printed on screen <strong>before the program crashes</strong>. Can you explain both the behavior and the significance of the “trigger” value? If you add a new line character “<strong>
</strong>” to the <strong>printf</strong>() statement, how does the output pattern changes? How can this information be useful?</li>

</ol>

<em> </em>

<ol>

 <li>(Design) Give an algorithm in <strong>high-level pseudo-code </strong>to provide a buffered read operation. Use the following function header as a starting point:</li>

</ol>

<em> </em>

<strong>BufferedFileRead(file, outputArray, arraySize) </strong>

// Read arraySize items from file and place the items in outputArray




<ol start="5">

 <li>(Wrapping File Operations, again) Study the attached program weird_read.c. Note that it is written to run with the given input alice.txt, but you can modify it to read your own file.</li>

</ol>




<ol>

 <li>Uncomment a(); in main, then compile and run the program. What do you observe and why?</li>

 <li>Uncomment b(); in main, then compile and run the program. What do you observe and why?</li>

 <li>Uncomment c(); in main, then compile and run the program. What do you observe and why?

  <ol>

   <li>What happens when the first fread and printf are removed instead?</li>

   <li>What happens when c() is run with multiple threads instead of processes?</li>

  </ol></li>

</ol>