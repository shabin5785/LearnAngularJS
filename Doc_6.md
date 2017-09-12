**Pipes**
-----------------
- Pipes are built into angular that allows us to transform output., like converting string to uppercase while displaying

- we have configure a pipe by sending it parameters

- Chained pipes are parsed left to right. So the order of pipes is very important

- we can write custom pipes. Just a calss with a transform method, returning the value converted from input. We then need to add the Pipe annotation to the class and give it a name, This name becomes the pipe name to be used in templates.Also add the class to declarations under app module
we can also parameters to our custom pipe as well.

- ng g p is the cli command to create pipe

- pipe input can be an array as well. We can iterate over that  in pipe and return a subset of the array.  So we apply pipe to an array loop , the pipe will transform what is the output of that loop, like without pipe it was 10 times iteration, pipe can remove some elements and it iterates only 5 times. 
So applying pipes we can change behaviour of loops.

- Angular wont re run the pipes when arrays or objects on the page cahgnes. Only if the pipe input changes, its re run. This is designed like that to avoid poor performance. Also due to this there are no inbuilt filter pipes in angular,as even with data changes the filters wont be run.

We can enforce this by setting pure true for the pipe. But this will affect the performance

- async pipe : if we have say a object assigned to a promise, and if we display that, it will be shown as a promise, even if promise resolves to a string. this is because angular knows it only as a promise and is not re evaluating it. To fix this, we can add the async pipe, so that angular will wait till the promise or observable resolves and then use it.

**Http**
---------------

- http functions in angular returns an observale which we can subscribe to and get teh result. So the requets are initiated only when we set up subsription. Also we dont need to clean them up as well as these are for extenal services.

- Use header object from angular to change http headers and http object to create requests. http method take a config object and one of the args is header.

- we can use map operator to transform the observable response and convert its data to a better json form and then create another objservable which other parts of the app can use.