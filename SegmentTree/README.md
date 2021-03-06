# SegmentTree(线段树)
    线段树主要应用在动态的更新和查询的问题,我们希望通过一种数据结构(线段树)使得查询和更新都在O(logn)时间完成.
    线段树的性质:
    1. 所有的输入元素都在叶子节点.
    2. 线段树是一个完全二叉树,共有n个叶子节点,2n-1个节点.
    3. node i的左右孩子节点分别是i*2+1,i*2+2, 其父节点是(i-1)/2.
    4. 树的高度是[log2N],需要开辟的空间是2*2^(log2n)-1.       

1. [SegmentTree(Sum of given range)](./sum_of_given_range.cpp)
    
    + 查询给定区间[l,r]直接的和,但是有多次查询,而且有动态更新.

2. [range_minimum_query.cpp](./range_minimum_query.cpp)

    + 动态查询区间的最小值,


 3. [lazy_propagation_segmentTree.cpp](./lazy_propagation_segmentTree.cpp)
    
    线段树的延迟传播,在第一节中我们更新一个值,可以用一个简单的递归函数解决,但是如果我们要更新一个区间呢,就需要调用多次这个更新函数,而且每一个都要更新在每一个区间的值.
    例如如果我们更新[2,7],就要调用6次单值更新函数.
    这里还是以区间和为例进行解释延迟传播,延迟传播是一种跟新区间值的
    优化的技术.
    思想是:在更新区间是,我们仅仅在查询的时候进行更新,对其他的延缓更新.     
    [!segment-tree1.png](../assert/segment-tree1.png)
    
    例如图中的节点27,[3-5],如果我们的更新查询是[2,5],我们就需要更新这个节点和所有的子节点.
    如果使用延迟更新,我们可以仅仅更新27这个值,通过存储更新的信息,延后更新所有子节点.我们需要创建一个lazy[]数存贮是否更新的信息.  
    初始化lazy[]={0},如果lazy[i]=0,表示未曾更新,如果lazy[i]!=0表明在查询这个节点之前需要添加到节点i的总数.
    查询的时候,需要判断这个节点是否更新,如果没有更新就先进行更新,否则直接返回.

4. [persistent_segmentTree.cpp](./persistent_segmentTree.cpp)
    
    + 持久化线段树,
    有这样的问题呢,给你一个数组和不同点的更新操作,对每一个更新操作创建一个线段树,
    需要这样的查询:    
        Q v l r: 输出第v的更新后对应的版本的[l,r]的和sum.      
    这个问题的解决方法很简单,我们可以对每一次更新后的数组建一个
    线段树定义版本0--v,但是我们每一次的时间和空间的复杂度都是
    O(nlogn);需要注意一点,每次只是更新一个点,这个点影响的值只有
    其祖先节点,原版本的线段树的其它节点不受影响,注意到这一点,我们
    只要重新创建修改的点,其它的树结构可以公共,只需要记录下来不同
    版本的线段树的节点即可.
5. [design_operate_set.cpp](./design_operate_set.cpp)
    
    + 给你一个空集合,请支持下面的操作:
    * 插入一个新的值x; 
    * 删除一个值x; 
    * 查询集合的中位树.     
    方法1,
    我们可以使用一个数组,vector进行设计,每次进行有序的插入,可以很简
    单的实现代码;也可以是根据最大元素的设置,开始设置一个新的数组空间.  
    方法2,
    使用线段树,我们使用线段树,例如计算如果我们查询[3,7]返回是下标[3,7]之间的和,就可以表示共有几个值.     
    insert x: 表示对应的x的下标的值+1     
    delete x: 表是x的下标对应的值减去1     
    medain : 便是查询线段总和的一半,在那个区间对应的左半区间.
6. [range_lcm_query.cpp](./range_lcm_query.cpp)

    + 查询给定区间的最小公倍数;
    简单明了的方法,直接暴力解决,或者之前存放lcm[i][j]表示[i,j]之间的最小公倍数.      
    线段树的应用,类似有求区间最小化的方法,我们可以构造一个线段树.


7. [MinMax_range_Query.cpp](./MinMax_range_Query.cpp)
    
    + 多次查询数组中的最大值和最小值   
    我们在前面介绍过区间最小值的查询，使用线段树查询，这里我们只需要增加一个维度表示最大值即可
 

8. [Count_and_Toggle_Query_on_BinaryArray.cpp](./Count_and_Toggle_Query_on_BinaryArray.cpp)

    + 给你一个2进制数组，初始时都为false，你有两个操作，Toggle(us,ue),更新数组arr[us,ue]的值，
    修改的要求的true->false， false->true。Count(qs,qe),计算arr[qs,qe]的和。

    解决方式：我们可以使用就简单的更新值，暴力解决即可。前面介绍过一个lazy Propagation的线段树的方式。
    
9. [Querying maximum number of divisors that a number in a given range](./max_number_of_divisors_in_range.cpp)  
    + 查询最大区间中的最大的因子个数，[L,R],L<=X <= R;  
    例如: [1,10]
    1有1个因子，2有2个因子，3有2个因子，4有3个因子，5有2个因子，     
    6有4个因子，7有2个因子，8有4个因子，9有3个因子，10有4个因子，
    最大值是4.

10. [二叉树的最近公共祖先](./LCA_With_RMQ.cpp)

    + 求二叉树的最近公共祖先。转化成RMQ问题，使用线段树提过速度。
    1. 线序遍历二叉树，记录每一个旅行中的节点。存到数组中，euler[]
    2. 记录每个节点的层次，这里的层次是层序遍历中的层，level[],(根节点是第0层)
    3. 记录每一个节点第一个出现在euler tour中的下标。[如图First Occurrence](../assert/first.png)
    [!如图，euler tour](../assert/euler.png)
    算法：
    1. euler tour遍历二叉树，得到euler, level, firstOccurrence 数组。
    2. 使用level数组，构造最小值的线段树
    3. 返回的值对应的是，查询的是节点对应的第一次出现的下标中间的值。如图中的查询节点[4,9]的LCA，
        转化对应的4,9第一个出现的位置[2,7]对应的最小值min，返回euler[min];
    




