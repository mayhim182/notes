# Stock exchange functional requirements
1. Buy and sell stocks at low latency according to limit order book
2. Cancel open orders, get volume of open orders at limit price

# Capacity Estimates
1. 100k messages per second at peak (eg message : BUY HDFC 100(QTY) 2000(PRICE) TIMESTAMP)
2. On an average 20 bytes per message
3. Therefore 20 gb/day
# API Design

# Matching Engine
(Is also responsible for broadcasting using udp multicast)
Limit Order Book
**Sell Tree**

**Buy Tree**

each node has a linkedlist

and two sets of hashmap
one hashmap points to every single start of the LinkedList \
second within each limit pointing to each node

what's the use? 
1. During cancellation let's say for any order we can directly take out the node from linkedlist
2. We can get the traffic of order at each node

UDP Multicast
1. Maximum fairness (since everything sent one)
2. Faster no handshakes required

Retransmitters
Second matching engine
Shard using tickers

![[lowlatencystockexchange.png]]


Q&A
Transaction Cache: An **in-memory, ultra-fast key-value store** that temporarily stores incoming transactions (orders, trades, cancellations) before they are committed to a persistent store (like an SQL DB).
Transaction sql db: A **relational database** (like PostgreSQL or MySQL) that stores all **confirmed transactions** for long-term durability, audit, and compliance.
retransmitters: A **resilience mechanism** that **detects missed or corrupted messages** (due to packet loss, network issues) and **re-sends them** to clients or internal systems.
tickers: In a **low-latency stock exchange system**, **tickers** (i.e., market data updates) are generated and **sent by the exchange itself**, typically via a **Market Data Broadcaster** component.
