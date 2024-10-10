File descriptor (FD) ใน Linux คือจำนวนเต็มที่ไม่ติดลบขนาดเล็กที่ใช้เป็นตัวระบุหรือ "handle" เพื่อเข้าถึงไฟล์หรือทรัพยากร input/output (I/O) อื่น ๆ เช่น pipe, socket หรืออุปกรณ์ต่าง ๆ ทุกครั้งที่กระบวนการ (process) ใน Linux เปิดไฟล์หรือสร้างช่องทางการสื่อสาร ระบบปฏิบัติการจะมอบหมายตัวระบุไฟล์ (file descriptor) เพื่อใช้ติดตามทรัพยากรนั้น ๆ

แนวคิดหลักของ File Descriptor:
หมายเลขของ File Descriptor:

ตัวระบุไฟล์จะแสดงเป็นตัวเลขจำนวนเต็ม
โดยปกติแล้ว กระบวนการหนึ่งจะเริ่มต้นด้วย file descriptor 3 ตัวที่เปิดใช้งาน:
0: Standard input (stdin) – สำหรับอ่านข้อมูลเข้า
1: Standard output (stdout) – สำหรับเขียนข้อมูลออก
2: Standard error (stderr) – สำหรับเขียนข้อความแสดงข้อผิดพลาด
หมายเลข file descriptor เพิ่มเติมจะถูกกำหนดเมื่อมีการเปิดไฟล์หรือทรัพยากรเพิ่มเติม โดยเริ่มตั้งแต่ 3 ขึ้นไป
การทำงานกับ File Descriptor: File descriptor จะถูกใช้ร่วมกับการเรียกระบบ (system call) ต่าง ๆ เช่น:

open(): เปิดไฟล์และคืนค่า file descriptor
read(fd, ...): อ่านข้อมูลจากไฟล์โดยใช้ file descriptor
write(fd, ...): เขียนข้อมูลลงไฟล์โดยใช้ file descriptor
close(fd): ปิดไฟล์ที่เชื่อมโยงกับ file descriptor นั้น ๆ
ประเภทของ File Descriptor:

ไฟล์ปกติ: เมื่อเปิดไฟล์ ระบบจะให้หมายเลข file descriptor
Pipe: ใช้สำหรับการสื่อสารระหว่างกระบวนการ
Socket: ใช้สำหรับการสื่อสารเครือข่าย
อุปกรณ์: เช่น USB, ดิสก์ หรือเทอร์มินัล

การเปิดไฟล์:
```
int fd = open("example.txt", O_RDONLY);
```

การเรียก open() นี้จะคืนค่า file descriptor ที่สามารถใช้ในการอ่านข้อมูลจากไฟล์ "example.txt" ได้

วัฏจักรของ File Descriptor
การสร้าง: file descriptor จะถูกสร้างขึ้นเมื่อมีการเปิดไฟล์หรือทรัพยากร
การใช้งาน: สามารถดำเนินการเช่น read(), write() หรือ seek() โดยใช้ file descriptor
การปิด: เมื่อใช้งานเสร็จแล้ว file descriptor ควรจะถูกปิดด้วย close(fd) เพื่อคืนทรัพยากรของระบบ

คุณสมบัติพิเศษ
Inheritance: file descriptor สามารถถูกส่งต่อให้กับกระบวนการลูก (child process) เมื่อมีการสร้างกระบวนการใหม่ (ผ่าน fork()) หากไม่ได้ระบุให้ปิดโดยชัดเจน
Duplication: file descriptor สามารถถูกทำสำเนาได้ด้วย dup() หรือ dup2() เพื่อให้หลาย ๆ descriptor อ้างอิงไปที่ไฟล์หรือทรัพยากรเดียวกัน

<img width="595" alt="Screenshot 2567-10-10 at 13 20 19" src="https://github.com/user-attachments/assets/2a8fc211-d2ce-423a-a21d-18027d9aa7bf">
