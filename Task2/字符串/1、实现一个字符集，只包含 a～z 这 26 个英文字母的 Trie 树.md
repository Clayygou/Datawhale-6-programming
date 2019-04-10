## 实现一个字符集，只包含 a～z 这 26 个英文字母的 Trie 树

分析：Trie树：字典树（N叉树），一种特殊的前缀树结构
前缀树是N叉树的一种特殊形式。通常来说，一个前缀树是用来存储字符串的。前缀树的每一个节点代表一个字符串（前缀）。
每一个节点会有多个子节点，通往不同子节点的路径上有着不同的字符。
子节点代表的字符串是由节点本身的原始字符串，以及通往该子节点路径上所有的字符组成的。

### 代码
```p
class Trie:
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = {}
        self.word_end = -1
 
    def insert(self, word):
        """
        Inserts a word into the trie.
        :type word: str
        :rtype: void
        """
        curNode = self.root
        for c in word:
            if not c in curNode:
                curNode[c] = {}
            curNode = curNode[c]
          
        curNode[self.word_end] = True
 
    def search(self, word):
        """
        Returns if the word is in the trie.
        :type word: str
        :rtype: bool
        """
        curNode = self.root
        for c in word:
            if not c in curNode:
                return False
            curNode = curNode[c]
            
        # Doesn't end here
        if self.word_end not in curNode:
            return False
        
        return True
 
    def startsWith(self, prefix):
        """
        Returns if there is any word in the trie that starts with the given prefix.
        :type prefix: str
        :rtype: bool
        """
        curNode = self.root
        for c in prefix:
            if not c in curNode:
                return False
            curNode = curNode[c]
        
        return True

trie = Trie()
li = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n',
       'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z']
for i in li:
    trie.insert(i)

print(trie.search("r"))
```



## 总结 
     根节点不包含字符，除根结点以外的每个节点只包含一个字符
     从根节点到某一个节点，路径上经过的字符连接起来，为该节点对应的字符串
     每个节点的所有子节点包含的字符串不相同
