# Linked List

## 1. Intersection of two linked list [Question](https://leetcode.com/problems/intersection-of-two-linked-lists/)

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
