# 并查集

## 模板

```java
class UnionFind {
    int[] father;
    int[] rank;

    UnionFind(int n) {
        this.father = new int[n];
        this.rank = new int[n];
        for (int i = 0; i < n; i++) {
            father[i] = i;
            rank[i] = 1;
        }
    }

    int find(int x) {
        return father[x] == x ? x : (father[x] = find(father[x]));
    }

    boolean isConnected(int x, int y) {
        return find(x) == find(y);
    }

    void union(int x, int y) {
        int fx = find(x);
        int fy = find(y);

        if (fx != fy) {
            if (rank[fx] == rank[fy]) {
                father[fy] = fx;
                rank[fx]++;
            } else if (rank[fx] > rank[fy]) {
                father[fy] = fx;
            } else {
                father[fx] = fy;
            }
        }
    }
}
```

## 题目1：省份数量

链接：[547. 省份数量](https://leetcode.cn/problems/number-of-provinces/)

```java
class Solution {
    public int findCircleNum(int[][] isConnected) {
        int n = isConnected.length;
        UnionFind uf = new UnionFind(n);

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                if (isConnected[i][j] == 1) {
                    uf.union(i, j);
                }
            }
        }

        return uf.size();
    }

    class UnionFind {
        int[] father;
        int[] rank;
        int size;

        UnionFind(int n) {
            this.father = new int[n];
            this.rank = new int[n];
            for (int i = 0; i < n; i++) {
                father[i] = i;
                rank[i] = 1;
            }
            this.size = n;
        }

        int find(int x) {
            return father[x] == x ? x : (father[x] = find(father[x]));
        }

        void union(int x, int y) {
            int fx = find(x);
            int fy = find(y);

            if (fx != fy) {
                if (rank[fx] == rank[fy]) {
                    father[fy] = fx;
                    rank[fx]++;
                } else if (rank[fx] > rank[fy]) {
                    father[fy] = fx;
                } else {
                    father[fx] = fy;
                }
                size--;
            }
        }

        int size() {
            return this.size;
        }
    }
}
```

## 题目2：判断二分图

链接：[785. 判断二分图](https://leetcode.cn/problems/is-graph-bipartite/)

```java
class Solution {
    public boolean isBipartite(int[][] graph) {
        int n = graph.length;
        UnionFind uf = new UnionFind(n);

        for (int i = 0; i < n; i++) {
            if (graph[i].length == 0) continue;

            int first = graph[i][0];
            for (int j : graph[i]) {
                if (uf.isConnected(i, j)) {
                    return false;
                }

                uf.union(first, j);
            }
        }

        return true;
    }

    class UnionFind {
        int[] father;
        int[] rank;

        UnionFind(int n) {
            this.father = new int[n];
            this.rank = new int[n];
            for (int i = 0; i < n; i++) {
                father[i] = i;
                rank[i] = 1;
            }
        }

        int find(int x) {
            return father[x] == x ? x : (father[x] = find(father[x]));
        }

        boolean isConnected(int x, int y) {
            return find(x) == find(y);
        }

        void union(int x, int y) {
            int fx = find(x);
            int fy = find(y);

            if (fx != fy) {
                if (rank[fx] == rank[fy]) {
                    father[fy] = fx;
                    rank[fx]++;
                } else if (rank[fx] > rank[fy]) {
                    father[fy] = fx;
                } else {
                    father[fx] = fy;
                }
            }
        }
    }
}
```
