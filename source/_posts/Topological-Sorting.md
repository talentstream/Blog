---
title: Topological Sorting
date: 2023-05-25 21:57:36
---

#### 介绍

> Topological Sorting(拓扑排序) 主要用于有向无环图（DAG），用来排序点的先后关系或者判断该图是否有环

- 将所有入度为0的点放入栈或队列中
- 然后遍历栈中的点，将点的出度边删除
- 然后重复前两部直到没有点可以放入栈中
- 当出栈数 == 总点数，说明是DAG、

#### 代码

```c++
// 力扣207
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<int> inDegree(numCourses);// 计算每个点的入度
        unordered_map<int,vector<int>> edgeMap;// 存表，在这里不需要排序所以用unordered_map

        // 第一步
        for(auto prerequisite : prerequisites)
        {
            ++inDegree[prerequisite[0]];
            edgeMap[prerequisite[1]].emplace_back(prerequisite[0]);
        }

        queue<int> q;
        for(int i = 0; i < numCourses; ++i) 
            if(inDegree[i] == 0) q.push(i);

        // 循环二三步
        int count = 0;
        while(!q.empty())
        {
            int now = q.front();
            q.pop();
            ++count;
            vector<int> nextCourses = edgeMap[now];
            if(!nextCourses.empty())
            {
                for(int i = 0; i < nextCourses.size(); ++i) 
                {
                    // 删出度边
                    if(--inDegree[nextCourses[i]] == 0) q.push(nextCourses[i]);
                }
            }
        }

        if(count == numCourses) return true;
        else return false;
    }
};
```

#### 参考

- [leetcode - 207. 课程表](https://leetcode.cn/problems/course-schedule/)
- [拓扑排序详解 通俗易懂](https://zhuanlan.zhihu.com/p/339709006)
