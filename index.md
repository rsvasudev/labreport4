# Lab Report 4


## Part 1

### A failure-inducing input for the buggy program, as a JUnit test and any associated code
```ruby
@Test
public void test(){
  int[] input2={3,5,6,5};
  ArrayExamples.reverseInPlace(input2);
  assertArrayEquals(new int[]{5,6,5,3}, input2);
  
  }

```

### An input that doesn’t induce a failure, as a JUnit test and any associated code 

```ruby
@Test
public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
```

### The symptom, as the output of running the tests 

![Image](Symptom.png)

### The bug, as the before-and-after code change required to fix it 
Before:
```ruby
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

After:
```ruby
  static void reverseInPlace(int[] arr){
  for (int i = 0; i < arr.length / 2; i++) {
        int temp = arr[i];
        arr[i] = arr[arr.length - i - 1];
        arr[arr.length - i - 1] = temp;
    }
}
```

Previously, the first element was being changed to the last element and the first element wasn't stored. Thus, when the for loop tries to change the last element to the first element. It is just changing it to the newly stored first element, which is the last element. This problem was there for the entirety of the second half of the array as they were just being changed to themselves. Hence, there was the bug. 

For example, using the example I had with the array {3,5,6,5}.
In the first iteration of the for loop, the first element is given the value of the last element. Thus, the array becomes {5,5,6,5}
Similarly, in the second iteration, the array becomes {5,6,6,5}. The second element is given the value of the the third element
In the third iteration, the array becomes {5,6,6,5}. The third element is given the value fo the new second element(6). Thus, the array stays the same. At this point, the array should become {5,6,5,5} but the old second value isnt stored so the thrid element is instead assigned the new value fo the second element.
Lastly, in the next iteration, the array becomes {5,6,6,5} as the last element is given the new value of the first element instead of becoming {5,6,5,3}. Thus, you can see the bug that appears in reversing the second half of the array as it is just reassigned the same value. 

The new code is changing the first element to the last element and storing the previous value of the first element and then setting that to the value of the last element in the same iteration of the for loop.This pattern is being repeated for all the other elements. Thus, the values are actually being swapped and reversed as the first element is being swapped with the last element. This is the same for the second last element and the second element and so on. Additonally, the for loop only runs for half of the length of the array as two element values are being changed in each iteration.

Again, using the same array as an example: {3,5,6,5}.
In the first iteration, the first and last elements are swapped. Thus, the array becomes {5,5,6,3}
In the second and last iteration, the second and third elements are swapped. Thus, the array becomes {5,6,5,3}, which is the correct solution. 
Therefore, the bug is fixed.

### Proof of symptom being fixed

![Image](Fixed.png)

## Part 2

Chosen command: grep 

### 4 command line options for grep
grep -r
grep -c 
grep -w 
grep -n 

I used the man grep command and ChatGPT to find and understadn these different commands.

### grep -r "example string" <path> with directory as argument 
```ruby
grep -r "Portland" ./technical

```

```ruby
rohanvasudev@Rohans-MacBook-Air docsearch % grep -r "Portland" ./technical        
./technical/government/About_LSC/State_Planning_Report.txt:twelve largest law firms in Portland. Between two and three "Coffin
./technical/government/Env_Prot_Agen/bill.txt:Martins Creek Portland Shawville
./technical/government/Media/Oregon_Poor.txt:(AAW) in Southeast Portland on Aug. 7 searching for a car. . . .
./technical/government/Media/Oregon_Poor.txt:Portland. It's 75,000 now.
./technical/government/Media/Survey.txt:Circuit in Portland, Me. He said the commission was to meet in
./technical/government/Media/Service_Agency.txt:Machias, Portland, Presque Isle and Rockland.
./technical/biomed/1471-2180-2-22.txt:          (Portland, OR). The other chemicals and solvents used
./technical/biomed/1471-244X-2-9.txt:        Treatment and Research (BMedCTR) in Portland, Oregon, among
./technical/biomed/gb-2001-3-1-research0005.txt:          R-phycoerythrin (Molecular Probes, Portland, OR) for 30
./technical/biomed/1476-4598-2-1.txt:          labeling was from Molecular Probe Inc. (Portland,
./technical/biomed/1472-6947-2-4.txt:          Providence Health System in Portland, Oregon provided
./technical/biomed/1472-6947-2-4.txt:        The results of this study were presented at the Portland
./technical/biomed/1472-6947-2-4.txt:        Technology, Portland Oregon, 1997 and 1999. The results
./technical/biomed/1472-6947-2-4.txt:        Management. Portland State University, PICMET
./technical/biomed/1472-6947-2-4.txt:        summary presented in proceedings, Portland International
./technical/biomed/1472-6947-2-4.txt:        Portland, Oregon, 1999, pp. 392-394.
./technical/biomed/1472-6947-2-4.txt:        Industry. Preliminary results presented at the Portland
./technical/biomed/1472-6947-2-4.txt:        Technology, published in proceedings, Portland, Oregon,
./technical/911report/chapter-13.5.txt:                the Portland flight. Although he may have believed that security was more relaxed at
./technical/911report/chapter-13.2.txt:                of why Atta and Omari drove to Portland, Maine, from Boston on the morning of
./technical/911report/chapter-13.2.txt:                However, Atta reacted negatively when informed in Portland that he would have to
./technical/911report/chapter-13.2.txt:                reason, the Portland Jetport was the nearest airport to Boston with a 9/11 flight
./technical/911report/chapter-13.2.txt:                interview (Nov. 6, 2003); Portland International Jetport site visit (Aug. 18, 2003).
./technical/911report/chapter-1.txt:    For those heading to an airport, weather conditions could not have been better for a safe and pleasant journey. Among the travelers were Mohamed Atta and Abdul Aziz al Omari, who arrived at the airport in Portland, Maine.
./technical/911report/chapter-1.txt:    Boston: American 11 and United 175. Atta and Omari boarded a 6:00 A.M. flight from Portland to Boston's Logan International Airport.
./technical/911report/chapter-1.txt:    While Atta had been selected by CAPPS in Portland, three members of his hijacking team-Suqami, Wail al Shehri, and Waleed al Shehri-were selected in Boston. Their selection affected only the handling of their checked bags, not their screening at the checkpoint. All five men cleared the checkpoint and made their way to the gate for American 11. Atta, Omari, and Suqami took their seats in business class (seats 8D, 8G, and 10B, respectively). The Shehri brothers had adjacent seats in row 2 (Wail in 2A, Waleed in 2B), in the firstclass cabin. They boarded American 11 between 7:31 and 7:40. The aircraft pushed back from the gate at 7:40.
./technical/911report/chapter-7.txt:                another hotel, and the two drove to Portland, Maine, for reasons that remain

```

Description:
grep -r "Portland" ./technical. This command searches for all the files and the lines in these files, which the provided string "Portland" is in. -r enables a search for this string not only in the ./technical directory but also its subdirectories. This is useful because it allows for a thorougha nd wide search to be done in one command. Thus, files containing a specific word can be found easily and quickly, meaning there is less work for the user.

### grep -r "example string" <path> with file as argument 
```ruby
grep -r "Portland" ./technical/government/About_LSC/State_Planning_Report.txt
```

```ruby
rohanvasudev@Rohans-MacBook-Air docsearch % grep -r "Portland" ./technical/government/About_LSC/State_Planning_Report.txt
./technical/government/About_LSC/State_Planning_Report.txt:twelve largest law firms in Portland. Between two and three "Coffin
```

Description:
grep -r "Portland" ./technical/government/About_LSC/State_Planning_Report.txt. This command searches for all the lines that have the provided string in the mentioned file. The -r here doesn't do much as there are no subdirectories or directories as the path provided is to an actual file. This is useful because it allows for us to see all the lines in the file with the word but also observe patterns within the file andf how freuqently the string is used. 

### grep -c "example string" <path> with directory as argument 

```ruby
grep -c "Portland" ./technical
```

```ruby
rohanvasudev@Rohans-MacBook-Air docsearch % grep -c "Portland" ./technical
grep: ./technical: Is a directory
```

The command returns an error as this command-line option -c only takes filepaths as arguments. It then returns the number of lines with the given string. However, you can recursively search using -r from the previous command-line option and use the diretcory as an argument as shopwn below. This isnt useful. The command is made useful below. 

```ruby
grep -r -c "Portland" ./technical/911report
```

```ruby
rohanvasudev@Rohans-MacBook-Air docsearch % grep -r -c "Portland" ./technical/911report
./technical/911report/chapter-13.4.txt:0
./technical/911report/chapter-13.5.txt:1
./technical/911report/chapter-13.1.txt:0
./technical/911report/chapter-13.2.txt:4
./technical/911report/chapter-13.3.txt:0
./technical/911report/chapter-3.txt:0
./technical/911report/chapter-2.txt:0
./technical/911report/chapter-1.txt:3
./technical/911report/chapter-5.txt:0
./technical/911report/chapter-6.txt:0
./technical/911report/chapter-7.txt:1
./technical/911report/chapter-9.txt:0
./technical/911report/chapter-8.txt:0
./technical/911report/preface.txt:0
./technical/911report/chapter-12.txt:0
./technical/911report/chapter-10.txt:0
./technical/911report/chapter-11.txt:0
```

Description:
-r enables the command to search recursively(ie in all of ./technical/911report's subdirectories and within the directory itself).-c then enables the command to provide a count of the number of times "Portland" is used in each of the files. The directory then tells the command where to search. This is useful because we are able to search quickly and see files with more of the same string very easily due to the way the data is presented to us. This can be helpful in spotting patterns. 

Note: I changed the directory as there were too many files listed if ./technical was used as the directory.

### grep -c "example string" <path> with file as argument 

```ruby
grep -r -c "Portland" ./technical/911report/chapter-13.5.txt
```

```ruby
rohanvasudev@Rohans-MacBook-Air docsearch % grep -r -c "Portland" ./technical/911report/chapter-13.5.txt
./technical/911report/chapter-13.5.txt:1
```

Description:
Here with the file as the argument. -c counts the number of lines with the "Portland" string in the filepath provided. The . in the filepath stands for the working diretory. This is useful because we are able to concisely see hwo many times a string is used in the file without having to indivdually count. Furthermore, you can comapre this with other files and perhaps get a slight gauge of what the text file's contents are about by finding this frequency.

### grep -w "example string" <path> with file as argument 
```ruby
grep -w  "Portland" ./technical/911report/chapter-13.5.txt
```

```ruby
rohanvasudev@Rohans-MacBook-Air docsearch % grep -w  "Portland" ./technical/911report/chapter-13.5.txt
                the Portland flight. Although he may have believed that security was more relaxed at
```

Description:
-w unlike -r allows for only exact matches to word to be given. For example, if the string in the command is "specific", it will only return lines that contain the word "specific". -r would return lines with words like "specifically" or "specifics". The argument has to be a file. As you can see, it returns all the lines in the text file with the word "Portland". This is useful because it allows for us to search the contents of the text file with ease but also because we are able to see when the exact word(s) is used rather than just the string itself. This can help get a more in depth search and prevent thre output providing us with lines that don;t have the word we were looking for. 

### grep -w "example string" <path> with directory as argument
```ruby
grep -w  "Portland" ./technical/911report
```

``` ruby
rohanvasudev@Rohans-MacBook-Air docsearch % grep -w  "Portland" ./technical/911report
grep: ./technical/911report: Is a directory
```

Like with -c we need to search recursively(-r) in order to be able to use a diretcory as an argument. 
```ruby

```
grep -r -w "Portland" ./technical/911report
```ruby
rohanvasudev@Rohans-MacBook-Air docsearch % grep -r -w "Portland" ./technical/911report
./technical/911report/chapter-13.5.txt:                the Portland flight. Although he may have believed that security was more relaxed at
./technical/911report/chapter-13.2.txt:                of why Atta and Omari drove to Portland, Maine, from Boston on the morning of
./technical/911report/chapter-13.2.txt:                However, Atta reacted negatively when informed in Portland that he would have to
./technical/911report/chapter-13.2.txt:                reason, the Portland Jetport was the nearest airport to Boston with a 9/11 flight
./technical/911report/chapter-13.2.txt:                interview (Nov. 6, 2003); Portland International Jetport site visit (Aug. 18, 2003).
./technical/911report/chapter-1.txt:    For those heading to an airport, weather conditions could not have been better for a safe and pleasant journey. Among the travelers were Mohamed Atta and Abdul Aziz al Omari, who arrived at the airport in Portland, Maine.
./technical/911report/chapter-1.txt:    Boston: American 11 and United 175. Atta and Omari boarded a 6:00 A.M. flight from Portland to Boston's Logan International Airport.
./technical/911report/chapter-1.txt:    While Atta had been selected by CAPPS in Portland, three members of his hijacking team-Suqami, Wail al Shehri, and Waleed al Shehri-were selected in Boston. Their selection affected only the handling of their checked bags, not their screening at the checkpoint. All five men cleared the checkpoint and made their way to the gate for American 11. Atta, Omari, and Suqami took their seats in business class (seats 8D, 8G, and 10B, respectively). The Shehri brothers had adjacent seats in row 2 (Wail in 2A, Waleed in 2B), in the firstclass cabin. They boarded American 11 between 7:31 and 7:40. The aircraft pushed back from the gate at 7:40.
./technical/911report/chapter-7.txt:                another hotel, and the two drove to Portland, Maine, for reasons that remain
```

Description:

As you can see, similar to -r, it returns the filepaths and the respective lines in the file where "Portland" is used. Note that it will only return lines where the word "Portland" is contained not lines where the string "Portland" is. For example, it wouldnt return a line where the word "Portland's" is used. This is how it differs to -r by itself. Again, -r enables for a search to be done for everything in the ./technical/911report directory and all its subdirectories. Agian the nature of the recurisve search is very useful due to its ease and speed. Additonally, the search is without phrase's like "Portland's" in its output or "Portlander" that help for a mroe specific and in depths earch when required. 

### grep -n "example string" <path> with file as argument
```ruby
grep -n "Portland" ./technical/911report/chapter-13.5.txt
```

```ruby
rohanvasudev@Rohans-MacBook-Air docsearch % grep -n "Portland" ./technical/911report/chapter-13.5.txt
577:                the Portland flight. Although he may have believed that security was more relaxed at
```

Description:
-n enables a simialr type of search to the other commands. However, it returns the line number as well as the line with the string "Portland". Note, unlike -w, it just looks for the string "Portland" not the word so a line with "Portland's" would be shown. The filepath is provided as the argument and this is the file that is searched. This is useful because it allows for us to see if there's areas where a certain string is used more due to the line number being provided. Thus, we can see if "Portland" is used 3 times in 3 lines. The contents of the line make the command even mroe useful by providing context. 

### grep -n "example string" <path> with directory as argument

```ruby
grep -n "Portland" ./technical/911report
```

```ruby
rohanvasudev@Rohans-MacBook-Air docsearch % grep -n "Portland" ./technical/911report                 
grep: ./technical/911report: Is a directory
```

Again, to pass a diretcory as an argument, we need to search recursively.

```ruby
grep -r -n "Portland" ./technical/911report
```

```ruby
rohanvasudev@Rohans-MacBook-Air docsearch % grep -r -n "Portland" ./technical/911report              
./technical/911report/chapter-13.5.txt:577:                the Portland flight. Although he may have believed that security was more relaxed at
./technical/911report/chapter-13.2.txt:62:                of why Atta and Omari drove to Portland, Maine, from Boston on the morning of
./technical/911report/chapter-13.2.txt:64:                However, Atta reacted negatively when informed in Portland that he would have to
./technical/911report/chapter-13.2.txt:66:                reason, the Portland Jetport was the nearest airport to Boston with a 9/11 flight
./technical/911report/chapter-13.2.txt:69:                interview (Nov. 6, 2003); Portland International Jetport site visit (Aug. 18, 2003).
./technical/911report/chapter-1.txt:8:    For those heading to an airport, weather conditions could not have been better for a safe and pleasant journey. Among the travelers were Mohamed Atta and Abdul Aziz al Omari, who arrived at the airport in Portland, Maine.
./technical/911report/chapter-1.txt:14:    Boston: American 11 and United 175. Atta and Omari boarded a 6:00 A.M. flight from Portland to Boston's Logan International Airport.
./technical/911report/chapter-1.txt:34:    While Atta had been selected by CAPPS in Portland, three members of his hijacking team-Suqami, Wail al Shehri, and Waleed al Shehri-were selected in Boston. Their selection affected only the handling of their checked bags, not their screening at the checkpoint. All five men cleared the checkpoint and made their way to the gate for American 11. Atta, Omari, and Suqami took their seats in business class (seats 8D, 8G, and 10B, respectively). The Shehri brothers had adjacent seats in row 2 (Wail in 2A, Waleed in 2B), in the firstclass cabin. They boarded American 11 between 7:31 and 7:40. The aircraft pushed back from the gate at 7:40.
./technical/911report/chapter-7.txt:1565:                another hotel, and the two drove to Portland, Maine, for reasons that remain
```

Description:
Search recursively so directory can be entered as an argument. Recurisve search means that returns line number and correesponding line with "Portland" for each file in working directory and all its subdirectories. -n enables line number and corresponding line to be returned. Then, directory is specified so command knows where to search. This is useful again as a recurisve search allows for a thorougha nd wide search without having to type the same thing multiple times for each file. -n allows for patterns in files to be seen easily and whhich part of each file, the desired string is being used amd if it's being sued in certain areas more. 


## Citing chatGPT sources

### Prompt 1
tell me how to sue the following commands grep -r grep -w grep -c and grep -n work in detail 

ChatGPT
Certainly! Let's go into detail on how each of the grep commands work:

1. grep -r (or grep --recursive)
Purpose:
Searches for a specified pattern recursively in a directory and its subdirectories.
Syntax:
bash
Copy code
grep -r "pattern" /path/to/directory
Example:
bash
Copy code
grep -r "keyword" /path/to/source_code_directory
This command will search for the pattern "keyword" in all files within the specified directory (/path/to/source_code_directory) and its subdirectories.
2. grep -w (or grep --word-regexp)
Purpose:
Searches for whole words, ensuring that the pattern is matched only if it forms a complete word.
Syntax:
bash
Copy code
grep -w "word" file.txt
Example:
bash
Copy code
grep -w "apple" fruits.txt
This command searches for the whole word "apple" in the file fruits.txt, avoiding matches with words like "pineapple" or "applesauce."
3. grep -c (or grep --count)
Purpose:
Counts the number of lines that match the specified pattern.
Syntax:
bash
Copy code
grep -c "pattern" file.txt
Example:
bash
Copy code
grep -c "error" logfile.txt
This command counts and outputs the number of lines in logfile.txt that contain the pattern "error."
4. grep -n (or grep --line-number)
Purpose:
Displays the line numbers along with the matching lines.
Syntax:
bash
Copy code
grep -n "pattern" file.txt
Example:
bash
Copy code
grep -n "warning" source_code.c
This command searches for the pattern "warning" in source_code.c and displays the line numbers of the matching lines.
Additional Tips:
These grep options can be combined based on your requirements. For example, you might use grep -r -n to search for a pattern recursively and display line numbers.
Regular expressions can be used with these commands to create more complex search patterns.
These examples cover some common use cases, but grep is a powerful tool with many more options. You can explore additional functionalities by referring to the manual (man grep) or relevant documentation for more advanced usage.


This prompt helped me unerstand these prompts after finding them in the manual and hwo to implement them in my lab report.


































