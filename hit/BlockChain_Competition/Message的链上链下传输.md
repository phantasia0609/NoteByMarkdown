> 从Kaleido提供的Firefly文档和昕哲学长之前说的一些描述，以及查看的一些论文，我大概总结了一下Message的区块链上链下的message交换的流程。

- 这里的message实际上分为了data和message的两个部分
- 所有的message的交换都是基于参与方遵循了BPMN图所提供的标准的并且被所有参与方认可的标准流程的顺序。（比如提供的编排图）
- 以下面的流程为例详细的过一遍这个Message的分发流程（很大一部分基于我的个人理解）
 ![image.png](https://iili.io/JuAUz9s.png)
#### 参与方
首先可以看出上面的BPMN图的参与方有
1. Customer
2. Retailer
3. Producer
##### 在不讨论流程的分支节点的情况下过一遍流程
- **BPMN图的一些流程规定，在执行当前的任务时，一定不可以进行当前任务之前的任务，并且只有在当前任务执行完毕后才能执行下一步任务。**
1. 开始传入的信息是“Customer询问商品的价格数量”，这个信息是一个链下的信息，可以有Customer的公司的管理员所传入，并且广播“Customer询问商品的价格数量”，具体的询问细节可以通过链下的消息直接发送（FireFly是提供了许多的链下传输信息的接口的）。在Retailer接受到这信息之后需要返回Response信息（商品的价格以及是否可用)，同样的，返回信息的行为仍然需要广播，但具体的细节可以通过链下的进行消息传输。
2. 如果商品不可用，Retailer就需要向Producer发送信息，”Retailer询问产品的数量“，这条信息的传入可以通过Retailer的管理员自己执行，也可以是在上一条信息判定Retailer中货物unavailable之后自动执行。同样的，广播”Retailer询问产品信息“，而实际的询问内容仍然不需要上链，而是直接的经过FireFly提供的API点对点向对应的生产商发送具体的询问内容。Producer进行reponse的信息也需要广播，具体细节仍然不一定要上链
3. 然后Retailer要发送一个支付订单（未支付），这是需要广播的，并且订单的细节也需要广播，以此来防止订单的信息被篡改，以达成企业之间的共识。Producer也需要返回订单的ID，同样将信息的细节广播。
4. Retailer向生产商发送`ship_info(string shipment_address)`消息，提供发货信息，发货信息也应当上链，生产商根据发货信息执行`shipment(string shipInfo)`操作，进行商品发货。
5. Cutomer执行`payment1()`操作，进行支付。广播支付细节，并且链下发送信息给Producer，Producer查看具体的支付细节。Producer返回支付后的细节（需要广播，并且链下发送信息给Customer，让Customer确认已支付的订单。
6. Customer确认已支付的订单后需要传入Address等细节，这同样也需要广播。Producer在接受信息后通过`retail_ship(string customerShipment)`操作来处理订单和安排发货。
7. 最终，客户收到货物，流程以结束事件结束。

消息的具体脸上链下传输在这个例子上可以总结如下：

在基于Hyperledger Firefly的区块链企业协作中，信息传输可以通过链上（on-chain）或链下（off-chain）的方式进行。Hyperledger Firefly 是一个企业级区块链集成的工具，它旨在通过提供一系列的工具和服务(大多数是API)来简化跨企业应用程序和系统的数据交换。

#### 链上（On-Chain）传输
***链上传输通常用于那些需要共识、不可篡改和验证的信息***。在这个流程中，这类信息一般包括：

1. **支付信息**: 如`payment()`和`payment1()`操作，可能会通过区块链来完成，以确保交易的不可篡改性和可追溯性。
2. **订单信息**: `order_info(string orderID)`可能会在链上记录，以利用区块链提供的不可变性，用于验证和审计。
3. **发货信息**: `shipment(string shipInfo)`也可能在链上记录，以确保交易的透明度和供应链追踪。

#### 链下（Off-Chain）传输
***链下传输通常用于不需要共识机制的大量数据或敏感信息***。在这个流程中，下面的信息一般会通过链下方式传输：

1. **询价信息**: 如`retail_quotation(string good, uint amount)`和`quotation(string product, uint quantity)`消息，可能链下传输，因为它们可能包含敏感的商业信息，不需要共识机制。
2. **产品可用性和成本响应**: 如`response(bool availability, uint cost)`和`retail_response(int price, bool av)`，也可能是链下传输，特别是如果这些信息频繁更改或包含敏感的定价数据。
3. **发货细节**: 尽管发货信息可能在链上记录，但详细的物流数据（如`ship_info(string shipment_address)`）可能因其大小或敏感性而链下传输。

Hyperledger Firefly 支持链上和链下的数据传输，并能够同步链上链下状态。它通过智能合约和分布式账本来处理链上交易，并使用现有的消息系统来处理链下数据的传输和通信。

在实际的企业环境中，选择哪些信息通过链上或链下传输，通常取决于业务需求、法规遵从、成本考虑和技术限制，。此外，为了保障隐私和效率，一些数据可能首先在链下进行汇总或加密，然后只将必要的信息或哈希值上链。