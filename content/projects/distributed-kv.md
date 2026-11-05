+++
title = "Raft Distributed Key-Value Store"
description = "A fault-tolerant, replicated key-value storage engine implementing the Raft consensus algorithm with gRPC communication."
date = 2026-01-20
weight = 2

[extra]
tech_stack = ["Go", "Raft", "gRPC", "Protobuf", "BoltDB"]
github = "https://github.com/yourusername/raft-kv"
demo = ""
featured = true
+++

## Overview

A strongly consistent, distributed key-value storage engine engineered to survive network partitions and node crashes. The system coordinates state transitions across an $N$-node cluster using the **Raft consensus algorithm**.

### Core Architecture

1. **Leader Election**: Randomized election timeouts, term numbers, and vote quorum mechanics.
2. **Log Replication**: AppendEntries RPCs with log consistency checks and committed index updates.
3. **Log Compaction & Snapshots**: Automated snapshotting prevents log storage unbounded growth and accelerates slow node recovery.
4. **Client API**: gRPC endpoints supporting `Get`, `Put`, `Delete`, and linearizable read requests.

```go
// Example state machine apply loop
func (kv *KVServer) applyLoop() {
    for msg := range kv.applyCh {
        if msg.CommandValid {
            op := msg.Command.(Op)
            kv.mu.Lock()
            kv.executeOperation(op)
            kv.mu.Unlock()
        }
    }
}
```
