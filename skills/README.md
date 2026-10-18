# Skills

Agent skill ที่ CoE แจกจ่ายให้ใช้ใน Kiro ยังไม่มีรายการ

## โครงสร้างหนึ่ง skill

```
skills/<skill-name>/
  README.md        ใช้ทำอะไร ติดตั้งอย่างไร ตัวอย่างประโยคเรียกใช้
  SKILL.md         frontmatter name + description แล้วตามด้วยคำสั่ง
  references/      เอกสารที่ SKILL.md อ้างถึง (ถ้ามี)
```

## ติดตั้ง

คัดลอก folder ของ skill ไปไว้ที่ `.kiro/skills/<skill-name>/` ใน workspace หรือ `~/.kiro/skills/<skill-name>/` สำหรับทุก workspace

## เกณฑ์รับเข้า

- workflow ที่ต้องคุม policy หรือ gate ให้ทำเป็น MCP server ใน [`../mcp`](../mcp) แทน เพราะ skill ถูกแก้บนเครื่องได้
- ห้ามมี secret, account ID หรือ endpoint ภายใน
