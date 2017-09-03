- Service is a normal typescript class. No annotation is added to it. Now dont just import the service class to another class and call methods inside that. Thats not the normal service behaviour.

- instead of us creating and using the object of service class, Use the Angular dependency injector to inject the objecct of the service and use it.
For this we declare the object that we want in the constructor of the component,We have to mandatorly give the type or class of the object as well. Now angular can inject the object. But this is not enough. We also have to provide an attribute providers within @component annotation config .Within the providers array we have to give the service class name as well. THis is needed as angular knows who is creating the object, and the type of that is given in the constructor part.

- we can store data as properties within component class. Then we have to emit it as part of events, bind it etc to pass data between components. Instead we can keep data in service and share it among components.

- Angular has hierarchial module injection. So if we provide a service or a provider to a parent , then all its child (infact all its tree below that to any level), will receive the same instance. Angular will make sure of that. 

- We can so add a servie to AppModule, and then make the servie available Application Wide. As appmodule is the root.(Available for all components and servies and classes)
We can provide a servie at appComponent, so that the service is avaibale for all components. As their is no upwards projection, non component hierarchy classes wont recieve the obejct
Lowest level we can give the service to single instance or component so that only its childs will get it.

- Lowest level servie injection takes precedence. If we give same service at appmodule, appcomponent and component level, lowest one will be taken.

- so if we inject the service to three childs of a componennt,then all three will get a unique instance. If we dont want that
