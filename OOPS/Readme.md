# OOPS

# OOP's Object Oriented Programming System/Structure

Note: We can also say `oop` , object oriented programming

## 1. What is OOPS ?

- OOP's is a programming paradigm/methodology

> paradigm : kuch bhi kaam krne ka way or style. In real world - hr person paise kmana chata hai, so there are many ways youtube job etc., Development krte tym we have many ways ki particular task kese achieve krna hai, vo jo way hai ya style hai usko kehte hai, hum programming paradigm

> Paradigm : It can also be termed as method to solve some problem or do some task. 

- Programming paradigm is an approach to solve problem using some programming langugae or also we can say, it is a method to solve a problem using tools and techniques that are avaliable to us following some appraoch

> Programming Paradigm is of many types

- Object Oriented paradigm
- Procedural paradigm
- Functional 
- Logical
- Structured

 - We do, Object Oriented Paradigm

> OOps bhi ek style hai jisse hum apni problems ko solve krte hai/ development krte hai

Procedural programming is about writing procedures or functions that perform operations on the data, while object-oriented programming is about creating objects that contain both data and functions.

- Advantages:
    1.  faster and easier to execute
    2.  provides a clear structure for the programs
    3.  helps to keep the C++ code DRY "Don't Repeat Yourself"
    4.  makes the code easier to maintain, modify and debug
    5.  makes it possible to create full reusable applications with less code and shorter development time

> Note : The "Don't Repeat Yourself" (DRY) principle is about reducing the repetition of code. You should extract out the codes that are common for the application, and place them at a single place and reuse them instead of repeating it.

## 6 Main Piller of OOPs are

1. Class
2. Object & Methods
3. Inheritence
4. Polymorphism
5. Abstraction
6. Encapsulization

## Which languages are purely OOP : SamallTalk (First oops langugage)

Other `Java,CPP,C#,PHP,Python`

## Class :
- A class is a `blueprint` that `defines the variables` and `the methods` `common` to `all objects of a certain kind.`
- Class is not real world entitiy , it's just blueprint or prototype
- Class comming from calssification
- Categorize Everything
- If we talk about college , we can say that these students belong to computer science, so this is class of computer science, and these students are of electronics, so there's another class of electronics.
- So we are classifying based on the subject or course they are going for
- `Classification is based on the criteria that you are adopting`
- So, you are grouping set of students based on their course, so there's a class of computer science and electronics
- But you can see, both computer science and electronics are student only, so strudent is again a class.
- Now, Students and Employee are human beings, so again there is a classification. so Human is class
- Example : Animals,Birds,Vechiles,Furniture,Fruits
- Class ke andar objects hote hai, 
    - Animal : Dog,Cat
    - Birds : Sparrow,Peacock
    - Vechile : Car,Jeep
- A class is a user-defined data type

## Object : 
- an object is an element (or instance) of a class; objects have the behaviors of their class.
- Car : Alto,Swift both are object of class Car
- class is defination and object is instance
- Example : Suppose civil engineer made a plan for the house, so, Then based on these plan there are many houses are constructed that follow the same design, So design is one and we have created many houses, so design is bassically a blueprint a class and houses are objects which ajapts the features from blueprint or you can say class
- Example : Making a design of fingerprint scanner, there is a circuit diagram, now, electronic enginner create multiple fingerprint scanner based on that design, so design is blueprint of fingerprint scanner i.e. class, and real world in which we ae trying our thumbs are objects, there can be multiple fingerprint scanner , it means there can be multiple objects of same class.

## Data Hiding - Realted to Encapsulation

## Principles of OOP
1. Abstraction : Hiding internal details and showing functionality is known as abstraction., Visible Outside - function, e.g. Telivision, we dont know how it work, just have button to change channels. Buttons-functions
2. Encapsulation : Data Hiding - Binding (or wrapping) code and data together into a single unit is known as encapsulation. In TV , buttons are function and hidden part is data.
3. Inheritence : When one object acquires all the properties and behaviours of parent object
4. Polymorphism

Why Hiding Data ?
- its for avoiding misshandling , someone changes variable datatype like, its not for security.

## 1. OOPS-
1. ```Object-Oriented Programming is a programming model which revolves around the concept of  class and object.```
2. ```basically a computer programming design methodology that organizes/ models software design around data, or objects rather than functions and logic.```

## 2.NEED OF OOPS
![image](https://user-images.githubusercontent.com/35686407/177007506-9016d2f1-a287-4bfb-8900-6b4d348c9278.png)

- the readability, 
- understandability, 
- maintainability of the code increase
- provide the feature of data hiding that is good for security concerns.
- Highly complex programs can be created, handled, and maintained easily using OOPS

## 3. Limitations of OOPS
1. The size of the programs created using this approach may become larger than the programs written using the procedure-oriented programming approach.
2. OOP code is difficult to understand if you do not have the corresponding class documentation.
3. Not suitable for small problems.
4. Software developed using this approach requires a substantial amount of pre-work and planning.

## 3. FEATURES/PILLARS OF OOPS
- Inheritance
- Encapsulation
- Polymorphism
- Data Abstraction

![image](https://user-images.githubusercontent.com/35686407/177007706-de1df8af-a22c-40bf-b9b3-e7400b503112.png)

## 4. CLASS
- Class is basically a blueprint of an objects which contains some values, known as `data member`, and some set of rules known as `functions`. So when an object is created, it automatically takes the data and functions that are defined in the class.
- For example, first, a car’s template is created. Then multiple units of car are created based on that template
![image](https://user-images.githubusercontent.com/35686407/177007599-a57f1774-cf46-43a8-8468-7b8a6a9e774e.png)

## 5. OBJECTS
- The object is an entity that has some states and behaviour. 
- For example, A dog is an object because it has states like colour, name, breed, etc., as well as behaviour like Barking, eating, sleeping, etc.
- In the real world, an object is an actual entity to which a user interacts
- An object refers to the instance of the class, which contains the instance of the data members and functions defined in the class. 

## 6. ENCAPSULATION
- Encapsulation can be defined in two different ways:
1) Data binding: Encapsulation is the process of binding the data members and the methods together as a whole, as a class
2) Data hiding: Encapsulation is the process of hiding unwanted information, by restricting access to others.
![image](https://user-images.githubusercontent.com/35686407/177007614-5c768bd8-c455-46d8-8c75-ede0c1a78d5d.png)


## 7. Advantages of ENCAPSULATION:
- Encapsulation is a way to achieve data hiding because other classes will not be able to access the data through the private data members.
- In Encapsulation, we can hide the data’s internal information, which is better for security concerns.
- By encapsulation, we can make the class read-only. The code reusability is also an advantage of encapsulation.

## 8. INHERITENCE
- Inheritance is a mechanism in which one class acquires the property of another existing class.
- For example, a child inherits the behaviour of his parents.

> `Sub Class/Derived class`: The class that inherits properties from another class is called Subclass or Derived Class.

> `Super Class/Base class`: The class whose properties are inherited by the subclass is called Base Class or Superclass.

![image](https://user-images.githubusercontent.com/35686407/177007623-7570079b-4fb7-4679-94ad-e0472c4ce107.png)

## MODES OF INHERITENCE,
- Public,Private,Protected
![image](https://user-images.githubusercontent.com/35686407/177007821-19bbe3f3-234e-4b94-ad46-9ee3fd2bd599.png)
![image](https://user-images.githubusercontent.com/35686407/177007854-8b9eae04-3358-461a-813f-659362785c81.png)

## 9. ADVANTAGES OF INHERITENCE
- The main advantage of inheritance is code reusability.
- The runtime polymorphism (method overriding) can be achieved by inheritance only.

## 10. TYPES OF INHERITENCE
1) Single inheritance
2) Multilevel inheritance
3) Multiple inheritance
4) Hierarchical inheritance
5) Hybrid inheritance

> `Single Inheritance in C++`
In this type of inheritance one derived class inherits from only one base class. It is the most simplest form of Inheritance.

![](https://user-images.githubusercontent.com/86204416/176682078-44a707a4-2da2-4fd6-af68-cfcf497d8212.png)

> `Multiple Inheritance in C++`
In this type of inheritance a single derived class may inherit from two or more than two base classes.

![](https://user-images.githubusercontent.com/86204416/176682131-7aa6215f-01fb-407e-aa12-0052275574bd.png)

> `Hierarchical Inheritance in C++`
In this type of inheritance, multiple derived classes inherits from a single base class.

![](https://user-images.githubusercontent.com/86204416/176682177-c3f83a93-e14a-4b97-997d-9040aac2b2ad.png)

> `Multilevel Inheritance in C++`
In this type of inheritance the derived class inherits from a class, which in turn inherits from some other class. The Super class for one, is sub class for the other.

![](https://user-images.githubusercontent.com/86204416/176682238-4a7ef7d4-0088-4bbd-b286-21e2cdb1da64.png)

> `Hybrid (Virtual) Inheritance in C++`
Hybrid Inheritance is combination of Hierarchical and Mutilevel Inheritance.

![](https://user-images.githubusercontent.com/86204416/176682272-d85b6856-e254-4420-816e-191e51bdf24b.png)

## A special case of hybrid inheritance: Multipath inheritance: (Diamond Problem)
![image](https://user-images.githubusercontent.com/35686407/177007948-6556969b-ab5e-473c-b988-a1050e261e0f.png)

- A derived class with two base classes and these two base classes have one common base class is called multipath inheritance. Ambiguity can arise in this type of inheritance. 
- ClassB and ClassC inherit ClassA, they both have a single copy of ClassA. However Class-D inherits both ClassB and ClassC, therefore Class-D has two copies of ClassA, one from ClassB and another from ClassC. 
- If we need to access the data member of ClassA through the object of Class-D, we must specify the path from which a will be accessed, whether it is from ClassB or ClassC, bcoz compiler can’t differentiate between two copies of ClassA in Class-D.

> Ambiguity Rises - There are 2 Ways to Avoid this Ambiguity: 

1. Avoiding ambiguity using the scope resolution operator: Using the scope resolution operator we can manually specify the path from which data member a will be accessed, as shown in statements 3 and 4, in the above example. 
```cpp
ClassD obj;
obj.ClassB::a = 10;
obj.ClassC::a = 100;
```

> Note: Still, there are two copies of ClassA in Class-D.

2. Avoiding ambiguity using the virtual base class
```cpp
class ClassA
{
  public:
    int a;
};
 
class ClassB : virtual public ClassA
{
  public:
    int b;
};
 
class ClassC : virtual public ClassA
{
  public:
    int c;
};
 
class ClassD : public ClassB, public ClassC
{
  public:
    int d;
};
```

## 11. ABSTRACTION
- Abstraction is the method of hide the implementation from the user but shows only essential information to the user. It is one of the main features of oop. 
- For example, consider a car. You only need to know how to run a car, and not how the wires are connected inside it. This is obtained using Abstraction

![image](https://user-images.githubusercontent.com/35686407/177007651-79baecb6-629e-4787-926c-0eb428fc960c.png)

> Two Ways to Achieve:

`Abstraction using Classes`: We can implement Abstraction in C++ using classes by making pure virtual functions in it.
`Abstraction in Header files`: One more type of abstraction in C++ can be header files

`Points` :
1. A class is abstract if it has at least one pure virtual function.
2. We can have pointers and references of abstract class type.
3. If we do not override the pure virtual function in derived class, then derived class also becomes abstract class. 
4. An abstract class can have constructors. 

> Advantages of Data Abstraction:

Helps the user to avoid writing the low level code
Avoids code duplication and increases reusability.
Can change internal implementation of class independently without affecting the user.
Helps to increase security of an application or program as only important details are provided to the user.

## Interface
- An interface does not have implementation of any of its methods
- In C++, an interface can be simulated by making all methods as pure virtual


## 12. POLYMORPHISM
- As the name suggests  poly means many, and morphs means forms
- So, Polymorphism is a concept that allows us to perform a single action in different ways
- For eg- A person at the same time can have different characteristics. Like a man at the same time is a father, a husband, and an employee. So the same person possesses different behavior in different situations. This is called polymorphism.
![image](https://user-images.githubusercontent.com/35686407/177008641-ee282bdb-ba9a-4e34-935d-7ebcf6977cb1.png)


## 13. TYPES OF POLYMORPHISM
- Compile-time polymorphism
- Runtime polymorphism
![image](https://user-images.githubusercontent.com/35686407/177008675-5e187674-1d67-4f27-8d43-7291e722ccf0.png)


> `COMPILE TIME POLYMORPHISM`: 
Compile-time polymorphism is also known as `static polymorphism`. This type of polymorphism can be achieved through function overloading or operator overloading.

a) Function overloading: 

- When there are multiple functions in a class with the same name but different parameters, these functions are overloaded. 
- The main advantage of function overloading is it increases the readability of the program. Functions can be overloaded by using different numbers of arguments and by using different types of arguments. 

b) Operator Overloading: 

- C++ also provides options to overload operators. For example, we can make the operator (‘+’) for the string class to concatenate two strings.

> `RUNTIME POLYMORPHISM:`
Runtime polymorphism is also known as `dynamic polymorphism`. Method overriding is a way to implement runtime polymorphism.

a) Method overriding:

Method overriding is a feature that allows us to redefine the parent class method in the child class based on its requirement. But, sometimes, a child class may not be satisfied with parent class method implementation. The child class is allowed to redefine that method based on its requirement. This process is called method overriding. 
- RULES
    - The method of the parent class and the method of the child class must have the same name.
    - The method of the parent class and the method of the child class must have the same parameters.
    - It is possible through inheritance only.
```cpp
class A{
public:
	void show(){ // virtual void show(){}
		print("This is from class A");
	}
};

class B : public A{
public:
	void show(){
		print("This is from class B");
	}
};

void solve(){
	A *a = new B;
	// Runtime Polymorphism
	// as show is virtual in A, therefore bindied at runtime
	a->show(); // display : This is from class A

	// Non-virtual function, binded at compile time
	// if A have virtual void show() then
	a->show(); // display : This is from class B
}
```

## Binding [Static/Early Binding and Dynamic/Late Binding](https://www.ques10.com/p/21862/what-is-bindingexplain-static-and-dynamic-bindin-1/?)

## Virtual Functions
- A C++ virtual function is a member function in the base class that you redefine in a derived class. It is declared using the virtual keyword.
- It is used to tell the compiler to perform dynamic linkage or late binding on the function.
- In late binding function call is resolved during runtime. Therefore compiler determines the type of object at runtime, and then binds the function call.
- Virtual functions ensure that the correct function is called for an object, regardless of the type of reference (or pointer) used for function call.
- They are mainly used to achieve Runtime polymorphism
- The resolving of function call is done at runtime.

> Rules :

1. Virtual functions must be members of some class.
2. Virtual functions cannot be static members.
3. They are accessed through object pointers.
4. They can be a friend of another class.
5. A virtual function must be defined in the base class, even though it is not used.
The prototypes of a virtual function of the base class and all the derived classes must be identical. If the two functions with the same name but different prototypes, C++ will consider them as the overloaded functions.
6. We cannot have a virtual constructor, but we can have a virtual destructor
Consider the situation when we don't use the virtual keyword.

#### What is the use? 
Virtual functions allow us to create a list of base class pointers and call methods of any of the derived classes without even knowing the kind of derived class object. 

#### Real-Life Example to Understand the Implementation of Virtual Function
Consider employee management software for an organization.
Let the code has a simple base class Employee, the class contains virtual functions like raiseSalary(), transfer(), promote(), etc. Different types of employees like Managers, Engineers, etc., may have their own implementations of the virtual functions present in base class Employee. 

In our complete software, we just need to pass a list of employees everywhere and call appropriate functions without even knowing the type of employee. For example, we can easily raise the salary of all employees by iterating through the list of employees. Every type of employee may have its own logic in its class, but we don’t need to worry about them because if raiseSalary() is present for a specific employee type, only that function would be called.
```cpp
// C++ program to demonstrate how a virtual function
// is used in a real life scenario

class Employee {
public:
	virtual void raiseSalary()
	{
		// common raise salary code
	}

	virtual void promote()
	{
		// common promote code
	}
};

class Manager : public Employee {
	virtual void raiseSalary()
	{
		// Manager specific raise salary code, may contain
		// increment of manager specific incentives
	}

	virtual void promote()
	{
		// Manager specific promote
	}
};

// Similarly, there may be other types of employees

// We need a very simple function
// to increment the salary of all employees
// Note that emp[] is an array of pointers
// and actual pointed objects can
// be any type of employees.
// This function should ideally
// be in a class like Organization,
// we have made it global to keep things simple
void globalRaiseSalary(Employee* emp[], int n)
{
	for (int i = 0; i < n; i++) {
		// Polymorphic Call: Calls raiseSalary()
		// according to the actual object, not
		// according to the type of pointer
		emp[i]->raiseSalary();
	}
}

```

## Pure Virtual Function
- A virtual function is not used for performing any task. It only serves as a placeholder.
- When the function has no definition, such function is known as "do-nothing" function.
- The "do-nothing" function is known as a pure virtual function. A pure virtual function is a function declared in the base class that has no definition relative to the base class.
- A class containing the pure virtual function cannot be used to declare the objects of its own, such classes are known as abstract base classes.
- The main objective of the base class is to provide the traits to the derived classes and to create the base pointer used for achieving the runtime polymorphism.
```cpp
class Base  
{  
    public:  
    virtual void show() = 0;  
};  
class Derived : public Base  
{  
    public:  
    void show()  
    {  
        std::cout << "Derived class is derived from the base class." << std::endl;  
    }  
};  
```

## 14. CONSTRUCTORS
- A constructor is a special type of member function that is called automatically when an object is created. 
- In C++, a constructor has the same name as that of the class
- it does not have any return type. 

> Note: Even if we do not define any constructor explicitly, the compiler will automatically provide a default constructor implicitly.

## 15. TYPES OF CONSTRUCTORS
- Default constructor
- Parameterized Constructor
- Copy Constructor

- `DEFAULT CONSTRUCTORS:`
    - The default constructor is the constructor that doesn’t take any argument. It has no parameters. 
    - If we have not defined a constructor in our class, then the C++ compiler will automatically create a default constructor with an empty code and no parameters.
- `Parameterized Constructor`
    - A constructor with parameters is known as a parameterized constructor.
    - The parameterized constructor takes its arguments provided by the programmer.
- `Copy Constructor`
    - A copy constructor is a member function that initializes an object using another object of the same class.
    - Shallow copy and Deep Copy Concept
    - Shallow Copy : Pointer Address will be copied
    - Deep Copy : it is done only by user, we have to read the data from poitner and put in the copied object.

## 16. Constructor Overloading
- More than one constructor in a class with the same name,each having different list of argumentsis known as Constructor Overloading.

## Copy Constructor :
```cpp
ClassName (const ClassName &old_obj); 
```
> When is the copy constructor called? 

In C++, a Copy Constructor may be called in the following cases: 
- When an object of the class is returned by value. 
- When an object of the class is passed (to a function) by value as an argument. 
- When an object is constructed based on another object of the same class. 
- When the compiler generates a temporary object.

> When is a user-defined copy constructor needed? 
If we don’t define our own copy constructor, the C++ compiler creates a default copy constructor for each class which does a member-wise copy between objects. The compiler-created copy constructor works fine in general. We need to define our own copy constructor only if an object has pointers or any runtime allocation of the resource like file handle, a network connection, etc.

> Note : Deep copy is possible only with a user-defined copy constructor. In a user-defined copy constructor, we make sure that pointers (or references) of copied objects point to new memory locations.  

- Copy constructor vs Assignment Operator 
    - The main difference between Copy Constructor and Assignment Operator is that the Copy constructor makes a new memory storage every time it is called while the assignment operator does not make new memory storage.

[More Question on Copy Contructor](https://www.geeksforgeeks.org/copy-constructor-in-cpp/?ref=lbp)

## 17.destructor 
- A destructor is a special member function that works just opposite to a constructor(unlike constructors that are used for initializing an object,) destructors destroy (or delete) the object.
- The name should begin with a tilde sign(~) and must match the class name.
- There cannot be more than one destructor in a class.
- Unlike constructors that can have parameters, destructors do not allow any parameter.
- They do not have any return type, just like constructors.
- When you do not specify any destructor in a class, the compiler generates a default destructor and inserts it into your code.

## 18. ACCESS SPECIFIERS
- Access specifiers, are a special type of keywords which are used to specify the accessibility of entities like classes, methods,
    - PUBLIC:  members are accessible from outside the class
    - PRIVATE: members cannot be accessed (or viewed) from outside the class
    - PROTECTED: members cannot be accessed from outside the class, however, they can be accessed in inherited classes.
    
## 19. SOME KEYWORDS
-  `STATIC` [Link](https://www.geeksforgeeks.org/static-keyword-cpp/)
    - When a variable is declared as static, the memory is allocated for the lifetime of the program. Even if the function is called multiple times, space for the static variable is allocated only once and the value can be updated if required

   
## 20. Getter and Setter
- Getters are those functions that allow us to access data members of the object. These are also called accessor functions.
- Setters are the member functions that allow us to change the data members of an object. These are also called mutator functions.

## 21. Scope Resolution Operator

- To access a global variable when there is a local variable with same name
    - ::x ~ global value
    - x local value
- To define a function outside a class.
- To access a class’s static variables.
- In case of multiple Inheritance, If same variable name exists in two parent classes, we can use scope resolution operator to distinguish.
    - class C : public A, public B
    - A::x
    - B::x
- For namespace, If a class having the same name exists inside two namespace we can use the namespace name with the scope resolution operator to refer that class without any conflicts
- Refer to a class inside another class, If a class exists inside another class we can use the nesting class to refer the nested class using the scope resolution operator

```cpp
class outside
{
public:
      int x;
      class inside
      {
      public:
            int x;
            static int y; 
            int foo();
  
      };
};
int outside::inside::y = 5; 
  
int main(){
    outside A;
    outside::inside B;
  
}
```

## DIFFERENCE B/W CONST AND DEFINE
1. Const consumes memory but define doesn't
2. CONSTs are handled by the compiler, where as #DEFINEs are handled by the pre-processor.
3. #defines can’t be type checked while const can.
4. const are considered variables, we can use pointers on them. This means we can typecast, move addresses

## PREPROCESSOR DIRECTIVES

- These are instructions to compiler
```cpp
#define c cout
int main(){
	c<<10;
	return 0;
}
```
```cpp
#define add(x,y)(x+y)
int main(){
	cout<<add(2,3);
	return 0;
}
```
```cpp
#define msg(x) #x

int main(){
	cout<<msg(hello);
	return 0;
}
```

## NAMESPACES
- when we have two different functions but with the same name , then we use namespaces 
- in this , we encapsule the whole function into two different namespaces to avod the ambiguity

![](https://user-images.githubusercontent.com/86204416/176899177-1c48be1b-4f6b-486d-b7bc-3737a4d13908.png)

- we can by default set to call always the first namespace by writting using namespace first 

![](https://user-images.githubusercontent.com/86204416/176899330-b6e6249d-8b9c-4a3b-8748-0ee9fd984c0b.png)

- in c++ , we write using namespace std, to avoid using std::cin or std::cout again n again

## DESTRUCTORS DETAILED
![](https://user-images.githubusercontent.com/86204416/176901476-2cc216aa-04a9-4b5e-9f29-d74b8042f835.png)

- here when program is going to over, then both the classes destructor are called
- first the child class destructor called then parent class

## VIRTUAL DESTRUCTORS

- If we are pointing to one class and making obj of other class, then when destructor is called then automatically it will be called of the parent not of child ,
- to call the child destructor , we use virtual keyword with destructor of parent class












