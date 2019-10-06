<h1>Trie</h1>

Trie is an efficient information retrieval data structure.
Every node of Trie consists of multiple branches. Each branch represents a possible character of keys. We need to mark the last node of 
every key as end of word node. A Trie node field isEndOfWord is used to distinguish the node as end of word node. 

Huffman Coding also called as Huffman Encoding is a famous greedy algorithm that is used for the lossless compression of data.
It uses variable length encoding where variable length codes are assigned to all the characters depending on how frequently they occur 
in the given text.
The character which occurs most frequently gets the smallest code and the character which occurs least frequently gets the largest code.

### Trie Implementation

Insert in O(|S|) and Erase in O(|S|)

```cpp
struct node {
	node *p[26];
	int count;
	node() {
		count=0;
		memset(p, 0, sizeof(p));
	}
}

class trie {
    node *root;
    public:
	
    trie(){
        root = new node()
    }

    void insert(char *s){
        node *x = root;
        int length = strlen(s);
        for (int i = 0; i < length; i++) {
            if (x->p[s[i] - 'a'] == NULL) {
                x->p[s[i] - 'a'] = new node()
            }
            x = x->p[s[i] - 'a'];
        }
        x->count++;
    }
	
    void erase(char *s){
        node *x = root;
        int length = strlen(s);
        for (int i = 0; i < length; i++) {
            x = x->p[s[i] - 'a'];
        }
        x->count--;
    }
	
};
```
