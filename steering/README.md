# Steering

Steering file กลางสำหรับวางใน `.kiro/steering/` ยังไม่มีรายการ

## โครงสร้าง

```
steering/<name>.md     หนึ่งไฟล์ต่อหนึ่งหัวข้อ
```

ระบุ inclusion ใน frontmatter ให้ชัด

```markdown
---
inclusion: fileMatch
fileMatchPattern: "buildspec/*.yml"
---
```

ค่าที่ใช้ได้: `always` (ค่าเริ่มต้น), `fileMatch`, `manual`, `auto` (ต้องมี `name` และ `description`)

## ติดตั้ง

คัดลอกไฟล์ไปที่ `.kiro/steering/` ใน workspace หรือ `~/.kiro/steering/` สำหรับทุก workspace

## เกณฑ์รับเข้า

steering ใน repo นี้ต้องเป็นมาตรฐานกลางที่ใช้ได้ทุกทีม ค่าเฉพาะองค์กร เช่น account ID, ARN, VPC
หรือ URL ภายใน ให้เก็บใน steering ของ repo ทีมนั้นเอง ไม่ใช่ที่นี่
