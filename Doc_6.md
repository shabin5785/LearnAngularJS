**Pipes**
-----------------
- Pipes are built into angular that allows us to transform output., like converting string to uppercase while displaying

- we have configure a pipe by sending it parameters

- Chained pipes are parsed left to right. So the order of pipes is very important

- we can write custom pipes. Just a calss with a transform method, returning the value converted from input. We then need to add the Pipe annotation to the class and give it a name, This name becomes the pipe name to be used in templates.Also add the class to declarations under app module
we can also parameters to our custom pipe as well.

- ng g p is the cli command to create pipe

- pipe input can be an array as well. We can iterate over that  in pipe and return a subset of the array.  So we apply pipe to an array loop , the pipe will transform what is the output of that loop, like without pipe it was 10 times iteration, pipe can remove some elements and it iterates only 5 times.