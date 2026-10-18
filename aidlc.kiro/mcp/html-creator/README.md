# msclabs.html-creator

เปลี่ยนรายงาน assessment ของ AWS Transform (CCA, BRE, MRA) เป็นเว็บเอกสารสองภาษา ไทย/อังกฤษ ที่เปิดจากไฟล์ได้โดยไม่ต้องต่อเน็ต

- แพ็กเกจ: [`msclabs.html-creator-mcp-server`](https://pypi.org/project/msclabs.html-creator-mcp-server/) 1.1.0
- tool prefix: `html_` (14 tool)

```json
"msclabs.html-creator": {
  "command": "uvx",
  "args": ["msclabs.html-creator-mcp-server==1.1.0"],
  "env": { "MCP_API_TOKEN": "${MCP_API_TOKEN}" }
}
```

## ประโยคเริ่มงาน

```
ทำเว็บเอกสารจากรายงาน ATX ในโฟลเดอร์ ATXDocumentation ให้ด้วย
```

## ขั้นตอน

| step | ทำอะไร |
| --- | --- |
| 1 Job plan | ตกลงโฟลเดอร์ปลายทางและรายการงาน **GATE 1** |
| 2 Get resources | หารายงาน ATX, transform config, source code และ spec ประกอบ |
| 3 Discover | ระบุ repo ต้นทาง ผู้อ่าน ขอบเขต และรายการหน้า **GATE 2** |
| 4 Assess code | วิเคราะห์ repo เทียบรายงาน ทุกคำกล่าวอ้างมี citation |
| 5 Prepare | ยืนยันชุดหน้าและข้อมูลแต่ละหน้า แล้ววาง scaffold **GATE 3** |
| 6 Generate HTML | เติม scaffold ฝัง content ตรวจ และทดลองอ่าน |

## กฎที่ไม่ผ่อน

- เว็บต้องเปิดได้แบบ offline ไม่มีหน้าไหนชี้ไป CDN
- ไม่ใส่สิ่งที่ไม่มีในต้นทาง คำกล่าวอ้างต้องมี `file:line` สิ่งที่ไม่รู้เขียนว่า not determined สิ่งที่อนุมานติดป้าย INFERRED

## tool เฉพาะทาง

| tool | ใช้ทำอะไร |
| --- | --- |
| `html_scaffold_manifest` | ดึง scaffold ของเว็บ อย่าประกอบเอง |
| `html_normalize_interfaces` | แปลง OpenAPI 2/3 หรือ Postman v2 เป็น Markdown มี citation และตัด credential ออกก่อนเขียนไฟล์ |
| `html_script_get` | ดู source ของ script ที่ server ใช้ |

## ควรเตรียม

โฟลเดอร์รายงาน ATX (เช่น `ATXDocumentation/`, `business-rules-extraction/`), source code ของระบบ และ spec ประกอบถ้ามี
