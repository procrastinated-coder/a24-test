# Answers for A24 Group React questions

## JS

### Q1

 One cool new feature in JavaScript is the optional chaining operator (?.). It allows you to safely access nested properties of an object without having to check for the existence of each level of the property chain. This can greatly simplify code and reduce the number of null or undefined checks needed. For example, instead of writing code like this:

```javascript
if (person && person.address && person.address.city) {
  console.log(person.address.city);
}
```

you can write:

```javascript
console.log(person?.address?.city);
```

It will return undefined if any of the properties are not defined.```

### Q2

One interesting way to use the optional chaining operator is to use it in combination with destructuring assignment. This allows you to extract and assign values from nested objects with a single line of code.
For example, consider the following data:

```javascript
const data = {
  user: {
    name: {
      first: 'John',
      last: 'Doe'
    },
    age: 30
  }
};
```

Normally, you would have to extract the first name from the nested object like this:

```javascript
let firstName = "";
if(data.user && data.user.name){
    firstName = data.user.name.first;
}
```

But with the optional chaining operator you can use destructuring assignment to extract the first name and last name in a single line of code:

```javascript
const {first: firstName, last: lastName} = data.user?.name || {};

```

This will set firstName to "John" and lastName to "Doe" if data.user and data.user.name are defined, otherwise it will set firstName and lastName to undefined. This is a more concise and readable way to extract nested properties from an object.

### Q3

Yes there is a difference

The regular function syntax uses the function keyword to define a function, and it has its own this and arguments bindings. It also has a prototype property, which allows for inheritance and method overloading.

arrow functions use the => syntax to define a function, and they do not have their own this or arguments bindings. Instead, they inherit the this value of the surrounding scope. Arrow functions also do not have a prototype property.

### Q4

The main difference is that in the first case the value passed to the function is already incremented while in the second case the function receives the original value and the increment happens after the function call.

### Q5

A class is defined using the "class" keyword, followed by the name of the class, and the class body wrapped in curly braces. The class body can include properties (variables) and methods (functions) that are shared by all instances of the class.

Example:

```javascript
class Car {
  constructor(make, model) {
    this.make = make;
    this.model = model;
  }
  startEngine() {
    console.log(`The ${this.make} ${this.model} is starting.`);
  }
}
```
A JavaScript function is a standalone block of code that can be executed when called. A function does not have the capability to create new objects or instances like a class does. While you can use a function to create an object and add properties and methods to it, it doesn't have the same structure, syntax and built-in features that a class has.

## CSS

### Q6

CSS specificity refers to the way that browsers decide which CSS styles to apply. When multiple styles are conflicting for a single element, the browser will apply the one with the highest specificity. A general rule of thumb is that the more specific the selector, the higher its specificity value.

### Q7

It gives a particular CSS rule priority over any other rules that may conflict with it.  It is added to the end of a CSS property value and overrides any other styles that have been applied to the same element.

Overuse of !important can make your CSS difficult to maintain, as it can be hard to determine which styles are being overridden by it. Additionally, using !important can make it harder to debug your code, as it can be difficult to tell which styles are being applied

### Q8

Flex.  It is responsive and flexible.  Flexbox allows elements to be aligned in any direction (horizontally or vertically) and to be stretched or shrunk to fill available space. It also allows elements to automatically adjust their size and position based on the size of the container or the size of the screen. This makes it easy to create responsive designs that adapt to different screen sizes.  Oh and as a bonus the syntax is simple.

### Q9

Yes they are. It essentially pulls an element outside of its parent container.

### Q10

The reason that the margin from the <p> tag shows up on the parent <div> is because margins on child elements collapse with the margins of their parent elements when the parent element has no border or padding.  

To prevent this from happening, you can use one of the following methods:

Add a non-zero value for padding or a border to the parent <div>. This will cause the margins of the child elements to no longer collapse with the margins of the parent element. 

Add an overflow value other than "visible" to the parent <div>. This will also cause the margins of the child elements to no longer collapse with the margins of the parent element. 

Apply a negative margin to the parent <div> that is equal in value to the margin of the child element. This will cancel out the effect of the margin collapsing.

Add a class to the parent <div> and use the CSS property 'display:inline-block'

## Unit Tests

### Q11

Jest as a test runner and React testing library.

### Q12

Using too many mock functions can make tests hard to read and understand, and can also make it difficult to catch bugs in the code.  I have been guilty of this in the past.

### Q13

by using the `getBy` and `queryBy` functions to select the child component and then using the toHaveAttribute or toHaveProperty matchers to check if the correct properties are present.

## REACT

### Q14

```javascript

import React, { useState, useEffect } from 'react';

function LiveWidth() {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    function handleResize() {
      setWidth(window.innerWidth);
    }

    window.addEventListener('resize', handleResize);
    return () => {
      window.removeEventListener('resize', handleResize);
    };
  }, []);

  return (
    <div style={{ border: '1px solid black' }}>
      <span>{width}px</span>
    </div>
  );
}

export default LiveWidth;


```

### Q15

```javascript

import React, { useState, useEffect } from 'react';

function LiveWidthHeight() {
  const [width, setWidth] = useState(window.innerWidth);
  const [height, setHeight] = useState(0);
  
  useEffect(() => {
    function handleResize() {
      setWidth(window.innerWidth);
    }

    window.addEventListener('resize', handleResize);
    return () => {
      window.removeEventListener('resize', handleResize);
    };
  }, []);

  function handleHeightChange(event) {
    const inputValue = event.target.value;
    if (!isNaN(inputValue)) {
      setHeight(inputValue);
    }
  }

  return (
    <div style={{ border: '1px solid black', height: `${height}px` }}>
      <span>Width: {width}px</span>
      <br />
      <label>Height: 
        <input type="text" onKeyPress={handleHeightChange}/>
      </label>
    </div>
  );
}

export default LiveWidthHeight;

```

### Q16

```javascript

import React, { useState, useEffect } from 'react';

let divHeight;
window.setDivHeight = (height) => divHeight = height;

function LiveWidthHeight(props) {
  const [width, setWidth] = useState(window.innerWidth);
  const [height, setHeight] = useState(divHeight || 0);

  useEffect(() => {
    function handleResize() {
      setWidth(window.innerWidth);
    }

    window.addEventListener('resize', handleResize);
    return () => {
      window.removeEventListener('resize', handleResize);
    };
  }, []);

  function handleHeightChange(event) {
    const inputValue = event.target.value;
    if (!isNaN(inputValue)) {
      setHeight(inputValue);
    }
  }

  return (
    <div style={{ border: '1px solid black', height: `${height}px` }}>
      <span>Width: {width}px</span>
      <br />
      <label>Height: 
        <input type="text" onKeyPress={handleHeightChange}/>
      </label>
    </div>
  );
}

const withHeight = (WrappedComponent) => (props) => {
  return <WrappedComponent {...props}/>
}

export default withHeight(LiveWidthHeight);


```
