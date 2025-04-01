#S
single responsibility principle : seprate your application into small pieces of classes
then its easy to read and maintain and change a class without changing another class
and every class you define should have only one duty that is clear and it should not 
implement all the methods that are irrelevant to it.
examples : 
1.in laravel we can use FormRequest classes to validate data instead of validating them in controller
2.move your logic from controller to another classes like services and note that the service should not
know about request but just about the items to be passed to it from request class
3.in our service class we can use method related to models and this methods or attribute must
be defined in our model in its boot method 
best structure : use dto to make from request and make from array method
and create it in controller and just pass it to service and service should create 
or do actions from repository pattern and repository should use that  dto for crud operations
this is a good structure for most of the scalable projects
and note that service class should use try catch so our application can be service based
#O
What violates the open-closed principle : if else and switch case (not that some if's are logical not options when ?
when if's determine Behavior of something that must be changed or added in future)
when adding new functionality requires changes to existing code
for example you can define an interface and sub classes must implement the same method name 
and every time we must a specific class we can make it manually by using Upper case string method
and make that class name space and the class is variable so we can make an instantiation of it
into our service class and just call the method name that we must implement it since they implemented that interface
in fact we use interfaces to specify the same method name in sub classes
so our sub classes can be variable and we dont need to know which one is
and the only thing we know is their same and common method names
in fact when you want to change the way of functionality of a package you dont go into vendor folder
and change it, but you define a new class and implement its interface and change the class in config or service provider
or just extend the class you are using in your new defined class and add your extra functionality to it and use your own
class -> in App/Classes/somethingclassExtended
another example is when you have an employee model and you wanna calculate every personel type with salaries like developer
and designer we can do that calculation in model its good but we can do better
we can define a folder in app and call is Calculators and inside calculators we can define classes like :
DeveloperSalaryCalculator and DesignerSalaryCalculator and every of these classes should implement
SalaryCalculatorInterface and this interface has calculate method
and then define an associative array in model method class and map keys with classes and boom!
#L
it says you should be able to replace a class T with class B that they both implement/extend the same class/interface
we can do that with specify type hint in methods parameters and the return type of that method
and imagine you need to define another parameter in just one class you have two choice :
1.define it and give it a default value in that class
2.add that parameter to all classes and interface
or you need a specific method in a class so you have to implement it in interface and other sub classes
and remember that if you need something in one subclass see it in the whole structure and make it private or implement
that method all classes including it interface/parent class
all point solid principle says : what if someone in a past or future change something?
#I
states that client code should not implement methods that is does not use
in laravel we have a model that implement many things but user implements authenticatable
and that model implements different methods
we must take care of this priciple that our custom classes
should not implement any interface that does not need to implemenet its methods
for exmaple your class implement an interface but one its method
you just write this is not available or you throw an error
well this violets the interface segregation principle and you must seprate that interface
into two interfaces
