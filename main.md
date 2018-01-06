What keeps you up at night? 😣
====
github.com / BrestJS / 2018-codelunch
by _shimaore_

introduction

## Promises
The Quest of The Simplest Example

```
async function() {
  await sleep(10*secondes)
  console.log('10s plus tard')
}
```

```
const sleep = (timeout) =>
  new Promise( (resolve) =>
    setTimeout(resolve,timeout)
  )
```

```
process.nextTick ≅ (cb) => cb()
// cb is added to "next tick queue"
// wait for event loop completion
// call callbacks in next tick queue
```

```
async function () {
  var a = await do_this();
  await nextTick();
  await do_that(a);
}
```

```
const nextTick = (...args) =>
  new Promise( (resolve) =>
    process.nextTick(resolve,...args)
  )
```

```
const nextTick = () =>
  new Promise( (resolve) =>
    process.nextTick(resolve)
  )
```

## Promises
A Correction

```
async function (ev) {
  await event(ev,'noël')
  console.log('Enfin!')
  livrer_les_cadeaux()
}
…
ev.emit('noël')
```

```
const event = (ev,name) =>
  new Promise( (resolve,reject) => {
    ev.once(name,resolve)
    ev.once('error',reject)
  })
```

Did You Spot The Memory Leak?

```
const event = (ev,name) =>
  new Promise( (resolve,reject) => {
    function cleanup() {
      ev.off(name, on_event)
      ev.off('error', on_error)
    }
    const on_event = (...args) => { cleanup(); resolve(...args) }
    const on_error = (error)   => { cleanup(); reject(error)    }
    ev.once('error',on_error)
    ev.once(name,on_event)
  })
```

## And Now For Something
## Completely Different

## issue #1
build daily reports
from an unbounded data stream

## Currently
- Redis Pub/Sub
- `EventEmitter2`
- build aggregates in Redis
- generate report "manually"

## issue #2
distribute realtime events at scale

## Node.js streams

```
npm install -g stream-adventure
&& stream-adventure
```

`src.pipe(dst)`

`a.pipe(b).pipe(c).pipe(d)` ≅ `a | b | c | d`

Node.js "object streams"
`objectMode:true`

data-in-space
vs
data-in-time

|                       | Single return value | Multiple return values              |
|-----------------------|---------------------|-------------------------------------|
| Pull/Sync/Interactive | Object              | Iterables (Array, Set, Map, Object) |
| Push/Async/Reactive   | Promise             | Observable                          |

### Promise
one time
one sender
many recipients

### EventEmitter
many times
many senders
many recipients

### Observable (DataStream)
- objects that inform other objects
  of the changes they publish
- Fluent/composable:
  `.map`, `.concat`, `.filter`, `.reduce`
- Observable of Observable: `.flatMap`, `.zip`, `.take`

Discrete vs Continuous
Bacon: EventStream / Property
Reactive(haskell): Events / Behaviors

`A.map(…).filter(…)`

```
A.merge(B)
  .onValue(…)
  .onError(…)
  .onEnd(…)
```

RxJs, BaconJS, Kefir.JS
TC39 Proposal

“Promises are Observables”

## Streaming events
inter-machine streaming

Pub/Sub
(Redis, RabbitMQ, MQTT, …)

AWS Streaming Data
Storm
Kafka

de·cen·tra·li·ze!

CERN: 0MQ

Axon
github:tj/axon

Issues
- discovery ("who wants my data?")
- registration ("how do I connect?")

(Similar to registration & message routing in SIP!)

Côte
→ Axon + discoverer
  (but: security?)

Dat
→ "hyperdiscovery"

## Current train of thought
- lightweight P2P (e.g. Axon, NodeRED's)
  between my applications
- at the boundary: "translate" to/from
  0MQ, Sock.js, Socket.io, AMQP, SMTP, …

## Manipulating
## & Composing
## Streams

Node-RED
nodered.org

Node-RED is _very_ cool, except:
- difficult to maintain as "code"
- not "production ready" yet

Amazon Lambda (Step Functions)
Apache Flink

## Aggregating
## is hard

`sum`, `avg`, `count`, `min`, `max`, `stddev`
… easy

median
deciles / percentiles
… harder

(hint: "Bloom filters")

⇒ transducers/transformers

❦ Merci! ❧
==========
github.com / BrestJS / 2018-codelunch
github.com / shimaore
