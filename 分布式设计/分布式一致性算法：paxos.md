# 算法思想
多数派思想，并且数量大于n/2<br/>
并发环境下的执行顺序
# Basic Paxos
basic paxos抽象出4个角色：
* client:系统外部决策，请求发起者
* proposer:接受client请求，向集群提出提议，并在冲突发生时起到冲突调节的作用
* acceptor:提议投票和接收者，只有在形成法定人数时，提议才会最终被接受
* learner：提议接受者，backup、备份，对集群一致性没有什么影响
## 算法步骤
1、prepare<br/>
proposer提出一个提案，编号为N，N大于这个proposer之前提出的提案编号，请求acceptors的quorum接受<br/>
2、promise<br/>
如果N大于这个accepor之前接受的任何提案编号，则接受，否则拒绝<br/>
3、accept<br/>
如果达到了多数派，proposer会发出accept请求，此请求包含提案编号N以及提案内容<br/>
4、accepted</br>
如果此acceptor在此期间没有收到任何编号大于N的提案，则接受此提案内容，否则忽略。
## 算法流程图
![image](https://github.com/longshengguoji/architecture/blob/master/img/basic%20paxos%E6%B5%81%E7%A8%8B.jpg)
