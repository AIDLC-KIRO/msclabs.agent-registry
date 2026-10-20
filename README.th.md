# MSC Labs Agent Registry

_ภาษาอื่น: [English](README.md)_

[![License: Apache-2.0](https://img.shields.io/badge/License-Apache%202.0-yellow.svg)](https://opensource.org/licenses/Apache-2.0)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)

Repository สาธารณะนี้เป็นจุดแจกจ่ายข้อกำหนดกลางสำหรับการพัฒนาซอฟต์แวร์ด้วย AI ซึ่งดูแลโดย
AI-DLC Center of Excellence (CoE) ภายในมี Kiro steering ที่นำไปใช้ซ้ำได้ และเอกสาร client สำหรับ
Model Context Protocol (MCP) workflow ที่ให้บริการจากส่วนกลาง 4 รายการ แต่ไม่มี source code ของ
hosted service และไม่ได้บังคับนโยบายการ deploy ด้วยตัวเอง

> [!IMPORTANT]
> Generative AI อาจให้ผลลัพธ์ผิดพลาด โปรดตรวจผลลัพธ์ การเปลี่ยนแปลง infrastructure ผลกระทบด้าน
> ความปลอดภัย และค่าใช้จ่ายก่อนดำเนินการ สิทธิ์ การอนุมัติ และ CI/CD pipeline ของ repository
> ยังคงเป็นกลไกบังคับใช้ที่มีผลจริง

## เริ่มต้นที่นี่

| เป้าหมาย | เอกสาร | เนื้อหาที่จะพบ |
| --- | --- | --- |
| นำมาตรฐานกลางไปใช้กับโครงการ | [คู่มือ Steering](aidlc.kiro/steering/README.md) | รายการข้อกำหนด โหมด inclusion และวิธีคัดลอกอย่างปลอดภัย |
| เลือกหรือประเมิน hosted workflow | [ภาพรวม MCP](aidlc.kiro/mcp/README.md) | รายการ server, prerequisite, รูปแบบ tool และขอบเขตการทำงาน |
| ติดตั้ง ตรวจสอบ หมุนเวียน key หรือแก้ปัญหา | [MCP client runbook](aidlc.kiro/mcp/RUNBOOK.md) | ขั้นตอนปฏิบัติแยกตาม platform |
| ทำความเข้าใจ workflow เฉพาะรายการ | [DevSecOps](aidlc.kiro/mcp/devsecops-cicd/README.md) · [HTML](aidlc.kiro/mcp/html-creator/README.md) · [BPMN](aidlc.kiro/mcp/bpmn-creator/README.md) · [Deck](aidlc.kiro/mcp/deck-creator/README.md) | Tool, ขั้นตอน และข้อจำกัดของแต่ละ workflow |
| เสนอการเปลี่ยนแปลง registry | [การร่วมพัฒนา](#การร่วมพัฒนา) | ขอบเขต การทบทวน และข้อห้ามสำหรับ public repository |

## สิ่งที่พร้อมใช้งาน

| ส่วน | เนื้อหา |
| --- | --- |
| [`aidlc.kiro/steering/`](aidlc.kiro/steering/README.md) | Guardrail, engineering convention และข้อกำหนดด้านความปลอดภัย 129 ข้อใน 4 pack |
| [`aidlc.kiro/mcp/`](aidlc.kiro/mcp/README.md) | Configuration และเอกสารสำหรับ hosted workflow server 4 รายการ |
| [`docs/diagrams/`](docs/diagrams/) | ไฟล์ต้นฉบับ draw.io และภาพสถาปัตยกรรมที่ render แล้ว |

Folder [`skills`](aidlc.kiro/skills/README.md) และ [`hooks`](aidlc.kiro/hooks/README.md) ระบุรูปแบบ
สำหรับผู้ร่วมพัฒนาเท่านั้น ขณะนี้ยังไม่มีรายการพร้อมแจกจ่าย

## กลไกกำกับดูแล

Registry รองรับการควบคุม 3 ชั้นที่มีหน้าที่ต่างกัน:

1. **Steering ชี้แนวทางให้ assistant** — ทีมคัดลอกไฟล์ที่เกี่ยวข้องเข้า workspace ไฟล์เหล่านี้
   แก้ไขในเครื่องได้ จึงมีผลต่อแนวทางการตอบ แต่ไม่รับประกันหรือบังคับผลลัพธ์
2. **Hosted MCP workflow ทำให้กระบวนการเป็นมาตรฐาน** — CoE ควบคุม workflow, reference และ
   policy content ส่วนกลาง Human gate บันทึกการตัดสินใจ แต่ service ไม่ deploy แทนผู้ใช้
3. **Repository และ pipeline บังคับใช้นโยบายส่งมอบ** — สิทธิ์ required review, policy gate และ
   deployment approval เป็นตัวตัดสินว่างานใด merge หรือ deploy ได้

| บทบาท | สิทธิ์ | ความรับผิดชอบ |
| --- | --- | --- |
| **AI-DLC CoE** — ผู้รับผิดชอบด้านวิศวกรรม ความปลอดภัย และสถาปัตยกรรม | เขียนผ่านการเปลี่ยนแปลงที่ผ่านการทบทวน | ดูแลมาตรฐานกลางและ hosted workflow service |
| **ทีมพัฒนา** | ใช้ registry และเสนอการเปลี่ยนแปลง | เลือกข้อกำหนดที่เกี่ยวข้อง รัน workflow ตรวจผลลัพธ์ และแจ้งช่องว่าง |

## นำ Steering ไปใช้

คัดลอกเฉพาะข้อกำหนดที่ประเมินแล้วว่าเกี่ยวข้องกับ workload ตัวอย่างต่อไปนี้ให้รันจาก project directory:

```bash
git clone --depth 1 https://github.com/AIDLC-KIRO/msclabs.agent-registry.git /tmp/registry
mkdir -p .kiro/steering/security-requirements/pci-dss
cp -R /tmp/registry/aidlc.kiro/steering/guardrails .kiro/steering/

# ตัวอย่าง: คัดลอก PCI DSS requirement หนึ่งรายการที่เลือกจากการประเมิน
PCI_REQUIREMENT=network-security-controls-for-traffic-segmentation.md
cp "/tmp/registry/aidlc.kiro/steering/security-requirements/pci-dss/$PCI_REQUIREMENT" \
   .kiro/steering/security-requirements/pci-dss/
```

อ่านไฟล์ก่อนคัดลอก แล้ว commit ข้อกำหนดที่เลือกเพื่อบันทึก version ที่โครงการใช้งาน คัดลอกทั้ง pack
เฉพาะเมื่อผลการประเมินระบุว่า pack ทั้งชุดเกี่ยวข้อง ไม่ควรคัดลอกทุก pack โดยอัตโนมัติ เพราะ
requirement แต่ละไฟล์ในปัจจุบัน match ทุกไฟล์ที่อยู่ใน context และอาจเพิ่ม standing context จำนวนมาก
ดูวิธีเลือกและโหมด inclusion ใน [คู่มือ steering](aidlc.kiro/steering/README.md)

### Security requirement pack

| Pack | จำนวนข้อ | ขอบเขต |
| --- | --- | --- |
| [ASA base pack](aidlc.kiro/steering/security-requirements/asa-base-pack/_index.md) | 10 | Authentication, authorization, audit logging, การป้องกัน secret, tenant isolation และ trusted cryptography |
| [AWS Well-Architected](aidlc.kiro/steering/security-requirements/aws-well-architected/_index.md) | 32 | Encryption, network segmentation, least privilege, credential management และ threat modeling |
| [NIST CSF](aidlc.kiro/steering/security-requirements/nist-csf/_index.md) | 37 | Identify, protect, detect, respond และ recover |
| [PCI DSS](aidlc.kiro/steering/security-requirements/pci-dss/_index.md) | 50 | ขอบเขตข้อมูลผู้ถือบัตร การแบ่ง segment, logging, key management และ secure development |

ปัจจุบันยังไม่มี pack สำหรับ ISO 27001 และพระราชบัญญัติคุ้มครองข้อมูลส่วนบุคคล (PDPA) ข้อกำหนด
ที่มีอยู่อาจทับซ้อนกับกรอบดังกล่าว แต่ repository นี้ไม่อ้างว่าครอบคลุมหากยังไม่มี mapping เฉพาะ

## เชื่อมต่อ Hosted MCP Workflow

| Server | วัตถุประสงค์ | Tools | เอกสาร |
| --- | --- | --- | --- |
| `aidlc.devsecops-cicd` | เตรียมแอปพลิเคชัน ตรวจ policy ติดตาม pipeline และส่งมอบงานเพื่อ deploy | 14 | [คู่มือ](aidlc.kiro/mcp/devsecops-cicd/README.md) |
| `aidlc.html-creator` | สร้างเอกสารสองภาษาแบบ offline จากรายงาน AWS Transform | 14 | [คู่มือ](aidlc.kiro/mcp/html-creator/README.md) |
| `aidlc.bpmn-creator` | สร้าง BPMN 2.0 swimlane และรองรับการทบทวนรายหน่วยงาน | 12 | [คู่มือ](aidlc.kiro/mcp/bpmn-creator/README.md) |
| `aidlc.deck-creator` | สร้าง HTML presentation, executive summary และ progress report | 16 | [คู่มือ](aidlc.kiro/mcp/deck-creator/README.md) |

PyPI package แต่ละรายการเป็น standard input/output (stdio) bridge บนเครื่องผู้ใช้ที่เชื่อมต่อไปยัง
hosted service ส่วนขั้นตอน reference, template และ policy content อยู่ฝั่ง service

### สิ่งที่ต้องมี

- Kiro IDE ซึ่งเป็น client ที่เอกสารนี้รองรับและผ่านการทดสอบ
- [uv](https://docs.astral.sh/uv/getting-started/installation/) และ Python 3.10 ขึ้นไป
- Access key จากองค์กรที่ติดตั้ง service หรือผู้ดูแล service
- การเชื่อมต่อ HTTPS ไปยัง `*.execute-api.ap-southeast-7.amazonaws.com`
- เฉพาะ BPMN: Node.js และ [draw.io MCP server](https://www.npmjs.com/package/@drawio/mcp)

ทำตาม [MCP client runbook](aidlc.kiro/mcp/RUNBOOK.md) เพื่อติดตั้งและตรวจสอบ Configuration ตัวอย่าง
[`mcp.json`](aidlc.kiro/mcp/mcp.json) เปิด AIDLC server ทั้ง 4 รายการ ให้ลบรายการที่ไม่ได้รับอนุญาต
หรือไม่จำเป็นออก ผู้ดูแล service อาจส่ง configuration ที่ลดเหลือเฉพาะรายการที่อนุมัติแล้วแทน
BPMN ต้องเพิ่ม draw.io entry แยกตาม [คู่มือติดตั้ง](aidlc.kiro/mcp/bpmn-creator/README.md#installation)

อธิบายผลลัพธ์ที่ต้องการในแชต ตัวอย่างเช่น:

```text
เตรียม repo my-org/my-service สำหรับ development pipeline
สร้างเว็บไซต์เอกสารจาก ./ATXDocumentation
สร้าง BPMN สำหรับกระบวนการขอลางาน
สร้าง executive summary จาก .kiro/specs/order-service
```

## การขอสิทธิ์ใช้งาน

การอ่าน repository ไม่ต้องใช้ credential ส่วน hosted service ต้องใช้ access key จากองค์กรที่ติดตั้ง
service หรือผู้ดูแล service Repository นี้ไม่ได้ระบุช่องทางสาธารณะสำหรับขอ key หรือช่องทางสนับสนุน
ที่รับประกัน ผู้ดูแล service ต้องแจ้งวิธีออก key, วันหมดอายุ, การหมุนเวียน, การเพิกถอน และช่องทาง
รายงานเหตุ ห้ามใช้ key ร่วมกันหรือ commit ลง source control ดูขั้นตอน
[หมุนเวียนและเพิกถอน key](aidlc.kiro/mcp/RUNBOOK.md#7-rotate-or-revoke-a-key)

## สถาปัตยกรรมและขอบเขตการทำงาน

![สถาปัตยกรรม registry: MCP client และ uvx bridge ในเครื่องเรียก API Gateway, hosted workflow server 4 รายการจัดการ session และ asset ส่วน Git, การค้นหา AWS ในเครื่อง และ delivery pipeline อยู่ฝั่งทีม](docs/diagrams/registry-architecture.drawio.png)

ไฟล์ต้นฉบับอยู่ที่ [`docs/diagrams/`](docs/diagrams/) ไฟล์ PNG ฝังข้อมูล draw.io จึงเปิดแก้ใน
draw.io ได้โดยตรง

- Local client อาจรันคำสั่งที่ได้รับอนุมัติด้วย credential บนเครื่องผู้ใช้
- Hosted service ไม่ได้รับ AWS credential ในเครื่อง ไม่รันคำสั่ง AWS แทนผู้ใช้ ไม่ push source code
  และไม่ deploy application
- Tool argument ถูกส่งไป hosted service ผ่าน HTTPS Validation tool ประเมินเฉพาะข้อมูลที่ส่งใน
  argument และไม่ได้อ่าน local filesystem ผ่านเครือข่าย
- การแก้ไฟล์ build, Git operation และ deployment ยังอยู่ภายใต้การอนุมัติในเครื่อง รวมถึง repository
  และ pipeline control ที่เป็นอิสระ

## การจัดการข้อมูลและความเป็นส่วนตัว

ห้ามส่ง secret, credential หรือข้อมูลที่มีกฎหมายหรือข้อกำหนดเฉพาะกำกับ เว้นแต่องค์กรอนุมัติ
service สำหรับการใช้งานดังกล่าว Repository นี้ไม่ได้ระบุนโยบายการเก็บรักษา การบันทึกข้อมูลฝั่ง
service หรือการรับประกันถิ่นที่จัดเก็บข้อมูล โปรดสอบถามผู้ดูแล service ก่อนส่งข้อมูลที่มีข้อกำหนด
ด้านการจัดการเป็นพิเศษ

## Environment Variable

| ตัวแปร | คำอธิบาย | ค่าเริ่มต้น |
| --- | --- | --- |
| `MCP_API_TOKEN` | Access key; จำเป็น | — |
| `MSCLABS_MCP_TOKEN` | ชื่อตัวแปร access key สำรอง | — |
| `MSCLABS_MCP_BASE_URL` | Service deployment อื่น | CoE endpoint |
| `MSCLABS_MCP_TIMEOUT` | Request timeout เป็นวินาที | `120` |

## การขอความช่วยเหลือ

ใช้ช่องทาง support และ incident ภายในองค์กรที่ผู้ดูแล service แจ้ง หากเปิด public issue ห้ามแนบ
credential, tool argument ที่มีข้อมูลอ่อนไหว, internal identifier หรือ log ที่ยังไม่ได้ปกปิดข้อมูล

## การร่วมพัฒนา

เปิดการเปลี่ยนแปลงที่ผ่านการทบทวนเข้า `main` ตามกระบวนการขององค์กร Compliance pack ใหม่ต้องอยู่
ใต้ `aidlc.kiro/steering/security-requirements/<pack>/` และอธิบายทั้งขอบเขตกับข้อจำกัด ห้ามเพิ่ม
secret, credential, account identifier, Amazon Resource Name (ARN), private network identifier
หรือ internal endpoint ลงใน public repository นี้

## สัญญาอนุญาต

Apache-2.0 ดู [LICENSE](LICENSE)
