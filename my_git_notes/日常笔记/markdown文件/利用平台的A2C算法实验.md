利用平台的PPO算法实验

###（一）学习总结

1.使用Rllib中PPO算法对atari游戏环境进行实验，分别使用8、16、32个节点查看达到收敛的曲线

###（二）实验总结

1.PPO

算法原理:PPO算法  https://www.jianshu.com/p/9f113adc0c50
实验硬件环境: 

1 个 Ray Head节点：1个GPU | 10个CPU核心 | 20G内存
6 个 Ray Node节点：0个GPU | 10个CPU核心 | 20G内存

实验软件环境: 

BreakoutNoFrameskip-v4 环境
10.10.10.1:5000/wargame/ray-deploy:cuda10 镜像

实验效果

增加节点（8->16）运行时间变短，reward值变大；但是当增加节点（16->32）时运行时间反而变长，reward值略微减小

![image-20200730212950834](lmq-img/image-20200730212950834.png)

（红色：num_works:8  橙色：num_works:16  蓝色：num_works:32）

实验问题分析：
问题1：在测试ppo算法的时候，使用64个节点任务长时间处于停滞状态

![image-20200730194808107](lmq-img/image-20200730194808107.png)

猜测原因：Head节点资源不足“卡住了”
解决方案：换用Node节点重新执行

###（三）代码托管


 项目描述