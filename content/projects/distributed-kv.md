+++
title = "Raft Key-Value Store"
description = "A replicated key-value store using the Raft consensus protocol in Go."
date = 2026-01-20
weight = 2

[extra]
tech_stack = ["Go", "Raft", "gRPC"]
github = "https://github.com/yourusername/raft-kv"
demo = ""
featured = true
+++

A distributed key-value store where nodes coordinate state through the Raft consensus algorithm. The cluster keeps working as long as a majority of nodes are reachable.

### Components

* **Leader election**: Nodes use randomized timeouts to trigger elections when heartbeats drop.
* **Log replication**: The leader sends log entries to followers, waiting for a quorum before committing.
* **Compaction**: Old log entries are written to snapshots on disk so the log does not grow indefinitely.
* **gRPC interface**: Exposes basic `Get`, `Put`, and `Delete` calls.

```go
func (kv *KVServer) applyLoop() {
    for msg := range kv.applyCh {
        if msg.CommandValid {
            op := msg.Command.(Op)
            kv.mu.Lock()
            kv.applyOperation(op)
            kv.mu.Unlock()
        }
    }
}
```
