# 贪心算法(Greedy)

1. [Action Select Problem](./action_select_problem.cpp)

    + 活动选择问题，
    有n个活动，每一个活动都有一个开始时间和结束时间,问一个人能够最多参加多少个活动。   
    这是一个经典的区间不相交问题的最大个数。我们可以用贪心解决这个问题。
    1. 根据结束时间对所有的活动排序，
    2. 在时间不冲突的情况下，从头到尾遍历所有活动，得到最大的活动个数
2. [kruskal](./kruskal.cpp)

    + kruskal最小支持树算法
    题目描述：有一个无向图，找到n-1边是这个图的n个点全部相连，是的这n-1条边的权重最小。   
    首先我们知道MST理论，最小支持属原理。存在而且唯一。
    kruskal算法：
    + 根据边的权重升序排序素有的边
    + 选择一个最小的边，检查这个边加入后是否组成一个环，如果不是就选择，否则就去掉。
    + 重复2，直到选择到n-1个边。
    我们需要使用并查集加速这个算法。有关资料见3和4

3. [detect Cycle in an Undirected Craph](./detect_cycle.cpp)
    + 检查一个无向图是否存在一个环。
    + 并查集(对所有的相关点设置一个相同的祖先，表示他们相连)


