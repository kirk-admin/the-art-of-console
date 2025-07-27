# Complete Console API Guide - From Basic to Advanced

## Table of Contents
1. [Basic Console Methods](#basic-console-methods)
2. [Intermediate Console Methods](#intermediate-console-methods)
3. [Advanced Console Methods](#advanced-console-methods)
4. [Console Formatting](#console-formatting)
5. [Console Grouping](#console-grouping)
6. [Console Timing](#console-timing)
7. [Console Profiling](#console-profiling)
8. [Console Assertions](#console-assertions)
9. [Console Table](#console-table)
10. [Console Styling](#console-styling)
11. [Console Utilities](#console-utilities)
12. [Browser-Specific Console Features](#browser-specific-console-features)
13. [Best Practices](#best-practices)

---

## Basic Console Methods

### 1. console.log()
**Description**: Outputs a message to the console
```javascript
console.log("Hello World");
console.log("User:", { name: "John", age: 30 });
console.log("Array:", [1, 2, 3, 4, 5]);
```

### 2. console.warn()
**Description**: Outputs a warning message with yellow styling
```javascript
console.warn("This is a warning message");
console.warn("Deprecated function called");
```

### 3. console.error()
**Description**: Outputs an error message with red styling
```javascript
console.error("This is an error message");
console.error("Failed to fetch data:", error);
```

### 4. console.info()
**Description**: Outputs an informational message with blue styling
```javascript
console.info("This is an informational message");
console.info("Application started successfully");
```

### 5. console.debug()
**Description**: Outputs a debug message (only visible when debug level is enabled)
```javascript
console.debug("Debug information");
console.debug("Variable value:", someVariable);
```

---

## Intermediate Console Methods

### 6. console.clear()
**Description**: Clears the console
```javascript
console.clear();
// Clears all console output
```

### 7. console.count()
**Description**: Counts the number of times this line has been called
```javascript
console.count("Button clicked");
console.count("API call");
console.countReset("Button clicked"); // Reset the counter
```

### 8. console.countReset()
**Description**: Resets the counter for a specific label
```javascript
console.count("User action");
console.count("User action");
console.countReset("User action");
console.count("User action"); // Will start from 1 again
```

### 9. console.trace()
**Description**: Outputs a stack trace to the console
```javascript
function firstFunction() {
    secondFunction();
}

function secondFunction() {
    thirdFunction();
}

function thirdFunction() {
    console.trace("Stack trace from thirdFunction");
}

firstFunction();
```

---

## Advanced Console Methods

### 10. console.group()
**Description**: Creates a new inline group in the console
```javascript
console.group("User Details");
console.log("Name: John Doe");
console.log("Age: 30");
console.log("Email: john@example.com");
console.groupEnd();
```

### 11. console.groupCollapsed()
**Description**: Creates a collapsed inline group in the console
```javascript
console.groupCollapsed("API Response Data");
console.log("Status: 200");
console.log("Data:", responseData);
console.groupEnd();
```

### 12. console.groupEnd()
**Description**: Exits the current inline group
```javascript
console.group("Section 1");
console.log("Content 1");
console.group("Subsection");
console.log("Sub content");
console.groupEnd(); // Ends subsection
console.groupEnd(); // Ends section 1
```

### 13. console.table()
**Description**: Displays tabular data as a table
```javascript
// Array of objects
const users = [
    { name: "John", age: 30, city: "NYC" },
    { name: "Jane", age: 25, city: "LA" },
    { name: "Bob", age: 35, city: "Chicago" }
];
console.table(users);

// Array of arrays
const data = [
    ["Name", "Age", "City"],
    ["John", 30, "NYC"],
    ["Jane", 25, "LA"]
];
console.table(data);

// With specific columns
console.table(users, ["name", "age"]);
```

### 14. console.time()
**Description**: Starts a timer to track how long an operation takes
```javascript
console.time("API Request");
fetch('/api/data')
    .then(response => response.json())
    .then(data => {
        console.timeEnd("API Request");
        console.log("Data received:", data);
    });
```

### 15. console.timeEnd()
**Description**: Stops a timer and outputs the elapsed time
```javascript
console.time("Processing");
// Some processing code
for (let i = 0; i < 1000000; i++) {
    // Do something
}
console.timeEnd("Processing");
```

### 16. console.timeLog()
**Description**: Outputs the current value of a timer without stopping it
```javascript
console.time("Long Operation");
// First part of operation
console.timeLog("Long Operation", "First checkpoint");
// Second part of operation
console.timeLog("Long Operation", "Second checkpoint");
console.timeEnd("Long Operation");
```

---

## Console Formatting

### 17. String Substitution
**Description**: Use placeholders for formatted output
```javascript
const name = "John";
const age = 30;
const city = "NYC";

// %s for strings
console.log("Name: %s", name);

// %d or %i for integers
console.log("Age: %d", age);

// %f for floats
console.log("Score: %f", 95.5);

// %o for objects
console.log("User object: %o", { name, age, city });

// %c for CSS styling
console.log("%cStyled text", "color: red; font-size: 20px; font-weight: bold;");
```

### 18. CSS Styling with %c
**Description**: Apply CSS styles to console output
```javascript
console.log(
    "%cWelcome to our app!",
    "color: white; background: linear-gradient(45deg, #ff6b6b, #4ecdc4); padding: 10px; border-radius: 5px; font-size: 16px;"
);

console.log(
    "%cError: %cSomething went wrong",
    "color: red; font-weight: bold;",
    "color: black;"
);
```

---

## Console Grouping

### 19. Nested Groups
**Description**: Create nested groups for better organization
```javascript
console.group("Application State");
console.log("App initialized");

console.group("User Session");
console.log("User logged in");
console.log("Session ID: abc123");

console.group("User Permissions");
console.log("Admin: true");
console.log("Can edit: true");
console.log("Can delete: false");
console.groupEnd(); // End User Permissions

console.groupEnd(); // End User Session

console.group("API Connections");
console.log("Database: Connected");
console.log("Cache: Connected");
console.groupEnd(); // End API Connections

console.groupEnd(); // End Application State
```

---

## Console Timing

### 20. Multiple Timers
**Description**: Use multiple timers simultaneously
```javascript
console.time("Total Operation");
console.time("Database Query");
// Database operation
setTimeout(() => {
    console.timeEnd("Database Query");
    
    console.time("Data Processing");
    // Data processing
    setTimeout(() => {
        console.timeEnd("Data Processing");
        console.timeEnd("Total Operation");
    }, 1000);
}, 500);
```

### 21. Timer with Labels
**Description**: Add descriptive labels to timers
```javascript
console.time("API:GET /users");
// API call
console.timeLog("API:GET /users", "Request sent");
// More processing
console.timeEnd("API:GET /users");
```

---

## Console Profiling

### 22. console.profile()
**Description**: Starts the JavaScript profiler (Firefox only)
```javascript
console.profile("My Profile");
// Code to profile
console.profileEnd("My Profile");
```

### 23. console.profileEnd()
**Description**: Stops the JavaScript profiler
```javascript
console.profile("Performance Test");
for (let i = 0; i < 1000000; i++) {
    Math.random();
}
console.profileEnd("Performance Test");
```

---

## Console Assertions

### 24. console.assert()
**Description**: Outputs an error message if the assertion is false
```javascript
const user = { name: "John", age: 30 };

console.assert(user.age >= 18, "User must be 18 or older");
console.assert(user.name, "User must have a name");
console.assert(user.email, "User must have an email"); // This will fail
```

### 25. Advanced Assertions
**Description**: Use assertions for debugging and validation
```javascript
function divide(a, b) {
    console.assert(b !== 0, "Division by zero is not allowed");
    return a / b;
}

function validateUser(user) {
    console.assert(typeof user.name === 'string', "User name must be a string");
    console.assert(user.age > 0, "User age must be positive");
    console.assert(user.email.includes('@'), "User must have a valid email");
}
```

---

## Console Table

### 26. Complex Table Examples
**Description**: Advanced table formatting
```javascript
// Table with different data types
const complexData = [
    { id: 1, name: "John", active: true, score: 95.5, lastLogin: new Date() },
    { id: 2, name: "Jane", active: false, score: 87.2, lastLogin: new Date() },
    { id: 3, name: "Bob", active: true, score: 92.1, lastLogin: new Date() }
];
console.table(complexData);

// Table with specific columns and formatting
console.table(complexData, ["name", "score", "active"]);

// Nested objects in table
const nestedData = [
    { 
        name: "John", 
        details: { age: 30, city: "NYC" },
        preferences: ["reading", "gaming"]
    },
    { 
        name: "Jane", 
        details: { age: 25, city: "LA" },
        preferences: ["music", "travel"]
    }
];
console.table(nestedData);
```

---

## Console Styling

### 27. Advanced CSS Styling
**Description**: Complex styling examples
```javascript
// Gradient text
console.log(
    "%cGradient Text",
    "background: linear-gradient(45deg, #ff6b6b, #4ecdc4); -webkit-background-clip: text; -webkit-text-fill-color: transparent; font-size: 24px; font-weight: bold;"
);

// Multiple styled elements
console.log(
    "%cSuccess: %cOperation completed successfully",
    "color: green; font-weight: bold;",
    "color: black;"
);

// Box with border
console.log(
    "%cImportant Notice",
    "border: 2px solid #ff6b6b; padding: 10px; border-radius: 5px; background: #fff5f5; color: #d63031; font-weight: bold;"
);
```

---

## Console Utilities

### 28. console.dir()
**Description**: Displays an interactive list of the properties of a specified object
```javascript
const element = document.getElementById('myElement');
console.dir(element);

const obj = {
    name: "John",
    age: 30,
    address: {
        street: "123 Main St",
        city: "NYC"
    }
};
console.dir(obj);
```

### 29. console.dirxml()
**Description**: Displays an XML/HTML element representation of the specified object
```javascript
const element = document.getElementById('myElement');
console.dirxml(element);
console.dirxml(document.body);
```

---

## Browser-Specific Console Features

### 30. Chrome DevTools Specific
```javascript
// Chrome-specific: console.memory
console.log(console.memory);

// Chrome-specific: console.exception (deprecated, use console.error)
console.exception("This is an exception");

// Chrome-specific: console.markTimeline (deprecated)
// console.markTimeline("Custom marker");
```

### 31. Firefox Specific
```javascript
// Firefox-specific: console.timeStamp
console.timeStamp("Custom timestamp");

// Firefox-specific: console.groupCollapsed
console.groupCollapsed("Collapsed group");
console.log("This is hidden by default");
console.groupEnd();
```

---

## Best Practices

### 32. Production vs Development
```javascript
// Development logging
if (process.env.NODE_ENV === 'development') {
    console.log("Debug info:", data);
    console.group("Component State");
    console.log("Props:", props);
    console.log("State:", state);
    console.groupEnd();
}

// Production logging (errors only)
if (process.env.NODE_ENV === 'production') {
    // Only log errors in production
    console.error("Critical error:", error);
}
```

### 33. Custom Console Wrapper
```javascript
class Logger {
    static log(message, ...args) {
        if (process.env.NODE_ENV === 'development') {
            console.log(`[LOG] ${message}`, ...args);
        }
    }

    static warn(message, ...args) {
        console.warn(`[WARN] ${message}`, ...args);
    }

    static error(message, ...args) {
        console.error(`[ERROR] ${message}`, ...args);
    }

    static group(label) {
        if (process.env.NODE_ENV === 'development') {
            console.group(`[GROUP] ${label}`);
        }
    }

    static groupEnd() {
        if (process.env.NODE_ENV === 'development') {
            console.groupEnd();
        }
    }
}

// Usage
Logger.log("Application started");
Logger.group("User Authentication");
Logger.log("User logged in successfully");
Logger.groupEnd();
```

### 34. Performance Monitoring
```javascript
class PerformanceMonitor {
    static timers = new Map();

    static start(label) {
        this.timers.set(label, performance.now());
        console.time(label);
    }

    static end(label) {
        const startTime = this.timers.get(label);
        if (startTime) {
            const duration = performance.now() - startTime;
            console.timeEnd(label);
            console.log(`${label} took ${duration.toFixed(2)}ms`);
            this.timers.delete(label);
        }
    }

    static measure(label, fn) {
        this.start(label);
        const result = fn();
        this.end(label);
        return result;
    }
}

// Usage
PerformanceMonitor.measure("Data Processing", () => {
    // Some expensive operation
    for (let i = 0; i < 1000000; i++) {
        Math.random();
    }
});
```

---

## Practice Exercises

### Exercise 1: Basic Console Methods
```javascript
// Practice using basic console methods
console.log("Hello, World!");
console.warn("This is a warning");
console.error("This is an error");
console.info("This is information");
console.debug("This is debug info");
```

### Exercise 2: Console Grouping
```javascript
// Create a structured log for a user registration process
console.group("User Registration Process");
console.log("Step 1: Validate input");
console.log("Step 2: Check if user exists");
console.group("Database Operations");
console.log("Connecting to database");
console.log("Executing query");
console.log("Query completed");
console.groupEnd();
console.log("Step 3: Send confirmation email");
console.groupEnd();
```

### Exercise 3: Console Timing
```javascript
// Measure different operations
console.time("Total Execution");
console.time("Data Fetch");
// Simulate API call
setTimeout(() => {
    console.timeEnd("Data Fetch");
    
    console.time("Data Processing");
    // Simulate processing
    setTimeout(() => {
        console.timeEnd("Data Processing");
        console.timeEnd("Total Execution");
    }, 500);
}, 1000);
```

### Exercise 4: Console Table
```javascript
// Create a table of products
const products = [
    { id: 1, name: "Laptop", price: 999.99, category: "Electronics", inStock: true },
    { id: 2, name: "Mouse", price: 29.99, category: "Electronics", inStock: true },
    { id: 3, name: "Keyboard", price: 79.99, category: "Electronics", inStock: false },
    { id: 4, name: "Desk", price: 199.99, category: "Furniture", inStock: true }
];

console.table(products);
console.table(products, ["name", "price", "inStock"]);
```

### Exercise 5: Console Assertions
```javascript
// Validate user data
function validateUser(user) {
    console.assert(user && typeof user === 'object', 'User must be an object');
    console.assert(user.name && typeof user.name === 'string', 'User must have a string name');
    console.assert(user.age && typeof user.age === 'number' && user.age > 0, 'User must have a positive age');
    console.assert(user.email && user.email.includes('@'), 'User must have a valid email');
}

// Test with valid and invalid data
validateUser({ name: "John", age: 30, email: "john@example.com" });
validateUser({ name: "Jane", age: -5, email: "invalid-email" });
```

---

## Summary

This guide covers all the console methods available in modern web browsers, from basic logging to advanced profiling and styling. The console API is a powerful tool for debugging, monitoring, and understanding your JavaScript applications.

**Key Takeaways:**
- Use appropriate console methods for different types of output
- Leverage grouping and timing for better organization
- Use assertions for validation and debugging
- Apply styling for better visual distinction
- Consider production vs development logging
- Create custom wrappers for consistent logging

**Next Steps:**
1. Practice each method in your browser's developer tools
2. Create custom logging utilities for your projects
3. Implement performance monitoring in your applications
4. Use console methods for debugging complex applications

Remember that console methods are primarily for development and debugging. In production, you should limit console output to essential error logging and use proper logging services for monitoring and analytics. 