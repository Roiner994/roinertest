# JS Developer Coding Exemplar

## Instructions
This coding exemplar is designed to highlight your skills and areas of expertise with the JS language in general. We rely mainly on JS as our front-end technology of choice. Because of this, it's important that developers have a well-rounded understanding of the JS language and its newest specifications (ES6/ES7).

Please complete the following questions to the best of your ability. If you are unable to solve a question, please indicate as such. You should feel free to use any online resources to solve these questions; after all, we expect that our developers will use their problem-solving skills at work! Some questions are intended to be difficult, while others are meant to be easy or obvious. Please post your answers in a Gist, using Markdown format, and send the link for review.

This exercise should take approximately one hour to complete.

Good luck!

## Question 1
You've been tasked with identifying a string that contains the word "superman" (case insensitive). You've written the following code:
```js
function validateString(str) {
    if (!str.toLowerCase().indexOf('superman')) {
        throw new Error('String does not contain superman');
    }    
}
```

The described function does not work with any of the cases by the operator (!) Within the if. The index function of Returns an integer value if it finds the word or -1 if it does not find it, denying that value obtains false and will never enter the exception unless index of Return 0 is false in this case Denying it returns true for what goes into the exception, so it does not work for any of the 2 cases as it is not evaluating correctly.
the solution is:

```js
function validateString(str) {
    if (str.toLowerCase().indexOf('superman') === - 1) {
        throw new Error('String does not contain superman');
    }
    console.log('String does contain superman')
}
```


QA has come to you and said that this works great for strings like "I love superman", but an exception is generated for strings like "Superman is awesome!", which should not happen. Explain why this occurs, and show how you would solve this issue (you must use `indexOf()` in your answer).

## Question 2
You're given a sorted index array that contains no keys. The array contains only integers, and your task is to identify whether or not the integer you're looking for is in the array. Write a function that searches for the integer and returns true or false based on whether the integer is present. Describe how you arrived at your solution.

R) The shortest option is to use array.includes (number to look for), but since the exercise speaks of a sorted index array that contains no keys and of writing a function, the most optimal is the binary search function in the case of the ordered arrangements where the central item if it is the one that is being searched for returns true if it is not compared if the element is greater or less than the central item to discard half of the elements, this process is repeated until finding the result, in case finding nothing returns false.

```js
const searchInArray = (value, list) => {
    let first = 0;
    let last = list.length - 1;
    let middle;
    while (first <= last){
        middle = Math.floor((first + last) / 2 );
        if (list[middle] == value )
            return true;
        else if (list[middle] > value)
            last = middle - 1;
        else
            first = middle + 1;
    }
    return false;
}
```



## Question 3
Write a function that takes a phone number in any form and formats it using a delimiter supplied by the developer. The delimiter is optional; if one is not supplied, use a dash (-). Your function should accept a phone number in any format (e.g. 123-456-7890, (123) 456-7890, 1234567890, etc) and format it according to the 3-3-4 US block standard, using the delimiter specified. Assume foreign phone numbers and country codes are out of scope.

*Note:* This question CAN be solved using a regular expression, but one is not REQUIRED as a solution. Focus instead on cleanliness and effectiveness of the code, and take into account phone numbers that may not pass a sanity check.

R) with regular expression
```js
const formatPhoneNumber = (number, delimiter = '-') => {
    let result = number.replace(/[^\d]/, '');
    let phone = '';
    
    for (var i = 0; i < result.length; i++){
        phone = i === 2 || i === 5 ? phone + result[i] + delimiter : phone + result [i];
    }
    return phone;
}
```
withouth regular expression
```js
const formatPhoneNumber = (number, delimiter = '-') => {
    let result = '';
    let phone = '';
    for (var i =0; i < number.length; i++){
        result = !isNaN(Number(number[i])) && (number[i] !== ' ') ? result + number[i] : result;
    }
    for (var i = 0; i < result.length; i++){
        phone = i === 2 || i === 5 ? phone + result[i] + delimiter : phone + result [i];
    }
    return phone;
}
```

## Question 4
Write a complete set of unit tests for the following code:

```js

function fizzBuzz(start = 1, stop = 100)
{
    let result = '';
    
    if (stop < start || start < 0 || stop < 0) {
        throw new Error('Invalid arguments');
    }
    
    for (let i = start; i <= stop; i++) {
        if (i % 3 === 0 && i % 5 === 0) {
            result += 'FizzBuzz';
            continue;
        }
        
        if (i % 3 === 0) {
            result += 'Fizz';
            continue;
        }
        
        if (i % 5 === 0) {
            result += 'Buzz';
            continue;
        }
        
        result += i;
    }
    
    return result;
}
```

R) with Jest
```js

test('fizzBuzzWithoutParameters', () => {
  expect(fizzBuzz()).toBe('12Fizz4BuzzFizz78FizzBuzz11Fizz1314FizzBuzz1617Fizz19BuzzFizz2223FizzBuzz26Fizz2829FizzBuzz3132Fizz34BuzzFizz3738FizzBuzz41Fizz4344FizzBuzz4647Fizz49BuzzFizz5253FizzBuzz56Fizz5859FizzBuzz6162Fizz64BuzzFizz6768FizzBuzz71Fizz7374FizzBuzz7677Fizz79BuzzFizz8283FizzBuzz86Fizz8889FizzBuzz9192Fizz94BuzzFizz9798FizzBuzz');
});

test('fizzBuzzMinorEnding', () => {
  expect(fizzBuzz(10,1)).toThrow('Invalid arguments');
});

test('fizzBuzzStartCero', () => {
  expect(fizzBuzz(0,100)).toThrow('Invalid arguments');
});

test('fizzBuzzEndCero', () => {
  expect(fizzBuzz(100,0)).toThrow('Invalid arguments');
});

test('FizBuzzWithParameters', () => {
  expect(fizzBuzz(1,10)).toBe('12Fizz4BuzzFizz78FizzBuzz');
});

```

## Question 5
I have an array of file names:

```js
const files = [
    '/src/common/api.js',
    '/src/common/preferences.js',
    '/src/styles/main.css',
    '/src/styles/base/_base.scss',
    '/src/assets/apple-touch-icon-57.png',
];
```

Below is a mixed list of specific file names, as well as file paths, that should be excluded. For example, ALL files under a file path should be excluded, but if the value is an actual file name, only that specific file should be excluded. 

```js
const exclude = [
    '/src/styles/',
    '/src/assets/apple-touch-icon-57.png',
];
```

For example, you'll want to exclude the styles directory (and all files in it), but ONLY the `apple-touch-icon-57.png` file.

Devise a method for applying the exclusion list against the file list WITHOUT nested `forEach()` loops.

R)
```js
const searchFile = (file, exclude) => {
    for (var i=0; i < exclude.length; i++){
        if(exclude[i].indexOf('.') !== -1){
            if(exclude[i] == file)
                return false;
        }else{
            if(file.indexOf(exclude[i]) !== -1 )
                return false;
        }
    }
    return true;
}

const excludeFiles = (files, exclude) => (files.filter( file => searchFile(file,exclude)) );

const result = excludeFiles(files,exclude);

```


## Question 6

Write a function that would generate a hex color code (`#f1f2f3`) from the full name of a person. It should always generate the same color for a given name. Describe how you arrived at your solution.

```js
const name = 'John Doe';
const color = getColorFromName(name); // e.g. #9bc44c
```

R)
```js
const getColorFromName = (name) => {
    let hash = 0;
    for var (i = 0; i < name.length; i++){
        hash = name.chartCodeAt(i) + ((hash << 5) - hash);
    }
    let color = '#';
    for var (i = 0; i < 3; i++){
        var value = (hash >> (i * 8)) & 0xFF;
        color += ('00' + value.toString(16).substr(-2));
    }
    return color;
}
```


## Question 7

Considering the following code in a page that has six buttons:

```js
const nodes = document.querySelectorAll('button');
for (let i = 0; i < nodes.length; i++) {
   nodes[i].addEventListener('click', function() {
      console.log(`You clicked button #${i}`);
   });
}
```

R)
The results are “You have clicked on button # 0” for the first button and “You have clicked on button # 3” for the fourth button, this is because the querySelectorAll gets a list of all the button elements in the document, then when traversing them the variable i begins at zero because the arrangements are iterated from the 0 position, then an event is assigned to each button that indicates its position in the arrangement. Therefore the results are those described above.


What will be printed on the console if a user clicks the first and the fourth button in the list? Explain why.


## Question 8

Write a function that determines if a given argument is array-like, in the sense that it is iterable.

```js
isIterable(null); // false
isIterable('hello world'); // true
isIterable(document.querySelectorAll('.error-message')); // true
```
R)The Symbol.iterator symbol specifies the default iterator of an object.
```js
const isIterable = (obj) => {
    if(obj == null)
        return false;
    return typeof obj[Symbol.iterator] === 'function';
}
```