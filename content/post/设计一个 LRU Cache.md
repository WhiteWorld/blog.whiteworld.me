{
    "date": "2015-01-22",
    "description": "LRU \u5373Least Recenty Used, \u662f\u5185\u5b58\u7ba1\u7406\u7684\u4e00\u79cd\u9875\u9762\u7f6e\u6362\u7b97\u6cd5, LRU\u6307\u5728\u5185\u5b58\u4e2d\u4f46\u662f\u53c8\u4e0d\u7528\u7684\u6570\u636e\u5757\u3002\u601d\u8def\uff1a\u4f7f\u7528\u4e00\u4e2a\u53cc\u5411\u94fe\u8868\u548c\u4e00\u4e2a\u54c8\u5e0c\u8868\uff0c\u54c8\u5e0c\u8868\u4fdd\u5b58\u8282\u70b9\u7684\u5730\u5740\uff0c\u4fdd\u8bc1\u5728 O(1) \u65f6\u95f4\u627e\u5230\u8282\u70b9\u3002\u53cc\u5411\u94fe\u8868\u63d2\u5165\u548c\u5220\u9664\u6548\u7387\u9ad8\u3002",
    "draft": false,
    "id": 13,
    "image": null,
    "meta_title": null,
    "slug": "lru-cache",
    "tags": [
        "LRU",
        "Java",
        "C++"
    ],
    "title": "\u8bbe\u8ba1\u4e00\u4e2a LRU Cache",
    "type": "post"
}


LRU 即Least Recenty Used, 是内存管理的一种页面置换算法, LRU指在内存中但是又不用的数据块。

思路：使用一个双向链表和一个哈希表，哈希表保存节点的地址，保证在 O(1) 时间找到节点。双向链表插入和删除效率高。

具体实现：C++ 使用unorder_map（需C++ 11） 和 list; Java 可以直接继承使用LinkedHashMap，重写removeEldestEntry方法。

C++ 实现
```cpp
class LRUCache{
	private:
		struct CacheNode{
			int key;
			int value;
			CacheNode(int k, int v):key(k),value(v){}
		};
		int capacity;
		list<CacheNode> cacheList;
		unordered_map<int, list<CacheNode>::iterator> cacheMap;

	public:
		LRUCache(int capacity){
			this->capacity = capacity;
		}
		int get(int key){
			if(cacheMap.find(key)==cacheMap.end()) return -1;
			cacheList.splice(cacheList.begin(), cacheList, cacheMap[key]);
			cacheMap[key] = cacheList.begin();
			return  cacheMap[key]->value;
		}
		void set(int key, int value){
			if(cacheMap.find(key) == cacheMap.end()){
				if(cacheList.size()==capacity){
					cacheMap.erase(cacheList.back().key);
					cacheList.pop_back();
				}
				cacheList.push_front(CacheNode(key, value));
				cacheMap[key]=cacheList.begin();
			}else{
				cacheMap[key]->value=value;
				cacheList.splice(cacheList.begin(), cacheList, cacheMap[key]);
				cacheMap[key] = cacheList.begin();
			}
		}
};
```


Java 实现
```java
package me.whiteworld;

import java.util.LinkedHashMap;
import java.util.Map;

public class LRUCache extends LinkedHashMap<Integer, String>{
	private int capacity;
	public LRUCache(int capacity, float loadFactor){
		super(capacity, loadFactor, true); //true 代表按照access-order, false 代表按照insertion-order
		this.capacity = capacity;
	}

	@Override
		protected boolean removeEldestEntry(Map.Entry<Integer, String> eldest){
			return size() > this.capacity;
		}

	public static void main(String[] args) {
		LRUCache cache = new LRUCache(4, 0.75f);
		cache.put(1, "123");
		cache.put(2, "abc");
		System.out.print(cache);
	}
}
```
