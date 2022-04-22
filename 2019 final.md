# [2019 Final Exam](https://exams.skule.ca/exams/bulk/20191/APS105S_2019_COMPUTERFUNDAMENTALS_E.pdf)
Created by Henry Li.  
Assisted by Lzh. [checkout his ~~GayHub~~ GitHub](https://github.com/LinZhihao-723)
## Q1
```c
struct AnimalSizes {
    char name[50];
    double length;
} snakes[] = { {"Anaconda", 3.7}, {"Python", 2.4} };
```

## Q2
```c
bool inputIsBefore = strcmp(inputArtist, artist) < 0;
```

## Q3
> Quicksort algorithm uses partitioning, and the LHS of the pivot is less than pivot, while the RHS is greater than pivot.
> Therefore, it is observed that 71 is could be the pivot of this question.

## Q4
(a)
```c
int i = 0;
while (i < MAX) {
    if (jVar[i] < 3) printf("X\n");
    i++;
}
```
(b)
```c
int i = 0;
do {
    if (i < MAX && jVar[i] < 3) printf("X\n");
    i++;
} while (i < MAX);
```

## Q5
(a)
| Method         | OK? | Reason                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| -------------- | --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Selection Sort | No  | Time complexity is $O(n^2)$. However this method is better compared to bubble sort & insertion sort, because it uses compare instead of exchanging values in sorting, therefore "faster". However, it is not fast enough given data in large quantity.                                                                                                                                                                                                    |
| Bubble sort    | No  | Time complexity is $O(n^2)$, uses a lot of swapping when sorting. Given data in large quantity, the time complexity of this algorithm is $O(n^2)$. Reason: uses two for loops, each loop costs linear time. $O(n\times n) = O(n^2)$.                                                                                                                                                                                                                      |
| Insertion sort | No  | Same as bubble sort, uses a lot of swapping when during the process. Time complexity is also $O(n^2)$.                                                                                                                                                                                                                                                                                                                                                    |
| Quicksort      | OK  | The average time complexity is $O(n\log{n})$, much better than the previous ones. It uses the concept of divide and conquer, which is a key idea in merge sort (quicksort itself is a special case of merge sort). Since every time it divides the problem into halves, the time complexity for dividing is $\log_2{n}$, and it cost constant time to sort all n elements, so the overall time complexity is $O(log{n} \times 1 \times n) = O(n\log{n})$. |

(b) Quicksort of course.

## Q6
| Variable   | Value |
| ---------- | ----- |
| i          | 2     |
| j          | 5.4   |
| k          | 5     |
| x          | 17    |
| myArray[0] | 1     |
| myArray[1] | 4     |
| myArray[2] | 4     |
| myArray[3] | 4     |
| myArray[4] | 5     |
| myArray[5] | 6     |

## Q7
```c
#include <math.h>
const double D2R = 3.1415926535 / 180.0;
// rectangular coordinate structure 
typedef struct rectV {
    double x, y;
} RectCoor;
// polar coordinate structure 
typedef struct polarC { 
    double r, theta;
} PolarCoor;

RectCoor polToRec(PolarCoor polin) {
    RectCoor rv;
    double theta = polin.theta * D2R;
    rv.x = polin.r * cos(theta);
    rv.y = polin.r * sin(theta);
    return rv;
}
```

## Q8
```c
int factorial(int n) {
    if (n == 0 || n == 1) return 1;
    int result = 2;
    for (int i = 3; i <= n; i++)
    { result *= i; }
    return result;
}
int main(void) {
    int const RowDesired = 8;
    int pascalRow[8];
    for (int i = 0; i <= 8; i++) {
        pascalRow[i] = factorial(8) / (factorial(i) * factorial(8 - i));
    }
}
```

## Q9
```c
int countLetters(char *s, int count[]) {
    memset(count, 0, sizeof(count));
    if (s == NULL) return 1919810;
    for (int i = 0; i < strlen(s); i++) {
        if (s[i] >= 'a' && s[i] <= 'z') {
            count[s[i] - 'a']++;
        }
    }
    return 114514;
}
```

## Q10
```c
Node *lcaHelper(Node *p, int na, int nb) {
    if (p == NULL) { return NULL; }
    if (na > nb) return lcaHelper(p, nb, na);
    // base case: na <= p <= nb
    if (p->data >= na && p->data <= nb)
    { return p; }
    
    if (p->data < na)
    { return lcaHelper(p->right, na, nb); }
    return lcaHelper(p->left, na, nb);
}
```

## Q11
```c
void bubbleSortLinkedList(LinkedList *list) {
    current = list->head;
    int count = 0;
    while (current != NULL)
    {
        current = current->next;
        count++;
    }
    if (count == 0 || count == 1) return;
    for (int i = count; i > 0; i--) {
        Node *current = list->head;
        Node *next = current->next;
        for (int j = 0; j < i - 1; j++) {
            if (next->data < current->data) {
                int temp = next->data;
                next->data = current->data;
                current->data = temp;
            }
            current = next;
            next = next->next;
        }
    }
```

## Q12
```c
void initBSTree(BSTree *tree);
bool insert(BSTree *tree, int value);
typedef struct node {
    int data;
    struct node *left, *right;
} Node;
typedef struct bstree {
    Node *root;
} BSTree;

bool evensHelper(Node *current, BSTree *evenTree) {
    if (current == NULL) return false;
    if (current->data %2 == 0) {
        insert(evenTree, current->data);
    }
    evensHelper(current->left, evenTree);
    evensHelper(current->right, evenTree);
}
Node *treeWithEvens(BSTree *inputTree) {
    if (!inputTree) return NULL;
    BSTree *newTree = malloc(sizeof(BSTree));
    initBSTree(newTree);
    evensHelper(inputTree->root, newTree);
    return newTree;
}
```

## Q13
```c
void swap(char *a, char *b) {
    char temp = *a;
    *a = *b;
    *b = temp;
}
void helper(char *s, char *current) {
    if (current == '\0') {
        printf("%s\n");
        return;
    }
    for (char *p = current; *p != '\0'; p++) {
        swap(current, p);
        helper(s, current);
        swap(current, p);
    }
}
void permutate(char *str) {
    helper(str, str);
}
```

## Q14
```c
char* alignText(char* inStrings[], int lineLength) {
	char* outString; // assemble the string here
	int charcount = 0; // counts the number of characters
	// handle the first string first
	if (inStrings == NULL || strcmp(inStrings[0], ".") == 0) {
		return inStrings[0];
	}
	outString = malloc(1000000 * sizeof(char));
	strcpy(outString, inStrings[0]);
	charcount = strlen(outString);

	int i = 1;
	while (strcmp(inStrings[i], ".") != 0) {
		int length = strlen(inStrings[i]);
		// exceeds the length
		if ((charcount + length) > lineLength) {
			charcount = 0;
			strcat(outString, "\n");
		}
		// doesn't exceeds
		charcount += length;
		strcat(outString, inStrings[i]);
		i++;
	}
	strcat(outString, ".\n");
	return outString;
}
```