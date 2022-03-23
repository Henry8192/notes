# APS105 Markdown Notes
#### Written By Henry
***
## 2022/02/07 Pointers

### Declaring
`int *p;`

### Initializing
`p = &x;`

### Changing values
```c
*p = 7;
x = *p + 1; //  (x = 8 and *p = 8)
int **p, *q = &x, x = 3;
*p = &q;
**p = 5;
```
### Example
```c
void swap(int *x, int *y);
int main()
{
    int x = 5, y = 7;
    swap(&x, &y);
}

void swap(int *x, int *y)
{
    int t = *x;
    *x = *y;
    *y = t;
}
```
### void pointers
`void *p`;

### NULL pointer
not a variable, a const.
value: 0.
    
`int *p = NULL;  // tell yourself p is not pointing to anything`
    
### Runtime Error
`Segmentation fault: dereferencing a non-allocated value`

### Example 2
```c
int *largerLoc(int *x, int *y);
int main()
{
    int x = 5, y = 7;
    //  printf("%d\n", *largerLoc(&x, &y));
    int *p = printf("%d\n", *largerLoc(&x, &y));
    *p = 0; // reseting the larger value to 0

}
int *largerLoc(int *x, int *y);
{
    return *x > *y ? x : y; // return the address of the larger val
    //  &*x = x;
}
```
***
## 2022/02/08 Plenary Lectures
### Question 1
咕咕咕

### Question 2
```c
#include <stdio.h>
#include <stdbool.h>
void prSpace(int n)
{
    for (int i = 0; i < n; i++)
        printf(" ");
}
void prLeaf(int n, bool flag)
{
    if (flag)
        for (int i = 0; i < n; i++)
            printf("/");
    else
        for (int i = 0; i < n; i++)
            printf("\\");
}
int tree(int height)
{
    if (height < 1)
        return 0;

    int i, j, leaf = height - 1;
    prSpace(leaf - 1);
    printf("*\n");
    for (i = 2; i <= leaf; i++)
    {
        prSpace(leaf - i);
        prLeaf(i - 1, 1);
        printf("|");
        prLeaf(i - 1, 0);
        printf("\n");
    }
    prSpace(leaf - 1);
    printf("|\n");
    return 0;
}
int main()
{
    int height = 5;
    scanf("%d", &height);
    tree(height);
    return 0;
}
```
### Question 3
```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
int factorial(int n)
{
    if (n == 0 || n == 1)
        return 1;
    int i, ans = 1;
    for (i = 2; i <= n; i++)
        ans *= i;
    return ans;
}
int mySine(double x, double accuracy)
{
    int i = 3, sign = -1;
    double sinx = x, terms, real_sin = sin(x);
    while (fabs(real_sin - sinx) > accuracy)
    {
        terms = sign * pow(x, i) / factorial(i);
        sinx += terms;
        sign *= sign;
        i += 2;
    }
    return i;
}
int main()
{
    printf("%d", mySine(3.14159265358979 / 2, 0.01));
}
```
***
## 2022/02/09 Functions
### Scope of variables
```c
int func(int x, int y)
{
    int i = 114514, j;
    for (int i = 1; ...)
    {
        // code
    }
    printf("%d", i);    // this will print out 114514
}
```
### Global Variables
```c
extern int global;
int main()
{
    global = 2;
}
```
### Test Goldbach Conjecture
```c
int getUserInput()
{
    int number;
    bool isFirstEntry = true;
    do
    {
        if (!isFirstEntry)
            printf("Invalid input, try again\n");
        printf("Enter a number: ");
        scanf("%d", &number);
        isFirstEntry = false;
    }
    while (number % 2 != 0 || number <= 2);
}
bool testGoldbach(int num)
{
    int firstPart = 2;
    int secondPart = number - firstPart;
    if (isPrime(secondPart))
    {
        //  print the output
        return true;
    }
    else
    {
        firstPart = nextPrimeAfter(firstPart);
    }
}
int main()
{
    int number = getUserInput();
    testGoldbach(number);
    return 0;
}
```
***
## 2022/02/11 Arrays

### Declaring
`int marks [400];`

### Initializing
```c
int mark = 0;
int marks[5] =  {1, 2, 3, 4, 5};    // instead of using marks[5] = {}, marks[]={} is fine
int marks[6] = {0}; //  or int marks[6] = {};
int marks[6];
for (int i = 0; i < 6; i++)
{
    marks[i] = scanf("%d", &marks[i]);
}
```
### Example
```c
double terms[MAX+1];
for (int i = 1; i <= MAX; i++)
{
    terms[i] = pow(2, -i);
    //  Warning! We are writing into unallocated memories! C has no range checking
}
```

### Example 2: Reversing the Array
```c
for (int low = 0, high = 4; low < high; low++, high--)
{
    swap(&marks[low], &marks[high]);
}
```
### Meaning of the Array Identifier
```c
int marks[6];
marks = 7;  // Wrong! marks is the pointer pointing to the first variable of marks[6];
*marks = 7; // Correct! It is equivilent to marks[0] = 7;
```
***
## 2022/02/14 Array Continued
```c
int marks[] = {1, 2, 3, 4, 5};
//  &marks = &marks[0]
marks = &x; //wrong!
```

### Example
```c
void read(int marks[])
{
    // this is a syntatic suger! it only passes the first address of marks from the main func to void read()
}
int main()
{
    int marks[] = {1, 2, 3, 4};
    int *p = &marks, *q = &marks[3];
    int num_in_between = q - p + 1;
    if (p <= q) {}
    if (p != NULL)
    {

    }
}
void read(int *marks, int size)
{
    for (int i = 0; i < size; i++)
        scanf("%d", marks+i);
}
int main()
{
    int a[] = {1, 2, 3, 4}, *ptr = a;
    read(a, sizeof(a)/sizeof(int));
    for (int i = 0; i < 4; i++)
        printf("%d ", a[i]);
    return 0;
}
```
***
## 2022/02/16 Dynamic Memory Allocation

```c
void swap(int marks[], int i, int j)
{
    int tmep = marks[i];    // temp = *(marks+i);
    marks[i] = marks[j];    // *(marks+i) = *(marks+j);
    marks[j] = temp;        // *(marks+j) = temp;
}
int main()
{
    int marks[] = {1, 2, 3, 4, 5};
    swap(marks, 1, 2);
}
```

### Dynamic Memory Allocation
```c
int marks[500];
int size = 10;
scanf("%d", &size);
int marks[size];    // syntactic sugar, D99 stnadard
```

|                MAX                |
| :-------------------------------: |
|        Call Stack Shrink ⬇️        |
|           ............            |
| Heap (majority of memory) Grows ⬆️ |
|      Global Vars + Constants      |
|               Code                |

### Malloc
```c
#include <stdlib.h>
void *malloc(type_size * size);
// (type) *marks = (cast_type*) malloc(size * sizeof(int));
int* marks = (int*) malloc(size*sizeof(int));
*(marks + i) = 100;
```

#### Memory Leak Problem: Remember to Release Memory!
>"If you have a memory leak problem, just try to turn the computer off and on again." –––– Tech support

Nah you don't. Try ```free(marks)```!

```c
int* read(int *marks, int size)
{
    int* marks = (int*) malloc(...);
    // xxx
    return marks;
}
read(marks, size);
```

### Garbage Collection
#### Java VS C++
![Garbage Collection Meme](https://i.redd.it/8enervg2wjo51.jpg)

***
## 2022/02/18 Midterm Prep
Exam time: 100 minutes
#### 5 short questions:
- One line coding question
- Error-finding: compile-time error
- Output
- Evaluating Expressions

#### 6 long answer questions:
- Easy (aim for full marks)
- Challenging (1~2)

digit (0~9)
Number (any length)
prompt user to enter valid input
***

## 2022/02/28 Lecture 19
***Written by Wen*** [check out his GitHub Profile](https://github.com/WenOu9)
### 2D Arrays
#### Declaring
```c
const int numRows = 2;
const int numCols = 3;

int marks[numRows][numCols];

// declare when initializing
int marks[2][3] = {
    {100, 90, 80};
    {90, 80, 70}
};

// declare with for loop
for (int i = 0; i < 2; i++) {
    for (int j = 0; j < 3; j++) {
        marks[i][j] = 0; // row and column would be better variable names
    }
}
```
#### Call Stack
#####marks
| i   | j   |       // comments        |
| --- | --- | :----------------------: |
| 1   | 2   |           ...            |
| 1   | 1   |           ...            |
| 1   | 0   |           +12            |
| 0   | 2   |            +8            |
| 0   | 1   | marks+4 (int is 4 bytes) |
| 0   | 0   |     address of marks     |
| -   | -   |          main()          |

```c
// &marks[i][j] = &marks[0][0] + sizeof(int) * (i * numCols + j);

int sum(int marks[][3], int numRows, int numCols) {
    // include the "3" for the second array is important
    for () {
        for () {
            sum += marks[i][j]; 
            // syntatic sugar for *(*(marks+i)+j)
        }
    }
    return sum;
}

int main(void) {
    int marks[2][3];
    printf("%d\n", sum(marks, 2, 3));
}
```

`*marks == *&marks[0]`
For 2D arrays, we can also dereference marks[0]: 
`*marks[0] == *&marks[0][0]`
***

## 2022/03/02 2D Arrays Continued

```c
int marks[2][3];
sum(marks, 2, 3);
int sum(int marks[][3], int rows, int cols)
marks === marks[0];
*marks === *&marks[0]; // both are addresses
```

| row  |
| ---- |
| int* |
| int* |
| int* |

first row:
| int | int | int | int |
| --- | --- | --- | --- |

```c
int **marks = (int**) malloc(rows * sizeof(int*));
for (int i = 0; i < rows; i++) {
    marks[i] = (int*) malloc(cols * sizeof(int));
    // marks[i] == *(marks + i)
}

for (int i = 0; i < rows; i++) {
    free(marks[i]);
}
free(marks);
```
***

## 2022/03/04 String
### string cells
 | 'H' | 'E' | 'L' | 'L' | 'O' | '\0' |
 | --- | --- | --- | --- | --- | ---- |

### Declaration & Playing Around
```c
char s[] = {'h', 'i', '\0'};

char s[] = "Hello";
char *t = "Hello";
t = "hello";
char *t = (char*) malloc(6 * sizeof(char));
char *temp = t;
t = "the quick brown fox jumps over a lazy dog";
free(temp);
```
|                 MAX                 |
| :---------------------------------: |
|         Call Stack Shrink ⬇️         |
|            ............             |
|  Heap (majority of memory) Grows ⬆️  |
|       Global Vars + Constants       |
| Including Strings, which is a const |
|                Code                 |

***
## 2022/03/07 String Continued
```c
int countBlanks(const char *s)
{
    // code
}
int main()
{
    // changable address, const char
    const char *s; // equivalent to char const *s;
    s = malloc(5);
    s[0] = 'H'; // compile time error

    // changable char, const address
    char* const s;

    // both fixed
    const char* const s;
}
```
### String I/O
```c
char *s = "Hello World!";

// output
printf("%s", s);
printf("%.5s", s); // print first 5 characters
puts(s); // append a '\n' character;

// input
scanf("%s", s);
// skips leading white spaces, till next white space
char *s = (char*) malloc(6);
char s[6]; // buffer overflow

// reads till arrives at '\0'. still unsafe, doesn't know the length of the input either
gets(s);

// use sizeof(s) if s is static;
fgets(s, num_of_chars_including_\0, stdin);
```
### Create Our Own Input Func!
```c
char *getStringFromInputSafely(char *s, int size)
{
    int i = 0;

    // returns character user enters
    char c = getchar();
    while (i < size - 1 && c != '\n')
    {
        s[i++] = c;
        c = getchar();
    }
    /* or
    char c;
    while (i < size - 1 && (c = getchar()) != '\n')
    {
        s[i++] = c;
    }
    */
    s[i] = '\0';
    return s;
}
int main()
{
    char s[6];
    // char *s = malloc(6*sizeof(char));

    // question: how can we allocate memory dynamically 
    // if we don't know how many characters we have?

    printf("%s", getStringFromInputSafely(s, 6));

}
```

***
## 2022/03/08 Plenary Lecture
### Arrays
> ### stack & Heaps
> - stack: where our local variables are stored
> - heap: where dynamic memory is accessed

### 2019 Final Q9
> Question 9 [8 Marks]
Write a function,countLetters, that counts the number occurrences of each alphabetical letter found in a string. The function has two parameters: a string (i.e., char *) and an array of integers.
The string should not be modified and can be any length. You may assume that the string is null- terminated and all letters are lower case. The string may contain characters that are not part of the alphabet (e.g., 0, 1, !, &, etc). The integer array has a size of 26, one for each letter in the alphabet. The first index corresponds to the letter 'a',thesecond index to the letter 'b', and so on. You may assume that, initially, all 26 elements in the array have a value of zero.
You must abide by the following constraints. Failure to meet a constraint will result in a grade of zero for this question.
> 1. You cannot modify the characters inside the string.
> 2. You cannot create any other data structures (e.g., array, linked list, etc).
> 3. Your function must only access valid indices of the array.
> 4. You cannot call any functions in your implementation.
> 
> An example of one run of the program is below. You only need to implement the countLetters function. Assume a main function (that reads in a string, calls your function, and outputs the integer array) already exists.
> Enter a sentence: hello, world
The frequency that each lower case letter appears is:
d: 1
e: 1 
h: 1 
l: 3
o:2 
r: 1 
w: 1
### Solution
```c
#include <stdio.h>
#define MAX_STRING_LENGTH 80
#define ALPHABET_LENGTH 26
void countLetters(char *s, int count[]) {
    while (*s != '\0') {
        int index = *s - 'a';
        if (index >= 0 && index < 26) {
            count[index]++;
        }
        s++;
    }
}
int main() {
    char str[MAX_STRING_LENGTH];
    int count[30] = {0};
    printf("Enter your letters: ");
    fgets(str, MAX_STRING_LENGTH, stdin);
    countLetters(str, count);

    printf("Frequency each letter occurs is: \n");

    for (int j = 0; j < ALPHABET_LENGTH; j++) {
        if (count[j] > 0)
            printf("%c: %d\n", j+'a', count[j]);
    }
    return 0;
}
```

### 2018 Final Q15
>Write a C function called sortOddEvenO that rearranges the order of the elements in an integer array such that all odd numbers are to the left of all even numbers. The function has two parame- ters: a pointer to the integer array and an integer specifying the number of elements in the array. The odd numbers can be in any order, as long as they are all to the left of any even number, and the even numbers can be in any order, as long as they are all to the right of any odd number.
For example, if the elements of the array initially are: `1 4 6 5 9 3 8 2`
then after sortOddEvenO processes the array, the elements may become: `1 3 9 5 6 4 8 2`
Note: In your solution, you may not declare or. use another array.
### Solution
```c
#include <stdio.h>
void sortOddEven(int input[], int size) {
    int left = 0, right = size - 1;
    while (left < right) {
        while (left < right && input[left] % 2 == 1)
            left++;
        while (left < right && input[right] % 2 == 0)
            right--;
        // swap(&input[left], &input[right]);
        int temp = input[left];
        input[left] = input[right];
        input[right] = temp;
    }

}
int main() {
    int a[] = {1, 2, 5, 4, 6};
    int n = sizeof(a) / sizeof(int);
    sortOddEven(a, n);
    for (int i = 0; i < n; i++)
        printf("%d ", a[i]);
    return 0;
}
```

### 2020 Final Q5
>An integer with the type unsigned int has 32 bits, and stores values from 0 to $2^{32-1}$. Write a function unsigned int generateInt(int list[], int size), that takes a list of distinct integers valued from 0 to 31 as its first parameter, and the size of such a list as its second parameter, and returns an integer with the corresponding bits set as 1.
For example, if the input list is the array `[0, 3, 4, 9]` with a size of 4, the function will return `1000011001` in binary (base-2) form, as bit 0, bit 3, bit 4, and bit 9 (counting from the least significant bit on the right) are set to 1. The following main() function will print result = 219 as the result `1000011001` is printed in hexadecimal form by using the format specifier `%x`:
```c
// To be continued
```

***
 ## 2022/03/09
```c
char *s = "sample";
printf("%s", s);

// print substring from s[0] to s[2]
printf("%s", s + 2);

// print s[0] + 2
printf("%c", *s + 2);
```

### Strlen: return length of the string
```c
#include <string.h>
unsigned int strlen(const char *s);
printf("%u", strlen(s));
```

### Implement our own stringLength!
```c
int stringLength(const char *s)
{
    int i = 0;
    // s[i] hits '\0' and jumps out of the loop
    // since '\0' == unsigned int 0
    while (s[i]) i++;
    return i;
}
```
| Stack | relative address |
| :---: | :--------------: |
| '\0'  |     6 <-- t      |
|  'e'  |        5         |
|  'l'  |        4         |
|  'p'  |        3         |
|  'm'  |        2         |
|  'a'  |        1         |
|  's'  |     0 <-- s      |
```c
// pointer arithmetic ver.
int stringLength(const char *s)
{
    const char *t = s;
    while (*t) t++;
    return t - s;
}

// dynamic memory ver.
int stringLength(const char *s)
{
    char *s = malloc(6*sizeof(char));
    // check if memory allocation is successful
    if (s != NULL)
    {
        // do the work
    }
}
```
### strcpy
```c
// definition
char *strcpy(char *dest, const char *src)
{
    int i = 0;
    while (src[i]) dest[i] = src[i++];
    
    // add '\0' to the end of the string
    dest[i] = '\0';
    return dest;
}

// pointer arithmetic ver.
char *strcpy(char *dest, const char *src)
{
    char *t = dest;
    /*
    while (*dest) *dest++ = src++;
    *dest = '\0';
    */

    while ((*dest = *src) != '\0)
        dest++, src++;
    
    // nerd ver., don't use!
    // while (*dest++ = *src++)
    return t;
}

```
## 2022/03/11 String Functions
### strcpy vs. strncpy
```c
// not safe!
// char *strcpy(char *dest, const char *src);

// safe
// char *strncpy(char *dest, const char *src, size_t n);

int main()
{
    char s[6];
    // copy the '\0' character here
    strncpy(s, "Hello", 6);
    return 0;
}
```
```c
int main()
{
    char s[] = "Hello World";
    // does not copy the '\0' character
    strncpy(s, "Hello", 5);
    return 0;
}
```
### Design Our Own String Copy Function!
```c
char *stringSafeCopy(char *dest, const char *src, int n)
{
    for (int i = 0; i < n && (dest[i] = src[i]) != '\0'; i++)
    {;}
    return dest;
}
```
### strcat vs. strncat
```c
// char *strcat(char *dest, const char *src);
int main()
{
    char s1[13] = "Hello";
    char *t = "World!";

    // would print "HelloWorld!"
    puts(strcat(s1, t));

    // the string is "HelloWorld\0"
    puts(strncat(s1, t, 6));
    return 0;
}
```
### strcmp vs. strncmp
```c
// int strcmp(const char *p, const char *q);
int main()
{
    // strcmp("abc", "bcd") < 0
    // strcmp("sam", "same") < 0
    // strcmp("114514", "114514") == 0
    // strncmp("sam", "same", 3) == 0
}
```
## Convert string to numbers: atoi vs. atof
```c
// int atoi(const char *s);
int main()
{
    printf("%d", atoi("314"));
    printf("%.2lf", atof("3.14"));
}
```
### strchr
```c
// return the first occurrence of char c in string s
// strchr(const char *s, char c);
char *s = "Hello";
char *p = strchr(s, 'e');
printf("%s\n%d", p, p-s);

// print out all of the occurrences
p = s;
while (p != NULL)
{
    p = strchr(p+1, 'e');
}
```

## 2022/03/14 String Continued
### strstr
```c
// char *strstr(const char *s1, const char *s2);
// returns an address to first occurrence of s2 in s1
char *s1 = "Hello again, my name is...", *s2 = "again";
strstr(s1, s2);
```
### self Implementation
```c
// use strncmp!
char *strstr(const char *s1, const char *s2)
{
    char *p = s1;
    int n1 = strlen(s1), n2 = strlen(s2);
    while (*p != '\0' && strncmp(p, s2, n2) && n-(p-s1) >= n2)
    {
        p++;
    }
    if (*p == '\0') return NULL;
    return p;
}
```
### Array of Strings
```c
// not commonly used
// we can write into  this character array
char months[][10] = {"January", "February", /* ... */ "September", /* ... */ "December"};

// Alternative version
char *months[12];
months[0] = "January"; // note that we cannot write into it
```
### Command-line Parameters
```c
// argc stands for argument count
// argv stands for argument vector
int main(int argc, char *argv[])
{
    if (argc != 3)
    {
        printf("Usage: ls .....\n");
        // this terminates the whole program
        exit(0);

        // this only terminates the function
        return 0;

        // for more information about the difference between return 0 and exit(0) check out the link below
    }
}
```
[Difference Between return 0 and exit(0)](https://stackoverflow.com/questions/3463551/what-is-the-difference-between-exit-and-return)

```c
int main(int argc, char *argv[])
{
    for (int i = 0; i < argc; i++)
    {
        printf("%s ", argv[i]);
        // wrong version
        // printf("%s ", *argv+i);
    }
    return 0;
}
```
## Conversation With Leo
Use `macro`
[#if, #elif, #else, and #endif directives ](https://docs.microsoft.com/en-us/cpp/preprocessor/hash-if-hash-elif-hash-else-and-hash-endif-directives-c-cpp?view=msvc-170)
```c
#if condition
// code
#elif condition
// code
#else
// code
#endif

// condition must be satisfied
assert(/* condition */);
```

## 2022/03/16 Recursion
![Recursion Meme](https://preview.redd.it/0wap3cp4khm01.jpg?width=960&crop=smart&auto=webp&s=a601188a147154b9d284ad9bcb279c6f56209614)
### Cutting the cake
```c
cutCake(chunk)
{
    // base case
    if (chunk < loog)
        return;
    else {
        // cut into two halves
        cutCake(chunk/2);
    }
}
```
### Example 1
f(n) = {
    2 * f(n-1) + 1, n > 0
    3, n = 0
}
```c
int f(int n)
{
    if (n == 0) return 3;
    return 2 * f(n-1) + 1;
}
```
### factorial
```c
int factorial(int n)
{
    if (n < 0)
    {
        printf("you fucked up");
        return 114514;
    }
    else if (n == 0 || n == 1) return 1;
    else return n * f(n-1);
}
```
### printRow
```c
void printRow(int n)
{
    if (n <= 0)
    {
        printf("\n");
        return;
    }
    else
    {
        printf("*");
        printRow(n-1);
    }
}
```
### printTriangle
```c
void printTriangle(int n)
{
    if (n > 0) {
        // swap the two rows if print a reversed triangle
        printTriangle(n-1);
        printRow(n);
    }
}
```
## 2022/03/18 Recersion Continued
### Example: Print Pattern
    ****
    ***
    **
    *
    **
    ***
    ****

```c
void printPattern(int n)
{
    if (n == 1) printRow(1);
    else {
        printRow(n);
        printRow(n-1);
        printRow(n);
    }
}
```
### Example: Power
```c
double power(double x, int n)
{
    if (n < 0) return 1 / power(x, -n);

    if (n == 0 && x != 0) return 0;
    else return -1;
    
    if (n == 1) return x;
    else {
        if (n % 2 == 0)
            return power(x, n/2);
        else
            return power(x, 1) * power(x, n/2);
    }
}
```
## 2022/03/21 Recursion Continued & Structures
### Strings with Recursion
```c
bool isPalindromeHelper(char *s, int low, int high);
bool isPalindrome(char *s)
{
    /* base cases: 
        isPalindrome("x") == true;
        isPalindrome("") == true;
    */
    // prof want to use pointers, so we have to (really?)
    // pass in two additional parameters into func
    // try global variables
    // (actually don't, cuz could cause additional problems to other funcs)

    return PalindromeHelper(s, 0, strlen(s) - 1);
}
bool isPalindromeHelper(char *s, int low, int high)
{
    if (low >= high) return true;
    if (s[low] != s[high]) return false;
    return isPalindromeHelper(s, low + 1, high - 1);
}
```
### Structures
| Structure | Type   |
| --------- | ------ |
| sku       | int    |
| quantity  | int    |
| size      | char   |
| price     | double |

```c
struct entry {
    int sku, quantity;
    char size;
    couble price;
} item;
struct entry item2;
```
### Typedef
```c
typedef struct entry Entry;
Entry item3;

// c legacy codes
typedef unsigned int size_t;
typedef int* IntPointer;

typedef struct date {
    int year, month, day;
} Date;
const Date confederation = {1867, 7, 1};

Date *p = &confederation;
// dot syntax
confederation.year = 1867;
p->month = 7;   // equivalent to (*p).month = 7;

// malloc
p = (Date*) malloc(sizeof(Sate));
free(p);
```

# 2022/03/23 Linear Lists
Linear lists is an Abstract data type (ADT)

![Always has been](https://preview.redd.it/oxoudjscrro81.jpg?width=960&crop=smart&auto=webp&s=6d7360b9f7fa8e5a3aacd6c1886338ff3ff37f6b)
### Interface
A collection of functions. (The following is a java example)
![A little bit away from java:](https://media.geeksforgeeks.org/wp-content/uploads/20200624222851/List-and-ArrayList-in-Java.png)

methods:
>create a new empty list;
insert into the list (beginning, middle, end)
search
deleteAll
print

### Linked List
![Linear List Example](https://cdn.programiz.com/sites/tutorial2program/files/linked-list-concept.png)

#### Implementation
```c
// made possible by multi-pass compilers
typedef struct node
{
    int data;
    struct node *next;
} List;
```