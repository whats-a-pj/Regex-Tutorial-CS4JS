# Regex Tutorial- Computer Science for Javascript

A quick and easy tutorial explaining a regular expression in Javascript code, with examples for using this tutorial in your own work.

## Summary

Here is an example of a Javascript string element:

### <code> const newExObj = new RegExp('hello'); </code>

The literal form would be written as such:

### <code> const newExObj = /hello/ </code>

This regex is a simple string containing 'hello' we can test it to be true or false based on what you need from 'hello'. So if you want to test where it lies in a string, if it's capitalized or if it's reversed, below I am going to show you some examples of how you can use regex to test truthiness of our regex object. Below I go over multiple ways you can match the <code> newExObj</code>'s properties. This includes examples of how you can use it with OTHER regex objects so you can easily take this tutorial to use it for your own work.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

These are used to negate a pattern:

<code> \d </code> matches any digit, equivalent to <code> [0-9] </code>

<code> \D </code> matches any character that’s not a digit, equivalent to <code> [^0-9] </code>

<code> \w </code> matches any alphanumeric character, equivalent to <code> [A-Za-z0-9] </code>

<code> \W </code> matches any non-alphanumeric character, equivalent to <code> [^A-Za-z0-9] </code>

<code> \s </code> matches any whitespace character: spaces, tabs, newlines and Unicode spaces

<code> \S </code> matches any character that’s not a whitespace

<code> \0 </code> matches null

<code> \n </code> matches a newline character

<code> \t </code> matches a tab character

<code> \uXXXX </code> matches a unicode character with code <code> XXXX </code> (requires the u flag)

<code> . </code> matches any character that is not a newline char (e.g. <code> \n </code>) (unless you use the s flag, explained later on)

<code> [^] </code> matches any character, including newline characters. It’s useful on multiline strings.

In the example above, we can target any string element and test to see if it includes 'hello'. This will come back as a boolean, either <code> true </code> or <code> false </code>. Anything inside the forward slashes <code> /</code> describes the regex pattern.

So if we ran some tests:

<code> newExObj.test('hello, my name is PJ') </code>
// this would pass as <code> true </code>, as it contains 'hello' in the exact order we are looking for, no matter if we have other string elements surrounding.

<code> newExObj.test('something here, hello something here too') </code>
// this would also pass as <code> true </code> even though we have string elements in front of the expression.

<code> newExObj.test('olleh') </code>
// this would fail and return <code> false </code>, even though it is just newExObj reversed, that is not the pattern, it is not in the correct order.


### Anchors

Anchoring can be used to match 'hello' based on wherever it is placed inside the string. You can further test if it is true based on EXACT placement of newExObj in a string. This helps to test exact matches or for loose matches based on what you need for your code to run properly.

If you used the ^ operator in front of your string element, this would test to see if the string you are testing STARTS with 'hello'.

<code> /^hello/.test('hello, my name is PJ') </code> //this would pass as <code> true </code> because hello is at the start of the string

<code> /^hello/.test('my name is PJ, hello') </code> //this would fail and return <code> false </code> because hello is at the end of the string

If you want to test that your string ENDS with 'hello' you would place a $ operator at the end of your string. So if you ran the same exact tests above, they would be reversed in truthiness.

<code> /hello$/.test('hello, my name is PJ') </code> //this would fail and return <code> false </code> because hello is at the beginning of the string

<code> /hello$/.test('my name is PJ, hello') </code> //this would pass as <code> true </code> because hello is at the end of the string

If you want newExObj to only run <code> true </code> when the string is by itself- you can combine these operators!

<code> /^hello$/.test('hello') </code> //this will return <code> true </code>

<code> /^hello$/.test('hello world') </code> //this will return <code> false </code> because you have more characters that aren't supposed to be there (' world')

### Quantifiers

Quantifiers can be used to check if a string has a digit in it, or multiple digits. This can be done using <code> \d </code> which matches any digit 0-9.

<code> /^\d+$/.test('1234') </code> //this will return <code> true </code> because it is searching for digits between 0 and 9

<code> /^\d+$/.test('4321') </code> //this will also return <code> true </code> for the same reason

<code> /^\d+$/.test('123abc') </code> //this will return <code> false </code> because this quantifier is specifically searching for digits, this contains letters

To search by length of your digits you can use what most people call a 'minimum and maximum' length. Just like so: <code> {n, m} </code>
So if you want to test your digits to be at least 2 digits but no more than 4, you would write this:

<code> /^\d{2,4}$/.test('123') </code> //this would return <code> true </code> because it is between 2 and 4 digits long

<code> /^\d{2,4}$/.test('1234') </code> //this would also return <code> true </code> because it is 4 digits long, our maximum length

<code> /^\d{2,4}$/.test('12345') </code> //this would return <code> false </code> because it is 1 digit longer than our maximum length

<code> /^\d{2,4}$/.test('1') </code> //this would also return <code> false </code> because it is 1 digit shorter than our minimum length

Further- you can leave your  <code> m </code> property blank so that you have just a minimum requirement.

<code> /^\d{2,}$/.test('123') </code> //this would return <code> true </code> because there are at least 2 digits


### OR Operator

OR Operators are super simple to use. You can use this when you want to search if multiple regex objects return <code> true </code> at a time. So say you are testing our original <code>newExObj</code> and you have another you want to test in the same context like: <code> const twoExObj = 'goodbye' </code>

You can run the test to return <code> true </code> while testing both using the OR Operator '|':

<code> /hello|goodbye/.test('hello')</code> //this will return <code> true </code> because it has 'hello'

<code> /hello|goodbye/.test('goodbye')</code> //this will also return <code> true </code> because it has 'goodbye'

<code> /hello|goodbye/.test('bye')</code> //this will return <code> false </code> because it doesn't exactly match our <code> twoExObj </code>

### Flags

Flags can be used on any regular expression for an extra search parameter when running your tests. You can use them at the end of a string in your regex literals and can combine them!

<code> g </code> matches the pattern multiple times

<code> i </code> makes the regex case insensitive

<code> m </code> enables multiline where <code> ^ </code> and <code> $ </code> match the start and end of the entire string, without <code> m </code> multiline strings only match the beginning and end of each line

<code> u </code> enables support for unicode 

<code> s </code> used for single lines, which makes <code> . </code> match new line characters as well

### Grouping and Capturing

You can create and search by a group of characters using parentheses <code> (...) </code>
So if you wanted to search by exactly 3 digits followed by some letters (alphanumeric characters)

<code> /^(\d{3})(\w+)$/.test('123') </code> //this will return <code> false </code> because it isn't followed by any alphanumeric characters

<code> /^(\d{3})(\w+)$/.test('123hello') </code> //this will return <code> true </code> because it is followed by alphanumeric characters

You can also CAPTURE a group by using <code> .match </code> instead of <code> .test </code>, and since we are 'capturing' a group- this will return an array.

<code> '123a'.match(/^(\d{3})(\w+)$/)</code> //this will return an array like so: <code> ["123a", "123", "a"] </code>

<code> 'hello'.match(/(hello|goodbye)/)</code> //this will return an array like so: <code> ["hello", "hello"] </code>

### Bracket Expressions

Bracket expressions to be put simply, are used to match singular or multiple characters. These are enclosed in square brackets as you could imagine.

<code> [abc] </code> //this would check if any of the characters match a, b or c.

<code> [a-z] </code> //this checks if any of the characters are alphanumeric and lowercase

This can be used with digits as well: <code> [0-9] </code> //which matches ANY digit from 0 to 9

### Greedy and Lazy Match

Regular expressions are 'greedy'. In simple terms, this means whenever you add more to your test, match or exec- this will continue to run your matches until the end of a string. So if you take this example specifically:

<code> /\$(.+)\s?/ </code> //it is supposed to take a dollar amount from a string like this:

<code> /\$(.+)\s?/.exec('This costs $100')[1] </code> //which takes 100. but if we were to add words:

<code> /\$(.+)\s?/.exec('This costs $100 and it is less than $200')[1] </code> //it takes the whole of it like this: <code> 100 and it is less than $200 </code>

This is due to the greedy-ness. To resolve this you have to make the regex 'lazy' by using the <code> ? </code> symbol directly after your quantifier:

<code> /\$(.+?)\s/.exec('This costs $100 and it is less than $200')[1] </code> //which again only takes 100

### Boundaries

Boundaries which are defined by the use of <code> \b </code> and <code> \B</code>, lets you inspect whether a string is at the beginning or at the end of a word

<code> \b </code> matches a set of characters at the beginning or end of a word

<code> \B </code> matches a set of characters NOT at the beginning or end of a word

<code> 'I am PJ, hello'.match(/\bhello) </code> //this array will look like this: <code> ["hello"] </code>

<code> 'I am PJ, hellow'.math(/\bhello) </code> //this array will look like this: <code> ["hello"] </code>

<code> 'I am PJ, hello'.match(/\bhello\b/) </code> //this is <code> null </code>

<code> 'oh_hello'.match(/\bhello\b/) </code> //this is <code> null </code>

### Look-ahead and Look-behind

Lookaheads match a string based on what follows it. You can use <code> ?= </code> for this operation.

<code> /PJ(?= hello)/.test('PJ is my name') </code> //this returns false as it doesn't contain hello anywhere after PJ

<code> /PJ(?= hello)/.test('My name is PJ hello') </code> //this returns true because it is followed directly with 'hello'

Lookbehinds match a string depending on what comes before another. You can use <code> ?<= </code> for this operation.

<code> /(?<=PJ) hello/.test('hello what is your name?') </code> //returns false because PJ isn't before hello at all.

<code> /(?<=PJ) hello/.test('My name is PJ and hello what is your name?') </code> //this returns true because PJ is before hello

## Author
This tutorial was written by: [PJ Rasmussen](https://github.com/whats-a-pj), who is currently attending the Edx Full Stack Web Development Bootcamp through the University of Utah. 
