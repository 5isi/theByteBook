# 共识问题

基于状态机的分布式系统最关键的是决定输入的顺序，因为相同的输入顺序才能使所有的非错误成员达到相同的状态，这样才能保证每一个成员之间的数据一致性，并能随时构建无限个一模一样的状态机（分布式成员）。

为了使一组成员拥有相同的一组输入，我们需要在状态机上再设计一个保证协议，即共识算法。

## 共识算法

共识问题是指，在分布式系统中，要求一组成员根据它们的输入，就共同输出达成共识，在分布式环境中，每个成员都可能因为请求顺序而接受不同的值，并且每个成员都可能发生故障，因此，想让所有的成员按照相同的顺序执行一系列操作并不容易。实现这一过程，能让分布式集群即使是在部分节点故障、网络延时、网络分割的情况下，仍能最终表现出整体一致的过程，就被称为各个节点的协商共识。

共识算法更多用于提高系统的容错性，共识算法的目的允许让分布式系统内部暂时存在不一致的状态，但要保证大多数节点的状态达成一致。同时，在外部看来，集群系统要始终保证整体一致性的状态。Paxos、ZAB、Raft 都属于共识算法。

但是，还是要注意，分布式事务 和 共识协议解决的是两类问题：

- 2PC 等协议解决的是分布式事务一致性，目标侧重于 ACID。
- Paxos/raft 解决的是副本间数据的一致性和高可用，存储的数据完全一致，目标侧重于集群系统容错能力。

