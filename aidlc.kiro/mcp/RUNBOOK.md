# Runbook: ติดตั้งและดูแล msclabs MCP servers

สำหรับนักพัฒนาที่ใช้ Kiro ต่อเข้ากับ MCP server ของ MSC Labs CoE

## 1. สิ่งที่ต้องมี

| รายการ | ตรวจด้วย |
| --- | --- |
| uv / uvx | `uvx --version` |
| Python 3.10+ | uv ดาวน์โหลดให้เองถ้ายังไม่มี |
| API key จาก CoE | รูปแบบ `aidlcmcp_<12 ตัว>_<ข้อความยาว>` |
| ออก HTTPS ไปยัง `*.execute-api.ap-southeast-7.amazonaws.com` ได้ | ดูข้อ 4 |
| draw.io MCP (เฉพาะ bpmn-creator) | ดู [bpmn-creator](bpmn-creator/README.md) |

ติดตั้ง uv:

```bash
# macOS / Linux
curl -LsSf https://astral.sh/uv/install.sh | sh
```

```powershell
# Windows
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

## 2. ตั้ง API key

key หนึ่งใบต่อหนึ่งคนหรือหนึ่งงาน อย่าแชร์ เพราะ session ผูกกับเจ้าของ key

### macOS

```bash
mkdir -p ~/.aidlc
printf '%s' 'PASTE_YOUR_KEY' > ~/.aidlc/mcp-token
chmod 600 ~/.aidlc/mcp-token
echo 'export MCP_API_TOKEN=$(cat ~/.aidlc/mcp-token)' >> ~/.zshrc
```

### Windows (PowerShell)

```powershell
setx MCP_API_TOKEN "PASTE_YOUR_KEY"
[Environment]::GetEnvironmentVariable('MCP_API_TOKEN','User')   # ตรวจว่าตั้งแล้ว
```

bridge อ่าน `MCP_API_TOKEN` ก่อน ถ้าไม่มีจะอ่าน `MSCLABS_MCP_TOKEN`

## 3. ตั้งค่า Kiro

### 3.1 MCP config

เปิด Command Palette ค้น `Kiro: Open user MCP config (JSON)` แล้วเติมสามก้อนจาก [`mcp.json`](mcp.json)
เข้าไปใน `mcpServers` ที่มีอยู่ อย่าสร้าง `mcpServers` ซ้อนสองอัน

ถ้าแก้ไฟล์ด้วย PowerShell ให้ใช้ `-Encoding utf8` ไม่อย่างนั้น Kiro อ่านไฟล์ไม่ออก

### 3.2 อนุญาตตัวแปร

เปิด `Preferences: Open User Settings (JSON)` แล้วเพิ่ม (ถ้ามีคีย์นี้อยู่แล้ว ให้เติมเข้าลิสต์เดิม)

```json
"kiroAgent.mcpApprovedEnvVars": ["MCP_API_TOKEN"]
```

ข้ามขั้นนี้ไม่ได้ ถ้าไม่อนุญาต Kiro จะไม่แทนค่า `${MCP_API_TOKEN}`

### 3.3 ปิดเปิด Kiro ให้สุด

- macOS: `Cmd+Q` แล้วเปิดใหม่ Reload Window ไม่พอ
- Windows: ปิดทุกหน้าต่าง ตรวจ Task Manager ว่าไม่เหลือ process Kiro แล้วเปิดใหม่

process รับ environment ตอนเปิดเท่านั้น ถ้าไม่แน่ใจให้เปิดจาก Terminal: `kiro ~/path/to/project`

## 4. ตรวจว่าใช้ได้

ใน Kiro เปิด MCP Server view ทั้งสามตัวต้องขึ้น Connected พร้อมจำนวน tool 14, 14, 12

ตรวจจาก Terminal ก่อนเปิด Kiro ก็ได้ ตัวแปร `B` คือ base URL ของ registry ดูได้จาก CoE

```bash
B=https://<registry-host>
curl -s "$B/devsecops-cicd/health"            # ไม่ต้องใช้ key ต้องได้ "status":"healthy"

curl -s -o /dev/null -w "%{http_code}\n" -X POST "$B/devsecops-cicd/mcp" \
  -H "Authorization: Bearer $MCP_API_TOKEN" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}'
# 200 = key ใช้ได้, 401/403 = key ผิดหรือถูก revoke
```

ทดสอบตัว bridge โดยตรง:

```bash
echo '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}' \
  | uvx msclabs.devsecops-cicd-mcp-server==1.1.0
```

ต้องได้ JSON ที่มี `result.tools` กลับมาทาง stdout และบรรทัด `bridging stdio to ...` ทาง stderr

## 5. ค่าที่ปรับได้

| ตัวแปร | ค่าเริ่มต้น | ใช้ทำอะไร |
| --- | --- | --- |
| `MCP_API_TOKEN` | ไม่มี | API key จำเป็นต้องมี |
| `MSCLABS_MCP_TOKEN` | ไม่มี | ชื่อสำรองของ key |
| `MSCLABS_MCP_BASE_URL` | endpoint ของ CoE | ชี้ไป deployment อื่น เช่น stage ทดสอบ |
| `MSCLABS_MCP_TIMEOUT` | `120` | วินาทีที่รอต่อหนึ่ง call |

## 6. อัปเกรดเวอร์ชัน

ใน config ปักเวอร์ชันด้วย `==1.1.0` โดยเจตนา `@latest` ทำให้แต่ละเครื่องดึง bridge ใหม่เงียบ ๆ
ทุกครั้งที่มีการ publish

1. ดูเวอร์ชันล่าสุดที่ PyPI หรือ [mcp/README.md](README.md)
2. แก้เลขใน `args` ของทั้งสามตัว
3. ล้าง cache ถ้า uvx ยังใช้ตัวเก่า: `uv cache clean msclabs.devsecops-cicd-mcp-server`
4. กด Retry ใน MCP Server view หรือปิดเปิด Kiro

ย้อนเวอร์ชันทำแบบเดียวกัน เปลี่ยนเลขกลับเป็นเวอร์ชันก่อนหน้า

เนื้อหา workflow อัปเดตฝั่ง server โดยไม่ต้องอัปเกรดแพ็กเกจ การอัปเกรดแพ็กเกจจำเป็นเฉพาะเมื่อตัว bridge เปลี่ยน

## 7. หมุนเวียนและ revoke key

| สถานการณ์ | ทำอะไร |
| --- | --- |
| key ใกล้หมดอายุ | ขอใบใหม่จาก CoE แล้วแทนค่าในข้อ 2 ปิดเปิด Kiro |
| key หลุด หรือเครื่องหาย | แจ้ง CoE ให้ revoke ทันที มีผลตั้งแต่ call ถัดไป กระทบแค่ใบนั้น |
| ย้ายเครื่อง | ขอใบใหม่สำหรับเครื่องใหม่ แล้วให้ revoke ใบเก่า |

CoE เก็บแค่ค่า hash ของ key จึงกู้ key ที่หายไม่ได้ ต้องออกใบใหม่เท่านั้น

## 8. แก้ปัญหา

### `Dynamic Client Registration rejected (HTTP 404)`

ไม่ใช่ปัญหา OAuth Kiro ส่ง key ที่ยังไม่ได้แทนค่า server ตอบ 401 แล้ว Kiro ไปลอง OAuth เอง
ตรวจตามลำดับ:

1. `MCP_API_TOKEN` อยู่ใน `kiroAgent.mcpApprovedEnvVars`
2. ตัวแปรมีค่าจริง (`echo $MCP_API_TOKEN` ใน Terminal ที่เปิดใหม่)
3. ปิดเปิด Kiro ให้สุดแล้ว

### log ขึ้น `No API key`

bridge หาตัวแปรไม่เจอและออกด้วย exit code 2 ตั้งค่าตามข้อ 2 แล้วปิดเปิด Kiro

### log ขึ้น `401` หรือ `403 from the registry: the API key was rejected`

key ไม่ครบ พิมพ์ผิด หมดอายุ หรือถูก revoke หรือ key ไม่มีสิทธิ์กับ server ตัวนั้น ขอ CoE ตรวจ

### log ขึ้น `could not reach the registry`

เครือข่ายออกไป endpoint ไม่ได้ ตรวจ proxy, VPN และ firewall ขององค์กร แล้วลอง `curl` health ในข้อ 4

### `uvx: command not found` หรือ server ไม่ start

Kiro หา `uvx` ไม่เจอใน PATH ใส่ path เต็มใน `command` เช่น `/Users/<you>/.local/bin/uvx`
หรือเพิ่ม `"PATH"` ใน `env` ของ server นั้น

### call นานแล้ว timeout

เพิ่ม `MSCLABS_MCP_TIMEOUT` ใน `env` ของ server เช่น `"300"`

### session หยุดเองกลางทาง

`run_log` นับว่าแก้เรื่องเดิมซ้ำครบสามรอบ เป็นกลไกกันการแก้แบบเดาสุ่ม หาสาเหตุจริงก่อน แล้วเริ่ม session ใหม่

### ใช้ชั่วคราวโดยไม่ตั้ง environment variable

วาง key แทน `${MCP_API_TOKEN}` ใน `mcp.json` ตรง ๆ ใช้ได้ทันที แต่ key จะอยู่ในไฟล์ที่คนอื่นบนเครื่องอ่านได้
เหมาะกับการลองเท่านั้น และห้าม commit ไฟล์นั้น

## 9. ขอความช่วยเหลือ

แจ้ง CoE พร้อมข้อมูลนี้ ห้ามแนบ API key:

- ชื่อ server และเวอร์ชันแพ็กเกจ
- บรรทัด log จาก MCP output ที่ขึ้นต้นด้วย `[msclabs.<server>]`
- ผลของ `curl .../health`
- เวลาที่เกิดปัญหา
