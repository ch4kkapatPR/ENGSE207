## Evaluation

### Comparison Table

| Criteria                | Weight   | Arch 1: Layered Monolith (Score) | Arch 1 (Weighted) | Arch 2: Microservices (Score) | Arch 2 (Weighted) |
| ----------------------- | -------- | -------------------------------- | ----------------- | ----------------------------- | ----------------- |
| Performance             | 20%      | 4                                | 0.8               | 4                             | 0.8               |
| Scalability             | 20%      | 2                                | 0.4               | 5                             | 1.0               |
| Complexity              | 15%      | 5                                | 0.75              | 2                             | 0.3               |
| Maintainability         | 15%      | 4                                | 0.6               | 4                             | 0.6               |
| Development Cost        | 15%      | 5                                | 0.75              | 3                             | 0.45              |
| Deployment & Operations | 15%      | 5                                | 0.75              | 3                             | 0.45              |
| **Total**               | **100%** |                                  | **4.05**          |                               | **3.60**          |

> หมายเหตุ: คะแนนใช้ช่วง 1 (แย่) – 5 (ดีมาก)

---

### Selected Architecture

**Decision:** Layered Monolith Architecture

**Reasons:**

1. ระบบจัดการคลังสินค้านี้เป็นระบบขนาดเล็กถึงกลาง จึงไม่จำเป็นต้องใช้โครงสร้างที่ซับซ้อนแบบ Microservices
2. Layered Monolith มีความซับซ้อนต่ำ โดยที่จะพัฒนา ทดสอบ หรือดูแลรักษานั้นทำได้ง่าย เหมาะกับทีมขนาดเล็ก
3. ค่าใช้จ่ายต่ำกว่า ไม่ต้องจัดการ Infrastructure และ DevOps ที่ซับซ้อน
4. สามารถรองรับ Requirement หลักได้ เช่น การบันทึกสินค้า การติดตามสต็อกแบบ Real-time และการแจ้งเตือนสินค้าใกล้หมดได้อย่างเพียงพอ
