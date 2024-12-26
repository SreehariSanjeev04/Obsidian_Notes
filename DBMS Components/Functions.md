
## main.cpp

```cpp
unsigned int readBlock(unsigned char* block, int blockNumber);
unsigned int writeBlock(unsigned char* block, int blockNumber);
```

## Static Buffer

Metadata

```cpp
int StaticBuffer::getFreeBuffer(int blockNum);
int StaticBuffer::getBufferNum(int blockNum);

```

## Block Buffer

```cpp
int BlockBuffer::getHeader(struct HeadInfo *head);
int RecBuffer::getRecord(union Attribute *rec, int slotNum);
int RecBuffer::setRecord(union Attribute *rec, int slotNum);
int BlockBuffer::loadBlockAndGetBufferPtr(unsigned char **bufferPtr);
```