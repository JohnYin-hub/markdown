### 图的基本概念

##### 顶点：Vertex；边：Edge；环：Loop；度：Degree

##### 联通分量：可以互相到达的集合

##### 无向图：Undirected Graph

##### 有向图：Directed Grap

有环图、无环图（可能满足树的定义，树就是一种无环图，无环图不一定是树（多个联通分量情况），联通的无环图是树）

连通图生成树



### 图的基本表示：邻接矩阵(AdjMatrix)

1、邻接矩阵就是一个方阵，可以用二维数组表示。

```java
public class ADjMatrix{
  private int V;
  private int E;
  private int[][] adj;
  
  public Adjmatrix(String filename){
  }
    public static void main(String[] args){
      AdjMatrix adjMatrix = new AdjMatrix(filename:"g.txt")
    }
}
```

