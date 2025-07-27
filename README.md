
-----

# AI Agent Project with Ollama & n8n

[](https://docs.docker.com/compose/)
[](https://ollama.ai/)
[](https://n8n.io/)
[](https://opensource.org/licenses/MIT) *(สามารถเปลี่ยนเป็น License ที่เหมาะสมกับโปรเจกต์ของคุณได้)*

โปรเจกต์นี้จัดเตรียมสภาพแวดล้อมที่ครบวงจรสำหรับการพัฒนาและรัน AI Agent แบบ Local โดยใช้ **Ollama** สำหรับ LLM inference และ **n8n** สำหรับการสร้าง Automation Workflow ทั้งหมดถูกจัดการด้วย **Docker Compose** เพื่อความสะดวกในการติดตั้งและทำซ้ำได้

## สารบัญ

1.  [คุณสมบัติ](https://www.google.com/search?q=%23%E0%B8%84%E0%B8%B8%E0%B8%93%E0%B8%AA%E0%B8%A1%E0%B8%9A%E0%B8%B1%E0%B8%95%E0%B8%B4)
2.  [ความต้องการของระบบ](https://www.google.com/search?q=%23%E0%B8%84%E0%B8%A7%E0%B8%B2%E0%B8%A1%E0%B8%95%E0%B9%89%E0%B8%AD%E0%B8%87%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B8%82%E0%B8%AD%E0%B8%87%E0%B8%A3%E0%B8%B0%E0%B8%9A%E0%B8%9A)
3.  [การติดตั้ง](https://www.google.com/search?q=%23%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B8%95%E0%B8%B4%E0%B8%94%E0%B8%95%E0%B8%B1%E0%B9%89%E0%B8%87)
      * [ขั้นตอนที่ 1: ติดตั้ง Docker Desktop](https://www.google.com/search?q=%23%E0%B8%82%E0%B8%B1%E0%B9%89%E0%B8%99%E0%B8%95%E0%B8%AD%E0%B8%99%E0%B8%97%E0%B8%B5%E0%B9%88-1-%E0%B8%95%E0%B8%B4%E0%B8%94%E0%B8%95%E0%B8%B1%E0%B9%89%E0%B8%87-docker-desktop)
      * [ขั้นตอนที่ 2: ตั้งค่า Docker Compose](https://www.google.com/search?q=%23%E0%B8%82%E0%B8%B1%E0%B9%89%E0%B8%99%E0%B8%95%E0%B8%AD%E0%B8%99%E0%B8%97%E0%B8%B5%E0%B9%88-2-%E0%B8%95%E0%B8%B1%E0%B9%89%E0%B8%87%E0%B8%84%E0%B9%88%E0%B8%B2-docker-compose)
      * [ขั้นตอนที่ 3: รัน Service](https://www.google.com/search?q=%23%E0%B8%82%E0%B8%B1%E0%B9%89%E0%B8%99%E0%B8%95%E0%B8%AD%E0%B8%99%E0%B8%97%E0%B8%B5%E0%B9%88-3-%E0%B8%A3%E0%B8%B1%E0%B8%99-service)
      * [ขั้นตอนที่ 4: ดาวน์โหลด LLM Model (Gemma3)](https://www.google.com/search?q=%23%E0%B8%82%E0%B8%B1%E0%B9%89%E0%B8%99%E0%B8%95%E0%B8%AD%E0%B8%99%E0%B8%97%E0%B8%B5%E0%B9%88-4-%E0%B8%94%E0%B8%B2%E0%B8%A7%E0%B8%99%E0%B9%8C%E0%B9%82%E0%B8%AB%E0%B8%A5%E0%B8%94-llm-model-gemma3)
4.  [การใช้งาน](https://www.google.com/search?q=%23%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B9%83%E0%B8%8A%E0%B9%89%E0%B8%87%E0%B8%B2%E0%B8%99)
      * [การเข้าถึง n8n UI](https://www.google.com/search?q=%23%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B9%80%E0%B8%82%E0%B9%89%E0%B8%B2%E0%B8%96%E0%B8%B6%E0%B8%87-n8n-ui)
      * [การ Import Workflow](https://www.google.com/search?q=%23%E0%B8%81%E0%B8%B2%E0%B8%A3-import-workflow)
      * [การทดสอบ Ollama ใน n8n](https://www.google.com/search?q=%23%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B8%97%E0%B8%94%E0%B8%AA%E0%B8%AD%E0%B8%9A-ollama-%E0%B9%83%E0%B8%99-n8n)
5.  [โครงสร้างโปรเจกต์](https://www.google.com/search?q=%23%E0%B9%82%E0%B8%84%E0%B8%A3%E0%B8%87%E0%B8%AA%E0%B8%A3%E0%B9%89%E0%B8%B2%E0%B8%87%E0%B9%82%E0%B8%9B%E0%B8%A3%E0%B9%80%E0%B8%88%E0%B8%81%E0%B8%95%E0%B9%8C)
6.  [การจัดการ Credential](https://www.google.com/search?q=%23%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B8%88%E0%B8%B1%E0%B8%94%E0%B8%81%E0%B8%B2%E0%B8%A3-credential)
7.  [การแก้ไขปัญหาที่พบบ่อย](https://www.google.com/search?q=%23%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B9%81%E0%B8%81%E0%B9%89%E0%B9%84%E0%B8%82%E0%B8%9B%E0%B8%B1%E0%B8%8D%E0%B8%AB%E0%B8%B2%E0%B8%97%E0%B8%B5%E0%B9%88%E0%B8%9E%E0%B8%9A%E0%B8%9A%E0%B9%88%E0%B8%AD%E0%B8%A2)
8.  [การปิด Service](https://www.google.com/search?q=%23%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B8%9B%E0%B8%B4%E0%B8%94-service)

## คุณสมบัติ

  * **Ollama Integration:** รัน LLM (เช่น Gemma3) แบบ Local ได้อย่างง่ายดายผ่าน Docker และสามารถเข้าถึงได้จาก n8n
  * **n8n Automation:** แพลตฟอร์ม Low-code/No-code สำหรับสร้าง Workflow และ AI Agent
  * **Containerized Environment:** จัดการและ Deploy Service ทั้งหมดผ่าน Docker Compose เพื่อความสามารถในการทำซ้ำและแยกส่วน (Isolation)
  * **GPU Acceleration:** รองรับการใช้งาน NVIDIA GPU สำหรับ Ollama เพื่อการประมวลผลที่รวดเร็ว (สำหรับเครื่องที่มี GPU)
  * **No Sign-in for n8n:** ตั้งค่า n8n ให้สามารถเข้าใช้งานได้ทันทีโดยไม่ต้องผ่านระบบ authentication (เหมาะสำหรับ Environment พัฒนา/Test)
  * **Git Version Control:** เตรียมพร้อมสำหรับการจัดการโค้ดและ Workflow ด้วย Git

## ความต้องการของระบบ

  * **Docker Desktop:** (รวม Docker Engine และ Docker Compose)
      * สำหรับ Windows: ต้องเปิดใช้งาน WSL 2
  * **RAM:** แนะนำ 16GB ขึ้นไป (32GB+ สำหรับโมเดล LLM ขนาดใหญ่)
  * **CPU:** Multi-core Processor
  * **GPU (Optional แต่แนะนำ):** การ์ดจอ NVIDIA (เช่น RTX 3060 ขึ้นไป) ที่มี VRAM 8GB ขึ้นไป สำหรับการรัน LLM ที่มีประสิทธิภาพสูงสุด

## การติดตั้ง

ทำตามขั้นตอนเหล่านี้เพื่อตั้งค่าโปรเจกต์บนเครื่องของคุณ:

### ขั้นตอนที่ 1: ติดตั้ง Docker Desktop

หากยังไม่มี Docker Desktop ให้ดาวน์โหลดและติดตั้งจาก [Docker Desktop official website](https://docs.docker.com/desktop/install/windows-install/)

  * **สำหรับ Windows:** ตรวจสอบให้แน่ใจว่าได้เปิดใช้งาน **WSL 2** แล้ว หากยังไม่ได้เปิด ให้รันคำสั่ง PowerShell (ในโหมด Administrator):
    ```powershell
    dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
    dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    wsl --set-default-version 2
    ```
    จากนั้น **รีสตาร์ทเครื่อง**

### ขั้นตอนที่ 2: ตั้งค่า Docker Compose

1.  **สร้างโฟลเดอร์โปรเจกต์:** สร้างโฟลเดอร์เปล่าสำหรับโปรเจกต์ของคุณ (เช่น `your-ai-agent-project`)

2.  **สร้างไฟล์ `docker-compose.yml`:** คัดลอกโค้ดด้านล่างนี้ และบันทึกเป็น `docker-compose.yml` ในโฟลเดอร์โปรเจกต์ของคุณ

    ```yaml
    version: '3.8'

    services:
      ollama:
        image: ollama/ollama:latest
        deploy:
          resources:
            reservations:
              devices:
                - driver: nvidia
                  count: all
                  capabilities: [gpu]
        ports:
          - "127.0.0.1:11434:11434"
        volumes:
          - ollama_data:/root/.ollama
        container_name: ollama

      n8n:
        image: n8nio/n8n:latest
        ports:
          - "5678:5678"
        environment:
          - N8N_BASIC_AUTH_ACTIVE=false
          - N8N_EDITOR_BASE_URL=http://localhost:5678/
          - WEBHOOK_URL=http://localhost:5678/
          - N8N_METRICS_ENABLED=false
          - N8N_LOG_LEVEL=info
        volumes:
          - n8n_data:/home/node/.n8n
        container_name: n8n
        depends_on:
          - ollama

    volumes:
      ollama_data:
      n8n_data:
    ```

      * **หมายเหตุ GPU:** หากคุณไม่มีการ์ดจอ NVIDIA หรือไม่ต้องการใช้ GPU ให้ลบส่วน `deploy` ใน `ollama` service ออก

3.  **สร้างไฟล์ `.gitignore`:** สร้างไฟล์ชื่อ `.gitignore` ในโฟลเดอร์โปรเจกต์ และเพิ่มเนื้อหาดังนี้

    ```
    # Docker Volumes
    ollama_data/
    n8n_data/

    # n8n specific files (if using embedded db)
    .n8n/

    # OS specific files
    .DS_Store
    Thumbs.db

    # Logs
    *.log
    ```

### ขั้นตอนที่ 3: รัน Service

เปิด Terminal หรือ Command Prompt, ไปยังโฟลเดอร์โปรเจกต์ของคุณ และรันคำสั่ง:

```bash
docker compose up -d
```

  * คำสั่งนี้จะดาวน์โหลด Docker Images ที่จำเป็น (Ollama, n8n), สร้าง Docker Volumes และรัน Service ทั้งหมดในพื้นหลัง
  * คุณสามารถตรวจสอบสถานะได้ด้วย: `docker compose ps`

### ขั้นตอนที่ 4: ดาวน์โหลด LLM Model (Gemma3)

หลังจาก Ollama Container เริ่มทำงาน คุณต้องดาวน์โหลดโมเดล `gemma3` ที่ต้องการ:

1.  เข้าถึง Ollama CLI ภายใน Container:
    ```bash
    docker exec -it ollama ollama run gemma3:4b
    ```
      * คุณสามารถเปลี่ยน `gemma3:4b` เป็นเวอร์ชันอื่นที่คุณต้องการ เช่น `gemma3:12b` หรือ `gemma3:latest`
      * Ollama จะเริ่มดาวน์โหลดโมเดล และเมื่อเสร็จสิ้น คุณสามารถพิมพ์ `bye` เพื่อออกจาก Chat ได้

## การใช้งาน

### การเข้าถึง n8n UI

เปิดเว็บเบราว์เซอร์ของคุณและไปที่:

```
http://localhost:5678
```

คุณจะเข้าสู่ n8n UI ได้ทันทีโดยไม่ต้อง Sign-in

### การ Import Workflow

หากคุณมี Workflow ที่ Export ไว้ในไฟล์ JSON (เช่น `n8n-workflows/my-first-agent-workflow.json`):

1.  ใน n8n UI, ไปที่ส่วน **"Workflows"**
2.  คลิก **"Add New"** หรือ **"New"**
3.  เลือก **"Import from File"** แล้วเลือกไฟล์ JSON ของ Workflow ที่คุณต้องการ

### การทดสอบ Ollama ใน n8n

คุณสามารถทดสอบการเชื่อมต่อ Ollama ได้โดยการสร้าง Workflow ใหม่ใน n8n:

1.  เพิ่ม Node **"HTTP Request"**
2.  ตั้งค่า:
      * **Authentication:** `None`
      * **Method:** `POST`
      * **URL:** `http://ollama:11434/api/generate`
      * **Body Parameters (JSON - Raw):**
        ```json
        {
          "model": "gemma3:4b", // หรือเวอร์ชันที่คุณดาวน์โหลด
          "prompt": "What is n8n and Ollama?",
          "stream": false
        }
        ```
3.  **Execute Workflow** หรือ **Test Node** เพื่อดูผลลัพธ์

## โครงสร้างโปรเจกต์

```
your-ai-agent-project/
├── .gitignore                      # ไฟล์สำหรับ Git เพื่อละเว้นไฟล์ที่ไม่จำเป็น
├── docker-compose.yml              # ไฟล์กำหนดค่า Docker services
├── n8n-workflows/                  # โฟลเดอร์สำหรับเก็บ exported n8n workflows (ไฟล์ .json)
│   └── my-first-agent-workflow.json
└── README.md                       # ไฟล์คำอธิบายโปรเจกต์นี้
```

## การจัดการ Credential

  * Credential ที่ใช้ใน n8n (เช่น API Key สำหรับบริการภายนอก) จะไม่ถูก Export ไปพร้อมกับ Workflow JSON
  * คุณจะต้อง **สร้าง Credential เหล่านั้นขึ้นมาใหม่** ภายใน n8n UI บนเครื่องที่คุณใช้งานโปรเจกต์ หรือจัดการผ่าน Environment Variables (สำหรับ Credential ที่ละเอียดอ่อนมากๆ)

## การแก้ไขปัญหาที่พบบ่อย

  * **Port Conflict:** หาก Port `5678` (n8n) หรือ `11434` (Ollama) ถูกใช้งานอยู่แล้ว คุณสามารถเปลี่ยน Port ที่ด้านซ้ายของ `ports:` ใน `docker-compose.yml`
  * **Ollama ไม่เห็น GPU:** ตรวจสอบว่าไดรเวอร์ NVIDIA เป็นเวอร์ชันล่าสุด, Docker Desktop อัปเดต และได้เปิดใช้งาน GPU support ใน WSL 2 settings
  * **n8n เชื่อมต่อ Ollama ไม่ได้:** ตรวจสอบ URL ใน n8n Node ว่าเป็น `http://ollama:11434` และ Ollama Container กำลังทำงานอยู่
  * **โมเดลไม่ถูกดาวน์โหลด:** รัน `docker exec -it ollama ollama run <model_name>` อีกครั้งเพื่อให้แน่ใจว่าโมเดลถูกดาวน์โหลดลงใน Volume แล้ว

## การปิด Service

เมื่อต้องการหยุดการทำงานของ Service ทั้งหมด:

```bash
docker compose down
```

หากต้องการลบ Docker Volumes และข้อมูลทั้งหมดด้วย ให้เพิ่ม `--volumes`:

```bash
docker compose down --volumes
```

-----