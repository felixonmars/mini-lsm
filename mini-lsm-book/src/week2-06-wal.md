# Write-Ahead Log (WAL)

![Chapter Overview](./lsm-tutorial/week2-06-overview.svg)

In this chapter, you will:

* Implement encoding and decoding of the write-ahead log file.
* Recover memtables from the WALs when the system restarts.

## Task 1: WAL Encoding

In this task, you will need to modify:

```
src/wal.rs
```

In the previous chapter, we have implemented the manifest file, so that the LSM state can be persisted. And we implemented the `close` function to flush all memtables to SSTs before stopping the engine. Now, what if the system crashes (i.e., powered off)? We can log memtable modifications to WAL (write-ahead log), and recover WALs when restarting the database. WAL is only enabled when `self.options.enable_wal = true`.

The WAL encoding is simply a list of key-value pairs.

```
| key_len | key | value_len | value |
```

You will also need to implement the `recover` function to read the WAL and recover the state of a memtable.

## Task 2: Integrate WALs

In this task, you will need to modify:

```
src/mem_table.rs
src/wal.rs
src/lsm_storage.rs
```

`MemTable` has a WAL field. If the `wal` field is set to `Some(wal)`, you will need to append to the WAL when updating the memtable. In your LSM engine, you will need to create WALs if `enable_wal = true`. You will also need update the manifest using the `ManifestRecord::NewMemtable` record when new memtable is created.

## Task 3: Recover from the WALs

In this task, you will need to modify:

```
src/lsm_storage.rs
```

If WAL is enabled, you will need to recover the memtables based on WALs when loading the database. You will also need to implement the `sync` function of the database. The basic guarantee of `sync` is that the engine is sure that the data is persisted to the disk (and will be recovered when it restarts). To achieve this, you can simply sync the WAL corresponding to the current memtable.

```
cargo run --bin mini-lsm-cli -- --enable-wal
```

## Test Your Understanding

* When can you tell the user that their modifications (put/delete) have been persisted?
* How can you handle corrupted data in WAL?

We do not provide reference answers to the questions, and feel free to discuss about them in the Discord community.

{{#include copyright.md}}
