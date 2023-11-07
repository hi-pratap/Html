# Logical Questions-Java

Created: February 24, 2023 5:01 PM
Related Notes: Resume (Resume%2034f14fc8af004a4d819647130f1f1418.md), Star Pattern Java (Star%20Pattern%20Java%20763d462119884563afab1960de40077c.md)
Select: Java
Tags: Interveiw

<aside>
💡 **Asked In Interviews: -UPDATED {2023}**
1. Count Unique Character From From
2. Write a Java program to find the maximum sum subarray within an array of integers.

</aside>

---

# 💖 Logical Questions

---

### 1. Reverse String.

![Untitled](Logical%20Questions-Java%20850195ff45bd4963bfaf6466c1ad2655/Untitled.png)

### 2. Armstrong Number.

![Untitled](Logical%20Questions-Java%20850195ff45bd4963bfaf6466c1ad2655/Untitled%201.png)

### 3. Prime number.

> prime numbers can't be divided by other numbers than itself or 1. For example 2, 3, 5, 7, 11, 13, 17.... are the prime numbers.
> 

![Untitled](Logical%20Questions-Java%20850195ff45bd4963bfaf6466c1ad2655/Untitled%202.png)

### 4. Permutation of String

```java
public class StringPermuntation {
    static void printallPermutns(String str, String str2) {
        // check if string is empty or null
        if (str.length() == 0) {
            System.out.print(str2 + " ");
            return;
        }
        for (int i = 0; i < str.length(); i++) {
            // ith character of str
            char ch = str.charAt(i);
            // Rest of the string after excluding
            // the ith character
            String str3 = str.substring(0, i) + str.substring(i + 1);
            // Recursive call
            printallPermutns(str3, str2 + ch);
        }
    }

    // Driver code
    public static void main(String[] args) {
        String s = "Hello";
        printallPermutns(s, "");
    }
```

### 4. Character Count

![Untitled](Logical%20Questions-Java%20850195ff45bd4963bfaf6466c1ad2655/Untitled%203.png)

### 5. Anagrams

![Untitled](Logical%20Questions-Java%20850195ff45bd4963bfaf6466c1ad2655/Untitled%204.png)

### 6. Remove Character

![Untitled](Logical%20Questions-Java%20850195ff45bd4963bfaf6466c1ad2655/Untitled%205.png)

### Factorial Number

![Untitled](Logical%20Questions-Java%20850195ff45bd4963bfaf6466c1ad2655/Untitled%206.png)

1. Reverse Array

![Untitled](Logical%20Questions-Java%20850195ff45bd4963bfaf6466c1ad2655/Untitled%207.png)

### **[P](https://mindmajix.com/program-logics-in-java#reverse)alidrom String**

![Untitled](Logical%20Questions-Java%20850195ff45bd4963bfaf6466c1ad2655/Untitled%208.png)

![Untitled](Logical%20Questions-Java%20850195ff45bd4963bfaf6466c1ad2655/Untitled%209.png)

### Largest and Smallest In Array

![Untitled](Logical%20Questions-Java%20850195ff45bd4963bfaf6466c1ad2655/Untitled%2010.png)

# Create sub-pages

---

# Embed links

---