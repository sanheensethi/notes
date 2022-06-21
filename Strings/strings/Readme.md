# Strings

## 1. Check one string is rotation of other string or not [Question](https://www.geeksforgeeks.org/a-program-to-check-if-strings-are-rotations-of-each-other/)

#### Appraoch 1:

- rotate a string by 1 - 1 rotation, moment it matches return true
- else return false
- rotate it to the end of the string
- e.g. ABCD ~ BCDA ~ CDAB ~ DABC ~ ABCD = which is same as starting string. if string is of 4 size, possible rotations = 3

![undefined-1655807742537](https://user-images.githubusercontent.com/35686407/174780536-56e1c023-339b-4a4e-95d6-28c6b824937b.jpg)


#### Approach 2:

- temp = str1 + str1;
- now check the str2 in temp, as it is substring in temp

> Check with Find Function

> Check with strstr Function (KMP Algorithm)

![undefined-1655807719136](https://user-images.githubusercontent.com/35686407/174780556-0a65898c-026e-43d3-bf25-0ce786a24d48.jpg)


#### Approach 3:

- Take Queue,
- put str1 and str2 in queue
- ab k = q2.length
- jb tk k 0 nhi ho jata , tb tk q2 mae se element nikalo piche daal do queue mae,
- isse actually hum rotations hi generate kr rhe hai ek trh se
- q1 q2 ko compare kro, if same then return true
- when k == 0 and same bhi nhi aaye to return false;

![undefined-1655807730726](https://user-images.githubusercontent.com/35686407/174780571-7230ac30-5c40-4aa6-a9dc-6ea3d0075861.jpg)
