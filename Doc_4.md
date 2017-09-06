- Service is a normal typescript class. No annotation is added to it. Now dont just import the service class to another class and call methods inside that. Thats not the normal service behaviour.

- instead of us creating and using the object of service class, Use the Angular dependency injector to inject the objecct of the service and use it.
For this we declare the object that we want in the constructor of the component,We have to mandatorly give the type or class of the object as well. Now angular can inject the object. But this is not enough. We also have to provide an attribute providers within @component annotation config .Within the providers array we have to give the service class name as well. THis is needed as angular knows who is creating the object, and the type of that is given in the constructor part.

- we can store data as properties within component class. Then we have to emit it as part of events, bind it etc to pass data between components. Instead we can keep data in service and share it among components.

- Angular has hierarchial module injection. So if we provide a service or a provider to a parent , then all its child (infact all its tree below that to any level), will receive the same instance. Angular will make sure of that. 

- We can so add a servie to AppModule, and then make the servie available Application Wide. As appmodule is the root.(Available for all components and servies and classes)
We can provide a servie at appComponent, so that the service is avaibale for all components. As their is no upwards projection, non component hierarchy classes wont recieve the obejct
Lowest level we can give the service to single instance or component so that only its childs will get it.

- Lowest level servie injection takes precedence. If we give same service at appmodule, appcomponent and component level, lowest one will be taken.

- so if we inject the service to three childs of a componennt,then all three will get a unique instance. If we dont want that .
To avoid this, and have same instance, dont give the servie to providers for childs. Still need it at constructor for object injection. Angular will then inject same instance to all the childs.

- if we try to inject a service to a service, it fails. For injection to work in angular, angular needs the injectable to have some meta data. Service normally doesnt have that.
So we need to add @Injectable to the servie. This make that class eligible for injection of other objects. Like we are making the class angular managerd. Like spring annotation. So angular can inject other objects to this class.
Note that we add the metadata or annotation to the servie that receives other objects from angular...

- We can define model or events or triggers etc that can be used across the app. no need for input output complexity
So can emit this event from one component and subscribe to it in another easily.

**Routing**
- a good location to add routes is in add module. Create object array of types Routes. Its of the form below
[
{path:"user", component:"UserComponent"},
{path:"", component:"HomeComponent"}
]
path is the url that we enter and component is the one to use. so path="user" can be pointing to locahost:4200/user

We then use  RouterModule.forRoot(appRoutes) to register the routes to angular

- Now adding the component to pages will  not load the components based on routes. So we have to use a directive from router package to load the component based on pages.
<router-outlet>
The above directive is enough to load all routes based on url. We dont have to specify each component in page like
<app-user> or <app-server> as the router will take care of loading the components.

- we can set href="user" in a link to navigate. but this will cause a reload of application as clicking a link normally does. Thats the default html behavioour. This should be avoided. Use routerlink directive provided by angular for this.

routerlink="/" for home and routerlink="user".. etc
we can also use property binding for this [routerlink]="['/user','shoppin','edit']". here we can specify all parts of the url as elements of array. Only the first part needs to have '/' to make it absolute. The array notation allows us to construct complex routes.

