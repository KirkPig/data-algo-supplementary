# Tree
คำนิยามของ Tree สามารถดูได้ในเรื่อง Basic Graph นะครับ คุณสมบัติของ Tree ที่น่าสนใจคือ เมื่อมี $N$ vertices จะมี $N - 1$ edges เสมอ 
## Rooted tree
**Rooted tree** หมายถึง tree ที่เรากำหนดให้ vertex นึงเป็น **root** ซึ่งจะเป็นเหมือนกับ vertex ที่อยู่ชั้น**บนสุด** แล้ว vertex ที่เชื่อมกับ root เราจะถือว่า **มี root เป็น parent (พ่อ/แม่)** และ root จะมี vertex เหล่านั้นเป็น **child(ลูก)** แล้วก็อยู่ชั้นที่ 2 ส่วน vertex ที่มี edge เชื่อมกับ vertex ในชั้นที่ 2 ก็จะเป็นชั้นที่ 3 แล้วก็มี vertex ในชั้นที่ 2 เป็น parent <br>
![ตัวอย่าง rooted tree](https://raw.githubusercontent.com/KirkPig/data-algo-supplementary/main/data/non%20linear/tree_bst/rooted%20tree.png)
\* vertex ที่ไม่มีลูก เราจะเรียกว่าใบ (leaf)
## Subtree
Subtree หมายถึง subset ของ rooted tree ซึ่งเราจะกำหนดให้ vertex นึง (ที่ไม่ใช่ root) เป็น root แล้วก็ไล่เพิ่มลูกของแต่ละ vertex ไปเรื่อย ๆ จนกว่าจะเพิ่มไม่ได้ เช่น <br>
![ตัวอย่าง subtree](https://raw.githubusercontent.com/KirkPig/data-algo-supplementary/main/data/non%20linear/tree_bst/subtree%20example.png)<br>
ส่วนที่วงน้ำเงินไว้คือ Subtree ที่มี vertex 2 เป็น root


## Binary tree
Binary Tree เป็น Rooted tree ที่ พ่อ/แม่ จะมีลูก ไม่เกิน 2 vertices
## Binary tree traversal
Binary tree traversal หมายถึง การเดินจาก root ไปจนทั่วครบทุก vertex แล้วเก็บผลลัพท์จากการเดินไว้ โดยมี 3 แบบหลัก ๆ ได้แก่
### 1. pre-order traversal
เป็นการเดินโดยที่ เมื่อเข้าสู่ vertex ไหน จะเพิ่ม vertex เข้า list แล้วไปทางลูกฝั่งซ้าย (ถ้ามี) แล้วพอ traversal ในลูกฝั่งซ้ายเสร็จจะทำฝั่งขวาต่อ
### 2. in-order traversal
เป็นการเดินโดยที่เริ่มมา จะ traversal ไปที่ลูกฝั่งซ้ายก่อน แล้วค่อยเพิ่ม vertex ตนเองเข้า list แล้วก็ traversal ไปฝั่งขวาต่อ
### 3. post-order traversal
เป็นการเดินโดยที่ไปทางลูกฝั่งซ้าย - ฝั่งขวา แล้วค่อยกลับมาเพิ่มตัวเองเข้า list 

base case ของ in-order และ post-order จะเป็นตอนที่ไปจนถึง leaf ก็เพิ่มค่าตัวเองเข้าไป 

## Binary Search Tree
เป็น Binary Tree ที่ลูกฝั่งซ้าย จะมีค่าน้อยกว่าพ่อแม่ ส่วนลูกฝั่งขวาจะมีค่ามากกว่าพ่อแม่

สังเกตว่า pre-order traversal ของ Binary Search Tree จะได้ลิสต์ที่เรียงจากน้อยไปมากเสมอ

## Balanced Binary Search Tree
เป็น Binary Search Tree ที่ไม่ว่าจะมีการ insert vertex ใหม่ยังไง จะมี algorithm จัดการให้ความสูงเป็น $O(log(N))$ เมื่อ $N$ หมายถึงจำนวน vertex เสมอ 

## AVL Tree 
เป็น Balanced Binary Search Tree แบบนึง ที่มีวิธีจัดการเวลา insert ทำให้ผลต่างความสูงของ subtree ซ้ายกับขวา จากทุก parent มีค่าไม่เกิน 1 ซึ่งตัวอัลกอริทึมสามารถดูเพิ่มเติมได้[ที่นี่](https://www.tutorialspoint.com/data_structures_algorithms/avl_tree_algorithm.htm) (ถ้าว่าง ๆ จะมาเพิ่มทีหลัง)
## STL
ปกติแล้ว ในระดับสอวน.เราไม่ต้องเขียน Balanced Binary Search Tree แต่เราจะใช้ std::set กับ std::map มาแทน
### std::set
- มองเป็น set ในคณิตศาสตร์ได้เลย ซึ่งข้างหลังของ std::set คือ balanced binary search tree 
- operation หลัก ๆ มี 3 อย่างคือ *insert*, *erase*, *query* ทำใน $O(log(N))$ ทุก operation
**วิธีใช้**

    ```
  #include <set>
  int main() {
		// สมมติเราต้องการเก็บ int
		std::set<int> our_set;
		// การ insert
		our_set.insert(15);
		our_set.insert(20);
		our_set.insert(15);// set ไม่เก็บตัวซ้ำ insert ไปก็ไม่ต่างจากเดิม
		// การลบ
		our_set.erase(15); // ลบ 15 ทิ้ง
		our_set.erase(15); // ไม่มีอะไรให้ลบก็ไม่เกิดอะไรขึ้น
		// การหา
		// วิธีที่ 1
		std::set<int>::iterator it = our_set.find(15);
		// ถ้าเกิดไม่เจอ it จะเท่ากับ our_set.end()
		// วิธีที่ 2
		int found = our_set.count(20);
		//ถ้าเจอจะเป็น 1 ไม่เจอจะเป็น 0 (ใน set แต่ใน multiset จะคนละเรื่อง)
		
		
	}
  ```
\* ในโค้ดนี้มีส่วนที่ใช้กับ std::multiset ไม่ได้หลายส่วน ถ้าอยากใช้ multiset ก็ศึกษาให้ดีก่อนใช้นะครับ

### std::map
จะเป็น set ที่มี key กับ value เช่น สมมติเราอยากเก็บความอร่อยของผลไม้ เราสามารถใช้ `std::map<string, int>` ได้ โดยที่ค่าใน map จะเรียงตามตัวหน้าของ template (เรียกว่า key) ส่วนตัวหลังเรียก value
```
#include <map>

int main() {
	std::map<string, int> deliciousness;
	// insert
	deliciousness["apple"] = 15;
	deliciousness["pineapples"] = 2121;
	// modify
	deliciousness["apple"] -= 3;
	// erase
	deliciousness.erase("apple");
	// query
	std::map<string, int>::iterator it = delicousness.find("mangkut");
	// ถ้าเจอ it จะไม่เป็น deliciousness.end()
	int found = deliciousness.count("pneapples");
	// แบบเดียวกับ std::set
}
```

