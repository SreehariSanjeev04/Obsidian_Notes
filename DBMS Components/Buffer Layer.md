
Whenever we need to use a block, the block is copied to the primary memory. All the functions dealing with disk block is handled in buffer layer.

NITCBase has the ability to store 32 Disk Blocks in buffer memory at a time. 64 KB.

## HeadInfo

Each disk block contains 32 byte header fixed, that contains the metainformation. 
setHeader() and getHeader() takes the pointer to struct HeadInfo as argument. 

```cpp
struct HeadInfo {
    int32_t blockType;
    int32_t pblock;
    int32_t lblock;
    int32_t rblock;
    int32_t numEntries;
    int32_t numAttrs;
    int32_t numSlots;
    unsigned char reserved[4];
};
```


## Attribute

Takes `INT` or `STRING` as value 

```cpp
union Attribute {
    double nVal;
    char sVal[ATTR_SIZE];
};
```

