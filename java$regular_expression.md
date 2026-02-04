### What is Regular Expression?
A Regular Expression (Regex or RegExp) is a sequence of characters that forms a search pattern. It is used for pattern matching within strings, allowing you to search, match, and manipulate text based on specific patterns.
### Java Regex Package
In Java, the `java.util.regex` package provides classes for working with regular expressions. The two main classes in this package are:
1. `Pattern`: This class is used to define a pattern (the regex).
2. `Matcher`: This class is used to perform match operations on a character sequence using the defined pattern.
### Example of Java Regular Expression
Here's a simple example demonstrating how to use regular expressions in Java to find a pattern in a string:
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;
public class RegexExample {
    public static void main(String[] args) {
        // Define a regex pattern to search for the word "Java"
        String regex = "Java";
        // Create a Pattern object
        Pattern pattern = Pattern.compile(regex);
        // Create a Matcher object
        Matcher matcher = pattern.matcher("I love Java programming. Java is fun!");

        // Find and print all occurrences of the pattern
        while (matcher.find()) {
            System.out.println("Found the word '" + matcher.group() + "' at index " + matcher.start());
        }
    }
}
```
### output
```
Found the word 'Java' at index 7
Found the word 'Java' at index 26
```
    String regex = "Java";              // Exact match - "Java"
    String regex = "\\d+";              // One or more digits
    String regex = "[a-z]+";            // One or more lowercase letters
    String regex = "\\w+@\\w+\\.com";   // Email pattern
    String regex = "[0-9]{3}-[0-9]{4}"; // Phone number pattern

### partten class methods
- `compile(String regex)`: Compiles the given regular expression into a pattern.
- `matcher(CharSequence input)`: Creates a matcher that will match the given input against this pattern.
### matcher class methods
- `find()`: Attempts to find the next subsequence of the input sequence that matches the pattern.
- `group()`: Returns the input subsequence matched by the previous match.
- `start()`: Returns the start index of the previous match.
- `end()`: Returns the end index of the previous match.
example of regex pattern matching

## matcher class 
regular expressions in java find matches ,search and replace text based on patterns. The `Matcher` class provides methods to perform these operations, such as `find()`, `group()`, `start()`, and `end()`. You can use these methods to extract specific parts of a string that match a given regular expression pattern.  
### Example of Matcher Class
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;
public class MatcherExample {
    public static void main(String[] args) {
        String input = "My email is support@example.com and my friend's email is admin@test.org";
        String regex = "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}";
        Pattern pattern = Pattern.compile(regex);
        Matcher matcher = pattern.matcher(input);
        while (matcher.find()) {
            System.out.println("Found email: " + matcher.group());
        }
    }
}
```
### Output
```
Found email: support@example.com
Found email: admin@test.org
```
In this example, we use the `Matcher` class to find and print all email addresses in the input string that match the specified regex pattern.
### Common Regex Patterns
- `.` : Matches any single character except newline.
- `\d` : Matches any digit (0-9).
- `\D` : Matches any non-digit character.
- `\w` : Matches any word character (alphanumeric + underscore).
- `\W` : Matches any non-word character.
- `\s` : Matches any whitespace character (spaces, tabs, line breaks).
- `\S` : Matches any non-whitespace character.
- `^` : Matches the beginning of a line.
- `$` : Matches the end of a line.
- `*` : Matches zero or more occurrences of the preceding element.
- `+` : Matches one or more occurrences of the preceding element.
- `?` : Matches zero or one occurrence of the preceding element.
- `{n}` : Matches exactly n occurrences of the preceding element.
- `{n,}` : Matches n or more occurrences of the preceding element.
- `{n,m}` : Matches between n and m occurrences of the preceding element.
### Example of Character Class
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;
public class CharacterClassExample {
    public static void main(String[] args) {
        String input = "cat, bat, rat, mat, hat";
        String regex = "[bcr]at"; // Matches 'bat', 'cat', 'rat'
        Pattern pattern = Pattern.compile(regex);
        Matcher matcher = pattern.matcher(input);
        while (matcher.find()) {
            System.out.println("Found word: " + matcher.group());
        }
    }
}
```
### Output
```
Found word: cat
Found word: bat
Found word: rat
```
In this example, the character class `[bcr]` matches any one of the characters 'b', 'c', or 'r' followed by 'at'.
## quantifiers
Quantifiers in regular expressions specify how many times an element in the pattern can occur. They help define the quantity of characters to match in a string.
### Example of Quantifiers
```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;
public class QuantifierExample {
    public static void main(String[] args) {
        String input = "aa aaaa aaa aaaaaa a";
        String regex = "a{2,4}"; // Matches 'aa', 'aaa', 'aaaa'
        Pattern pattern = Pattern.compile(regex);
        Matcher matcher = pattern.matcher(input);
        while (matcher.find()) {
            System.out.println("Found match: " + matcher.group());
        }
    }
}
```
### Output
```
Found match: aa
Found match: aaaa
Found match: aaa
Found match: aaaaaa
```
In this example, the quantifier `{2,4}` specifies that the letter 'a' should appear at least 2 times and at most 4 times in a row to be considered a match.
