---
title: Trie
date: 2023-05-25 20:23:41
---

#### 介绍

> Trie(字典树) 是一种树形结构，用于高效存储和检索字符串集中的键。

- Trie 是一个多叉树，通常是英文单词，有26个字母为26叉
- 我们只要存储子节点，和一个bool变量来判断到达该节点时是否构成一个单词集里的词
- 通常有Insert和Search两个函数

假设有单词表有n个单词，单词最长长度为m

|Operation|	时间复杂度|	空间复杂度|
| ----------- | ----------- |------------|
|Insertion|	O(m)	|O(n*m)|
|Searching|	O(m)	| O(1)|

![](https://cdn.jsdelivr.net/gh/talentstream/PictureCDN/OSTEP/20230525202618.png)

#### 示例代码

```c++
#include <iostream>
#include <vector>

const int CHILDREN_SIZE = 26;
using std::cout;
using std::endl;

class TrieNode
{

private:
    bool isEndOfWord; // 该节点是否是一个单词的结尾
    std::vector<TrieNode *> children;// 该节点的子节点

public:
    TrieNode() : isEndOfWord(false), children(26, 0) {}

    void Insert(std::string word)
    {
        TrieNode *node = this;
        for (auto c : word)
        {
            if (node->children[c - 'a'] == nullptr)
                node->children[c - 'a'] = new TrieNode();
            node = node->children[c - 'a'];
        }
        node->isEndOfWord = true;
    }

    bool Search(std::string word)
    {
        TrieNode *node = this;
        for (auto c : word)
        {
            node = node->children[c - 'a'];
            if (node == nullptr)
                return false;
        }

        return node->isEndOfWord;
    }
};

int main()
{
    std::string keys[] = {"the", "a", "there",
                          "answer", "any", "by",
                          "bye", "their"};

    TrieNode *obj = new TrieNode();
    for (auto key : keys)
        obj->Insert(key);

    std::string words[] = {"the","these","thire","their","th","thaw"};
    char output[][32] = {"Not present in trie", "Present in trie"};

    for (auto word : words)
        cout << word << " --- " << output[obj->Search(word)] << endl;
    return 0;
}

// Trie.cpp             output
// the --- Present in trie
// these --- Not present in trie
// thire --- Not present in trie
// their --- Present in trie
// th --- Not present in trie
// thaw --- Not present in trie
```