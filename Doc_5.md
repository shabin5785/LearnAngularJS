**FORMS**
--------------------
**Proerty binding, if value is username we can omit the square brakcts and put like [abcd]="xxx". If we put like normal property binding [abc]="xyz", angular will search for xyz in TS class. To stop this we can use like [abcd]="'xxx'". This si complex, So use the first one**
 
- Angular has two approaches for forms: Template driven, where we define a template and angular will infer the form elements and controls from that template. Other one is Reactive approach, where we define the elements, link them up and control the finer elements of the form.

- We want angular to handle the forms. Not sent a http request on form submit. So we should not submit forms like normal http ones, but use angular to handle them

Template Approach
-----------------------

- Here we start with a form or a template defined within a component html. Then we use that template to drive everything. the form submit, data etc

- Now the template driven appraoches, restricts our control of form witin the template of html file. We cannot control it from ts file. We interact of configure the template and angular takes care of implementing it. In reactive approach, we have the complete control, so we can submit form and then interact or control it from ts file.

- Make use to import the FormsModule in module.ts and add it to imports array. The formsmodule has a lot of inbuilt functions.
One being, angular will automatically create a JS object when it detecs a form tag within a component. But the individual components are not autmatically as we may choose not to use all elements in form in the object. We have to do this manually
To do this add ngModel to the form elements we want to be part of the form object. Make sure to add the name attribute to the element.

- Use ngSubmit to submit the form. This will hook into the defautl form submit and trigger the angular method we added to the listener.

- We can set #f="ngForm" in the form element. Now the reference f is pointing to the angular created form object for the template. THe object will be of type ngForm. 

- The form object has a lot of controls or info about the form. Tons of. We can get elements of the form and they also have a lots of information

- We can access the form by using ViewChild annotation to get access to the local reference object we created, instead of passing it. This can be useful if we want to refer an earlier submitted form while submittign another form.

- We can add validations to template. Angular detects these and will enforce them for us.

- Angular provides a lot of directives to be used for validations, one being email. It can also work with existing html attributes for validation like required, which is treated as an attribute, or inbuilt directives. This we put in template and angular takes care of the rest.

- Angular dynamically adds some classes to elements for validation. like ng-dirty, ng-valid. So we can re define this classes in our css file and style components. These classes are dynamically added and removed by angular.
So use ng-invalid and ng-touched to show error for elements that are invalid but only after its touched.

- Due to template apporach, we have to control from from tempalte. So we can get the form object referecen, and use it to contril the form, like disable the submit button on invlaid form.

- to access individual elements of a form, we can creatae a reference in element and set it equal to ngModel. Now this will give access to the element and we can then check its state or control it from the template.

- we can bind the ngmodel property to a backend variable and set default value for that or hard code it in template.
Now with property binding the value change reflects after submit or when an event is fired. We can instead set up two way binding and control from from backend . 

- ngModel without binding, results in we geettign value from form object, or use property bindig where value can be set to refeclt on page load. or use two way binding for instantly change it. We still get the two way binded object in backend.

- we can group elements in form together, like wihtin a div. Then give it a ngModelGroup directive with a name. In the form value, the results will be grouped together under a key with the name that we gave. Like a custom object.Other fields outside groupd will be like normal. We can even validate the group together as one object. Like name and password under user key and then validate user together.  Also this custom object will have controls like an individual element and we can interact it with like normal element, like cehck isDirty or valid.

We can also add a local ref pointing it to the ngModelGroup like #user="ngModelGroup" and put it in the grouping element. We can then acccess it by passing it or by ViewChild.

- to set value of a form element from TS, we can as alwasys use two way binding  to set value. Or if we have the form referene in TS, we can use the setValue method. It takes a JS object of exact structure as the form, like if we have grouping then group it like that. SO check the strucutre by printing hte form object once before setting it. Now here we have to set values for all the elements within the form that angular manages. Cannot miss anything at all. So not the best approach.

- instead we can access the form object from the reference. Then use the patchdata method ,where we only need to set the required element. BUt keep in mind that we nned to keep the structure, ie, if the element is inside a grp, we have to maintain that structure..

- call the reset method on form to reset the form and clear all state of form. We can pass values to reset form to set values and still get a clean state of valid and touched.


**Reactive Approach**
----------------------------

- Here we have to create the form object. IN reactive approach, angualr creates the object of type formgroup and wraps it around with ngform. Here we create an object of type formgroup and use it. Formgroup is a collection of form elements.  Formgroup inturn takes a js object as value. 
This JS object has the type for the elements inside the form, which usually are type of FormControl. Now formcontrol acccepts three params as values, initial state, array of validator and array of async validators. We can say set initial value of username ot 'abcd' or let be null etc
 this.singupForm = new FormGroup({
      'username' : new FormControl(null),
      'email' : new FormControl(null),
      'gender' : new FormControl('male')
    });
    
 - for reactive approach,  works on basis of ReactiveFormsModule class from angular forms. So need to add that to imports under module imports of appmodule. by defautl angular is using formsModule which is the template one. replace it wiht reactive One.
 
 - we then bind form to formgroup and elements to formcontrol elements like below.
 < form  [formGroup]="singupForm"> 
 < input type="text formControlName="email">
 
 - Here while submittng, we dont need to pass the form from temaplte to backend of refer it. As we have created and linked it from TS file.. Just refer it in submit method.
 
 - important that we dont configure form in template. So the directives or validators in tempalte like required or ngvalid etc wont work. Our form resides on TS file. We only create a shadow of that in html, and sync it with TS file. So all form related operations has to be in TS file.


- For validation, use Validators from angular/forms and use it in formgroup definition within every formcontrol field that we need to have validated, like ,
 'email' : new FormControl(null,[Validators.required, Validators.email]),
 
 - to access form controls in template, we use the get method of the formgroup variable we synced up. We cannot just refere formname.valid like in template appraoch, like below
  < span class="help-block"
             *ngIf=" !signupFrom.get('username').valid && signupFrom.get('username').touched">
             
  - to get overall form status we dont need the get operator. Like signupFrom.valid or signupFrom.touched
  
  - Form group not only represents whole form, but a group of elements within form. This is our grouping from template approach. So we have a nested set of form groups.
   this.signupForm = new FormGroup({
      'userData': new FormGroup({
        'username' : new FormControl(null, Validators.required),
        'email' : new FormControl(null,[Validators.required, Validators.email])
      }),
      'gender' : new FormControl('male')
    });
    
 - now if we have nesting in TS like above we shld have nesting in html as well. A form, then may be div inside , then elements, ie, the same schema as the Object definition above..
 <form  [formGroup]="signupForm" (ngSubmit)="onSubmit()">  
        <div formGroupName="userData">
  
  - Now with this nesting, the get methods will  have to take care of nesting as well. like 
  get(userData.username)
  
  - We can use fromArray to dynamically add form elements. FormArray holds form control fields inside it, we can then add to it dynamically.
  
  
 
 
 

   