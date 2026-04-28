## 🚀 Why HashMap?

- Goal: **O(1) lookup**
- Used when:
  - Fast search needed
  - Key → Value mapping
- Compared to:
  - Array → O(n)
  - BST → O(log n)
  - HashMap → **O(1) (amortized)**

---

## 🧠 Core Idea

- Stores **key → value pairs**
- Uses:
  1. **Hash Function**
  2. **Array (bucket)**
  3. **Collision handling**

---

## 🔑 Hashing Concept

### Step 1: Convert key → integer
```
int hash = key.hashCode();
```
Step 2: Reduce range
```
index = hash % size;
```
-----
⚠️ Collision
- When multiple keys map to same index

-----

#### 🔧 Collision Handling
###### 1. Chaining (Most Important)
- Each index stores a LinkedList
- Example:
```
index 3 → [Kunal → Rahul → Armo]
```
##### Time Complexity:
- Best: O(1)
- Worst: O(n)
- Average: O(1 + α)
- 
###### ❓ Why O(1 + α) and NOT O(1 + n)?

👉 Because:
- We **don’t traverse all n elements**
- We only traverse the **linked list at one bucket**

👉 That list size = **α (load factor)**
```
α = n / m
```
### 📊 Understanding Load Factor ($\alpha$)

If we assume **Simple Uniform Hashing** (where any given key is equally likely to hash into any of the $m$ slots), the elements will be distributed evenly across the array.

* **Scenario:** You have $n = 100$ elements and $m = 20$ buckets.
* **Calculation:** Each bucket will, on average, contain $\frac{100}{20} = 5$ elements.
* **Conclusion:** Therefore, the **average length of the linked list** in any bucket is exactly $\alpha$.

$$\alpha = \frac{n}{m}$$

> [!TIP]
> This is why we say the average time complexity for a search is $O(1 + \alpha)$. As long as $\alpha$ is kept constant (via rehashing), the search remains $O(1)$.


- So: Search = O(1) + O(α)
- ✔ If α ≈ constant → O(1)  
- ❌ If all elements collide → α = n → O(n)

---

##### 2. Open Addressing
- No linked list
- Find next empty slot

##### Types:
- Linear probing
- Double hashing
- ⚠️ Not commonly used in interviews

----

## 📊 Load Factor (VERY IMPORTANT)


α = n / m


- n → number of elements
- m → size of table

### Meaning:
- Average elements per bucket

---

## ⚡ Resizing Rule (FIXED)

❌ Wrong: resize at half full  
✅ Correct:


Resize when α ≥ threshold


👉 In Java:

threshold ≈ 0.75


---

### 🔄 What happens during resizing?

1. Size doubles
2. All elements are **rehashed**
3. New indices are recalculated

---
## ⏱️ Time Complexity

| Operation | Average | Worst |
|----------|--------|------|
| Insert   | O(1)   | O(n) |
| Search   | O(1)   | O(n) |
| Delete   | O(1)   | O(n) |

---

## ⚡ Amortized Constant Time

- Resizing is costly but rare


- n inserts → O(n)
- 1 insert → O(1) amortized
- HashMap is O(1) because we jump directly to the bucket instead of searching everything.

---

## 📦 Space Complexity (IMPORTANT)


Space = O(n + m)


- n → elements
- m → bucket array

👉 Usually:

m ≈ n
⇒ Space ≈ O(n)

---
#### 🎯 Hash Function (Interview POV)
##### Division Method:
```
index = key % m
```
- ✔ Use prime m
- ✔ Avoid powers of 2/10
---
##### 🧠 Important Assumption
###### Simple Uniform Hashing
- Every key has equal probability
- Ensures:
```
Avg time = O(1)
```
##### ⚠️ Worst Case Scenario
- All elements go to same bucket
- Becomes:
```
LinkedList → O(n)
```
#### 🔄 Java Implementation
##### Basic Usage
```java
HashMap<String, Integer> map = new HashMap<>();

map.put("Kunal", 88);
map.put("Rahul", 95);

map.get("Kunal"); // O(1)
```
---

##### 📌 Important Methods
```java
map.put(key, value)
map.get(key)
map.remove(key)
map.containsKey(key)
map.getOrDefault(key, default)
map.size()
```
---
```
⚖️ HashMap vs HashTable
Feature	      HashMap	HashTable
Thread-safe	     ❌	     ✅
Null key	  1 allowed	   ❌
Performance	   Faster	 Slower
```
---
```
🌳 HashMap vs TreeMap
Feature 	HashMap	TreeMap
Order	    Random	Sorted
Time	    O(1)	O(log n)
```
---

##### 💡 Where Used
- Frequency count
- Two-sum
- Caching
- Graphs
- DP
- Routing / compilers
---

#### 🧠 Interview Patterns (VERY IMPORTANT)
##### 1. Frequency Map
```java
map.put(x, map.getOrDefault(x, 0) + 1);
```
##### 2. Two Sum
Store number → index
##### 3. Prefix Sum + HashMap
- Subarray problems
##### 4. Set + Map Combo
- Remove duplicates
- Sliding window
---

#### ❗ Common Mistakes
- Forgetting collisions exist
- Assuming strict O(1)
- Not handling null
- Ignoring load factor
- Overusing HashMap when sorting needed
---

#### 🧭 When NOT to Use
- Need sorted order → use TreeMap
- Memory constraints
- Predictable worst-case needed
---
#### 🔥 Final Summary
- HashMap = Fast lookup
- Core = Hashing + Buckets + Collision handling
- Real complexity = Amortized O(1)
- Most used DS in interviews
---

#### 🧠 Golden Rule

If problem says:

- “Find fast”
- “Check existence”
- “Count frequency”
---
