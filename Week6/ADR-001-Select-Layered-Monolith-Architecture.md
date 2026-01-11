# ADR-001: Select Layered Monolith Architecture for Inventory Management System

**Date:** 2026-01-11
**Status:** Accepted
**Deciders:** นายจักรภัทร พรมทา

---

## Context

### Background

ทางผู้จัดทำต้องการที่จะพัฒนาระบบจัดการคลังสินค้า (Inventory Management System) เพื่อแก้ปัญหาการบันทึกสินค้าเข้า–ออกที่ไม่เป็นระบบ ข้อมูลสต็อกไม่ตรงกับความเป็นจริง และขาดการแจ้งเตือนเมื่อสินค้าใกล้หมด ซึ่งส่งผลต่อการบริหารจัดการสินค้าและการตัดสินใจของผู้ดูแลคลัง

### Problem Statement

การจัดการคลังสินค้าในรูปแบบเดิมมีความล่าช้า ข้อมูลไม่เป็นปัจจุบัน และมีความเสี่ยงต่อความผิดพลาดจากการบันทึกข้อมูลด้วยมือ รวมถึงไม่สามารถรองรับการขยายระบบในอนาคตได้อย่างเหมาะสม

### Key Drivers

* **Functional:**

  * ระบบสามารถบันทึกสินค้าเข้า–ออกได้
  * ระบบสามารถติดตามจำนวนสินค้าคงเหลือแบบ Real-time
  * ระบบแจ้งเตือนเมื่อสินค้าใกล้หมด
* **Quality Attributes:**

  * **Maintainability:** ระบบต้องแก้ไขและดูแลรักษาได้ง่าย
  * **Scalability:** ระบบสามารถรองรับการขยายฟีเจอร์และปริมาณข้อมูลในอนาคต
* **Constraints:**

  * ระบบต้องเป็น Web Application
  * ใช้เทคโนโลยีพื้นฐานที่ทีมสามารถพัฒนาและดูแลได้

---

## Decision

We will use **Layered Monolith Architecture**.

### Components

* **Presentation Layer:** ส่วนติดต่อผู้ใช้สำหรับจัดการสินค้า แสดงสต็อก และแจ้งเตือน
* **Application Layer:** จัดการ API และควบคุมลำดับการทำงานของระบบ
* **Business Logic Layer:** ประมวลผลกฎทางธุรกิจ เช่น การคำนวณสต็อก และการตรวจสอบสินค้าใกล้หมด
* **Data Access Layer:** ติดต่อและจัดการข้อมูลสินค้าและประวัติการทำรายการในฐานข้อมูล
* **Notification Layer:** จัดการการแจ้งเตือนสินค้าใกล้หมดภายในระบบ

### Technologies

* Frontend: React
* Backend: Node.js (Express)
* Database: MySQL / PostgreSQL
* Others: REST API, JWT Authentication

### Architectural Patterns

* Layered Architecture
* MVC (Model-View-Controller)

---

## Rationale

### Why this decision?

1. โครงสร้างแบบ Layered Monolith มีความชัดเจน แยกหน้าที่ของระบบออกเป็นส่วน ๆ ทำให้เข้าใจง่าย
2. ง่ายต่อการบำรุงรักษาและปรับปรุงระบบ เหมาะกับทีมพัฒนาขนาดเล็ก
3. รองรับ Functional Requirements ของระบบคลังสินค้าได้ครบถ้วน
4. ลดความซับซ้อนเมื่อเทียบกับ Microservices ซึ่งเกินความจำเป็นในบริบทของระบบนี้

### Alternatives Considered

1. **Monolith Architecture (ไม่แยก Layer ชัดเจน)**

   * Pros: พัฒนาได้รวดเร็ว โครงสร้างไม่ซับซ้อน
   * Cons: ดูแลยากเมื่อระบบขยายตัว
   * Why not chosen: ไม่ตอบโจทย์ด้าน Maintainability ในระยะยาว

2. **Microservices Architecture**

   * Pros: รองรับ Scalability ได้ดี เหมาะกับระบบขนาดใหญ่
   * Cons: ซับซ้อน ใช้ทรัพยากรและความรู้ด้าน DevOps สูง
   * Why not chosen: ไม่เหมาะสมกับขนาดและบริบทของโครงการในปัจจุบัน

---

## Consequences

### Positive (ข้อดี)

* ✅ โครงสร้างโค้ดเป็นระเบียบและเข้าใจง่าย
* ✅ ดูแลรักษาและแก้ไขระบบได้สะดวก
* ✅ รองรับการเพิ่มฟีเจอร์ในอนาคตได้ในระดับหนึ่ง

### Negative (ข้อเสีย)

* ❌ มี Overhead จากการเรียกใช้งานผ่านหลาย Layer
  → Mitigation: ออกแบบ Layer ให้กระชับและลดการเรียกที่ไม่จำเป็น
* ❌ ความสามารถในการขยายระบบมีข้อจำกัดเมื่อระบบมีขนาดใหญ่มาก
  → Mitigation: เตรียมโครงสร้างให้สามารถ Refactor ไปสู่ Microservices ได้ในอนาคต

### Risks

* ⚠️ โครงสร้างซับซ้อนเกินความจำเป็นสำหรับบางฟีเจอร์

  * Impact: Medium
  * Probability: Low
  * Mitigation: ควบคุมขอบเขตความรับผิดชอบของแต่ละ Layer ให้ชัดเจน

### Trade-offs

* Maintainability vs Performance
* Simplicity vs Scalability

---

## Compliance

### Constraints Met

* ✅ Web Application: ระบบถูกพัฒนาในรูปแบบ Web Application
* ✅ Technology Constraint: ใช้เทคโนโลยีมาตรฐานที่ทีมสามารถดูแลได้

### Quality Attributes Addressed

* ✅ Maintainability: แยก Layer ชัดเจน ง่ายต่อการแก้ไข
* ✅ Scalability: สามารถขยายฟีเจอร์และปรับโครงสร้างในอนาคตได้

---

## Notes

### Assumptions

* ผู้ใช้งานเข้าถึงระบบผ่าน Web Browser
* จำนวนผู้ใช้งานอยู่ในระดับเล็กถึงกลาง

### Future Considerations

* พิจารณาแยก Notification หรือ Reporting ออกเป็น Service เฉพาะหากระบบเติบโต
* รองรับการเชื่อมต่อ Mobile Application ในอนาคต

### References

* Software Architecture in Practice
* Clean Architecture – Robert C. Martin
