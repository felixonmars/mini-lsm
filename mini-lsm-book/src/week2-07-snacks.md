# Batch Write and Checksums

<!-- ![Chapter Overview](./lsm-tutorial/week2-07-overview.svg) -->

In the previous chapter, you already built a full LSM-based storage engine with. At the end of this week, we will implement some easy but important optimizations of the storage engine. Welcome to Mini-LSM's week w snack time!

In this chapter, you will:

* Implement the batch write interface.
* Add checksums to the blocks, SST metadata, manifest, and WALs.

## Task 1: Write Batch Interface

## Task 2: Block Checksum

## Task 3: SST Checksum

## Task 4: WAL Checksum

## Task 5: Manifest Checksum

## Test Your Understanding

* Consider the case that an LSM storage engine only provides `write_batch` as the write interface (instead of single put + delete). Is it possible to implement it as follows: there is a single write thread with an mpsc channel receiver to get the changes, and all threads send write batches to the write thread. The write thread is the single point to write to the database. What are the pros/cons of this implementation? (Congrats if you do so you get BadgerDB!)
* Is it okay to put all block checksums altogether at the end of the SST file instead of store it along with the block? Why?

We do not provide reference answers to the questions, and feel free to discuss about them in the Discord community.

## Bonus Tasks

* **Try Recovering**. If there is a checksum error, open the database in a safe mode so that no writes can be performed and non-corrupted data can still be retrieved.

{{#include copyright.md}}
