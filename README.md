# msclabs.agent-registry

ทะเบียนกลางของ MSC Labs CoE สำหรับของที่ใช้ต่อกับ Kiro: MCP server, skill, steering และ hook

repo นี้เก็บแค่เอกสารและ config ตัวอย่าง ไม่มี source code ของ server ตัว workflow, เอกสารอ้างอิง,
template และ policy รันอยู่ฝั่ง CoE ส่วนที่ติดตั้งลงเครื่องคือแพ็กเกจ bridge บน PyPI เท่านั้น

| folder | เก็บอะไร | สถานะ |
| --- | --- | --- |
| [`mcp/`](mcp/) | MCP server ที่ publish แล้ว วิธีติดตั้ง และ runbook | ใช้งานได้ 3 ตัว |
| [`skills/`](skills/) | Agent skill ที่ CoE แจกจ่าย | ยังไม่มีรายการ |
| [`steering/`](steering/) | Steering file กลางสำหรับ `.kiro/steering/` | ยังไม่มีรายการ |
| [`hooks/`](hooks/) | Agent hook สำหรับ `.kiro/hooks/` | ยังไม่มีรายการ |

## MCP server ที่พร้อมใช้

| server | แพ็กเกจ PyPI | ใช้ทำอะไร |
| --- | --- | --- |
| `msclabs.devsecops-cicd` | [msclabs.devsecops-cicd-mcp-server](https://pypi.org/project/msclabs.devsecops-cicd-mcp-server/) | เอาแอปขึ้น pipeline DevSecOps ตั้งแต่ buildspec, IaC จนถึง push และไล่ให้ pipeline เขียว |
| `msclabs.html-creator` | [msclabs.html-creator-mcp-server](https://pypi.org/project/msclabs.html-creator-mcp-server/) | เปลี่ยนรายงาน assessment ของ AWS Transform เป็นเว็บเอกสารสองภาษาที่เปิด offline ได้ |
| `msclabs.bpmn-creator` | [msclabs.bpmn-creator-mcp-server](https://pypi.org/project/msclabs.bpmn-creator-mcp-server/) | วาด business process เป็น BPMN swimlane `.drawio` |

เริ่มที่ [mcp/README.md](mcp/README.md) แล้วทำตาม [mcp/RUNBOOK.md](mcp/RUNBOOK.md)

## ก่อนเริ่ม

- ขอ API key จาก CoE หนึ่งคนหนึ่งใบ key แสดงครั้งเดียวตอนสร้าง ถ้าหายต้องขอใบใหม่
- ติดตั้ง [uv](https://docs.astral.sh/uv/getting-started/installation/) เพื่อใช้ `uvx`
- Python 3.10 ขึ้นไป (uv จัดการให้ได้)

## เพิ่มของเข้า registry

แต่ละ folder มี README บอกโครงสร้างที่ต้องการ ส่งเป็น pull request เข้า `main`
ห้ามใส่ secret, API key, account ID หรือ endpoint ภายในองค์กรลงใน repo นี้ เพราะเป็น public repo
