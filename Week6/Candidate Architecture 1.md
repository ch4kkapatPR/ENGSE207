
## Candidate Architecture 1: Layered Monolith Architecture

### Overview

สถาปัตยกรรมแบบ Layered Monolith โดยจะเป็นโครงสร้างที่รวมระบบทั้งหมดไว้ในแอปพลิเคชันเดียว แต่จะแยกความรับผิดชอบออกเป็นLayer อย่างชัดเจน จะเหมาะกับระบบจัดการคลังสินค้าขนาดเล็กถึงกลาง และทีมพัฒนาที่ต้องการความเรียบง่ายในการดูแลระบบ

### Components

* Presentation Layer (Web UI)
* Application Layer (Business Logic)
* Domain Layer (Inventory Logic)
* Data Access Layer
* Database

### Technology Stack

* Frontend: HTML, CSS, JavaScript 
* Backend: Node.js 
* Database: MySQL / PostgreSQL
* Others: REST API, JWT Authentication

### Architectural Patterns

* Layered Architecture
* MVC (Model-View-Controller)

### Diagram

![alt text](<layered monolith.png>)

### Pros & Cons

**Pros:**

* ✅ โครงสร้างเข้าใจง่าย เหมาะกับนักศึกษาและทีมเล็ก
* ✅ พัฒนาและ Deploy ง่าย
* ✅ Debug และทดสอบระบบได้สะดวก

**Cons:**

* ❌ ขยายระบบ (Scalability) ได้จำกัดเมื่อระบบใหญ่ขึ้น
* ❌ หากระบบซับซ้อนมาก จะดูแลยาก

---

## Candidate Architecture 2: Microservices Architecture

### Overview

สถาปัตยกรรมแบบ Microservices จะเป็นการแยกระบบออกเป็นบริการย่อยๆ ตามหน้าที่ เช่น จัดการสินค้า สต็อก และการแจ้งเตือน ช่วยให้ระบบสามารถขยายตัวได้ดีและรองรับผู้ใช้งานจำนวนมาก โดยจะเหมาะกับระบบที่มีการเติบโตในอนาคต

### Components

* Inventory Service
* Stock Transaction Service
* Notification Service
* API Gateway
* Authentication Service
* Database (แยกตาม Service)

### Technology Stack

* Frontend: React 
* Backend: Node.js 
* Database: PostgreSQL / MongoDB (แยกแต่ละ Service)
* Others: Docker, REST API, Message Queue

### Architectural Patterns

* Microservices Pattern
* API Gateway Pattern
* Database per Service

### Diagram

(สามารถวาด Diagram ด้วย Draw.io โดยแสดง User → API Gateway → แต่ละ Microservice → Database ของแต่ละ Service)

### Pros & Cons

**Pros:**

* ✅ รองรับ Scalability ได้ดี
* ✅ แต่ละ Service พัฒนาและ Deploy แยกกันได้
* ✅ เหมาะกับระบบขนาดใหญ่และมีผู้ใช้งานจำนวนมาก

**Cons:**

* ❌ โครงสร้างซับซ้อนกว่ามาก
* ❌ ใช้เวลาและทรัพยากรในการพัฒนาสูง
* ❌ ต้องมีความรู้ด้าน DevOps เพิ่มเติม
