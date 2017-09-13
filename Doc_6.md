**Depending on where we put data, we have to send out updates or changes to all the components that use the data. So we use subject and subcribe.**

**if there are multipe lines to be controlled by an ngIf in ui, put them together in a ngTemplate and then control that with if**

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

- we can use map operator to transform the observable response and convert its data to a better json form and then create another objservable which other parts of the app can use. We can even alter data and return new data!!!

- as http returns an observable, instead of us subscribing and getting the data , we can use the async pipe to get the data out of the component.Easy... Async pipe will subscribe to the observable from http respnse and then get the data from that.

- if we are not using hte observable returned by http request, the request wont be fired at all

**Authentication**
---------------------
- challenge in SPA is that the connection between ui and backend is nto strong. There is no binding between them. Loosely coupled. So no session stored in server or server remembers the client. Here its better to use a token based storage like JWT ( read why session in jwt is bad)

**Modules**
------------------------
- imports have all other modules which exports a module. We can then use it within app. Declaraitons holds the components or directievs that we use within the app.

- we can combine a set of components into a feature module and then exporting it and using it in our app module. Now app becomes easier to maintain. Like division of features.

- Delcarations are nto shared between modules.

- now while forming a module, should we keep the service for that feature inside the module? Probably no as its used outside the feature as well. So keep it outside. Though even if we keep it inside the module, it will work as anuglar injects all services inside the modules it loads into root level. But probably keeping it outside is better

- Now if the components in the feature use some angualr import, and if only they use that, we should move that import to the feature module and not put in root module. Like reactiveformcomponent or like that

- we cannto declare the same component or directive in more than one module. So put them in one place, at the app module.

- to share directives or components between modules, we create a shared module, that doesnt contain any components or features. Then put the common one inside shared module and then import and use it. typically we have one shared module in the app. By default everything in a module is avaibale within that only. So we need to export to use it.

- Now if two modules needs same directieve, like a custom one , we need to import them in both. Also all modules needs the commonModule to be imported whenever they use the common directives like for  if etc

- Browser moodule contains all features of common module plus features extra for bootstrap. So we should use brwser module in our app module and common modules for all others

- with different modules, we cannto put routes in one palce and import to app module. it wont work for other modules. SO we have to define routes for each module in separate files and use it wihtih that module, importing them there.

But in app module we use RouteModuel.root and in all other modules we should use RouterMoudle.forChild. This will take care of the route handling.  Our child module is imported to app module and hence the child route as well. SO child route should be forChild , and on importing to app module having forRoot, the routes will be merged. As feature module is a child of app module and imported within that,

So we define routes in individual modules and then import imports to app module, though that the routes as well.

- Routes can be anywhere in the app. Just need to define them before the route is used. (Then what about above?).

- But if we use selectors instead of routing then we have to define the component within the same module or use a moduel that expports thee routes. Confusing...

- Everyting in imports under app module is loaded at app start. This is eager loading. To avoid this and do lazy loading, we have to change this. We want to load a module only if the user visits it or needs it.
