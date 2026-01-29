## What is a loop in Java?

### A loop is a programming structure that allows you to execute the same block of code repeatedly as long as a given condition is true.

#### In simple words:
- 👉 Loops are used to avoid writing the same code again and again.

Example idea:
- If you want to print numbers from 1 to 10, instead of writing 10 print statements, you use a loop.

- Why loops are used

- Loops are used to:

- repeat tasks automatically

- reduce code length

- process arrays and collections

- perform calculations multiple times

- save time and avoid errors

### How many types of loops are there in Java?

#### Java has 4 main types of loops.

### 1. for loop

Used when you know the number of iterations in advance.

Example:
```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}
```

### 2. while loop

Used when the condition is checked first and the number of iterations is not fixed.

Example:

int i = 1;
while (i <= 5) {
    System.out.println(i);
    i++;
}

### 3. do-while loop

#### Used when the loop must execute at least once, even if the condition is false.

Example:
```java
int i = 1;
do {
    System.out.println(i);
    i++;
} while (i <= 5);
```
### 4. for-each loop

Used to traverse arrays and collections easily.

Example:
```java
int[] numbers = {1, 2, 3, 4, 5};
for (int num : numbers) {
    System.out.println(num);
}
```
Summary table (easy to remember)

- for loop → fixed number of times

- while loop → condition checked first

- do-while loop → runs at least once

- for-each loop → used for arrays and collections

| Loop Type         | When to Use                                  | Condition Checking                  | Executes At Least Once? |
| ----------------- | -------------------------------------------- | ----------------------------------- | ----------------------- |
| **for loop**      | When you know the exact number of iterations | Before loop body (Entry-controlled) | No                      |
| **while loop**    | When the condition must be checked first     | Before loop body (Entry-controlled) | No                      |
| **do-while loop** | When the loop must run at least once         | After loop body (Exit-controlled)   | Yes                     |
| **for-each loop** | When iterating over arrays or collections    | Internally handled                  | No                      |
