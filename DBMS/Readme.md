## File System vs DBMS

[Link](https://www.javatpoint.com/dbms-vs-files-system)
|BASIS|DBMS|FILE SYSTEM|
|---|---|---|
|Meaning|DBMS is a collection of data. In DBMS, the user is not required to write the procedures.|The file system is a collection of data. In this system, the user has to write the procedures for managing the database.|
|Searching|Searching Fast|Searching Slow||
|Data Access|1kb (By Query)|25GB|
|Data about Data|Access|Not Access|
|Concurrency|Multiple People uses same website, at 1 time 1000/2000 people are doing trasaction in IRCTC (DBMS mae protocol exits krte hai)|No Protocols|
|Security|Role based kaam hai, sara data sbhi nhi access kr skte (Role base access control)|No Security, controled by OS, No hirrarchical system|
|Redundancy/Data Dublicacy|There is no Redundancy if we design the good structure|File system mae same data in multiple directories|



## Architecture

#### 2 Tier Example
 
- Indian Railways : agar station pr jakr form fill krke or ticket reserve krwau, jo khidki ke dusri side bethe hai, uske paas ek machine hai client machine, usme vo information dalenge, and database mae se us train ki detail call krenge and kaam krenge
- Bank mae physicaly jakr form bhrke credit/debit krwa rha hu, unke paas client machine hai clerk ke paas,jo sb check krke credit/debit krenge
- limited clinets hai, auntenticated
- maintaince is easy

> Disadvantages :

- Scalability
- problem with scalabiiy
- number of users bhtt jayeda hai, data access krna hai kisi bhi time pr , tb ye architecture fail ho jata hai
- security : client database se direct access , then they create problem


#### 3 Tier Architecture

- interface hai, php/java/node anything
- query process in business layer/Application Server
- Database Server
- User ko pta hi nhi data actual mae kha pr pda hai
- web application sari 3 tier architecture hai


## Schema

- Logical Representation of Database
- How data is represented
- RDBMS


## 3 Schema Architecture

![image](https://user-images.githubusercontent.com/35686407/184066441-71935cea-b843-42f4-9c8e-c03e356082f1.png)

- Any data which is stored, what is it's structure ?
- Data ko save krne ke liye 2D table mae daal dia

- Motive : Data Indepedance
- User needs not to know where data is store

> External Schema : View Level

> Conceptual : ER Model 

> Physical Level : Database Adminn , how data is stored - Centralized / Distributed

- Actual mae harddisk ke andar Files ki form mae store ho rha hai, lekin hme vo viwe show hota hai jo Physical level pr decide ho rha hai.


## Who maintain refrential integrity : Foreign Key
