
## Disk Buffer

Due to principle of Locality, NITCbase buffers all the disk i/o operations. We will be pre-allocating memory for holding 32 disk blocks. All operations will be done on that buffer until the disk block is swapped with more recently required disk block (LRU Algorithm).

We will be using `loadBlockandGetBufferPointer()` instead of read Block

We use `unsigned char block[BUFFER_CAPACITY][BLOCK_SIZE]` in Static Buffer

## Cache 

All operations require relation catalog and attribute catalog data, due to which we need cache

`Relation Catalog` and `Attribute Catalog` are arrays of size 12 (MAX_OPEN)

Each entry stores the catalog entries for a relation.
