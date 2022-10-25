# **将关系对转为邻接矩阵**

- #### 方法一：原生操作

```python
relation_list = [('赵四', '王五'), ('赵四', '理论'), ('赵四', '王琦'), ('王五', '王琦'),
                 ('王五', '赵四'), ('王琦', '王五'), ('王琦', '赵四'), ('理论', '赵四')]

member_dict = {}
member_index = 0
for name_tuple in relation_list:
    for name in name_tuple:
        if name in member_dict:
            continue
        member_dict[name] = member_index
        member_index += 1

relation_matrix = [[0 for i in range(len(member_dict))]
                   for i in range(len(member_dict))]

for (x, y) in relation_list:
    x_index = member_dict[x]
    y_index = member_dict[y]
    relation_matrix[x_index][y_index] = 1

print(relation_matrix)
```

- #### 方法二：导包操作

```python
import scipy as sp
import networkx as nx

relation_list = [('赵四', '王五'), ('赵四', '理论'), ('赵四', '王琦'), ('王五', '王琦'),
                 ('王五', '赵四'), ('王琦', '王五'), ('王琦', '赵四'), ('理论', '赵四')]
g = nx.graph(relation_list)
A = nx.to_numpy_matrixx(g)
print(A)
```

