# Anonymous Functions
## Problem:
I want to call a function that requires parameters from an eventlistener, but event listeners do not allow for the passing of parameters:
````js
Object.property = 5;

function myFunction(num){
    for (var i = 0; i <= num; i++){
        console.log("Hello " + i + " Time(s)");
    }
}

myStage.Object.addEventListener("click", myFunction(Object.property)); // doesn't work because syntax is wront, can't use brackets and pass parameters.
myStage.Object.addEventListener("click", myFunction); // works, but... doesn't because function isn't receiving parameter.
````

## Solution
You can get around this by calling an anonymous function instead!

````js
myStage.Object.addEventListener("click", function(){
    myFunction(Object.property);
});
````

This basically calls a one off function that just calls the function that requires a parameter and passes the parameter to it.