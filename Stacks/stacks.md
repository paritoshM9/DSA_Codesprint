<h1>stacks</h1>

Q) Check redundant brackets

#### Given a string mathematical expression, return true if redundant brackets are present in the expression. Brackets are redundant if there is nothing inside the bracket or more than one pair of brackets are present.

##### Assume the given string expression is balanced and contains only one type of bracket i.e. ().

```c++
#include<stack>
using namespace std;

bool checkRedundantBrackets(char *input) {
	// Write your code here
    stack<char> st;
    int c = 0;
    int i = 0;
    while(input[i] != '\0'){
        if(input[i] == ')'){
            while(st.top() != '('){
                st.pop();
                c++;
            }
            if(c == 0){
                return true;
            }
            c = 0;
            st.pop();
            
        }
        else{
            
            st.push(input[i]);
            
            
        }
        i++;
        
    }
    
    return false;
}
```





