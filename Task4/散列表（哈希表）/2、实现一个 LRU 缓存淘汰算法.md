## 实现一个 LRU 缓存淘汰算法
LRU（Least recently used）最近最少使用算法。由于缓存的大小固定，最近出现的元素会被保存，之前的元素会被删除。
### 代码
```p
class LRUcache:
    def __init__(self, size=3):
        # 缓存大小固定为3
        # keys 排名由顺序表示
        self.cache = {}
        self.keys = []
        self.size = size

    def get(self, key):
        #取值
        if key in self.cache:
            self.keys.remove(key)
            self.keys.insert(0, key)
            return self.cache[key]
        else:
            return None

    def set(self, key, value):
        if key in self.cache:
            self.keys.remove(key)
            self.keys.insert(0, key)
            self.cache[key] = value
        elif len(self.keys) == self.size:
            # 删除最老的元素
            old = self.keys.pop()
            self.cache.pop(old)
            self.keys.insert(0, key)
            self.cache[key] = value
        else:
            self.keys.insert(0, key)
            self.cache[key] = value

if __name__ == '__main__':
    test = LRUcache()
    test.set('a',2)
    test.set('b',2)
    test.set('c',2)
    test.set('d',2)
    test.set('e',2)
    print(test.get('c'))           # 2
    test.set('f',2)
    print(test.get('b'))           # None
    print(test.get('a'))           # None
    print(test.get('e'))           # 2     只保留了后3个e,c,f的值

```

### 总结
代码中的set和get都表示使用元素，但是使用get的时候，如果get的元素不在缓存中的话，就不会再次加入缓存。
