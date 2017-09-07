- Always use property binding if the value is not just a plain string, like an JS object or complex one, or dynamic.
else its just a simple string assignment.

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

Absolute vs Relative path
--------------------------

paths starting with '/' is an absolute path while wihtout '/' is relative.Relative paths will append the path to the current url. Relative paths can also be written as './'.
Now anything related to base path or home path, can be relative or absolute. Because if its relative, it will be appended to '/' and will work. But from next level onwards, we have to carefully see if the url is to be relative or absolute and based on that give the link

For relative we can give paths like '../', which causes the path to go one level above in url, then append current path. Like browsing a directory. Also '../' will remove the currentyl loaded module or path, not just the last part of the url.

- to set active link style in routing, we can use routerLinkActive directive to set the class or style. Angular will add the class to the current route.
RouteLinkActive works by matching the paths by string match. So a url like /user, will match the root url '/' and user path, leading to both of them being styled. To control this we can use routelinkactiveoptions directive.

- To programatically navigate, inject the Router to the comopnent and call the navigate method of the router. 
Now the navigate method takes an array , which should have the parts of the url, either absolute or relative.

- Programetic navigation, the navigate method does not know which url or path is currently loaded. But if we are using routerlink, its put in ui code and it can know the component. So the programetic navigation by default doesnt work with relative navigation. So we have to inform it the current path.

For this we can pass Current Active path to the navigate method. FOr this we inject ActivatedRoute, which points to the current path and then configure navigate method to work relative to that path.
The config to the navigate method is an js object. We can set many options in that, one being relative to

Parameters to Routes
--------------------
Usual way to passing parameters. Set path like '/users/:id' and point it to some component that we need. Now we can access the id value on loading the route.
To get teh value, inject ActivatedRoute to the TS file ,and get value from the object, which has a huge set of data about current path, including params, 
id: this.currRoute.snapshot.params['id'].

Now the issue with using snapshot and getting params, is that, after loading the component if we change the url, the component is not loaded again. So param values are not updated in the TS class. 
To solve this, Router has an observable object called, params. We can subscribe to changes in params object, and so whenever the param value is changed, the observable is triggered and we get new values.
 this.currRoute.params
      .subscribe(
        (params: Params) => {
          this.user.id = params['id'];
          this.user.name = params['name'];
        }
      );
 the subscription runs only when params change. During load the subscruption is setup and run for all further url changes.
 
 We need to use observable only in cases where the url pattern or syntax wont change( like reload page etc), but data is changing, Angular cannot load new data in this case using subscription, so we have to use observable.
 
 - Also wheneve we are manually setting  a subscription like above, we should unsubscribe it as well. Subsrciption is not strongly linked to component, So even if component is destryoed subscription is kept alive. Angular will clean it up for us, but its better for us to clean up ourselves.
 
 - We can use queryparams attribute to pass query parameters to a path
 [queryParams]="{allow:1}" which gets converted to xxxx?allow=1
 Similary fragments="abcd" adds the value to end of url. xxxx#abcd. There can only be one fragment though.
 Same can be done using programettically using navigate method. using queryparmas
 this.router.navigate(['/server',id,'edit'],{queryParams: {allow:1},fragment:'abcd'}
 
 These can be accessed like parameters.. 
 console.log(this.currRoute.snapshot.queryParams);
 console.log(this.currRoute.snapshot.fragment);
 
 Or if we want this to be reactive we can set up an observer using queryParams.subscribe() and fragment.subscribe()
 
 **All data from path or url is always string. convert it if needed.**
 
 - We can have child routes by putting nested routes inside the path against a children array:
  { path:'server', component:ServersComponent, children:[
    { path:':id/edit', component:EditServerComponent},
    { path:':id', component:ServerComponent}
  ]}
  
  Now the child components cannot be loaded inside router-outlet put for parent. For above, server component is parent and is usually loaded in app-root where it is inside router-outlet. now :id cannot load there. So we need to put a router-outlet within server component where we wants its childs to be loaded.
  
Doing this causes the child routes to load in same page as parent. Not on separate page, as they are now nested routes, so within same page.

- Query params are not reatined between routes. To retain, we can pass an extra config to the naviage function

 this.router.navigate(['edit'], {relativeTo:this.currRoute, queryParamsHandling:'preserve'});
 preserve: keep old, by overwriting new
 merge : old + new
 
 params : abcd/:id
 queryparams: abcd?id=
 fragment: abcd#ffff
 
 
 - Wild card route is like { path :'** '}. Should be last in routes
 Also we can use redirectTo:'pathname' to redirect to an already defined path.
 
 -default matching strategy is "prefix" , Angular checks if the path you entered in the URL does start with the path specified in the route. Of course every path starts with ''. So setting that as path will match all urls
 To fix this behavior, you need to change the matching strategy to "full" :
{ path: '', redirectTo: '/somewhere-else', pathMatch: 'full' } 
Now, you only get redirected, if the full path is ''


- We can put all routes in a separate module, configure it there, export it and use this module within the main app module. Makes the app more manageable.

Protecting Routes
------------------

we can use a guard to protect routes. Each route takes a canActiavte property, which is an array of guards or just normal methods that evaulated some condition and return true or false. Based on this the path is either allowed or rejected.

We can use canActivateChild guard and protect all child routes of a parent. The implementation is similar to the canActivate guard.


CanDeactivate is used to control if we can leave a service .Like edit a form and then leave without sasving.. we can prevent that. For this, the best way is for a component to check if its data or state is changed. We cannot do that normally like the canactivate way, as the separate guard doesnt have access to data inside the component. So we create a custom interface that needs to be implemented by all components needed deactivate guard, then we create a guard with CanDeactivate implemented, and provide it with all required arguments plus the custom interface we created. Now using that interface, we can access the data in components as the componet should haev implemented our custom interface. So using this technique we can use the inbuilt service customized wiht our service.

- we can send data to a componet though a path declartion. Use the data property of the path for this. WE can then access this data in the component using the currRoute object snapshot.

- We can use a resolver in a path to load or fetch some data before rendering the component. This will not check for validity of path like guard, but will allow some operation to be run before rendering. Same could be done in onInit, but it happends after render of the component. This is especially useful for async data to be initialized.

- With normal url, the server hosting parses the url first before handling it to angular. So there is some contract to be acheived like on 404, index page should be returned etc. If we cannot achieve that, we can turn on hash mode in routing configuration and then the hosting server only takes care the part till # and angular will take of the part after that.
