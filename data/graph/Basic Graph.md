


# Basic Graph
## กราฟ (Graph) คืออะไร
กราฟ ถ้าจะให้พูดในเชิงคณิตศาสตร์ สามารถเขียนในรูป $G = (V, E)$ เมื่อ $V$เป็นเซ็ตของจุด (vertex หรือ node ใช้ได้ 2 คำ) และ $E \subseteq (V\times V)$ เป็นมัลติเซ็ต (เซ็ตที่มีสมาชิกซ้ำกันได้) ของเส้นเชื่อม (edge) ซึ่งถ้าเขียนแบบนี้อาจจะไม่เข้าใจ
###  ภาษาบ้าน ๆ
กราฟ คือ โครงสร้างของการเชื่อมกันระหว่างสมาชิกในเซ็ต เช่น ถ้าเราให้ $S$ =  $\{A, B, C, D, E \}$ เป็นเซ็ตของคง 5 คน กราฟของ 5 คนนี้ก็จะมี $V = S$ กล่าวคือ แต่ละคนก็จะกลายเป็นจุดไป ส่วนสมมติว่า 5 คนนี้มีความสัมพันธ์กันคือ
- A เป็นเพื่อนกับ B
- B เป็นเพื่อนกับ C
- D เป็นเพื่อนกับ E

ซึ่งถ้าเราสร้างเส้นเชื่อมตามความเป็นเพื่อน เซ็ต $E$ ของเราก็จะป็น $\{(A, B), (B, C), (D, E)\}$  ซึ่งสามารถวาดรูปออกมาได้เป็น
![ภาพกราฟ](https://raw.githubusercontent.com/KirkPig/data-algo-supplementary/main/data/graph/example1.png)
## ชนิดของกราฟ
กราฟมีวิธีแบ่งหลายวิธีมาก ๆ แล้วก็มีกราฟที่มีคุณสมบัติน่าสนใจ จนมีชื่อเรียกของตัวเองเยอะมาก เช่น planar graph, bipartite graph ฯลฯ ซึ่งจะลงลึกในพาร์ท graph algo ในส่วนบทนี้เลยแบ่งแค่ตามชนิดของ Edge ไปก่อน
## ชนิดของกราฟตามเส้นเชื่อม
เราจะแบ่งคุณสมบัติของเส้นเชื่อมเป็น 2 คุณสมบัติคือ ทิศทางกับน้ำหนักซึ่งสรุปได้ตามด้านล่าง
1. **Direct vs Undirect:** 
	- ***Directed graph*** หมายถึง กราฟที่เส้นเชื่อมมีทิศทาง คือ ตัว edge $(A, B)$ หมายความว่า $A$ เชื่อมไปถึง $B$ ได้ แต่ $B$ ไม่ได้เชื่อมถึง $A$ ถ้าเกิดว่าอยากให้เชื่อมทั้งคู่ต้องมี $(A, B)$ และ $(B, A)$
	- ***Undirected graph*** หมายถึงกราฟที่ edge $(A, B)$ จะหมายความว่าทั้ง $A$ และ $B$ จะเชื่อมถึงกัน

เปรียบเทียบง่าย ๆ คือ **Directed graph** เหมือนระบบ **Follow** ส่วน **Undirected graph** เหมือนระบบ **Friend** ใน**social network**

2. **Weight vs Unweight**
	- ***Unweighted graph*** หมายถึง กราฟที่แต่ละเส้นเชื่อม เราจะนิยามด้วยแค่ 2  จุดสองฝั่งของเส้น เหมือนที่เราทำมาตลอด
	- ***Weighted graph*** หมายถึง กราฟที่นอกจากจุดยอด 2 ข้างบนเส้นเชื่อมแล้ว ยังมีค่าอะไรบางอย่างด้วย เช่น แผนที่ที่มี Edge เป็นถนนเชื่อมสองสถานที่ แล้วก็ระบุระยะทางเป็น weight เช่น $(A, B, 25)$ หมายถึงว่าจากจุด A ไป B เป็นระยะทาง 25 เมตร
	**Note:** เซ็ต $E$ จะเป็น $V \times V \times W$ แทน เมื่อ $W$ เป็นเซ็ตของน้ำหนักที่เป็นไปได้

เราสามารถเอา 2 อย่างนี้มาผสมกันได้ด้วย เช่น weighted undirected graph หมายถึงกราฟไม่มีทิศทางที่มีน้ำหนักด้วย เช่นแผนที่ที่ถนนทุกเส้นวิ่งได้ทั้ง 2 ทิศเป็นต้น

**ภาพแต่ละแบบ**
	1. Unweighted undirected graph 
	![Unweighted undirected](https://raw.githubusercontent.com/KirkPig/data-algo-supplementary/main/data/graph/unweighted_undirected.png)
	2. Unweighted directed graph 
	![Unweighted directed](https://raw.githubusercontent.com/KirkPig/data-algo-supplementary/main/data/graph/unweighted_directed.png)
	3. Weighted undirected graph 
	![Weighted undirected](https://raw.githubusercontent.com/KirkPig/data-algo-supplementary/main/data/graph/weighted_undirected.png)
	4. Weighted directed graph  
	![Weighted directed](https://raw.githubusercontent.com/KirkPig/data-algo-supplementary/main/data/graph/weighted_directed.png)

## คำศัพท์น่ารู้เกี่ยวกับกราฟ
คำศัพท์พวกนี้จะเจอบ่อย ซึ่งแต่ละที่อาจนิยามต่างกันเล็กน้อย แต่ปกติ
 
1. **Path** หมายถึงเส้นทางเดินจากจุดนึงไปตามเส้นเชื่อมไปอีกจุดในกราฟ เช่น  
![path](https://raw.githubusercontent.com/KirkPig/data-algo-supplementary/main/data/graph/example2.png)
จากกราฟด้านบน path A-B-C หมายถึง path ที่เริ่มจาก A เดินไป B แล้วก็จาก B ไป C ตามเส้นเชื่อม แต่ว่าไม่มี path A-B-E เพราะว่า ระหว่าง B กับ E ไม่มีเส้นเชื่อม หรือว่า A-B-D-C ก็ไม่ได้เช่นเดียวกัน เพราะว่า edge $(C, D)$ มีทิศทางจาก $C$ ไป $D$ (ถ้าอยากให้ทำได้ ต้องเพิ่ม $(D, C)$ เข้ามาด้วย
	**ตัวอย่าง Path อื่น ๆ ที่ทำได้**
	1. A-B-D-E
	2. A-B-C-A-B
2. **Cycle** หมายถึง path ที่จุดเริ่มกับจบเป็นจุดเดียวกัน เช่นจากกราฟข้างบน path A-B-C เป็น Cycle
3. **Connected graph** หมายถึงกราฟที่ ถ้าสมมติว่าเส้นเชื่อมไม่มีทิศทาง สำหรับคู่จุดใด ๆ จะมี path ไปหากันเสมอ เช่น 
![connected graph](https://raw.githubusercontent.com/KirkPig/data-algo-supplementary/main/data/graph/example3.png)
เป็น Connected graph เพราะว่า ถ้าสมมติว่ามันไม่มีทิศทาง (B ไป A ได้ หรือ C ไป A ได้) ทุก ๆ คู่จะมี path ไปหากันเสมอ ส่วน 
![disconnected graph](https://raw.githubusercontent.com/KirkPig/data-algo-supplementary/main/data/graph/example1.png) 
ไม่เป็น Connected graph เพราะว่า A ไปหา D หรือ E ไม่ได้
4. **Tree** หมายถึง Connected graph ที่ไม่มี cycle
5. **Subgraph** หมายถึง Subset ของกราฟที่ สำหรับจุด A กับ B ใด ๆ ถ้าจุด A กับ B อยู่ใน Subgraph นี้แล้ว edge $(A, B)$ ต้องอยู่ใน Subgraph นี้ด้วย
6. **Self-loop** หมายถึง edge $(A, A)$
7. **Parallel edge** หมายถึง edge ที่หน้าตาซ้ำกัน 

## Graph Representation
มาถึงตรงนี้อาจจะสงสัยกันว่าเราสามารถเก็บกราฟในคอมได้อย่างไรบ้าง ซึ่งหลัก ๆ ก็มี 3 วิธีที่ใช้ ได้แก่
**1. Adjacency matrix:** สำหรับวิธีนี้เป็นการเก็บกราฟด้วย Matrix โดยตัวที่ $A_{ij}$ แทน edge จาก vertex $i$ ไป vertex $j$ ซึ่งส่วนใหญ่ unweighted graph จะแทน 0 ว่าไม่มี edge ส่วน 1 ว่ามี edge ส่วน weighted graph ก็อาจจะมีวิธีแตกต่างกันได้ตามความเหมาะสม เช่นถ้ารู้ว่าไม่มี edge weight ค่าไหน ก็ให้เก็บเป็นค่านั้นไป ส่วน undirected graph $A_{ij}$ จะเท่ากับ $A_{ji}$
**ข้อดี:** เข้าใจง่าย ใช้ได้ดีกับกราฟที่ edge เยอะ ๆ
**ข้อเสีย:** เปลืองที่ในเคสที่ edge ไม่เยอะ ต่อให้ไม่มี edge ก็ยังต้องเก็บ แล้วก็ทำให้ traversal ช้าด้วย (รอบทถัดไป)
**2. Adjacency list (ใช้บ่อยสุด):** แทนที่เราจะเก็บทุกตัว เราเก็บแค่ Edge ที่เพิ่มเข้ามา โดยที่ตอนแรกเราจะสร้างลิสต์สำหรับแต่ละ vertex แล้วพอมี edge ที่เริ่มจาก vertex นั้น ก็ Add ปลายทาง (หรือ weight ด้วย ถ้าจำเป็น) เข้าไปในลิสต์ของ vertex นั้น
**ข้อดี:** ใช้ได้ดีในเคสทั่ว ๆ ไป ไม่ถึงกับแย่ในเคสที่ edge เยอะๆ
**ข้อเสีย:** ช้ากว่า Adjacency Matrix ในเคส edge เยอะ แล้วก็ทำ matrix operation ไม่ได้ (ได้ใช้บ้าง)
**3. Edge list:** เก็บแต่ละ edge ตามจุดปลาย (แล้วก็ weight) ไว้ในลิสต์อันนึง 
**ข้อดี:** ใช้ที่น้อย แล้วก็สามารถเรียง edge ตาม weight ได้
**ข้อเสีย:** เขียน traversal ไม่สะดวกเท่าไหร่ (ทำได้นะ แต่ 2 แบบบนทำง่ายกว่าเยอะ)

 
