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
- The number of entities to which another entity can be associated through a relationship is known as cardinality

![](https://www.gatevidyalay.com/wp-content/uploads/2018/05/Cardinality-Ratios-in-DBMS.png)

- **Many-to-Many Cardinality**-
    In many-to-many mapping, an entity in E1 is associated with any number of entities in E2, and an entity in E2 is associated with any number of entities in E1.

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

