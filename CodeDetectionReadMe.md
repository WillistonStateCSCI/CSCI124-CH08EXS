# Programming Example:  Code Detection
When a message is transmitted in secret code over a transmission channel, it is usually sent as a sequence of bits, that is, **0**s and **1**s.  
Due to noise in the transmission channel, the transmitted message may become corrupted.  
That is, the message received at the destination is not the same as the message transmitted; some of the bits may have been changed.  
There are several techniques to check the validity of the transmitted message at the destination.  
One technique is to transmit the same message twice.  
At the destination, both copies of the message are compared bit by bit.  
If the corresponding bits are the same, the message received is error-free.  
  
Let’s write a program to check whether the message received at the destination is error-free.  
  
For simplicity, assume that the secret code representing the message is a sequence of digits (**0** to **9**)  
and the maximum length of the message is **250** digits.  

Also, the first number in the message is the length of the message.  
For example, if the secret code is:  
**7 9 2 7 8 3 5 6**  
then the actual message is 7 digits long, and it is transmitted twice.  
  
The above message is transmitted as:  
**7 9 2 7 8 3 5 6 7 9 2 7 8 3 5 6**

**Input** A file containing the secret code and its copy  
**Output** The secret code, its copy, and a message—if the received code is error-free—in the following form:  
|**Code Digit Code**|**Digit Copy**|
|-------------------|--------------| 
|**9**|**9**| 
|**2**|**2**|  
|**7**|**7**|
|**8**|**8**|  
|**3**|**3**|  
|**5**|**5**|  
|**6**|**6**|  
**Message transmitted OK.**  
  
## Problem Analysis and Algorithm Design
Because we have to compare the corresponding digits of the secret code and its copy, we
first read the secret code and store it in an array. Then we read the first digit of the copy
and compare it with the first digit of the secret code, and so on. If any of the
corresponding digits are not the same, we indicate this fact by printing a message next
to the digits. Because the maximum length of the message is 250, we use an array of 250
components. The first number in the secret code, and in the copy of the secret code,
indicates the length of the code. This discussion translates into the following algorithm:
1. Open the input and output files.
2. If the input file does not exist, exit the program.
3. Read the length of the secret code.
4. If the length of the secret code is greater than **250**, terminate the
program because the maximum length of the code in this program is **250**.
5. Read and store the secret code into an array.
6. Read the length of the copy.
7. If the length of the secret code and its copy are the same, compare
the codes. Otherwise, print an error message.
To simplify the function main, let us write a function, readCode, to read the secret
code and another function, compareCode, to compare the codes

## readCode
This function first reads the length of the secret code. If the length of the
secret code is greater than **250**, a bool variable **lenCodeOk**, which is a
reference parameter, is set to false and the function terminates.  
  
The value of **lenCodeOk** is passed to the calling function to indicate whether the secret code was read successfully.  
  
If the length of the code is less than **250**, the **readCode** function reads and stores the secret code into an array.  
  
Because the input is stored into a file and the file was opened in the function **main**, the input stream variable corresponding to the input file must be passed as a parameter to this function.  
  
Furthermore, after reading the length of the secret code and the code itself, the **readCode** function must pass these values to the function main.  
Therefore, this function has four parameters: an input file stream variable, an array to store the secret code, the length of the code, and the bool parameter **lenCodeOk**.

## compareCode
This function compares the secret code with its copy.  
Therefore, it must have access to the array containing the secret code and the length of the secret code.  
The copy of the secret code and its length are stored in the input file.  
Thus, the input stream variable corresponding to the input file must be passed as a parameter to this function.  
  
Also, the **compareCode** function compares the secret code with the copy and prints an appropriate message.  
Because the output will be stored in a file, the output stream variable corresponding to the output file must also be passed as a parameter to this function.  
  
Therefore, the function has four parameters: an input file stream variable, an output file stream variable, the array containing the secret code, and the length of the secret code.  

This discussion translates into the following algorithm for the function **compareCode**:
1. Declare the variables.
2. Set a bool variable **codeOk** to true.
3. Read the length of the copy of the secret code.
4. If the length of the secret code and its copy are not the same, output
an appropriate error message and terminate the function.
5. For each digit in the input file:
    5. Read the next digit of the copy of the secret code.
    5. Output the corresponding digits from the secret code and its copy.
    5. If the corresponding digits are not the same, output an error message and set the bool variable **codeOk** to false.
6. If the bool variable **codeOk** is true, Output a message indicating that the secret code was transmitted correctly. Else, Output an error message.

## Main Algorithm
1.  Declare the variables.
2. Open the files.
3. Call the function **readCode** to read the secret code.
4. if (length of the secret code **<= 250**), Call the function **compareCode** to compare the codes.  Else, Output an appropriate error message.