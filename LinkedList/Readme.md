# Linked List

## 1. Uses
![Fraz - Uses of Linked List ( Real Life ) EP 1  fxuVD1e66QA - 885x498 - 3m36s](https://user-images.githubusercontent.com/35686407/172987362-65e48efe-2c24-4eef-8b1e-e0112db5e904.png)

## 2. Representation of Linked List

- In Array , we can directly access the position of elements as internally there is mathematical calculation to find the address of element,
- Array is stored in Contiguous memory.

![Fraz - Representation of Linked List (C++ and JAVA) EP 2  Xtvo7Y2q4NA - 885x498 - 2m40s](https://user-images.githubusercontent.com/35686407/172987583-8deb85a0-7182-47bf-8a9f-e54b946e440b.png)

- Whereas, Linked List need not to be in contiguous, in Linked List node, we store data and also the address of next node.

![Fraz - Representation of Linked List (C++ and JAVA) EP 2  Xtvo7Y2q4NA - 885x498 - 5m44s](https://user-images.githubusercontent.com/35686407/172987800-fbae9255-c6a6-4e08-8e70-3eca6349a186.png)

- 1 is head of linked list, we should never loose the head of the linked list, it is the starting point of the linked list, and below is the visulization how linked list is represented in memory.

![Fraz - Representation of Linked List (C++ and JAVA) EP 2  Xtvo7Y2q4NA - 885x498 - 9m50s](https://user-images.githubusercontent.com/35686407/172987842-e90df05b-4dbf-4be0-ad9b-810dc3bc1432.png)

## 3. Delete Node in Linked List (if you didn't given head of linked list, or the previous node of the deleted node)

![Screenshot Capture - 2022-06-10 - 09-35-07](https://user-images.githubusercontent.com/35686407/172988213-da0f2711-257b-4d72-91a7-5143b49cc6c6.png)

In this, given node is 5 , which has to be deleted.

- isme jis dali pr bethe hai, usi ko katne ki koshish kr rhe hai, but agli dali kis-se jodoge pta hi nhi,
- we use trick,
- next node ki value current mae copy krke next node ko delete krenge.

```cpp
void deleteNode(ListNode* node) {
    ListNode* temp = node->next;
    ListNode* temp2 = temp->next;
    swap(node->val,temp->val);
    delete temp;
    temp = NULL;
    node->next = temp2;
}
```

## 4. Arrays vs Linked List

#### A. LL is Memory Efficient
- array suppose 7 size ka bna rhe hai, to system ko, 28 bytes (if int is of 4 byte) dhundni pdegi ikhate memory mae, tbhi array bn payega
- suppose hme linked list 7 size ki bnani hia, and 1 linked list ka node approx 8 bytes hota hai, due to pointer. 56 bytes we need, and haan agar vo different different parts mae bhi present hai 56 bytes, then yes i can create a linked list of size 7, kyuki 8 bytes dhudna itna mushkil nhi hia
- in array memory allocator 28 bytes ko search krega, where 8 byte ko search krega in linked list node
- so 8 byte dhudna aasan hai w.r.t. 28 bytes.

#### B. Array is of Fixed Size, and Linked List of Dynamic size

#### C. Access in array O(1) and in LL O(n) - Random Access in ARRAY

![Fraz - Arrays vs Linked List EP 4  KMc-B051ne8 - 885x498 - 6m08s](https://user-images.githubusercontent.com/35686407/172988981-57f05e1a-1cb9-4843-84bb-90ee9a6eb210.png)

#### D. Deletion in Linked List is Easy, wheather in Array if we delete then right valo ko left mae shift krna hoga. 
- Deletion in LL O(1) if Node pointer is given.
- Deletion in Array O(n)

![Fraz - Arrays vs Linked List EP 4  KMc-B051ne8 - 885x498 - 8m05s](https://user-images.githubusercontent.com/35686407/172989266-da93e120-9562-42b2-be5c-b9d1f157bbb8.png)


> Both have its advantages and disadvantages, it depends on situation which we have to perform.

- Sorting - Arrays
- Image Gallery - Linked List


## 5. Middle of Linked List.

> 3 Cases : Odd length , Even Lenght LL and NULL pointer is given as input.

![Screenshot Capture - 2022-06-10 - 09-54-26](https://user-images.githubusercontent.com/35686407/172990064-4ec946ce-1ceb-40cb-877b-544d3354b24f.png)

#### Approach 1:

- find length of LL,
- traverse upto length/2,
- where you land is Middle Node
- TC : O(n) + O(n/2)

```cpp
int llSize(ListNode* head){
    if(head == NULL) return 0;
    return 1 + llSize(head->next);
}

ListNode* middleNode(ListNode* head) {

    if(head == NULL) return NULL;

    int size = llSize(head);

    ListNode* temp = head;
    int k = size/2;
    while(k--){
        temp = temp->next;
    }

    return temp;
}
```

#### Approach 2:

- suppose 2 person hai, ek x ki speed se chlta hai to ek 2x ki speed se,
- dono ko simultaneously chlao, jb 2x vala bnda last mae poch jayega to hmara x vala bnda middle pr hoga.
- TC : O(n)
- SC : O(1)

![Fraz - Middle of the Linked List EP 5  5blSG0JZNbg - 1536x864 - 7m03s](https://user-images.githubusercontent.com/35686407/172990315-8b1aa941-efcb-417f-9730-066d49f9d9fc.png)

- Two Pointers : slow and fast.
- slow = slow->next
- fast = fast->next->next
- `Odd and Even Lenght ki Linked List ka dhyan rkhe`

```cpp
ListNode* middleNode(ListNode* head) {
        
    if(head == NULL) return NULL;

    ListNode* slow = head;
    ListNode* fast = head;

    while(fast != NULL && fast->next != NULL){
        slow = slow->next;
        fast = fast->next->next;
    }

    return slow;
}
```

## 6. Convert Binary Number in Linked List to Integer

#### Approach 1: Reverse Linked List and convert

- Not Efficient Approach,

![Fraz - Convert Binary Number in a Linked List to Integer EP 6  rPbzUW7usJE - 1536x864 - 4m22s](https://user-images.githubusercontent.com/35686407/172991059-3f3abee1-cdfd-4bf8-b84f-d1021e920550.png)

```cpp
ListNode* newHead = NULL;
ListNode* reverseLL(ListNode* head){
    if(head->next == NULL){
        newHead = head;
        return newHead;
    } 
    ListNode* ll = reverseLL(head->next);
    ll->next = head;
    return head;
}

int getDecimalValue(ListNode* head) {
    if(head == NULL) return 0;

    ListNode* tail = reverseLL(head);
    tail->next = NULL;

    int p = 0;
    int ans = 0;
    while(newHead != NULL){
        ans = ans + pow(2,p)*(newHead->val);
        p++;
        newHead = newHead->next;
    }
    return ans;
}
```

#### Approach 2: Find Length of Linked List

![Fraz - Convert Binary Number in a Linked List to Integer EP 6  rPbzUW7usJE - 853x480 - 5m10s](https://user-images.githubusercontent.com/35686407/172991160-22e0a574-8e99-4b6c-8612-cddd1f3aebcb.png)

```cpp
int size(ListNode* head){
    if(head == NULL) return 0;
    return 1 + size(head->next);
}
int getDecimalValue(ListNode* head) {
    if(head == NULL) return 0;
    int len = size(head);

    int p = len-1;
    int ans = 0;
    while(head != NULL){
        ans = ans + pow(2,p)*(head->val);
        p--;
        head = head->next;
    }
    return ans;
}
```

#### Approach 3:

- In this we assume that, our first node is last node, to vo 2^0 se multiply hona chahiye , koi ni, krdo and ans ko store kr do.
- ab jese hi mae aage gya,use pta chla ki are nhi ye vali last node hai to isko 2^0 se multiply krna hai, to pichle sbhi ki power 1 se increment kr denge.
- ab vha jakr increment nhi krenge, bs ans ko 2 se multuply kr denge and fr current value ko 2^0 se multiply krke add kr denge

![Fraz - Convert Binary Number in a Linked List to Integer EP 6  rPbzUW7usJE - 1435x807 - 6m20s](https://user-images.githubusercontent.com/35686407/172991253-7df46775-6a25-4e6e-a669-d3d405542ae1.png)

![Fraz - Convert Binary Number in a Linked List to Integer EP 6  rPbzUW7usJE - 1536x864 - 6m45s](https://user-images.githubusercontent.com/35686407/172991297-614b32ff-c8d4-43f5-99b2-2d81d4ee1c35.png)

![Fraz - Convert Binary Number in a Linked List to Integer EP 6  rPbzUW7usJE - 1435x807 - 6m53s](https://user-images.githubusercontent.com/35686407/172991303-57bf4d21-8307-4501-8066-1f2ab9baf9b3.png)

![Fraz - Convert Binary Number in a Linked List to Integer EP 6  rPbzUW7usJE - 885x498 - 8m32s](https://user-images.githubusercontent.com/35686407/172991460-1ac57454-5577-4857-829b-e9ffa7a88004.png)

```cpp
int getDecimalValue(ListNode* head) {
    if(head == NULL) return 0;

    int ans = 0;

    ListNode* temp = head; 

    while(temp != NULL){
        ans = ans*2; // when discovered new node so previous all power increase by 1 i.e. each prev values * 2 => ans should be * 2
        ans = ans + (temp->val); // *pow(2,0)
        temp = temp->next;
    }

    return ans;
}
```
## 7. Doubly Linked List (STL ALSO)

- Deletion is Simple in Doubly Linked List,
- Singly LL mae to fr bhi mne trick use krli thi int ke case mae, suppose image hoti to usme trick ni use krenge kuki 2 images ko swap krna is huge task, if we take real world example.

![Fraz - Doubly Linked List and STLs EP 7  cTm0AR5_O54 - 1435x807 - 4m43s](https://user-images.githubusercontent.com/35686407/172993858-35a85c3a-6aa6-4f1b-b873-1cce18c96fa1.png)

![Fraz - Doubly Linked List and STLs EP 7  cTm0AR5_O54 - 1435x807 - 5m01s](https://user-images.githubusercontent.com/35686407/172993860-3982f346-7ade-45a3-9f7d-c0f6af00e88a.png)

- Singly Linked List is `forward list<datatype>` in STL
- Doubly Linked List is `list<datatype>`in STL

![Fraz - Doubly Linked List and STLs EP 7  cTm0AR5_O54 - 853x480 - 7m04s](https://user-images.githubusercontent.com/35686407/172994388-ff16af4c-98bf-4942-be1b-6a0612c582b6.png)


![Fraz - Doubly Linked List and STLs EP 7  cTm0AR5_O54 - 1435x807 - 8m07s](https://user-images.githubusercontent.com/35686407/172994351-177ffb01-d13b-4367-9269-19f68f496124.png)

![Fraz - Doubly Linked List and STLs EP 7  cTm0AR5_O54 - 1536x864 - 7m55s](https://user-images.githubusercontent.com/35686407/172994361-f9892bcb-c2b5-4622-8bea-d51b0f381725.png)

## 8. HashSet

![Fraz - Design HashSet EP 8  IjxkD8L2cOM - 885x498 - 3m28s](https://user-images.githubusercontent.com/35686407/172995890-0342cfcd-b264-41b5-8e1e-8b69e0e7f582.png)

#### Approach 1: Brute - Make array of largest lenght as hash array

![Fraz - Design HashSet EP 8  IjxkD8L2cOM - 853x480 - 5m09s](https://user-images.githubusercontent.com/35686407/172995870-baebc9b5-4842-4193-874e-b66b0d3a814b.png)

- This will work if you can create array of maxRange.
- but if range > 10^7 , it's difficult to create array.

```cpp
vector<int> vec;
    int size;
    MyHashSet() {
        size = 10e6+1;
        vec.resize(size,0);
    }

    void add(int key) {
        vec[key] = 1;
    }

    void remove(int key) {
        vec[key] = 0;
    }

    bool contains(int key) {
        return vec[key] == 1;
    }
```

#### Approach 2: Using Chaining Technique.

- if I had to input 22 and vector array is of length 11, then generate index 22%11 = 0
- 0 or store kr do
- index = number%size
- 0%11 = 0, 11%11 = 11, 22%11 = 0, 33%11 = 0 , Collisions
- Collision Handle 1 method : Chaining method - hm ek list rkhenge and usme traverse krke dekhenge.
- make vector of linked list
- now doubly or singly ?
- jis element pr khade hai vhi delete krna hai to list use krenge, forwardlist mae hme uske pehle vale ka address dena pdega.
- we used doubly linked list

![Fraz - Design HashSet EP 8  IjxkD8L2cOM - 885x498 - 15m28s](https://user-images.githubusercontent.com/35686407/172998764-2474b414-5c57-458c-9b9b-569129b4ccf5.png)


```cpp
class MyHashSet {
public:
    vector<list<int>> vec;
    int size;
    MyHashSet() {
        size = 100;
        vec.resize(size);
    }
    
    void add(int key) {
        if(contains(key)) return;
        int idx = hash(key);
        vec[idx].push_back(key);
    }
    
    void remove(int key) {
        if(!contains(key)) return;
        list<int> :: iterator address = search(key);
        int idx = hash(key);
        vec[idx].erase(address);
    }
    
    bool contains(int key) {
        int idx = hash(key);
        return search(key) != vec[idx].end();
    }

private:
    int hash(int key){
        return key%size;
    }
    
    list<int> :: iterator search(int key){
        int idx = hash(key);
        return find(vec[idx].begin(),vec[idx].end(),key);
    }
};
```
## 9. HashMap

#### Approach 1: Brute - Use Array , key as index value as value in array at index = key

```cpp
class MyHashMap {
public:
    vector<int> vec;
    int size;
    MyHashMap() {
        size = 10e6+1;
        vec.resize(size);
        fill(vec.begin(),vec.end(),-1)
    }
    
    void put(int key, int value) {
        vec[key] = value;
    }
    
    int get(int key) {
        return vec[key];
    }
    
    void remove(int key) {
        vec[key] = -1;
    }
};
```
#### Approach 2: Use Doubly Linked List to store key and value.

```cpp
class MyHashMap {
public:
    vector<list<pair<int,int>>> vec;
    int size;
    MyHashMap() {
        size = 150;
        vec.resize(size);
    }
    
    void put(int key, int value) {
        int idx = hash(key);
        list<pair<int,int>> :: iterator address = search(key);
        
        if(address != vec[idx].end()){
            // key already exists update value
            address->second = value;
        }else{
            // key not exists
            vec[idx].push_back({key,value});
        }
    }
    
    int get(int key) {
        int idx = hash(key);
        list<pair<int,int>> :: iterator address = search(key);
        
        if(address != vec[idx].end()){
            return address->second;
        }else{
            return -1;
        }
    }
    
    void remove(int key) {
        int idx = hash(key);
        
        auto address = search(key);
        
        if(address != vec[idx].end()){
            // key exists
            vec[idx].erase(address);
        }
        return;
    }

private:
    int hash(int key){
        return key%size;
    }
    
    list<pair<int,int>> :: iterator search(int key){
        int idx = hash(key);
        
        list<pair<int,int>> :: iterator it = vec[idx].begin();
        
        while(it != vec[idx].end()){
            if(it->first == key){
                return it;
            }
            it++;
        }
        return vec[idx].end();
    }
};
```
## 10. Reverse Linked List

#### Approach 1: Reverse only values (but ye nhi krna hai.)
- Not the good way to approach
- agar krna hai to , ek vector bnao, usme sari values daal do traverse krke
- ab vector ko traverse kro piche se, and linked list ko fr se traverse kro aage se and put those values

![Fraz - Reverse Linked List EP 10  MsIRa740mQY - 1536x864 - 1m02s](https://user-images.githubusercontent.com/35686407/173001427-ab4879ea-4767-4766-87cd-b7218892c2e3.png)

#### Approach 2: Chainging Pointers

- node ke address same rhenge, bs connections reverse ho jayenge

![Fraz - Reverse Linked List EP 10  MsIRa740mQY - 885x498 - 2m31s](https://user-images.githubusercontent.com/35686407/173003113-e649cf9e-a89a-4ff0-b409-491206e9719c.png)

- 3 Pointers needed, Current, Prev, Next ,
- Currnt jispr khade hai jiska link reverse krna hai
- prev , jisse current ko jodna hai
- jb jod denge cur->next = prev to aage bhadne ke lihye bhi address chahiye , if 3rd pointer nhi lenge so we loose aage ke nodes, so next pointer needed.

![Fraz - Reverse Linked List EP 10  MsIRa740mQY - 885x498 - 7m51s](https://user-images.githubusercontent.com/35686407/173003643-0e6e10ff-a1c8-47b0-b531-443ea35d6f60.png)

> Iterative:

```cpp
ListNode* reverseList(ListNode* head) {
    if(head == NULL) return NULL;

    ListNode* prev = NULL;
    ListNode* cur = head;
    ListNode* next = NULL;

    while(cur != NULL){
        next = cur->next;
        cur->next = prev;
        prev = cur;
        cur = next;
    }
    return prev;
}
```

> Recursion:

![Fraz - Reverse Linked List EP 10  MsIRa740mQY - 853x480 - 14m22s](https://user-images.githubusercontent.com/35686407/173004449-640a5a3b-881e-4bec-bf8b-901b2bae3710.png)

- Recursion 2 se kaam krwakr le aaya.
- newHead mne alag se store kr lia 

```cpp
ListNode* newHead = NULL;
    
ListNode* reverseLL(ListNode* head){
    if(head->next == NULL){
        newHead = head;
        return newHead;
    }

    ListNode* ll = reverseLL(head->next);
    ll->next = head;
    
    return head;
}

ListNode* reverseList(ListNode* head) {
    if(head == NULL) return NULL;

    ListNode* tail = reverseLL(head);
    tail->next = NULL;
    
    return newHead;
}
```
## 11. Reverse Nodes in k-Group

![Fraz - Reverse Nodes in k-Group EP 11  TeDcLjOOiK4 - 1536x864 - 3m54s](https://user-images.githubusercontent.com/35686407/173005382-82c02a09-1442-4571-b4de-c192490bbcad.png)

> Recursive:

![Fraz - Reverse Nodes in k-Group EP 11  TeDcLjOOiK4 - 1435x807 - 10m42s](https://user-images.githubusercontent.com/35686407/173006816-3588aca6-93f5-4602-ab3a-b3e2b769c19d.png)

- mae first 2 ko change krwaunga, baki recursion khud kaam krdega, first k nodes , if k = 2, then use muje reverse krwana aata hi hai. by iterative or recursive kese bhi krwa lu.
- kai baar jb end ko aage move kr rhe honge niche solution mae esa bhi ho skta hai ki, end null ho jaye lekin k group pure na ho, to us case mae hum head ko hi return kr denge.
- TC : O(n)
- SC : O(n/k) ~ Auxillary Recursion Stack Space

```cpp
void reverse(ListNode* start,ListNode* end){
        ListNode* prev = NULL;
        ListNode* cur = start;
        ListNode* next = NULL;
        
        while(prev != end){
            // we know prev is becoming new Head and also end we know is new head , therefore we end while loop like this
            
            next = cur->next;
            cur->next = prev;
            prev = cur;
            cur = next;
        }
    }
    
    ListNode* reverseKGroup(ListNode* head, int k) {
        if(head == NULL || head->next == NULL || k == 1) return head;
        
        ListNode* start = head;
        ListNode* end = head;
        // now move head, k-1 times to know from where to where we have to reverse manualy.
        
        int inc = k-1;
        
        while(inc--){
            end = end->next;
            if(end == NULL) return head; // esa bhi ho skta hai, k group pure na ho
        }
        
        ListNode* end_next = end->next;
        
        reverse(start,end); // when reverse, end become head and start become tail
        
        ListNode* aageKaHead = reverseKGroup(end_next,k);
        
        start->next = aageKaHead;
        
        return end;
    }
```
> Iterative: (To Tell to the interviewer) O(1) Memory Optimized.

![Fraz - Reverse Nodes in k-Group (NO EXTRA SPACE) EP 12  dbRJFnQoKTI - 885x498 - 11m20s](https://user-images.githubusercontent.com/35686407/173027300-15d451a0-3754-4d9f-9635-e1005deaeb5b.png)

- isme hum recursive solution ko iterative bnayenge,
- ek dummy node bnaya usko next ko head pr lga dia,
- ab, hum ek pointer bna rhe hai before start name ka usko dummy pr rkh dia,
- and end ko head pr
- to ab end ko k-1 tk move krenge jb move ho jayega to hmara start = beforestart ka next hoga,
- ab start to end reverse krdo, lekin reverse krne se pehle ye dekh lo, uske baad kin kin pointers ko jodna hai, to kya unka address store hai tumhare paas ? if nhi hai to store kr lo, jese afterEnd store kr rha hai end->next, ye jb reverse ho jayega to next kaam afterEnd se hi start hoga.

```cpp
class Solution {
public:
    
    void reverse(ListNode* start,ListNode* end){
        ListNode* prev = NULL;
        ListNode* cur = start;
        ListNode* next = NULL;
        
        while(prev != end){
            // we know prev is becoming new Head and also end we know is new head , therefore we end while loop like this
            
            next = cur->next;
            cur->next = prev;
            prev = cur;
            cur = next;
        }
    }
    
    ListNode* reverseKGroup(ListNode* head, int k) {
        if(head == NULL || head->next == NULL || k == 1) return head;
        
        ListNode* dummy = new ListNode(-1);
        dummy->next = head;
        ListNode* beforeStart = dummy;
        ListNode* end = head;
        
        int i = 0;
        while(end != NULL){
            i++;
            if(i%k != 0){
                end = end->next;
            }else{
                ListNode* start = beforeStart->next;
                ListNode* afterEnd = end->next;
                reverse(start,end);
                beforeStart->next = end;
                start->next = afterEnd;
                beforeStart = start;
                end = afterEnd;
            }
        }
        return dummy->next;
    }
};
```
## 12. Merge Two Sorted Linked List

#### If Allowed by Interviewer to change the structure.

> Recursive:

![Fraz - Merge Two Sorted Lists EP 13  0QPpgAsd4IY - 885x498 - 5m07s](https://user-images.githubusercontent.com/35686407/173037700-5d5fc3d8-4de7-4f75-b48f-0b6897f16b00.png)

![Fraz - Merge Two Sorted Lists EP 13  0QPpgAsd4IY - 853x480 - 5m27s](https://user-images.githubusercontent.com/35686407/173037740-08ed41dd-0af9-4baa-840f-04769be7de41.png)

- agar h1 chota hai to h1->next = call lgado jisme h1 ko aage bhadado, and h2 apni jagah rehne do
- agar h2 chota hai to h2->next = call lgado jisme h2 ko aage bhadado and h1 apni jagah rehne do

```cpp
ListNode* merge(ListNode* h1,ListNode* h2){
    if(h1 == NULL) return h2;
    if(h2 == NULL) return h1;

    if(h1->val <= h2->val){
        h1->next = merge(h1->next,h2);
        return h1;
    }else{
        h2->next = merge(h1,h2->next);
        return h2;
    }
}

ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
    return merge(list1,list2);
}
```
> Iterative:
- Create a dummy node, and mark it also as cur pointer,
- dummy->next will store ans head address
- cur->next we will join pointers here.
- agar `h1->val <= h2->val` then `cur->next = h1`, and h1 ko aage bhadao `h1 = h1->next`
- agar `h1->val > h2->val` then `cur->next = h2`, and h1 ko aage bhadao `h2 = h2->next`
- agar ek bhi null ho jati hai, to dusri ko join kr do cur ke next mae.

![Fraz - Merge Two Sorted Lists EP 13  0QPpgAsd4IY - 885x498 - 13m42s](https://user-images.githubusercontent.com/35686407/173044045-c0eee150-0002-4fa3-a9fc-bd34db05aae9.png)

```cpp
ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
    if(list1 == NULL) return list2;
    if(list2 == NULL) return list1;

    ListNode* dummy = new ListNode(-1);
    ListNode* cur = dummy;


    while(list1 && list2){
        if(list1->val <= list2->val){
            cur->next = list1;
            list1 = list1->next;
        }else{
            cur->next = list2;
            list2 = list2->next;
        }
        cur = cur->next;
    }
    if(list1 == NULL) cur->next = list2;
    else cur->next = list1;
    return dummy->next;
}
```
## 13. Merge K-sorted Linked List

#### Appraoch 1: Brute Force
- Store all elements in vector
- sort and create new linked list and return
- TC : NK*log(NK)
- SC : NK

![Fraz - Merge k Sorted Lists EP 14  RYJ3vs8qx10 - 1536x864 - 3m31s](https://user-images.githubusercontent.com/35686407/173045413-009450aa-57a2-415b-a34d-8bc7cc0aa0c0.png)

#### Approach 2: Take two linked list at a time and merge
- 2 / 2 linked list lekr merge kro
- pehle first 2 ko krdo usse ke new linked list aayegi
- us new linked list ko agle valo ke sath ek ek uthakr merge krte rho
- we will do this in total k-1 times

#### Approach 3: 
- Sari Linked List ke starting pr pointers rkh denge
- ab jo smallest element milega among all pointers,compare and smallest le lo
- Total Nodes N*K hai

![Fraz - Merge k Sorted Lists EP 14  RYJ3vs8qx10 - 885x498 - 5m46s](https://user-images.githubusercontent.com/35686407/173046363-f2bf00f3-a731-4579-ba9c-426bfa148cdd.png)

![Fraz - Merge k Sorted Lists EP 14  RYJ3vs8qx10 - 885x498 - 6m55s](https://user-images.githubusercontent.com/35686407/173046525-1db2b7d3-6564-4296-81e9-5a88186c2492.png)

#### Approach 4: Heap (Min Heap)
- whenever we get question jisme hme har baar minimum chahiye to sorting bhi use kr skte hai, ya min heap bhi kr skte hai min heap mae insert bhi kr skte hai, vector mae sort krna pdta.
- Heap mae dalo nikalo, top pr minimum element hi rehta hai
- Insert : NlogN in Heap
- Get : NlogN from Heap
- Dekhne ke liye : O(1) time lgega,
- We put all first K nodes in Heap, l1,l2,l3,l4 --- lk
- ek element bhr nikala and uska next heap mae daal dia, jon= nikala usko join kr do.
- TC : O(logK)
- SC : O(K) ~ heap mae at max K nodes pdi hai.

![Fraz - Merge k Sorted Lists EP 14  RYJ3vs8qx10 - 885x498 - 11m34s](https://user-images.githubusercontent.com/35686407/173047726-53449122-797a-4f9c-a928-794f314679cf.png)

```cpp
class myCompare{
public:
    bool operator()(const ListNode* a,ListNode* b){
        return a->val > b->val;
    }    
};

class Solution {
public:
    
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        priority_queue<ListNode*,vector<ListNode*>,myCompare> pq;
        
        for(int i = 0;i < lists.size(); i++){
            if(lists[i]!=NULL){
                pq.push(lists[i]);
            }
        }
        
        ListNode* dummy = new ListNode(-1);
        ListNode* cur = dummy;
        
        while(!pq.empty()){
            ListNode* node = pq.top();
            pq.pop();
            if(node->next != NULL) pq.push(node->next);
            cur->next = node;
            cur = cur->next;
        }
        cur->next = NULL;
        return dummy->next;
    }
};
```

## 14. Remove Dublicates From Sorted Linked List

> Recursive

- mae recursion ko khunga merse aage sare dublicates hta de, to vo muje vo 1 2 3 return kr dega last vala 3 nhi krega hta dega.
- ab jo recursion se aayega, usko mae compare krunga abhi vale head se, ki bhai tu mere equal hai ye nhi agar hota hai to head ko skip krke recursion vala ans de denge
- otherwise, agar equal nhi hota to hum abhi vale head ko recursion se attach krke, return kr denge head ko

![Fraz - Remove Duplicates from Sorted List EP 15  _Dc1IqY2WpQ - 885x498 - 3m20s](https://user-images.githubusercontent.com/35686407/173051930-b9612372-e215-4edc-ba71-783523ac551f.png)

```cpp
ListNode* remove(ListNode* head){
    if(head->next == NULL) return head;

    ListNode* recAns = remove(head->next);
    if(recAns->val == head->val){
        return recAns;
    }else{
        head->next = recAns;
        return head;
    }
}

ListNode* deleteDuplicates(ListNode* head) {
    if(head == NULL) return NULL;
    return remove(head);
}
```
> Iterative:

![Fraz - Remove Duplicates from Sorted List EP 15  _Dc1IqY2WpQ - 1536x864 - 6m36s](https://user-images.githubusercontent.com/35686407/173053686-229ee499-f519-42e2-9168-c5eb8fbc3827.png)

- agar meri abhi vali value mere aage vale ke sath equal hui, to mae abhi ke next ko aage ke next ke sath join kr dunga and aage vala delete kr dunga
- if value equal na hui to aage bhad jaunga

```cpp
ListNode* deleteDuplicates(ListNode* head) {
        ListNode* cur = head;
        while(cur != NULL && cur->next != NULL){
            if(cur->val == cur->next->val){
                ListNode* del = cur->next;
                cur->next = del->next;
                delete del;
            }else{
                cur = cur->next;
            }
        }
        return head;
    }
```
## 15. Linked List Cycle

#### Approach 1: (HashMap)

![Fraz - Linked List Cycle (With Proof) EP 16  nbQUEN3IRFk - 853x480 - 3m02s](https://user-images.githubusercontent.com/35686407/173055735-a7f12e44-6cd9-4e35-b4c2-c3c20c3c61ee.png)

- Linked List ko traverse krna start kro, if 1 bhi node 2 bari aa jaye to mtlb vha cycle hai
- We can use any ds like `HashMap`
- TC : O(n)
- SC : O(n)

#### Approach 2: (Slow and Fast Pointer)

![Fraz - Linked List Cycle (With Proof) EP 16  nbQUEN3IRFk - 885x498 - 4m44s](https://user-images.githubusercontent.com/35686407/173056162-cd73efbc-a0fd-437f-9ccf-b08e52654019.png)

```cpp
bool hasCycle(ListNode *head) {
    ListNode *slow = head,*fast = head;
    while(fast != NULL && fast->next != NULL){
        slow = slow->next;
        fast = fast->next->next;
        if(slow == fast) return true;
    }
    return false;
}
```

> Proof:

![Fraz - Linked List Cycle (With Proof) EP 16  nbQUEN3IRFk - 1536x864 - 12m34s](https://user-images.githubusercontent.com/35686407/173057323-49abe0af-5cbc-4d1a-ae2b-d59e5c74494f.png)

## 16. Detect Starting Point of The Cycle in Linked List

![Fraz - Linked List Cycle II (with proof) EP 17  tsQT0MT73Og - 885x498 - 2m02s](https://user-images.githubusercontent.com/35686407/173057896-d86f20b2-14ea-48b1-8663-fa6b587a5ec7.png)

- d = n-k , if wjhole ciricle is n

![Fraz - Linked List Cycle II (with proof) EP 17  tsQT0MT73Og - 885x498 - 6m46s](https://user-images.githubusercontent.com/35686407/173058625-729088af-ceed-49a5-9f33-0d54b77fe5dd.png)

- pehle check kro, slow and fast milte hai aapas mae ya nhi, mtlb loop hai bhi ya nhi,
- jb mile, fast ko dobara starting point pr rkho, ab dono ko 1 distance se chlao same speed se, to jha milenge vhi first point hoga cycle ka

```cpp
ListNode *detectCycle(ListNode *head) {
    ListNode *slow = head,*fast = head;

    while(fast!=NULL && fast->next != NULL){
        slow = slow->next;
        fast = fast->next->next;
        if(slow == fast) break;
    }

    if(fast == NULL || fast->next == NULL) return NULL;

    fast = head;

    while(slow != fast){
        slow = slow->next;
        fast = fast->next;
    }
    return slow;
}
```

## 17. Intersection of two linked list [Question](https://leetcode.com/problems/intersection-of-two-linked-lists/)

![Fraz - Intersection of Two Linked List EP 18  DGEqY5rLyVc - 1536x864 - 5m00s](https://user-images.githubusercontent.com/35686407/172180060-3c3e8077-7cdb-41f0-80c1-72a7ed665d44.png)


#### Method 1: Brute Force

- Steps:
    1. tempA ko ek ek krke aage bhadao. first linked list ke element pr pointer ek ek krke aage bhadao
    2. for each tempA, traverse all second linked list
    3. if somewhere you found tempA == tempB , that is ans,
    4. if not, tempA ko fr se ek bhadao, and tempB ko starting pr rkhlr fr se pura traverse kro.
    5. TC : O(M X N) , M = No. of nodes in LL1 and N = No. of nodes in LL2
    
```cpp
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        
        ListNode *tempA = headA;
        ListNode *tempB = headB;
        
        ListNode *ans = NULL;
        
        while(tempA != NULL){
            
            bool found = false;
            
            while(tempB != NULL){
                
                if(tempA == tempB){
                    ans = tempA;
                    found = true; 
                    break;
                }
                
                tempB = tempB->next;
            }
            
            tempB = headB;
            
            if(found == true) break;
            
            tempA = tempA->next;
        }
        
        return ans;
        
    }
```

### Method 2: Using HashMap

- Steps:
    1. ek list ko traverse krke map mae daal do
    2. ab dusre ko traverse krte wakt find kro ki vo map mae exists krti hai ya nhi ?
    3. jese hi pehli node mile jo krti hai , return krdo us address ko
    4. otherwise return null
    5. TC : O(m+n)
    6. SC : O(m or n) whatever you put in hashmap

```cpp
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        
        unordered_map<ListNode*,bool> umap;
        
        ListNode* tempA = headA;
        
        while(tempA != NULL){
            umap[tempA] = true;
            tempA = tempA->next;
        }
        
        ListNode* tempB = headB;
        
        while(tempB != NULL){
            if(umap.find(tempB) != umap.end()){
                return tempB;
            }
            tempB = tempB->next;
        }
        
        return NULL;
    }
```



#### Method 3: (Size of LinkedList Method)

- Steps:
    1. Dono linked list ka size nikalo
    2. diff = abs difference nikalo sizes ka, jo ye bayega kiske paas jada nodes hai or kitne jada nodes hai
    3. jiske paas jada nodes honge uske pointer ko pehle hi diff jitna chla do aage, isse dono barabar lenght mae aa jayegi
    4. ab dono ko ikahte chlao , jha mili vo intersection point hai.

```cpp
int size(ListNode* head){
        int count = 0;
        while(head != NULL){
            count++;
            head = head->next;
        }
        return count;
    }
    
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        int sizeA = size(headA);
        int sizeB = size(headB);
        
        ListNode *tempA = headA;
        ListNode *tempB = headB;
        
        // nodes difference nikala
        int diff = abs(sizeA - sizeB);
        
        // jo jada hai uske pointer ko utna aage move kr dia
        if(sizeA > sizeB){
            while(diff--){
                tempA = tempA->next;
            }
        }else{
            while(diff--){
                tempB = tempB->next;
            }
        }
        
        // dono ikate 1 step se chlao
        while(tempA != tempB){
            tempA = tempA->next;
            tempB = tempB->next;
        }
        
        // dono mil gye, to vhi node hai intersection vali.
        return tempA;
        
    }
```

#### Method 4:

![Fraz - Intersection of Two Linked List EP 18  DGEqY5rLyVc - 885x498 - 12m24s](https://user-images.githubusercontent.com/35686407/172188867-55f3e129-1f88-4f40-854e-2bc1c6846e9f.png)


1. Intuation:
    - suppose L1 m+x length ki hai, x is common list length from intersection
    - suppose L2 n+x kength ki hai, x is common list length from intersection
    - `L1 = (m+x)` and `L2 = (n+x)`
    - to suppose mae L1 ko kuch length or traverse krwadu i.e., n+x ~ L1 = (m+x) + `(n+x)`
    - suppose mae L2 ko kuch length or traverse krwadu i.e., m+x ~ L2 = (n+x) + `(m+x)`
    - ab yha se L1 = L2 hogyi, so, we are able to move them together.
 
2. Steps:
    - tempA = headA
    - tempB = headB
    - tempA and tempB ko aage bhadao ikate,
    - jo pehle null pr pohcha , usko uske opposite mae initialize krdo and aage bhadao
    - agar dusre vala bhi null hogya , usko bhi uske opposite mae initialize krdo
    - ab dono barabar jagag pr synchronize hogye
    - ab dono ko ikate chlao,
    - jha vo mile vo intersection point.

```cpp
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        // let L1 = (m+x)
        // let L2 = (n+x)
        
        ListNode* tempA = headA;
        ListNode* tempB = headB;
        
        // now L1 = (m+x) + (n+x)
        // now L2 = (n+x) + (m+x)
        
        // to make both pointer sync
        
        while(tempA != tempB){
            
            if(tempA == NULL) tempA = headB;
            else tempA = tempA->next;
            
            if(tempB == NULL) tempB = headA;
            else tempB = tempB->next;
            
        }
        
        return tempA;
    }
```
## 18. Palindrome Linked List

![Fraz - Palindrome Linked List EP 19  XYY2tc_8KDM - 1536x864 - 1m50s](https://user-images.githubusercontent.com/35686407/173061014-b8376ca9-b677-43bc-a700-34cb8a8edde8.png)

#### Approach 1: vector mae dalo and check kro

#### Approach 2: Reversal

- Even :
![Fraz - Palindrome Linked List EP 19  XYY2tc_8KDM - 885x498 - 3m09s](https://user-images.githubusercontent.com/35686407/173061111-27be92e0-204f-4c45-8c62-da1b77907fcc.png)

- Odd:
![Fraz - Palindrome Linked List EP 19  XYY2tc_8KDM - 853x480 - 4m17s](https://user-images.githubusercontent.com/35686407/173061289-6ff207e2-7291-43c4-9514-13d89e1a8e73.png)

![Fraz - Palindrome Linked List EP 19  XYY2tc_8KDM - 885x498 - 3m57s](https://user-images.githubusercontent.com/35686407/173061242-b10e3706-6aa8-42bf-94a0-920dd592fbea.png)

- Find midlle se pehle ka point
- Do reversal after middle
- check for palindrome
- again reverse whom you reverse
- connect pointers to maintain structure of LL.
- return ans

```cpp
ListNode* reverse(ListNode* head){
    ListNode* prev = NULL, *next = NULL;
    ListNode* cur = head;
    while(cur!=NULL){
        next = cur->next;
        cur->next = prev;
        prev = cur;
        cur = next;
    }
    return prev; // newHead
}

ListNode* middle(ListNode* head){
    ListNode* slow = head,*fast = head;
    while(fast->next != NULL && fast->next->next != NULL){
        slow = slow->next;
        fast = fast->next->next;
    }
    return slow;
}

bool isPali(ListNode* h1,ListNode* h2){
    while(h1 && h2){
        if(h1->val != h2->val) return false;
        h1 = h1->next;
        h2 = h2->next;
    }
    return true;
}

bool isPalindrome(ListNode* head) {
    ListNode* firstLLTail = middle(head);
    ListNode* secondLL = firstLLTail->next;
    firstLLTail->next = NULL;
    secondLL = reverse(secondLL);

    bool ans = isPali(head,secondLL);

    secondLL = reverse(secondLL);
    firstLLTail->next = secondLL;

    return ans;
}
```
## 19. Remove Linked List Elements

![Fraz - Remove Linked List Elements EP 20  JrRoR7ycM8U - 885x498 - 2m42s](https://user-images.githubusercontent.com/35686407/173065592-c6bf3164-6f3f-4938-a800-7a366a389e4b.png)

> Iterative:

- Take dummy, dummy->next = head
- Now normal traverse and delete the nodes
- Why Dummy ? maybe there is head also which as same value as val, we need prev to whom we update prev->next,
- changing head again and again is complex part, that is why we take dummy node which have dummy->next as head of new LL after removing elements

```cpp
ListNode* removeElements(ListNode* head, int val) {
        
    ListNode* dummy = new ListNode(-1);
    dummy->next = head;
    ListNode* prev = dummy;
    ListNode* cur = head;

    while(cur != NULL){
        if(cur->val == val){
            ListNode* del = cur;
            prev->next = cur->next;
            cur = cur->next;
            delete del;
        }else{
            prev = cur;
            cur = cur->next;
        }
    }
    return dummy->next;
}
```
> Recursive:

- hum mankr chlenge recursion aage ka kaam krke la dega, muje abhi current value pr kaam krna hai.
- to recursion call lgadi head->next mae,
- ab jo bhi recursion se ans/address of head aaya usko recAns mae store kr liya
- ab, abhi vali value agar same hai given val ke, to return krdo recAns
- otherwise, abhi vale address ke next mae recAns lgakr return krdo abhi vala address.

```cpp
ListNode* remove(ListNode* head,int val){
        
    if(head == NULL || head->val == NULL) return NULL;

    ListNode* recAns = remove(head->next,val);

    if(head->val == val){
        return recAns;
    }else{
        head->next = recAns;
        return head;
    }

}

ListNode* removeElements(ListNode* head, int val) {
    return remove(head,val);
}
```

## 20. Design Browser History [Question](https://leetcode.com/problems/design-browser-history/)

![Fraz - Design Browser History EP 21  SPDhPuMsM9A - 1536x864 - 3m02s](https://user-images.githubusercontent.com/35686407/173070911-270e2e77-8f7e-48ba-af7b-226890479827.png)

- if same tabe se new website pr visit kre to forward history sari delete ho jati hai srf backward history rehti hai

![Fraz - Design Browser History EP 21  SPDhPuMsM9A - 1435x807 - 4m41s](https://user-images.githubusercontent.com/35686407/173070933-be339b06-a1e0-4ce1-bb41-b3a132cbeb69.png)

![Fraz - Design Browser History EP 21  SPDhPuMsM9A - 1435x807 - 4m44s](https://user-images.githubusercontent.com/35686407/173071049-d77eff41-8d72-43d4-9539-1ccc2996b475.png)

- ek iterator bhi rkhna hoga, jo ye btaega current aap konc website pr ho.

```cpp
class BrowserHistory {
public:
    list<string> history;
    list<string> :: iterator it;
    
    BrowserHistory(string homepage) {
        history.push_back(homepage);
        it = history.begin();
    }
    
    void visit(string url) {
        auto del = it;
        del++;
        history.erase(del,history.end());
        history.push_back(url);
        it++;
    }
    
    string back(int steps) {
        while(it != history.begin() && steps--){
            it--;
        }
        return *it;
    }
    
    string forward(int steps) {
        while(it != (--history.end()) && steps--){
            it++;
        }
        return *it;
    }
};
```
## 21. Copy List with Random Pointer

#### Approach 1: Using HashMap

- we create hashmap of node and its copy node
- now after creating hashmap,
- for next pointer : a->next = b then, mp[a]->next = mp[a->next]
- and for random pointer : a->random = d , then : mp[a]->random = mp[a->random]
- TC : O(n)
- SC : O(n)

![Fraz - Copy List with Random Pointer ( with extra space ) EP 23  ctFmFbeyTVU - 885x498 - 9m03s](https://user-images.githubusercontent.com/35686407/173106639-8e8b4a82-e0ff-4b31-8713-2b3b2ae087fa.png)

```cpp
class Solution {
public:
    void fillMap(Node* head,unordered_map<Node*,Node*>& umap){
        while(head != NULL){
            Node* copy = new Node(head->val);
            umap[head] = copy;
            head = head->next;
        }
    }
    
    Node* setRandom(Node* head,unordered_map<Node*,Node*>& umap){
        Node* newHead = umap[head];
        while(head != NULL){
            umap[head]->next = umap[head->next];
            umap[head]->random  = umap[head->random];
            head = head->next;
        }
        return newHead;
    }
    
    Node* copyRandomList(Node* head) {
        if(head == NULL) return NULL;
        unordered_map<Node*,Node*> umap;
        fillMap(head,umap);
        return setRandom(head,umap);
    }
};
```

#### Approach 2:

![Fraz - Copy List with Random Pointer ( NO extra space ) EP 24  uBjpRedaNKQ - 885x498 - 7m25s](https://user-images.githubusercontent.com/35686407/173106890-d17a8748-53ca-4d41-82b9-679e2061a26d.png)

- TC : O(n)
- SC : O(1)
- first create copy node and attach it to real node
- now a->next->random = a->random->next , if a->random != NULL
- then detach nodes and restructure the given linked list and also, return new linked list.


```cpp
class Solution {
public:
    void CopyList(Node* head){
        Node* temp = head;
        while(temp){
            Node* copy = new Node(temp->val);
            Node* next = temp->next;
            temp->next = copy;
            copy->next = next;
            temp = next;
        }
    }
    
    void setRandom(Node* head){
        Node* temp = head;
        while(temp){
            if(temp->random != NULL){
                temp->next->random = temp->random->next;    
            }
            temp = temp->next->next;
        }
    }
    
    Node* detach(Node* head){
        Node* temp = head;
        Node* dummy = new Node(-1);
        Node* cur = dummy;
        while(temp){
            cur->next = temp->next;
            cur = cur->next;
            temp->next = cur->next;
            temp = temp->next;
        }
        Node* ret = dummy->next;
        delete dummy;
        return ret;
    }
    
    Node* copyRandomList(Node* head) {
        if(head == NULL) return NULL;
        CopyList(head);
        setRandom(head);
        return detach(head);
    }
};
```
