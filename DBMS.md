# DBMS(Database Management System)

Other Notes Links:
- [DBMS](https://github.com/sanheensethi)
- [CN]() 
- [OS]()


## Database
- It is an organized collection of interrelated information that show some aspects of the real world. Database System is designed to make the information easily accessible and manageable.

## DBMS

Database Management System. It is a software which is used to manage the data easily. It provides an interface to perform various operations like creating database , creating table in it , insertion , updation , deletion of data and lot more.
It provides security to the data and maintain consistency.

> DBMS allow users to maintain the following tasks.
1. **Data Defination** : It is used to create update delete the defination that defines the organization of data in databse.
2. **Data Updation** : It is used to insert , delete , update the actual data in the database.
3. **Data Retrival** : It is used to retrive the data from the databse to use in various applications.
4. **User Administration** : It is used to register and monitoring users and data. It enforces the data security and monitoring recovery information curroupted by unexpected failures.

> Characteristics : 
- Provide clear and logical view of process that manipulates the data
- Contain Automatic backup and recovery procedures
- Provide Security of the data
- Reduce complex relationship between the data
- It can view the data in various viewpoints according to the requirement of the users.
- It contains ACID properties which maintain the data in healty state in case of failure.
- ACID - Automacity,Consistency,Isolation, Durability

> Advantages : 
- **Data Sharing** : Autorised users of an organization can share tge data among various users.
- **Easily Maintenance** : It can be easily maintained due to centralized nature of the database.
- **Backup and Recovery** : It provides backup and recovery features which is used during the hardware and software failures.
- It Provides multiple user interface like GUI , API (graphical user interface and application program interface)

> Disadvantages :
- **Cost of Hardware and Software** : Reuqire high speed of data processor and large memory size to run DBMS efficiently.
- **Size** : It occupies Large space of disks and large memory to run them efficiently.
- **Higher Impact of Failure** : Failure impact the database highly  because in most of the organization, all the data is placed in a single darabase and if database is corruped then data may lost forever.

## ER-Diagram
*ER-Diagram* : It stands for Entity Relationship Diagram.

- It is a conceptual model that gives graphical representation of the logical structure of the database.
- It shows all the constraints and relationships among the entities.
- An ER-Diagram has three main components : 
    1) Entity
    2) Relationships
    3) Attributes

> Entity: An object which has a physical existence is entity. For E.g. : Student is an entity

> Attribute : It is used to describe the property of an entity, for e.g. Student has attributes like rollnumber , name , dob , address etc.

> Relationship : It is used to describe the connection between entities.
    
`Enrolled in` is a relationship that exists between entities Student and Course.

![https://www.gatevidyalay.com/relationship-sets/](https://www.gatevidyalay.com/wp-content/uploads/2018/05/Relationship-in-ER-Diagram-Example.png)

## Entity Sets and Relationship Set

• Entity Set - set of same type of entities

- **Strong entity set** : 
  1) it is an entity set that contains sufficient attributes that can uniquely identify all its entities.
  2) In this , primary key exists for a strong entity set.
  3) it is represented by underline

- **Weak entity set** : 
   1) an entity set that does not contain sufficient attribute that can uniquely identify all its entities.
   2) a primary key doesnot exist for a weak entity set
   3) it contains a partial key called discriminator
   4) discriminator can identify a group of entites from the entity sets.
   5) discriminator is represented by underlining with a dashed line.


• Relationship Set : A relationship set is a set of relationships of same type.

-Example: Set representation of above ER diagram is-

![https://www.gatevidyalay.com/relationship-sets/](https://www.gatevidyalay.com/wp-content/uploads/2018/05/Set-Representation-of-ER-Diagram.png)

> Degree of a Relationship Set-
    # Degree of a relationship set = Number of entity sets participating in a relationship set

[Types of Relationship Sets] -
![https://www.gatevidyalay.com/relationship-sets/](https://www.gatevidyalay.com/wp-content/uploads/2018/05/Type-of-Relationship-Sets.png)

 1. **Unary Relationship Set** : It is a relationship where only one entity set participate in a relationship set.
Example: One person is married to only one person
![](https://www.gatevidyalay.com/wp-content/uploads/2018/05/Unary-Relationship-Set.png)

 2. **Binary Relationship Set** : It is a relationship where only two entity sets participates in a relationship set.
 Example: Student is enrolled in a Course.
![](https://www.gatevidyalay.com/wp-content/uploads/2018/05/Binary-Relationship-Set.png)

 3. **Ternary Relationship Set** : It is a relationship set where only three entity set participates in a relationship set.
 ![](https://www.gatevidyalay.com/wp-content/uploads/2018/05/Ternary-Relationship-Set-1.png)
 
 4. **N-ary Relationship Set** : where `n` entity sets particitaes in relationship set.
 

## Cardinality Constraint

- The number of entities to which another entity can be associated through a relationship.
- We have four types of cardinality constraints.

![](https://www.gatevidyalay.com/wp-content/uploads/2018/05/Cardinality-Ratios-in-DBMS.png)

- **Many-to-Many Cardinality**-
    In many-to-many mapping, an entity in E1 is associated with any number of entities in E2, and an entity in E2 is associated with any number of entities in E1.
    (Association - to make a connection between people or things in your mind)
    
![](https://static.javatpoint.com/dbms/images/dbms-mapping-constraints4.png)
    
    Example: Here,
    1. One student can enroll in any number (zero or more) of courses.
    2. One course can be enrolled by any number (zero or more) of students.
    
![](https://www.gatevidyalay.com/wp-content/uploads/2018/05/Many-to-Many-Relationship-ER-Diagram.png)

- **Many-to-One Cardinality**-
    In one-to-many mapping, an entity in E1 is associated with at most one entity in E2, and an entity in E2 is associated with any number of entities in E1.

![](https://static.javatpoint.com/dbms/images/dbms-mapping-constraints3.png)
    
    Example: Here,
    1. One student can enroll in at most one course.
    2. One course can be enrolled by any number (zero or more) of students.
    
    ![](https://www.gatevidyalay.com/wp-content/uploads/2018/05/Many-to-One-Relationship-ER-Diagram-1.png)
    
- **One-to-Many Cardinality**-
 In one-to-many mapping, an entity in E1 is associated with any number of entities in E2, and an entity in E2 is associated with at most one entity in E1.

![](https://static.javatpoint.com/dbms/images/dbms-mapping-constraints2.png)
    
    Example: Here,
    1. One student can enroll in any number (zero or more) of courses.
    2. One course can be enrolled by at most one student.
    
![](https://www.gatevidyalay.com/wp-content/uploads/2018/05/One-to-Many-Relationship-ER-Diagram.png)
    
- **One-to-One Cardinality**-
    In one-to-one mapping, an entity in E1 is associated with at most one entity in E2, and an entity in E2 is associated with at most one entity in E1.

![](https://static.javatpoint.com/dbms/images/dbms-mapping-constraints.png)
    
    Example: Here,
    1. One student can enroll in at most one course.
    2. One course can be enrolled by at most one student.
    
![](https://www.gatevidyalay.com/wp-content/uploads/2018/05/One-to-One-Relationship-ER-Diagram.png)

## Attributes
> It is used to describe the property of an entity

> There exist a specific domain or set of values for each attribute from where that attribute can take its values.

### Types of Attributes-

![](https://www.gatevidyalay.com/wp-content/uploads/2018/06/Attributes-in-DBMS-Types.png)

- Simple attributes
- Composite attributes
- Single valued attributes
- Multi valued attributes
- Derived attributes
- Key attributes

`Simple attributes -` : Simple attributes are those attributes which can not be divided further.
Example: Here, all the attributes are simple attributes as they can not be divided further.

![](https://www.gatevidyalay.com/wp-content/uploads/2018/06/Simple-Attributes-Example.png)
    
`Composite Attributes -` : Composite attributes are those attributes which are composed of many other simple attributes. (Which can be further divided).
Example: Here, the attributes “Name” and “Address” are composite attributes as they are composed of many other simple attributes.

![](https://www.gatevidyalay.com/wp-content/uploads/2018/06/Composite-Attributes-Example.png)

`Single Valued Attributes -` : Single valued attributes are those attributes which can take only one value for a given entity from an entity set.
Example: Here, all the attributes are single valued attributes as they can take only one specific value for each entity.

![](https://www.gatevidyalay.com/wp-content/uploads/2018/06/Single-Valued-Attributes-Example.png)

`Multi Valued Attributes -` : Multi valued attributes are those attributes which can take more than one value for a given entity from an entity set.
Example: Here, the attributes “Mob_no” and “Email_id” are multi valued attributes as they can take more than one values for a given entity.

![](https://www.gatevidyalay.com/wp-content/uploads/2018/06/Multi-Valued-Attributes-Example.png)

` Derived Attributes -` : Derived attributes are those attributes which can be derived from other attribute(s).
Example: Here, the attribute “Age” is a derived attribute as it can be derived from the attribute “DOB”.

![](https://www.gatevidyalay.com/wp-content/uploads/2018/06/Derived-Attributes-Example.png)

`Key Attributes - ` : Key attributes are those attributes which can identify an entity uniquely in an entity set.
Example : Here, the attribute “Roll_no” is a key attribute as it can identify any student uniquely.

![](https://www.gatevidyalay.com/wp-content/uploads/2018/06/Key-Attributes-Example.png)

## KEYS 

(Do any one defination)
- It is set of attribute that uniquely identifies any record from the table.
- A key is a set of attributes that can identify each tuple uniquely in the given relation.

> Different Types Of Keys in DBMS -

*Video* - [Youtube Link](https://youtu.be/RRUeFwuJ39Q)

There are following 10 important keys in DBMS - 

    Super key
    Candidate key
    Primary key
    Alternate key
    Foreign key
    Partial key
    Composite key
    Unique key

![](https://www.gatevidyalay.com/wp-content/uploads/2018/04/Keys-in-DBMS.png)

- `Super Key` : 
    1. It the combination of all possible attributes that can be uniquely identify the rows in the given relation.
    2. A super key may consist of any number of attributes.
    
    Example-
    Consider the following Student schema-
    - Student ( roll , name , sex , age , address , class , section )
    Given below are the examples of super keys since each set can uniquely identify each student in the Student table
    - ( roll , name , sex , age , address , class , section )
    - ( class , section , roll )
    - (class , section , roll , sex )
    - ( name , address )

NOTE - 
All the attributes in a super key are definitely sufficient to identify each tuple uniquely in the given relation but all of them may not be necessary.
    
- `Candidate Key` : 
    1. A minimal super key is called as a candidate key.
    2. It is an attribute with uniquely identify a tuple
    Example-
    Consider the following Student schema-
    - Student ( roll , name , sex , age , address , class , section )
    
    Given below are the examples of candidate keys since each set consists of minimal attributes required to identify each student uniquely in the Student table-
    - ( class , section , roll )
    - ( name , address )

NOTES -
1. All the attributes in a candidate key are sufficient as well as necessary to identify each tuple uniquely.
2. Removing any attribute from the candidate key fails in identifying each tuple uniquely.
3. The value of candidate key must always be unique.
4. The value of candidate key can never be NULL.
5. It is possible to have multiple candidate keys in a relation.
6. hose attributes which appears in some candidate key are called as prime attributes.

- `Primary Key` :
    1. It is one of the candidate key which uniquely identify the tuple in a table.
    2. A primary key is a candidate key that the database designer selects while designing the database.

NOTES-
- The value of primary key can never be NULL.
- The value of primary key must always be unique.
- The values of primary key can never be changed i.e. no updation is possible.
- The value of primary key must be assigned when inserting a record.
- A relation is allowed to have only one primary key.

![](https://www.gatevidyalay.com/wp-content/uploads/2018/04/Super-Key-Candidate-Key-Primary-Key.png)

- `Alternate Key` : 
    1. Alternate keys out of all the candidate is only one get selected as primary key but the remaining ki are alternate keys.
    2. Unimplemented candidate keys are called as alternate keys.
    
- `Foreign Key` :
    It is used to link the two tables together it references the primary key of another table
    Example : Here, t_dept can take only those values which are present in dept_no in Department table since only those departments actually exist.
    ![](https://www.gatevidyalay.com/wp-content/uploads/2018/04/Foreign-Key.png)

NOTES-
- Foreign key references the primary key of the table.
- Foreign key can take only those values which are present in the primary key of the referenced relation.
- Foreign key may have a name other than that of a primary key.
- Foreign key can take the NULL value.
- There is no restriction on a foreign key to be unique.
- In fact, foreign key is not unique most of the time.
- Referenced relation may also be called as the master table or primary table.
- Referencing relation may also be called as the foreign table.


- `Composite Key` : 
    1. It having more than one attribute to identify the tuple is called the composite key.
    2. A primary key comprising of multiple attributes and not just a single attribute is called as a composite key.

- `Unique Key` : Unique key is a key with the following properties-
    1. It is unique for all the records of the table.
    2. It may have a NULL value.
    3. Once assigned, its value can not be changed i.e. it is non-updatable.
   
    Example:
    The best example of unique key is Adhaar Card Numbers.
    - The Adhaar Card Number is unique for all the citizens (tuples) of India (table).
    - If it gets lost and another duplicate copy is issued, then the duplicate copy always has the same number as before.
    - Thus, it is non-updatable.
    - Few citizens may not have got their Adhaar cards, so for them its value is NULL.
