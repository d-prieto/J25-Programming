# Explorations on arduino IDE

download arduino IDE: https://www.arduino.cc/en/software


Template for a file on Arduino:

1) Create an item in this file (or readMe.md)
2) Explain the concept behind the program (this is for practicing Serial.println, this is part of the cooking system/morse code)
3) Avoid personal information (names, phone numbers, addresses)
4) extra marks: add style. You can use also emojis https://gist.github.com/rxaviers/7360908

Task for Monday
- Serial.print task
- Cooking system 2, 3 and 4.
- Cooking system 3 has only one own recipee
- Cooking system 4

Add more than 1 recipee. Add inventory system. 

```C++
else if (input == "show"){
  Serial.println("These are the ingredients that we have");
  Serial.print(potato);
  Serial.println(" potatoes");
  Serial.println(onion);
  Serial.println(" onions");
  if(oil){Serial.println("We have oil");}
  else{Serial.println("We don't have oil");}
 }
```
