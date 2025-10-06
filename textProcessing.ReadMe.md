# Programming Example:  Code Detection  
Let us now write a program that reads a given text, outputs the text as is, and also prints the number of lines and the number of times each letter appears in the text.  
An uppercase letter and a lowercase letter are treated as being the same; that is, they are tallied together.  
Because there are 26 letters, we use an array of **26** components to perform the letter count. We also need a variable to store the line count.  
  
The text is stored in a file, which we will call **textin.txt**. The output will be stored in a file, which we will call **textout.out**.   
  
**Input** A file containing the text to be processed.  
**Output** A file containing the text, number of lines, and the number of times a letter appears in the text.

## Problem Analysis and Algorithm Design  
Based on the desired output, it is clear that we must output the text as is.  
That is, if the text contains any whitespace characters, they must be output as well.  
Furthermore, we must count the number of lines in the text.  
Therefore, we must know where the line ends, which means that we must trap the newline character.  
This requirement suggests that we cannot use the extraction operator to process the input file.  
Because we also need to perform the letter count, we use the **get** function to read the text.

### Variables  
We need to store the line count and the letter count.  
Therefore, we need a variable to store the line count and 26 variables to perform the letter count.  
We will use an array of **26** components to perform the letter count.  
We also need a variable to read and store each character in turn, because the input file is to be read character by character.  

Because data is to be read from an input file and output is to be saved in a file, we need an input stream variable to open the input file and an output stream variable to open the output file.  
These statements indicate that the function main needs (at least) the following variables:

- **int lineCount**; //variable to store the line count
- **int letterCount[26]**; //array to store the letter count
- **char ch**; //variable to store a character
- **ifstream infile**; //input file stream variable
- **ofstream outfile**; //output file stream variable

In this declaration, **letterCount[0]** stores the A count, **letterCount[1]** stores the B count, and so on.  
Clearly, the variable **lineCount** and the array **letterCount** must be initialized to **0**.  

The algorithm for the program is:
1. Declare the variables.
2. Open the input and output files.
3. Initialize the variables.
4. While there is more data in the input file:  
    4. A. For each character in a line: Read and write the character. Increment the appropriate letter count.  
    4. B. Increment the line count.  
5. Output the line count and letter counts.
6. Close the files.  

To simplify the function main, we divide it into four functions:  
- Function **initialize**  
- Function **copyText**  
- Function **characterCount**  
- Function **writeTotal**  

### initialize  
This function initializes the variable **lineCount** and the array **letterCount** to **0**.  
It,therefore, has two parameters: one corresponding to the variable **lineCount** and one corresponding to the array **letterCount**.  
Clearly, the parameter corresponding to **lineCount** must be a reference parameter.  

### copyText
This function reads a line and outputs the line.  
After reading a character, it calls the function **characterCount** to update the letter count.  
Clearly, this function has four parameters: an input file stream variable, an output file stream variable, a char variable, and the array to update the letter count.  

Note that the **copyText** function does not perform the letter count, but we still pass the array **letterCount** to it.  
We take this step because this function calls the function **characterCount**, which needs the array **letterCount** to update the appropriate letter count.  
Therefore, we must pass the array **letterCount** to the **copyText** function so that it can pass the array to the function **characterCount**.

### characterCount  
This function increments the letter count.  
To increment the appropriate letter count, it must know what the letter is.  
Therefore, the **characterCount** function has two parameters: a char variable and the array to update the letter count.  
  
In pseudocode, this function is:
1. Convert the letter to uppercase.
2. Find the index of the array corresponding to this letter.
3. If the index is valid, increment the appropriate count. At this step, we must ensure that the character is a letter. We are counting only letters, so other characters—such as commas, hyphens, and periods—are ignored.  

### writeTotal  
This function outputs the line count and the letter count. It has three parameters: the
output file stream variable, the line count, and the array to output the letter count.

## Main Algorithm  
We now describe the algorithm for the function **main**.
1. Declare the variables.
2. Open the input file.
3. If the input file does not exist, exit the program.
4. Open the output file.
5. Initialize the variables, such as **lineCount** and the array **letterCount**.
6. Read the first character.  
7. While (not end of input file):  
    7.1. Process the next line; call the function **copyText**.  
    7.2. Increment the line count. (Increment the variable **lineCount**.)  
    7.3. Read the next character.  
8. Output the line count and letter counts. Call the function **writeTotal**.
9. Close the files.