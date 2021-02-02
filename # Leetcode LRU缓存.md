# Leetcode LRU缓存
```c++
#include <iostream>

using namespace std;

typedef struct LRUCacheNode {
    int key;
    int value;
    int count;
} Node;

class LRUCache {
public:
    LRUCache(int capacity) {
        max_size = capacity;
        size = 0;
        list = new Node[max_size];
    }

    int get(int key) {
        int value = -1;
        for (int i = 0; i < size; ++i) {
            Node *tmp = &list[i];
            if (tmp->key == key) {
                tmp->count = 0;
                value = tmp->value;
            } else {
                tmp->count++;
            }
        }
        return value;
    }

    void put(int key, int value) {
        bool contains = false;
        for (int i = 0; i < size; ++i) {
            Node *tmp = &list[i];
            if (tmp->key == key) {
                tmp->count = 0;
                tmp->value = value;
                contains = true;
            } else {
                tmp->count++;
            }
        }

        if (contains) { return; }

        if (size >= max_size) {
            int max_count = -1;
            Node *max_node;
            for (int i = 0; i < size; ++i) {
                Node *tmp = &list[i];
                if (tmp->count > max_count) {
                    max_count = tmp->count;
                    max_node = tmp;
                }
            }
            max_node->key = key;
            max_node->value = value;
            max_node->count = 0;
        } else {
            Node n;
            n.key = key;
            n.value = value;
            n.count = 0;
            list[size++] = n;
        }
    }

    void show() {
        for (int i = 0; i < size; ++i) {
            Node *tmp = &list[i];
            cout << tmp->key << "\t" << tmp->value << "\t" << tmp->count << "\n";
        }
    }

private:
    int size;
    int max_size;
    Node *list;
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */

int main() {
    LRUCache cache = LRUCache(2 /* 缓存容量 */ );
    cache.put(1, 1);
    cache.put(2, 2);
    cout << cache.get(1) << "\n";       // 返回  1
    cache.put(3, 3);    // 该操作会使得密钥 2 作废
    cout << cache.get(2) << "\n";       // 返回 -1 (未找到)
    cache.put(4, 4);    // 该操作会使得密钥 1 作废
    cout << cache.get(1) << "\n";       // 返回 -1 (未找到)
    cout << cache.get(3) << "\n";       // 返回  3
    cout << cache.get(4) << "\n";       // 返回  4

    return 0;
}

```