# Arrays and functions in PSEUDOCODE

###### tags: `Computer Science` `IB`

[ToC]

:::warning

These notes come from the same version in C++ but we have now more IB flavor. 
:::

## Functions in C++ (and other Programming Languages)

In programming since we have to deal with very complex problems we have a way to divide our algorithms in smaller parts using **functions** (also called "actions" in Object Oriented Programming, "subprocedures" in IB, "methods" in Java). 

These functions are **portions of code that are executed anytime that they are called.**

One way to see this is a doorbell 

![old-doorbell-1493998372dHV](https://hackmd.io/_uploads/Hkn_RgJup.jpg)
([source](https://www.publicdomainpictures.net/es/view-image.php?image=212432&picture=viejo-timbre-de-puerta))

Anytime that you press the button (the call) the bell is going to ring (execute the function). If you press twice, the ring is going to ring twice and so on. 

## Definition and call

To use a function it needs to be defined and implemented. That definition can be done by us or we can use a library and directly call it. 

For example in the code of blink of arduino we have 5 intructions that are 5 calls of 3 functions:



```cpp=
void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  digitalWrite(LED_BUILTIN, HIGH);  
  delay(1000);                       
  digitalWrite(LED_BUILTIN, LOW);
  delay(1000);                    
}
```

In this case we are calling the functions called ```pinMode()```, ```digitalWrite()``` and ```delay()``` . In this case we don't have to implement (that means to actually do the inner workings) these functions. They are already defined in a **library** called arduino.h and we just access to it. In programming is common to use functions that are already defined. 


But when we did the morse code we actually defined the dot() and dash() functions in our code. 

In those examples we had a code similar to this




```cpp=
void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
    dot();
    dash(); //repeated some times to get the message
}

void dot() {
  digitalWrite(LED_BUILTIN, HIGH);  
  delay(500);                       
  digitalWrite(LED_BUILTIN, LOW);
  delay(500);      
}


void dash() {
  digitalWrite(LED_BUILTIN, HIGH);  
  delay(1500);                       
  digitalWrite(LED_BUILTIN, LOW);
  delay(500);       
}
```


```=
PSEUDOCODE 

dot() 
    lightLED() //we can be a little bit more abstract in pseudocode
    wait(0.5) //for example using seconds instead of milliseconds
    offLED()
    wait(0.5)
end method


dot() 
    lightLED()
    wait(1.5)
    offLED()
    wait(0.5)
end method
```


Here in the lines 6 and 7 we can see the call of the functions and in the lines 10 to 15 we see the **implementation** of dot() and from lines 18 to 23 the **implementation** of dash()

:::warning
In an exam you can be asked to write the implementation of a function (in IB it's called method or subprocedure) and/or just use it, using a call. 
:::


We will get into more detail of the syntax later, before we need to get into the surroundings of it. We need to talk about parameters and return values. 


:::info

**Call, definition an implementation**

To be precise

A **function call** is an expression containing the function name followed by the function call operator, usually "()". If the function has been defined to receive parameters, the values that have to be sent into the function are listed inside the parentheses of the function call operator. This will execute the function and return the value if it's defined [source](https://www.ibm.com/docs/en/i/7.3?topic=operators-function-call-expressions)

A **function definition** includes the name the parameters that are required and the return type if any. 

The **implementation of a function** is the code that is actually executed. The particular solution that, in C++ is inside the brackets. 
:::


## Parameters and return values

One of the best things that are implemented in functions in almost all modern programming languages is that functions can have parameters and return values. This means that we can make a function that can be used in different circumstances. 

### Parameters

Take as an example the function delay(). This function accepts a parameter with the number of milliseconds that we want to wait. 

```cpp=
void setup() {
}

void loop() {
  delay(1000); // Wait for a second               
  delay(500);  // Wait for a half a second    
  delay(2000);  // Wait for 2 seconds    
}
```

If we didn't have that, then we would have need to have a definition of a delay of a specific number of milliseconds (such as 10 milliseconds) that we would need to repeat as needed. 

Being precise, a parameter (or argument) is a variable provided as an input to the function. A function can have none, one or several parameters. When the function is defined the number of parameters is set. When the function is called the parameters has to been sent. 

:::info 
We can define two functions with the same name and different number or type of parameters. This is called "method overload" because we are "charging" one name of a function (method) with more than one definition. This is called also polymorphism. This is done in Java (Option D for IB)

For more info in this [LINK](https://data-flair.training/blogs/polymorphism-in-java/) or this other [LINK](https://www.mygreatlearning.com/blog/polymorphism-in-java/)
:::

### Tone() an example of use in detail

An example of use in C++ is the function tone(pin, frequency, duration). You can check more on that in the reference of Arduino [here](https://www.arduino.cc/reference/en/language/functions/advanced-io/tone/)

In the case o this method you need to send 3 parameters (or arguments) to this function to work. 

The first is the pin (a number), the second is the frequency also as a number and the third is the duration of the sound. 

So if we write a program like this:


```cpp=
void setup() { 
    tone(8, 440, 5000);
}

void loop() {  
}
```

The arduino is going to emit a sound in the pin number 8 on a frequency of 440 Hertz (a A4) during 5 seconds. 

We can use variables not to repeat values and be more clear. For example look at this example

```cpp=
const int BUZZER_PIN = 8;
int time = 500;

void setup() { 
}

void loop() {  
    tone(BUZZER_PIN, 440, time);
    delay(time);
    noTone(BUZZER_PIN);
    delay(1000);
    time = time + 500;
}
```

This program will send a sound of half a second then will make a pause of a second (the second delay in line 11). After this it will repeat the same procedure but the time sounding will be longer (the silence will be the same). This will go on until we reach the end of the boundaries of the int type (around 32 000). 

To avoid that limitation we can add an if that puts a limit when we go over 32000. We also may use another numeric type (long) for the same variable that can go on for longer. Long can get to values around [32 000 000 000](https://www.arduino.cc/reference/en/language/variables/data-types/long/) (way more than int).

This is the option if we have a cap and we decide to reset the duration, that use an if. 

```cpp=
const int BUZZER_PIN = 8;
int time = 500;

void setup() { 
}

void loop() {  
    tone(BUZZER_PIN, 440, time);
    delay(time);
    noTone(BUZZER_PIN);
    delay(1000);
    time = time + 500;
    if (time > 30000) // the condition is not the limit but a little bit earlier
    {
        time = 500;
    }
}
```

This is the version with the long option without cap. 

```cpp=
const int BUZZER_PIN = 8;
long time = 500; //this is the only change

void setup() { 
}

void loop() {  
    tone(BUZZER_PIN, 440, time);
    delay(time);
    noTone(BUZZER_PIN);
    delay(1000);
    time = time + 500;
}
```

#### Exercise 1

Create an Arduino sketch that creates pulses of 200 milliseconds of duration that increases of tone by 50 from 200 to 1500 and then repeats itself

You can see a solution in the spoiler section

:::spoiler

```cpp=
const int BUZZER_PIN = 8;
int pitch = 200; //this is the only change

void setup() { 
}

void loop() {  
    tone(BUZZER_PIN, pitch, 200);
    delay(200);
    noTone(BUZZER_PIN);
    delay(200);
    pitch = pitch + 50;
    if (pitch > 1500) {
        pitch = 200;
    }
}
```

:::

#### Using loops

We can also use a loop for or a loop while to repeat the instuction a certain number of times. Let's say that we want to make 4 times a tone in a pitch (440) and then 3 times a tone in another pitch (880) and then silence. All the tones have a duration of 0.2 seconds 

In this example I'm going to use a for loop and a while loop. Can be done with both. 


C++ arduino:
```cpp=
const int BUZZER_PIN = 8;
int time = 200; //the duration

void setup() { 
    for (int x = 1;  x < 5, x ++) //we want to happen 4 times, 1, 2, 3, 4 and when we arrive to 5 it's going to stop
    {
        tone(BUZZER_PIN, 440, time);
        delay(time);
        noTone(BUZZER_PIN);
        delay(time);
    }
    int y = 1;
    while (y < 4) // 3 times. Values of y: 1, 2, 3
    {
        tone(BUZZER_PIN, 880, time);
        delay(time);
        noTone(BUZZER_PIN);
        delay(time);
        y++;
    }
    
}

void loop() {  

}
```

PSEUDOCODE:

```
//time and BUZZER_PIN are given
  loop for X from 1 to 4
        tone(BUZZER_PIN, 440, time)
        delay(time)
        noTone(BUZZER_PIN)
        delay(time) 
  end loop
  Y = 1
  loop while Y<4
        tone(BUZZER_PIN, 880, time)
        delay(time)
        noTone(BUZZER_PIN)
        delay(time)
        Y = Y + 1
  end loop

```


#### Exercise 2

Create an Arduino sketch that creates pulses of 200 milliseconds of duration that increases of tone by 50 from 200 to 1500 and doesn't repeat itself. 

Solution in the spoiler section



:::spoiler

Using a while version:

```cpp=
const int BUZZER_PIN = 8;
int pitch = 200; 

void setup() { 
    while (pitch <= 1500) {
        tone(BUZZER_PIN, pitch, 200);
        delay(200);
        noTone(BUZZER_PIN);
        delay(200);
        pitch = pitch + 50;
    }
}

void loop() {  
    
}
```

PSEUDOCODE:

```
BUZZER_PIN = 8
PITCH = 200
loop while PITCH <= 1500 
        tone(BUZZER_PIN, pitch, 200)
        delay(200)
        noTone(BUZZER_PIN)
        delay(200)
        pitch = pitch + 50
end loop 

```
Using a for version: 

```cpp=
const int BUZZER_PIN = 8;


void setup() { 
    for (int pitch = 200; pitch <= 1500; pitch = pitch + 50) {
        tone(BUZZER_PIN, pitch, 200);
        delay(200);
        noTone(BUZZER_PIN);
        delay(200);
    }
}

void loop() {  
    
}
```
PSEUDOCODE:

```
 //Since the loop for in Pseudocode is condition to have a step of + 1 we need to find a way to bypass that. One option is to state the step clearly
 
  loop for PITCH from 200 to 1500 step by 50
        tone(BUZZER_PIN, pitch, 200)
        delay(200)
        noTone(BUZZER_PIN)
        delay(200)
  end loop
     
```

Another option is to loop from 4 to 30 by steps of 50 in the tone. 

```

  loop for P from 4 to 30
        tone(BUZZER_PIN, P*50, 200)
        delay(200)
        noTone(BUZZER_PIN)
        delay(200)
  end loop
     
```

This last option could be also written in C++ like this:

```cpp=
const int BUZZER_PIN = 8;


void setup() { 
    for (int p = 4; p <= 30; p++) {
        tone(BUZZER_PIN, p*50, 200);
        delay(200);
        noTone(BUZZER_PIN);
        delay(200);
    }
}

void loop() {  
    
}
```
:::



To sumarize, tone is a function with 3 parameters, the three of them are numbers (pin, frequency and duration). 

### Return value

Return of a function is a value (that in C++ or Java also need to have a type specified) that the function is going to return to the point where is it called. 

An example would be a function that it's call "add(x, y)" that returns the value of adding x and y. In many programming languages we would use just the operator "+"

```cpp=
 int x = 50;
 int y = 100;
 int z = x + y; //150
```

```cpp=
 int x = 50;
 int y = 100;
 int z = add(x,y); //150
```

#### Example functions with return type 

Even if we don't use "add" we have many mathematical functions that we might use in C++, Java or other programming languages. Here some math functions

* max(x,y) returns the maximum value of two values (variables or constants). More info [HERE](https://www.arduino.cc/reference/en/language/functions/math/max/)
* sqrt(x) readed square root, returns the square root of any number in a double type. More info [here](https://www.arduino.cc/reference/en/language/functions/math/sqrt/)
* random(max) and random(min, max). This give a pseudo random number either from zero to max -1 or from min to max - 1

    If we want to have a random number from certain range we need to know what are the maximum and the minimum values that we need. 
    For example, random(6) is going to give us a 6 possible random values, but they are going to be ranged from 0 to 5. 
    If we write random(1,7) the function is going to return values of 6 possible values from 1 to 6. In this case the results of rolling a dice (rolling a D6 to be precise)

:::warning

In any exam you're not suposed to know these functions, but the exam can describe them to you and you should be able to use them. 

:::

#### Example of math functions 

We can use random to generate a random melody. With pitches from 200 to 1500 Hz and constant duration


```cpp=
const int BUZZER_PIN = 8;


void setup() { 
}

void loop() {  
    int pitch = random(200,1500); 
    tone(BUZZER_PIN, pitch, 200);
    delay(200);
}
```

We can even make it more _one liner_ like this:

```cpp=
const int BUZZER_PIN = 8;


void setup() { 
}

void loop() {  
    tone(BUZZER_PIN, random(200,1500), 200);
    delay(200);
}
```

Remember that each time that we call random is going to return a different number. 

#### Exercise 3

Create an Arduino sketch that creates pulses of random duration of milliseconds in a range from 300 to 1200 seconds and intersecated with silences of the same duration. The picth is 440.

Solution in the spoiler section

:::spoiler
```cpp=
const int BUZZER_PIN = 8;


void setup() { 
}

void loop() {  
    int time = random(300,1201); //We need to use a variable to keep the same value the 3 times that we are using it
    tone(BUZZER_PIN, 440, time);
    delay(time);
    noTone(BUZZER_PIN);
    delay(time);
}
```
:::

#### Exercise 4

Create an Arduino sketch that creates pulses of random duration of milliseconds in a range from 300 to 1200 seconds and intersecated with silences of the same duration. The pitch is also a pseudo random number from 330 to 660 Hertz.

Solution in the spoiler section

:::spoiler
```cpp=
const int BUZZER_PIN = 8;


void setup() { 
}

void loop() {  
    int time = random(300,1201); //We need to use a variable to keep the same value the 3 times that we are using it
    tone(BUZZER_PIN, random(330,661), time);
    delay(time);
    noTone(BUZZER_PIN);
    delay(time);
}
```
:::

#### Exercise 5

:::success

This is one that can be set in the exam since combines functions and also arrays. 

:::


Create an Arduino sketch that creates pulses of random duration of milliseconds in a range from 300 to 1200 seconds and intersecated with silences of the same duration. The duration has to be a multiplier of 100 (300,400 and so on). The pitch is selected at random from these pitches 440,292, 880 and 653

The solution with the explanation in the comments is in the spoiler section

:::spoiler
```cpp=
const int BUZZER_PIN = 8;
const int frequencies[] = {440,292,880,653};
// we write the available frequencies in an array so then we select one of those. 

void setup() { 
}

void loop() {  
    int time = random(3,13) *100; //we have a random number from 3 to 12 inclusive and then we multiply it by 100
    tone(BUZZER_PIN, frequencies[random(4)], time);
    // we access to the pitch using a random index that goes from 0 (that points to 440) to 3 (that pints to 653)
    delay(time);
    noTone(BUZZER_PIN);
    delay(time);
}
```

** Beware incorrect solution **

```cpp=
const int BUZZER_PIN = 8;
const int frequencies[] = {440,292,880,653};
// we write the available frequencies in an array so then we select one of those. We write 2 zeros because 2 out of six 

void setup() { 
}

void loop() {  
    int time = random(3,13) *100; //we have a random number from 3 to 12 inclusive and then we multiply it by 100
    tone(BUZZER_PIN, frequencies[random(4)], time);
    // we access to the pitch using a random index that goes from 0 (that points to 440) to 5 (that pints to the second 0)
    delay(time);
}
```


:::

#### Exercise 6

Create an Arduino sketch that creates pulses of random duration of milliseconds in a range from 300 to 1200 seconds. The duration has to be a multiplier of 100 (300,400 and so on). The pitch is selected at random from these pitches 440,292, 880 and 653. One over 3 notes should be a silence. 

The solution with the explanation in the comments is in the spoiler section

:::spoiler
```cpp=
const int BUZZER_PIN = 8;
const int frequencies[] = {440,292,880,653,0,0};
// we write the available frequencies in an array so then we select one of those. We write 2 zeros because 2 out of six 

void setup() { 
}

void loop() {  
    int time = random(3,13) *100; //we have a random number from 3 to 12 inclusive and then we multiply it by 100
    tone(BUZZER_PIN, frequencies[random(6)], time);
    // we access to the pitch using a random index that goes from 0 (that points to 440) to 5 (that pints to the second 0)
    delay(time);
}
```


**Beware incorrect solution:**
```cpp=
const int BUZZER_PIN = 8;
const int frequencies[] = {440,292,880,653};
// we write the available frequencies in an array so then we select one of those. We write 2 zeros because 2 out of six 

void setup() { 
}

void loop() {  
    tone(BUZZER_PIN, frequencies[random(4)], random(3,13) *100); //the first time we're going to get a number that goes from 300 to 1200
    delay(random(3,13) *100);//the second time we're going to get a number that goes from 300 to 1200 THAT MAY OR NOT BE THE SAME
}
```


:::

#### Other return types

Up to here we have discussed numeric return types but we can have other return types such as booleans, characters or strings. Characters and Strings will be discussed later in the Array section. 

#### Boolean return types in funtions

Functions that return booleans usually are in 2 great branches

* Error-returning functions. Functions that do something else and return true if everything went well and false if there was any kind of error.  
* Evaluating functions. Functions with the only purpose is to return true or false to validate some variables. 

#### Error-returning functions

Error returning functions are common in tasks that can be difficult and may generate any kind of error so the algorithm can do something about it. 

For example we might have a function that is called "proofTheLastFermatTheorem()" that makes a very complex mathematical work (more info [here](https://en.wikipedia.org/wiki/Fermat%27s_Last_Theorem)). Makes sense that this is something that sometimes will work and sometimes the computer may not finish. If it finish we print "Hooray" and if it doesn't we print "let's keep working on it"

![Pierre_de_Fermat](https://hackmd.io/_uploads/ByGIa_x_a.jpg)
[source](https://upload.wikimedia.org/wikipedia/commons/f/f3/Pierre_de_Fermat.jpg)


```cpp=
if (proofTheLastFermatTheorem()) {
    Serial.println("Hooray!");
}
else {
    Serial.println("Let's keep working on it")
}
```

Also sometimes we want to do something only if the things didn't went as expected. Let's say that we need to iniatilize a 3D printer with a method called "initalize3Dprinter(pin)" that has the pin as a parameter where is connected the 3Dprinter. We want to print an error message if something went wrong. 

We are going to use the not operator '!' to make it work

```cpp=
if (!initalize3Dprinter(3D_PIN)) {
    Serial.println("Something went wrong with the 3D printer initialization");
}
```

#### Exercise 7 

We have a function called solveProblem(int numberOfProblem) that tries to solve our physics problems so we don't have to do it. However it doesn't always work as intended and it has implemented a boolean return type that tells if it was actually solved or not. 

Create an Arduino sketch that try to solve the problems 3, 4 and 5. If something goes wrong it should print an error message with the problem that generated the error. 


The solution with the explanation in the comments is in the spoiler section

:::spoiler

Without loops: 
```cpp=
void setup() { 
    Serial.begin(9600); //since this is a complete skecth we need to remember to initialize the Serial communication
    if(!solveProblem(3)) //remember that it's going to return True if everything goes well
    {
        Serial.println("There was an error in the problem 3");
    }
    if(!solveProblem(4))
    {
        Serial.println("There was an error in the problem 4");
    }
    if(!solveProblem(5))
    {
        Serial.println("There was an error in the problem 5");
    }
}

void loop() {  

}
```

Solution with a for loop:

```cpp=
void setup() { 
    Serial.begin(9600); //since this is a complete skecth we need to remember to initialize the Serial communication
    for (int problem = 3; problem <=5; problem ++)
    {
       if(!solveProblem(problem)) {
           Serial.print("There was an error in the problem "); //I added the space after problem and 5
           Serial.println(problem);
       } 
    }   
}

void loop() {  

}
```

:::

#### Exercise 8

We have a function called solveProblem(int numberOfProblem) that tries to solve our physics problems so we don't have to do it. However it doesn't always work as intended and it has implemented a boolean return type that tells if it was actually solved or not. 

Create an Arduino sketch that try to solve the problems from 10 to 15. If something goes wrong it should print an error message with the problem that generated the error and continue. If everything goes well, we should print a message saying that that problem was solved. 

#### Evaluating funtions

These functions are usually validating information that we have. For example validate an ID card or validate a form. We might also validate a character or a number. We can think of a isPrime(int n) for evaluating if a number is prime or not. 

Usually these evaluating functions are going to be set as a condition or part of it (in combination with other conditions connected with operators)

Let's say that we have to validate an Spanish DNI. We may use a function called "validateDNI(string dni)" that will return true if the DNI is valid and false if it's not. 

```cpp=
if (validateDNI("77799966X")) {
    Serial.println("Identification valid");
}
else {
    Serial.println("Identification not valid");
}
```

Some of these evaluating functions have names that start with "is" or "has". IsFormValid(form) or hasAttathment(email)

::: info
In Object Oriented Programming (in C++ and in Java) is very common to have accessors/getters that return booleans. We will cover it when we arrive to OOP
:::

#### Exercise 9 

:::warning
Typical exam question. With an introduction of a function that you need to understand and a loop in the solution.
:::

We have an evaluating function called "isPrime(int number)" that returns true if a number is positive and prime.

Create an Arduino sketch that outputs how many prime numbers are in the first 100 numbers. Use isPrime() described before

The solution with the explanation in the comments is in the spoiler section

:::spoiler
PSEUDOCODE
```
   COUNTER = 0 
   loop for I from 1 to 100
       if(isPrime(I)) then
           COUNTER =  COUNTER + 1
       end if
   end loop
   output COUNTER

```

PSEUDOCODE
```
   I = 1
   COUNTER = 0 
   loop while I < 101
       if(isPrime(I)) then
           COUNTER =  COUNTER + 1           
       end if
       I = I +1
   end loop
   output COUNTER

```


```cpp=

void setup() { 
    Serial.begin(9600);
    int counter = 0; //We need a variable to count how many primes we find
    for (int x = 1; x < 101; x++) //for loop 
    {
        if (isPrime(x)){
            counter ++;
        }
    }
    Serial.println(counter);
}

void loop() {  

}
```
:::

#### Exercise 10


We have an evaluating function called "isPrime(int number)" that returns true if a number is positive and prime.

Create an Arduino sketch that outputs the biggest prime in the numbers from 1 to 300.

The solution with the explanation in the comments is in the spoiler section

:::spoiler





PSEUDOCODE
```
   MAX = 0
   loop for X from 1 to 300
       if(isPrime(X)) then
            MAX = X
       end if
    end loop 
    output MAX
```

PSEUDOCODE
```
   X= 300
   loop while X > 1
       if(isPrime(X)) then
            output X
            break
       end if
       X = X -1
    end loop 

```

```
   I= 300
   loop while NOT(isPrime(I)) and I>0
       I = I -1
   end loop 
   output I

```

Solution 2. We increment in the for loop and we only save the last value that we're going to print. If we use this solution, we need to loop through all the values because we need the last value. 

PSEUDOCODE
```
   MAX = 0
   loop X from 1 to 300
       if(isPrime(X)) then
            MAX = X
       end if
   end loop
   output MAX

```

Solution 1. We increment in the for loop and we only save the last value that we're going to print. If we use this solution, we need to loop through all the values because we need the last value. 

```cpp=

void setup() { 
    Serial.begin(9600);
    int biggest = 0; //We need a variable to store the value
    for (int x = 1; x < 300; x++) //for loop 
    {
        if (isPrime(x)){
            biggest =x;
        }
    }
    Serial.println(biggest);
}

void loop() {  

}
```

Solution 2. We descend from the maximum value to the minimum and we break the loop once we find a prime number. 

```cpp=

void setup() { 
    Serial.begin(9600);
    for (int x = 300; x > 1; x--) //for loop that is decreasing. Starts with x = 300 and then 299 and so on
    {
        if (isPrime(x)){
            Serial.println(x);
            break; // This instruction exits from the loop, preventing the printing of all the rest of prime numbers. 
        }
    }
    
}

void loop() {  

}
```

:::


### Syntax of an implementation of a function 

Now that we have discussed return types and parameters we can arrive to the proper definition of the implementation of a function in C++.

```cpp=
[returnType] nameOfTheFunction([typeParameter1] internalNameOfParameter1, [typeParameter2] internalNameOfParameter2) {
    //Code of the Function    
}
```

We start with the return type, this means if the function returns an integer, a long, a boolean, a String or other type of variable. If it doesn't return anything we write "void". 

:::info

In arduino this is why we have to write void setup() and void loop(). Because these functions don't return any type of values, they just execute instructions

:::

The nameOfTheFunction is written in camelCase, if we're writing code, this name should be meaningful enough. If we're more fluent in other language that it's not English is common to have names of functions in different languages. 

The parameters are optional and they are written in the format of type and internal name. For example if we are implenting add(x,y) the definition of the function should be something like this:


```cpp=
double add(double x, double y) {
    return x + y;
}
```

In this case the implementation is trivial (return x + y) but can be more complicated


:::danger

Remember that return and output are totally different concepts. Return is a value that goes into another part of the code and output will go out of the program (through a console, messaging, screen or somewhere else)

In the exams some questions will be about **outputing values** and others about **returning values**

In Arduino returning values is always done with return and output is done with Serial.println() or Serial.print() 

:::

Another example would be a simple implementation of abs(x), a function that returns the absolute value of an input

```cpp=
double abs(double x) {
    if (x<0) {
        return -x;
    }
    return x;
}
```
:::info
Remember that the return statement ends the function so any other statement inside the function will be ignored.
:::

In this case if x is negative it will arrive to the line 3 and with that it's going to end the function so the line 5 is not going to be executed. 

#### Exercise 11

Implement the function isOddAndMultiplierOf3 that has an input of an int and returns true if the number is Odd and also is a multiplier of 3 and false otherwise. 

The solution with the explanation in the comments is in the spoiler section

:::spoiler


PSEUDOCODE
```
    isOddAndMultiplierOf3(X) 
        if X mod 2 = 1 AND X mod 3 = 0 then
            return true
        else
            return false
        end if
    end method   
```

PSEUDOCODE
```
    isOddAndMultiplierOf3(X) 
        if X mod 2 = 1 AND X mod 3 = 0 then
            return true
        end if
        return false
    end method   
```


We don't need to write setup or loop since we only need to implement the function, not the whole sketch


```cpp=
//remember that in C++ boolean type is written "bool" for short
bool isOddAndMultiplierOf3 (int x) {
 if (x%2 == 1 && x%3 == 0) //if the reminder of the number divided by 2 is one and the reminder of the number divided by 3 is 0
 {
     return true;
 }
 else
 {
     return false;
 }   
}
```

Another correct implementation 
```cpp=

bool isOddAndMultiplierOf3 (int x) {
 if (x%2 == 1 && x%3 == 0) 
 {
     return true;
 }
    //Since return will finish the function, if it returns true it's not going to continue anymore. 
     return false;
}
```

:::

#### Exercise 12

Implement the function outputIfNegative(int x). This function outputs through serial a message only if the input is a negative number.

We can consider that the instruction Serial.begin(9600); has been already called.

The solution with the explanation in the comments is in the spoiler section.


:::spoiler


We don't need to write setup or loop since we only need to implement the function, not the whole sketch

```

PSEUDOCODE

outputIfNegative(X)
    if X<0 then
       output “The input is a negative number”
    end if
end method
```

Another correct implementation 
```cpp=

```cpp=
//remember that this function doesn't say "RETURN" but "OUTPUT" this is why this function has a return type of void. 
void outputIfNegative (int x) {
 if (x<0) {
     Serial.println("The input: " + x + " is a negative number");
 }

}
```
In this case the statement doesn't specify if we have to output the actual negative number. If we do it's going to be fine. 

:::

#### Exercise 13

:::success

This is an exam like question. You need to understand a problem that is given to you and give a solution. 

:::


![imagen](https://hackmd.io/_uploads/SkB0TWz_p.png)
[source](https://www.instructables.com/Arduino-Plant-Watering-System/)

We are implementing in an arduino a program as a part of a project to grow plants. We have a connection to a humidifier that tells the percentage of water in the soil. We already have implemented a variable in percentage. 

We need to implement a function called decide(int water). 

The parameter of this function is the humidity in percentage. 

The function decides if we need to call the function "activateWaterPump()" or "stopWaterPump()". If we activate the pump we need to output through serial "Started pumping" and when we stop the pump we need to output "Stopped pumping".

If the humidity is lower than 30 % the water pump should start working and it should stop if the humidity is over 35 %. 

We can consider that the instruction Serial.begin(9600); has been already called. 

Construct the code of this function. 

The solution with the explanation in the comments is in the spoiler section

:::spoiler


We don't need to write setup or loop since we only need to implement the function, not the whole sketch

```cpp=
//remember that this function doesn't say "RETURN" but "OUTPUT" this is why this function has a return type of void. 
void decide (int water) {
 if (water<30) {
     activateWaterPump();
     Serial.println("Started pumping");
 }
    //two different ifs because start and stop are different things.
 if (water>35) {
     stopWaterPump();
     Serial.println("Stopped pumping");  
 }
}
```
Another correct implementation:
```cpp=
void decide (int water) {
 if (water<30) {
     activateWaterPump();
     Serial.println("Started pumping");
 }
 else if (water>35) { //we can consider also that we are not going to start and stop the pump in the same call
     stopWaterPump();
     Serial.println("Stopped pumping");  
 }
}
```
:::
