## The Prophet of Floom exposes bugs in distributed systems.

This is dlv code. Download dlv from http://www.dlvsystem.com.

The *_test.dlv programs contain instructions for running.

Dependencies:

```
po.dlv <- po_test.dlv
       <- delivery.dlv <- delivery_test.dlv
                       <- pick_received.dlv <- kv.dlv <- kv_test.dlv  <-+ paxos_test.dlv
                                            <- paxos.dlv              <-+                <- ensemble_test.dlv
```
