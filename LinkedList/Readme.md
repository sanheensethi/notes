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

## 11. Intersection of two linked list [Question](https://leetcode.com/problems/intersection-of-two-linked-lists/)

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
