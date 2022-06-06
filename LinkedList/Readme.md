# Linked List

## 1. Intersection of two linked list [Question](https://leetcode.com/problems/intersection-of-two-linked-lists/)

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



#### Method 3:

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

#### Method 2:
