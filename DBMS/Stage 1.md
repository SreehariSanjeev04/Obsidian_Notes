Disk contains 8192 blocks each has a size of 2048 bytes, total 16MB

Block allocation map tells whether a block is empty is empty or not → 4 blocks for BAM

0-3 → Block allocations Map

4 → Relation Catalog

5 → Attribute Catalog

Rest -> Relations 

Since the first four blocks of the disk are used for storing the Block Allocation Map, **the first four entries in the Block Allocation Map are marked as occupied** by setting the values to `BMAP`. This is done when the XFS interface command of [`fdisk`](https://nitcbase.github.io/docs/User%20Interface%20Commands/efs#format-disk) is executed to generate the disk file. Marking of block 4 and block 5 as `REC` type in Block Allocation Map is also done during the `fdisk` command.

## Relation Catalog (Relation Catalog is also a relation)

Relation Catalog is used to store the meta information of relations → 96 bytes

Relation, # Attributes, # Records, First Block, Last Block, # Slots (Remember all retarded facts about relation’s location)

Relation → Stores the name of the relation

Note → Record Blocks of a relation are arranged using linked list

Number of slots = 20

Minimum number of records = 2 (For relation and attribute catalog)

Maximum number of records = 18 (20 - 2)

## Attribute Catalog (Attribute Catalog is also a relation)

- Relation Name
- Attribute Name
- Attribute Type
- Primary Key
- Root Block → Root block number of the B+ tree used for indexing, else -1
- Offset

Minimum 12 entries require (Attribute Catalog + Relation Catalog)

## Record Block Structure (Important)

Each block in a linked list is called record block.

Block1 → Block2 → Block3 → …

In addition to actual data, some header is also stored with the block.

4 Bytes each metainformation

- Type of record block (REC, IND_INTERNAL, IND_LEAF)
- Parent block (-1 for RECORD blocks)
- Left Block
- Right Block
- Number of Records
- Number of Attributes
- Number of slots
- Slot Map → Indicates whether a slot is empty or not (SLOT_OCCUPIED OR SLOT_UNOCCUPIED)
- Number of slots = maximum number of records (L)

[[Mnemonics#Record Block Header]]

$32 + L + (16 * K)* L <= 2048$

$L = 20$

Each Record Block is divided into variable size slots → each slots have a record generally.

### Block Structure

| Metadata (Header) | Record 1 | Record 2 | ... | Record N | Slot Array (Optional) |

![[Pasted image 20241225214203.png]]

# Disk Class

```cpp
class Disk {
public:
    Disk();
    ~Disk();
    static int readBlock(unsigned char *block, int blockNum);
    static int writeBlock(unsigned char *block, int blockNum);
};

```

Disk → **Used to make a temporary copy of the disk contents before the starting of a new session.** This ensures that if the system has a forced shutdown during the course of the session, the previous state of the disk is not lost.

~Disk → To make sure the changes are saved on graceful goddamn exit

readBlock → To transfer contents of the block onto the input memory buffer

writeBlock → To transfer contents of input memory buffer to the block 

```cpp
int main(int argc, char *argv[]) {
  Disk disk_run;

  unsigned char buffer[BLOCK_SIZE];
  Disk::readBlock(buffer, 7000);
  char message[] = "hello";
  memcpy(buffer + 20, message, 6);
  Disk::writeBlock(buffer, 7000);

  unsigned char buffer2[BLOCK_SIZE];
  char message2[6];
  Disk::readBlock(buffer2, 7000);
  memcpy(message2, buffer2 + 20, 6);
  std::cout << message2;

  return 0;
}
```


