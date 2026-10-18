# Hooks

Agent hook สำหรับวางใน `.kiro/hooks/` ยังไม่มีรายการ

## โครงสร้าง

```
hooks/<hook-id>.json     หนึ่งไฟล์ต่อหนึ่ง hook
hooks/<hook-id>.md       อธิบายว่าทำอะไร trigger เมื่อไร และผลข้างเคียง
```

```json
{
  "version": "v1",
  "hooks": [{
    "name": "Lint on Save",
    "trigger": "PostFileSave",
    "matcher": "\\.(ts|tsx)$",
    "action": { "type": "command", "command": "npm run lint" }
  }]
}
```

trigger: `SessionStart`, `UserPromptSubmit`, `PreToolUse`, `PostToolUse`, `Stop`, `PreTaskExec`,
`PostTaskExec`, `PostFileCreate`, `PostFileSave`, `PostFileDelete`

action: `command` (รัน shell, exit 2 = block) หรือ `agent` (เติม prompt เข้า context)

## ติดตั้ง

คัดลอกไฟล์ `.json` ไปที่ `.kiro/hooks/` ใน workspace แล้วตรวจใน Agent Hooks panel

## เกณฑ์รับเข้า

- command ต้องอ่านเข้าใจได้ ไม่ดาวน์โหลดและรัน script จาก URL
- ห้ามส่ง source code หรือ secret ออกนอกเครื่อง
