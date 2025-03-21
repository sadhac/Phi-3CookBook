# แชทบอท Interactive Phi 3 Mini 4K Instruct พร้อม Whisper

## ภาพรวม

แชทบอท Interactive Phi 3 Mini 4K Instruct เป็นเครื่องมือที่ช่วยให้ผู้ใช้สามารถโต้ตอบกับ Microsoft Phi 3 Mini 4K instruct demo ผ่านการป้อนข้อความหรือเสียง แชทบอทนี้สามารถใช้สำหรับงานต่าง ๆ เช่น การแปลภาษา การอัปเดตสภาพอากาศ และการค้นหาข้อมูลทั่วไป

### เริ่มต้นใช้งาน

เพื่อใช้งานแชทบอทนี้ ทำตามขั้นตอนดังนี้:

1. เปิด [E2E_Phi-3-mini-4k-instruct-Whispser_Demo.ipynb](https://github.com/microsoft/Phi-3CookBook/blob/main/code/06.E2E/E2E_Phi-3-mini-4k-instruct-Whispser_Demo.ipynb)
2. ในหน้าต่างหลักของโน้ตบุ๊ก คุณจะเห็นอินเทอร์เฟซแชทบ็อกซ์ที่มีช่องป้อนข้อความและปุ่ม "Send"
3. เพื่อใช้งานแชทบอทแบบข้อความ ให้พิมพ์ข้อความของคุณลงในช่องป้อนข้อความและคลิกปุ่ม "Send" แชทบอทจะตอบกลับด้วยไฟล์เสียงที่สามารถเล่นได้โดยตรงในโน้ตบุ๊ก

**หมายเหตุ**: เครื่องมือนี้ต้องการ GPU และการเข้าถึง Microsoft Phi-3 และ OpenAI Whisper models ซึ่งใช้สำหรับการรู้จำเสียงและการแปลภาษา

### ข้อกำหนดของ GPU

ในการรันเดโมนี้ คุณต้องมีหน่วยความจำ GPU อย่างน้อย 12GB

ข้อกำหนดหน่วยความจำสำหรับการรัน **Microsoft-Phi-3-Mini-4K instruct** demo บน GPU จะขึ้นอยู่กับปัจจัยหลายอย่าง เช่น ขนาดของข้อมูลที่ป้อน (เสียงหรือข้อความ) ภาษาในการแปล ความเร็วของโมเดล และหน่วยความจำที่มีอยู่ใน GPU

โดยทั่วไป Whisper model ได้รับการออกแบบให้ทำงานบน GPU โดยมีหน่วยความจำ GPU ขั้นต่ำที่แนะนำคือ 8GB แต่สามารถรองรับหน่วยความจำที่มากขึ้นได้หากจำเป็น

โปรดทราบว่าการรันข้อมูลจำนวนมากหรือคำขอที่มีปริมาณมากบนโมเดล อาจต้องการหน่วยความจำ GPU เพิ่มเติมและ/หรืออาจเกิดปัญหาด้านประสิทธิภาพ แนะนำให้ทดสอบกรณีการใช้งานของคุณด้วยการตั้งค่าต่าง ๆ และตรวจสอบการใช้งานหน่วยความจำเพื่อกำหนดการตั้งค่าที่เหมาะสมที่สุดสำหรับความต้องการเฉพาะของคุณ

## ตัวอย่าง E2E สำหรับแชทบอท Interactive Phi 3 Mini 4K Instruct พร้อม Whisper

โน้ตบุ๊ก Jupyter ที่ชื่อ [Interactive Phi 3 Mini 4K Instruct Chatbot with Whisper](https://github.com/microsoft/Phi-3CookBook/blob/main/code/06.E2E/E2E_Phi-3-mini-4k-instruct-Whispser_Demo.ipynb) แสดงให้เห็นวิธีการใช้ Microsoft Phi 3 Mini 4K instruct demo เพื่อสร้างข้อความจากการป้อนเสียงหรือข้อความ โดยโน้ตบุ๊กนี้กำหนดฟังก์ชันหลายตัว:

1. `tts_file_name(text)`: ฟังก์ชันนี้สร้างชื่อไฟล์จากข้อความที่ป้อนเพื่อบันทึกไฟล์เสียงที่สร้างขึ้น
2. `edge_free_tts(chunks_list,speed,voice_name,save_path)`: ฟังก์ชันนี้ใช้ Edge TTS API เพื่อสร้างไฟล์เสียงจากรายการข้อความที่ป้อน โดยมีพารามิเตอร์คือรายการข้อความ ความเร็วเสียง ชื่อเสียง และที่อยู่สำหรับบันทึกไฟล์เสียง
3. `talk(input_text)`: ฟังก์ชันนี้สร้างไฟล์เสียงโดยใช้ Edge TTS API และบันทึกไปยังชื่อไฟล์แบบสุ่มในไดเรกทอรี /content/audio โดยมีพารามิเตอร์คือข้อความที่ต้องการแปลงเป็นเสียง
4. `run_text_prompt(message, chat_history)`: ฟังก์ชันนี้ใช้ Microsoft Phi 3 Mini 4K instruct demo เพื่อสร้างไฟล์เสียงจากข้อความที่ป้อนและเพิ่มเข้าไปในประวัติการแชท
5. `run_audio_prompt(audio, chat_history)`: ฟังก์ชันนี้แปลงไฟล์เสียงเป็นข้อความโดยใช้ Whisper model API และส่งต่อไปยังฟังก์ชัน `run_text_prompt()`
6. โค้ดนี้เปิดตัวแอป Gradio ที่ช่วยให้ผู้ใช้โต้ตอบกับ Phi 3 Mini 4K instruct demo ได้โดยการพิมพ์ข้อความหรืออัปโหลดไฟล์เสียง ผลลัพธ์จะแสดงเป็นข้อความในแอป

## การแก้ไขปัญหา

การติดตั้งไดรเวอร์ Cuda GPU

1. ตรวจสอบให้แน่ใจว่าแอปพลิเคชัน Linux ของคุณเป็นเวอร์ชันล่าสุด

    ```bash
    sudo apt update
    ```

2. ติดตั้งไดรเวอร์ Cuda

    ```bash
    sudo apt install nvidia-cuda-toolkit
    ```

3. ลงทะเบียนตำแหน่งไดรเวอร์ Cuda

    ```bash
    echo /usr/lib64-nvidia/ >/etc/ld.so.conf.d/libcuda.conf; ldconfig
    ```

4. ตรวจสอบขนาดหน่วยความจำ Nvidia GPU (ต้องการหน่วยความจำ GPU 12GB)

    ```bash
    nvidia-smi
    ```

5. ล้างแคช: หากคุณใช้ PyTorch คุณสามารถเรียก torch.cuda.empty_cache() เพื่อปล่อยหน่วยความจำที่ไม่ได้ใช้งานทั้งหมดเพื่อให้สามารถใช้กับแอปพลิเคชัน GPU อื่นได้

    ```python
    torch.cuda.empty_cache() 
    ```

6. ตรวจสอบ Nvidia Cuda

    ```bash
    nvcc --version
    ```

7. ทำตามขั้นตอนต่อไปนี้เพื่อสร้าง Hugging Face token

    - ไปที่ [Hugging Face Token Settings page](https://huggingface.co/settings/tokens?WT.mc_id=aiml-137032-kinfeylo)
    - เลือก **New token**
    - ป้อนชื่อโปรเจกต์ **Name** ที่คุณต้องการใช้
    - เลือก **Type** เป็น **Write**

> **หมายเหตุ**
>
> หากคุณพบข้อผิดพลาดดังนี้:
>
> ```bash
> /sbin/ldconfig.real: Can't create temporary cache file /etc/ld.so.cache~: Permission denied 
> ```
>
> เพื่อแก้ไขปัญหานี้ ให้พิมพ์คำสั่งดังต่อไปนี้ในเทอร์มินัลของคุณ
>
> ```bash
> sudo ldconfig
> ```

**ข้อจำกัดความรับผิดชอบ**:  
เอกสารนี้ได้รับการแปลโดยใช้บริการแปลภาษาอัตโนมัติด้วย AI แม้ว่าเราจะพยายามให้การแปลมีความถูกต้อง แต่โปรดทราบว่าการแปลอัตโนมัติอาจมีข้อผิดพลาดหรือความไม่ถูกต้อง เอกสารต้นฉบับในภาษาต้นทางควรถูกพิจารณาเป็นแหล่งข้อมูลที่น่าเชื่อถือที่สุด สำหรับข้อมูลที่สำคัญ ขอแนะนำให้ใช้บริการแปลภาษามนุษย์ที่เป็นมืออาชีพ เราไม่รับผิดชอบต่อความเข้าใจผิดหรือการตีความที่ผิดพลาดซึ่งเกิดจากการใช้การแปลนี้