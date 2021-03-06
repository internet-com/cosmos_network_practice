## KVStore

KVStore是cosmos-sdk应用的基本存储层

```golang
type KVStore interface {
    Store

    // Get returns nil iff key doesn't exist. Panics on nil key.
    Get(key []byte) []byte

    // Has checks if a key exists. Panics on nil key.
    Has(key []byte) bool

    // Set sets the key. Panics on nil key.
    Set(key, value []byte)

    // Delete deletes the key. Panics on nil key.
    Delete(key []byte)

    // Iterator over a domain of keys in ascending order. End is exclusive.
    // Start must be less than end, or the Iterator is invalid.
    // CONTRACT: No writes may happen within a domain while an iterator exists over it.
    Iterator(start, end []byte) Iterator

    // Iterator over a domain of keys in descending order. End is exclusive.
    // Start must be greater than end, or the Iterator is invalid.
    // CONTRACT: No writes may happen within a domain while an iterator exists over it.
    ReverseIterator(start, end []byte) Iterator

 }

```
> note 如果Key为nil,程序会进入恐慌

当前KVStore的主要实现是IAVL store，未来将会支持Merkle KVStores, like Ethereum's radix trie.

我们很快就会看到，应用程序有许多不同的KVStore，每个都有不同的名称和不同的关注点。对store的访问由需要key，在应用程序启动期间必须将其授予处理程序分配key




