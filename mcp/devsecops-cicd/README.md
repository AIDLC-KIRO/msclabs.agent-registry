# msclabs.devsecops-cicd

เอาแอปขึ้น pipeline DevSecOps ของ CoE ตั้งแต่เขียน buildspec และ IaC ไปจนถึง push และไล่ให้ pipeline เขียว

- แพ็กเกจ: [`msclabs.devsecops-cicd-mcp-server`](https://pypi.org/project/msclabs.devsecops-cicd-mcp-server/) 1.1.0
- tool prefix: `cicd_` (14 tool)

```json
"msclabs.devsecops-cicd": {
  "command": "uvx",
  "args": ["msclabs.devsecops-cicd-mcp-server==1.1.0"],
  "env": { "MCP_API_TOKEN": "${MCP_API_TOKEN}" }
}
```

## ประโยคเริ่มงาน

```
deploy repo <org>/<repo> ขึ้น pipeline dev ให้ด้วย
```

ใช้ภาษาปกติได้ เช่น `ขึ้น AWS ให้ด้วย`, `pipeline แดง ช่วยดู`, `เอา code เข้า git แล้ว push dev`

## ขั้นตอน

| step | ทำอะไร |
| --- | --- |
| 1 Plan | ยืนยัน AppName และภาษา **GATE 1** |
| 2 Get resources | อ่าน account, pipeline, region, network แบบ read-only |
| 3 Discover | อ่านเอกสาร AI-DLC เก็บทุกคำกล่าวอ้างพร้อมแหล่งที่มา **GATE 2** |
| 4 Assess | ตรวจ workspace จริงเทียบกับคำกล่าวอ้างและ contract |
| 5 Prepare | เตรียม change set: buildspec, portability fix, IaC, ค่าต่อ env, แผน git **GATE 3** |
| 6 Generate | เขียนไฟล์ที่อนุมัติแล้วและตรวจในเครื่องก่อน push |
| 7 Deploy | push ขึ้น dev เมื่อทีม OK แล้ววนแก้ action ที่แดงจนเขียวหมด |
| 8 Summary | สรุป URL ผลแต่ละ action สิ่งที่แก้ และงานที่ค้าง |

## tool ที่ใช้บ่อย

| tool | ใช้ทำอะไร |
| --- | --- |
| `cicd_changeset_validate` | รัน policy ของ CoE ทับไฟล์ที่จะเขียน ใช้ก่อน push ได้ตลอด |
| `cicd_policy_get` | ดูกฎ naming, สิ่งที่เขียนได้, ขอบเขต IaC, artifact contract |
| `cicd_request_draft` | ร่างคำขอถึงทีมอื่น เช่นขอ SSM parameter หรือ certificate |
| `cicd_render_pipeline_status` | แปลงผล `aws codepipeline get-pipeline-state` เป็นหน้า HTML สรุปสถานะ |

## ควรเตรียม

ชื่อ repo และ branch, region ที่ตั้งใจ deploy, AWS credential แบบ read-only บนเครื่อง และคนที่มีสิทธิ์ตอบ OK ตอน push

server ไม่เรียก AWS แทนคุณและ deploy เองไม่ได้ การ deploy เกิดจาก `git push` ของทีมเท่านั้น
