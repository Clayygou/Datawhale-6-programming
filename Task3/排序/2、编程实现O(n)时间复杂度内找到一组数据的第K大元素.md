## 编程实现O(n)时间复杂度内找到一组数据的第K大元素
借助快速排序来实现

### 代码实现
```p
def partition(data_list,begin,end):
    #选择最后一个元素作为分区键
    partition_key = data_list[end-1]
 
    #index为分区键的最终位置
    index= begin  
    for i in range(begin,end-1):
        if data_list[i] < partition_key:
            data_list[i],data_list[index] = data_list[index],data_list[i]  #交换
            index+=1
    
    data_list[index],data_list[end-1] = data_list[end-1],data_list[index] #交换
    return index
def find_top_k(data_list,K):
    length = len(data_list)
    begin = 0
    end = length
    index = partition(data_list,begin,end) #这里的partition函数就是上面快排用到的函数
    while index != length - K:
        if index >length - K:
            index = partition(data_list,begin,index)
        else:
            index = partition(data_list,index+1,end)
    return data_list[index]
data_list = [25, 77, 52, 49, 85, 28, 1, 28, 100, 36]
for i in [1,2,3,4,5]:
    print(f"第 {i} 大元素是 {find_top_k(data_list,i)}")
```
