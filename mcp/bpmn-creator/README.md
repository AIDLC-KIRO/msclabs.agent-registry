# msclabs.bpmn-creator

วาด business process เป็น BPMN 2.0 swimlane ไฟล์ `.drawio` หนึ่ง lane ต่อหนึ่งแผนก บทบาท หรือระบบ
แล้วทำแบบฟอร์มทบทวนต่อแผนกเพื่อปรับ flow เป็น v2, v3

- แพ็กเกจ: [`msclabs.bpmn-creator-mcp-server`](https://pypi.org/project/msclabs.bpmn-creator-mcp-server/) 1.1.0
- tool prefix: `bpmn_` (12 tool)
- ต้องใช้คู่กับ draw.io MCP เพราะ server นี้ไม่วาดเอง

```json
"msclabs.bpmn-creator": {
  "command": "uvx",
  "args": ["msclabs.bpmn-creator-mcp-server==1.1.0"],
  "env": { "MCP_API_TOKEN": "${MCP_API_TOKEN}" }
},
"drawio": {
  "command": "npx",
  "args": ["-y", "@drawio/mcp@1.7.0"]
}
```

draw.io MCP ต้องมี Node.js (`npx`) บนเครื่อง

## ประโยคเริ่มงาน

```
วาด flow งานขอใบลา เป็น BPMN ให้ด้วย
```

ใช้คำที่คนทำงานพูดได้ เช่น `flow งาน`, `ขั้นตอนการทำงาน`, `สัมภาษณ์เก็บ process`, `แบบสอบถามแผนก`

## ขั้นตอน

| step | ทำอะไร |
| --- | --- |
| 1 Explore workspace | อ่านของที่มีอยู่ก่อนถาม |
| 2 Scope | ยืนยันบริบท ถามเฉพาะช่องว่าง |
| 3 Interview | ถามทีละข้อพร้อมตัวเลือก A-D และ Other **ข้ามได้** |
| 4 Model | บันทึก lane, step, input, output, ระบบ, กฎ, SLA ลง `process-model.md` ซึ่งเป็นแหล่งความจริง |
| 5 Draw | แปลงโมเดลเป็น swimlane `.drawio` |
| 6 Review | เดินทุกเส้นทางจาก Start ถึง End รวมเส้นทางที่ล้มเหลว |
| 7 Department forms | แบบฟอร์มทบทวนต่อแผนก (Markdown หรือ Google Form) |
| 8 Iterate | เอาคำตอบเข้าโมเดล วาดใหม่ เก็บ change log |

ข้าม interview ได้ด้วยประโยค `ข้าม interview วาดเลย`

## tool เฉพาะทาง

`bpmn_validate` ตรวจ XML ด้วย validator ของ CoE จับ XML เสีย, id ซ้ำ, เส้นที่ปลายหาย ใช้ทุกครั้งหลังวาด
และอย่าสรุปว่าไม่มีเส้นทับกันถ้ายังไม่ได้เปิดดูภาพที่ export จริง
