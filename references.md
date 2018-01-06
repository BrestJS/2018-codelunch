Observables
-----------

- [Observables in ES](https://github.com/tc39/proposal-observable)
- [RxJS](https://github.com/reactivex/rxjs)
- [Kefir](https://kefirjs.github.io/kefir/)
- [BaconJS](https://www.npmjs.com/package/baconjs) and [Node streams](https://www.npmjs.com/package/bacon-node-stream)

Node.js streams
---------------

- https://github.com/ryanramage/living-the-stream-dream
- https://maxogden.com/index.html
- https://github.com/substack/stream-handbook

Streaming
---------

- [AWS Streaming Data](https://aws.amazon.com/streaming-data/)
- [Storm](https://storm.apache.org/talksAndVideos.html)
- [Kafka](https://www.confluent.io/blog/stream-data-platform-1/)

In-stream processing
--------------------

- [NodeRED](https://nodered.org/)
- [Amazon Step Functions](https://aws.amazon.com/step-functions/)
- [Apache Flink](https://en.wikipedia.org/wiki/Apache_Flink)

Note: map-reduce (to name one) is not applicable here because the set size is unbounded.

0MQ
---

- http://zguide.zeromq.org/page:all
- https://github.com/booksbyus/zguide
→ [Paranoid Pirate Pattern](https://www.npmjs.com/package/zeromq-ppqueue)

- https://github.com/edwardchoh/zmqbus-node (auto-discover)
- [Zyre.js](https://www.npmjs.com/package/zyre.js) which implements ZRE, a 0MQ extension for a local bus

Axon
----

Axon: utiliser [`@dashersw/axon`](https://github.com/dashersw/axon). Dans les patches intéressants il y a aussi (potentiellement) [TLS](https://github.com/tj/axon/compare/master...Atlantis-Software:master).

[Côte](https://github.com/dashersw/cote) includes Axon with [node-discoverer](https://github.com/dashersw/node-discover) to auto-build the mesh.

Côte tries to resolve the registration/discovery problem using multicast/broadcast. Côte also supports Redis as a discovery mechanism.

(However Côte is susceptible to attacks by rogue endpoints during the master election; also master is a SPF.)

Transducers
-----------

https://github.com/cognitect-labs/transducers-js#the-transducer-protocol
(which makes the case for [immutable](https://www.npmjs.com/package/immutable))
