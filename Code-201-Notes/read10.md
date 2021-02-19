### Order of Execution

* function greetUser() {
    return 'Hello ' + getName();
}

* function getName() {
    let name = 'Molly';
    return name;
}

* let greeting = greetUser();
alert(greeting);

### The Stack

* Creates greeting variable and calls greetUser() to get value

* greetUser() returns 'Hello' and the results of getName()

* getName() returns the value 'Molly' to greetUser()

* greetUser() returns 'Hello Molly' to the greeting variable

* greeting holds the value 'Hello Molly'

### Prepare

* The new scope is created
* Variable, functions, and argumentsare created

### Execute

* Now it can assign values to variables
* Reference functions and run their code
* Execute statements

### Error Objects Continued

* SyntaxError
* ReferenceError
* EvalError
* UrlError
* TypeError
* RangeError
* Error
* NaN
