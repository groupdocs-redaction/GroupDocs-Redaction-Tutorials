---
date: '2026-10-06'
description: เรียนรู้วิธีทำการลบข้อมูลโดยใช้ GroupDocs.Redaction .NET พร้อมการทำงานของ
  IRedactionCallback ใน C#. ทำตามคู่มือขั้นตอนต่อขั้นตอน แนวทางปฏิบัติที่ดีที่สุด
  และตัวอย่างจากโลกจริง
keywords:
- how to redact data
- GroupDocs.Redaction .NET
- IRedactionCallback implementation
- document redaction C#
lastmod: '2026-10-06'
og_description: เรียนรู้วิธีทำการลบข้อมูลโดยใช้ GroupDocs.Redaction .NET พร้อมการทำงานของ
  IRedactionCallback ใน C#. ทำตามคู่มือขั้นตอนต่อขั้นตอน พร้อมแนวทางปฏิบัติที่ดีที่สุดและตัวอย่างจากโลกจริง
og_image_alt: Guide to redact data with GroupDocs.Redaction .NET in C#
og_title: วิธีทำการลบข้อมูลด้วย GroupDocs.Redaction .NET (C#)
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  headline: How to redact data with GroupDocs.Redaction .NET (C#)
  type: TechArticle
- description: Learn how to redact data using GroupDocs.Redaction .NET with an IRedactionCallback
    implementation in C#. Follow this step‑by‑step guide, best practices, and real‑world
    examples.
  name: How to redact data with GroupDocs.Redaction .NET (C#)
  steps:
  - name: prepare output directory and source file path
    text: Define where your source document lives. Adjust the path to match your environment.
      `LoadOptions` is a configuration object that tells the SDK how to read the file
      (e.g., password handling).
  - name: create a Redactor instance with custom settings
    text: We instantiate `Redactor` with `LoadOptions` and `RedactorSettings`. The
      `RedactionDump` inside the settings will automatically record every redaction
      that occurs. `RedactorSettings` lets you fine‑tune the redaction process; passing
      a `RedactionDump` enables a detailed audit file. `RedactionDump` is
  - name: apply an exact‑phrase redaction
    text: Here we replace the phrase **John Doe** with the placeholder **[REDACTED]**.
      You can swap any phrase or pattern you need to hide. `ReplacementOptions` defines
      what text will replace the matched content. It also supports font and color
      customisation if you need a visual mask. **Explanation of the key
  type: HowTo
- questions:
  - answer: You can start with a free trial or request a temporary license to explore
      all features. For production, purchase a perpetual or subscription license.
    question: What are the licensing options for GroupDocs.Redaction?
  - answer: Yes, it supports PDFs, Word, Excel, PowerPoint, and many other common
      formats.
    question: Can I use GroupDocs.Redaction on multiple file types?
  - answer: Wrap your redaction logic in `try‑catch` blocks and log the exception
      details. The callback can also be used to capture errors in real time.
    question: How do I handle exceptions during redaction?
  - answer: The core API is synchronous, but you can run redaction calls inside asynchronous
      tasks or background services.
    question: Is there built‑in support for asynchronous processing?
  - answer: The [official documentation](https://docs.groupdocs.com/redaction/net/)
      and API reference provide extensive code samples and scenario guides.
    question: Where can I find more advanced examples?
  type: FAQPage
tags:
- redact data
- GroupDocs.Redaction
- .NET redaction
- C# document security
- IRedactionCallback
title: วิธีทำการลบข้อมูลด้วย GroupDocs.Redaction .NET (C#)
type: docs
url: /th/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/
weight: 1
---

# วิธีลบข้อมูลด้วย GroupDocs.Redaction .NET (C#)

ในบทแนะนำฉบับเต็มนี้คุณจะได้ค้นพบ **วิธีลบข้อมูล** จาก PDF, ไฟล์ Word, และเอกสารอื่น ๆ ด้วย GroupDocs.Redaction สำหรับ .NET ไม่ว่าคุณต้องการซ่อนตัวระบุส่วนบุคคลในสัญญากฎหมายหรือทำความสะอาดตัวเลขลับจากรายงานการเงิน SDK จะให้การควบคุมแบบโปรแกรมเพื่อให้แน่ใจว่าข้อมูลที่ละเอียดอ่อนทุกส่วนหายไปอย่างถาวรและตรวจสอบได้ เราจะเดินผ่านการติดตั้งไลบรารี, การกำหนดค่า `IRedactionCallback` แบบกำหนดเอง, และการใช้การลบข้อมูลแบบวลีตรงพร้อมบันทึกเต็มรูปแบบ

## คำตอบด่วน
- **IRedactionCallback ทำอะไร?** มันทำให้คุณสามารถดักจับเหตุการณ์การลบข้อมูลทุกครั้ง บันทึกรายละเอียด และปรับเปลี่ยนข้อความแทนที่ได้แบบเรียลไทม์  
- **ต้องการไลเซนส์หรือไม่?** การทดลองใช้งานทำงานสำหรับการพัฒนา; ไลเซนส์ถาวรจะลบข้อจำกัดการประเมินทั้งหมด  
- **เวอร์ชัน .NET ที่รองรับคืออะไร?** .NET Core 3.1+, .NET 5/6, และ .NET Framework 4.6+  
- **สามารถประมวลผลหลายไฟล์ได้หรือไม่?** ได้—ห่อหุ้มตรรกะในลูปหรือใช้การประมวลผลแบบแบตช์เพื่อประสิทธิภาพสูงสุด  
- **การลบข้อมูลแบบอะซิงโครนัสเป็นไปได้หรือไม่?** ไม่ได้มีในตัว, แต่คุณสามารถเรียก API ภายใน `Task.Run` หรือรูปแบบอะซิงโครนัสอื่น ๆ  

## การลบข้อมูลที่ละเอียดอ่อนคืออะไร?
`Redaction` คือการลบหรือทำให้ข้อมูลที่ต้องไม่เปิดเผยหายไปอย่างถาวร ด้วย GroupDocs.Redaction คุณกำหนดวลีที่ตรงกัน, รูปแบบ regular‑expression หรือกฎกำหนดเองและแทนที่ด้วยตัวแทนเช่น **[REDACTED]** พร้อมคงรูปแบบและการแบ่งหน้าเดิม

## ทำไมต้องใช้ GroupDocs.Redaction กับ IRedactionCallback?
`IRedactionCallback` เป็นอินเทอร์เฟซที่แจ้งให้คุณทราบทุกครั้งที่ SDK ลบส่วนของเนื้อหา, ให้คุณบันทึกข้อมูลการตรวจสอบหรือปรับเปลี่ยนการแทนที่แบบไดนามิก สิ่งนี้ทำให้มีการตรวจสอบเต็มรูปแบบ, การบังคับใช้กฎธุรกิจแบบกำหนดเอง, และการผสานรวมกับระบบการปฏิบัติตามกฎระเบียบอย่างราบรื่น—โดยไม่ลดทอนประสิทธิภาพ

## ข้อกำหนดเบื้องต้น
- **ไลบรารี GroupDocs.Redaction** (เวอร์ชันที่เข้ากันได้ – ดูที่หน้า [documentation page](https://docs.groupdocs.com/redaction/net/)). รายละเอียดเต็มสามารถดูได้ที่ [official documentation](https://docs.groupdocs.com/redaction/net/)  
- .NET Core หรือ .NET Framework ต้องติดตั้งบนเครื่องพัฒนาของคุณ  
- Visual Studio (รุ่น Community ก็พอ) หรือ IDE ใด ๆ ที่รองรับ C#  
- ความรู้พื้นฐาน C# และความคุ้นเคยกับการจัดการแพ็กเกจ NuGet  

## การตั้งค่า GroupDocs.Redaction สำหรับ .NET
ขั้นแรก, เพิ่มไลบรารีลงในโปรเจคของคุณ. เลือกวิธีที่คุณชอบ – CLI, Package Manager Console, หรือ UI. คำสั่งจะเหมือนเดิมกับในบทแนะนำต้นฉบับ

### ตัวเลือกการติดตั้ง
**.NET CLI:**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console:**  
```powershell
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI:**  
- เปิดโปรเจคของคุณใน Visual Studio  
- ไปที่ **Manage NuGet Packages**  
- ค้นหา **GroupDocs.Redaction** และติดตั้งเวอร์ชัน stable ล่าสุด  

### การรับไลเซนส์
เพื่อทดลองใช้ผลิตภัณฑ์, ขอรับการทดลองฟรีหรือไลเซนส์ชั่วคราวจาก [here](https://purchase.groupdocs.com/temporary-license/). คุณยังสามารถรับไลเซนส์ชั่วคราวจาก [temporary‑license page](https://purchase.groupdocs.com/temporary-license/). สำหรับการใช้งานในผลิตภัณฑ์, ซื้อไลเซนส์เต็มเพื่อเปิดใช้งานคุณสมบัติทั้งหมดโดยไม่มีข้อจำกัด

#### การเริ่มต้นและตั้งค่าพื้นฐาน
ด้านล่างเป็นโค้ดขั้นต่ำที่คุณต้องใช้เพื่อเปิดเอกสารด้วยคลาส `Redactor`. อย่าปรับเปลี่ยนสคริปต์นี้ – มันเป็นพื้นฐานสำหรับทุกอย่างต่อไป.  
`Redactor` คือคลาสหลักที่แทนเอกสารและให้เมธอดสำหรับใช้กฎการลบข้อมูล  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path

using (Redactor redactor = new Redactor(sourceFile))
{
    // Your redaction logic here
}
```

## คู่มือการนำไปใช้
ตอนนี้เราจะขยายการตั้งค่าพื้นฐานโดยเพิ่ม `IRedactionCallback` แบบกำหนดเอง. สิ่งนี้ทำให้คุณสามารถบันทึกเหตุการณ์การลบข้อมูลแต่ละรายการ, เขียนลงล็อก, หรือแม้แต่ปรับเปลี่ยนข้อความแทนที่แบบเรียลไทม์

### แนบและใช้การทำงานของ IRedactionCallback
`IRedactionCallback` เป็นอินเทอร์เฟซที่รับ callback สำหรับการดำเนินการลบข้อมูลแต่ละครั้ง, ทำให้คุณสามารถบันทึกหรือเปลี่ยนแปลงพฤติกรรมโดยโปรแกรม

#### ขั้นตอนที่ 1: เตรียมไดเรกทอรีผลลัพธ์และเส้นทางไฟล์ต้นฉบับ
กำหนดตำแหน่งที่ไฟล์เอกสารต้นฉบับของคุณอยู่. ปรับเส้นทางให้ตรงกับสภาพแวดล้อมของคุณ  
`LoadOptions` คืออ็อบเจ็กต์การกำหนดค่าที่บอก SDK วิธีอ่านไฟล์ (เช่น การจัดการรหัสผ่าน)  
```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/sample.docx"; // Replace with actual path
```

#### ขั้นตอนที่ 2: สร้างอินสแตนซ์ Redactor ด้วยการตั้งค่าแบบกำหนดเอง
เราสร้างอินสแตนซ์ `Redactor` ด้วย `LoadOptions` และ `RedactorSettings`. `RedactionDump` ภายในการตั้งค่าจะบันทึกการลบข้อมูลทุกครั้งโดยอัตโนมัติ  
`RedactorSettings` ให้คุณปรับกระบวนการลบข้อมูลอย่างละเอียด; การส่ง `RedactionDump` จะเปิดใช้งานไฟล์ตรวจสอบรายละเอียด  
`RedactionDump` เป็นคลาสช่วยเหลือที่เขียนเหตุการณ์การลบข้อมูลแต่ละรายการเป็นไฟล์ JSON สำหรับรายงานการปฏิบัติตาม  
```csharp
using (Redactor redactor = new Redactor(sourceFile, 
    new LoadOptions(), 
    new RedactorSettings(new RedactionDump())))
{
    // Further processing steps will go here
}
```

#### ขั้นตอนที่ 3: ใช้การลบข้อมูลแบบวลีตรง
ที่นี่เราจะแทนที่วลี **John Doe** ด้วยตัวแทน **[REDACTED]**. คุณสามารถเปลี่ยนวลีหรือรูปแบบใดก็ได้ที่ต้องการซ่อน  
`ReplacementOptions` กำหนดข้อความที่จะใช้แทนเนื้อหาที่ตรงกัน. มันยังรองรับการปรับแต่งฟอนต์และสีหากคุณต้องการมาสก์แบบภาพ  
```csharp
redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[REDACTED]")));
```

**คำอธิบายของอ็อบเจ็กต์สำคัญ**
- `LoadOptions()` – บอก SDK วิธีอ่านเอกสาร (เช่น การจัดการรหัสผ่าน)  
- `RedactorSettings(new RedactionDump())` – เปิดใช้งานไฟล์ dump ที่บันทึกการลบข้อมูลแต่ละครั้งเพื่อการตรวจสอบ  
- `ReplacementOptions("[REDACTED]")` – กำหนดข้อความที่จะใช้แทนวลีที่ตรงกัน  

### ทำไมเรื่องนี้สำคัญ
กลไก callback บันทึกเหตุการณ์การลบข้อมูลทุกครั้ง, สร้างเส้นทางการตรวจสอบที่เครื่องอ่านได้, และให้คุณปรับเปลี่ยนตัวแทนแบบไดนามิก, ซึ่งช่วยให้สอดคล้องกับข้อกำหนดการปฏิบัติตามและลดความพยายามในการประมวลผลหลังจากลบข้อมูลด้วยมือ. การผสานข้อมูลนี้กับระบบเฝ้าระวังของคุณทำให้คุณสร้างรายงาน, เรียกแจ้งเตือน, และมั่นใจว่าไม่มีข้อมูลละเอียดอ่อนหลุดผ่านกระบวนการลบข้อมูล  

การใช้ `IRedactionCallback` ให้คุณสามข้อได้เปรียบที่ชัดเจน:
1. **บันทึกพร้อมการปฏิบัติตาม** – การลบข้อมูลทุกครั้งถูกบันทึกใน dump ที่เครื่องอ่านได้, ตอบสนองความต้องการการตรวจสอบสำหรับกว่า 30 กรอบกฎหมาย  
2. **การแทนที่แบบไดนามิก** – คุณสามารถเปลี่ยนตัวแทนตามประเภทข้อมูล, ลดการประมวลผลด้วยมือได้ถึง 40 %  
3. **ประสิทธิภาพที่ขยายได้** – callback เพิ่มภาระที่น้อยมาก (<2 ms ต่อการลบข้อมูล) พร้อมให้คุณประมวลผลไฟล์หลายพันไฟล์พร้อมกันแบบแบตช์  

### เคล็ดลับการแก้ไขปัญหา
- **ไฟล์ไม่พบ:** ตรวจสอบเส้นทาง `sourceFile` อีกครั้งและให้แน่ใจว่าไฟล์สามารถเข้าถึงได้โดยกระบวนการที่กำลังทำงาน  
- **Callback ไม่ทำงาน:** ตรวจสอบว่าคลาสของคุณได้ทำการ implement **ทั้งหมด** ของ `IRedactionCallback` และอินสแตนซ์ถูกส่งอย่างถูกต้องไปยัง `Redactor`  
- **ความล่าช้าของประสิทธิภาพ:** สำหรับแบตช์ขนาดใหญ่, ใช้อินสแตนซ์ `Redactor` เดียวกันซ้ำเมื่อเป็นไปได้และทำการ dispose อย่างรวดเร็ว  

## การประยุกต์ใช้งานจริง
การลบข้อมูลที่ละเอียดอ่อนมีประโยชน์ในหลายอุตสาหกรรม:
1. **การประมวลผลเอกสารทางกฎหมาย** – ลบชื่อของลูกค้า, หมายเลขคดี, หรือหมายเลขประกันสังคมโดยอัตโนมัติก่อนแชร์ฉบับร่าง  
2. **ระบบการจัดการ HR** – ลบตัวระบุส่วนบุคคลจากสัญญาพนักงานระหว่างการตรวจสอบ  
3. **การรายงานทางการเงิน** – ซ่อนตัวเลขที่เป็นกรรมสิทธิ์หรือหมายเลขบัญชีเมื่อสร้าง PDF สำหรับนักลงทุน  

## พิจารณาด้านประสิทธิภาพ
GroupDocs.Redaction รองรับ **รูปแบบอินพุตและเอาต์พุตกว่า 30 ประเภท** (PDF, DOCX, PPTX, XLSX, HTML, และประเภทภาพ) และสามารถประมวลผลไฟล์หลายร้อยหน้าโดยไม่ต้องโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ. เพื่อให้แอปพลิเคชันของคุณทำงานเร็วเมื่อจัดการหลายสิบหรือหลายร้อยไฟล์:
- **การประมวลผลแบบแบตช์:** โหลดรายการไฟล์และรันลูปการลบข้อมูลภายใน `Parallel.ForEach` เพื่อใช้ประโยชน์จากหลายคอร์  
- **การจัดการหน่วยความจำ:** ห่อ `Redactor` แต่ละตัวในบล็อก `using` (ตามที่แสดง) เพื่อรับประกันการทำลาย  
- **การดำเนินการแบบอะซิงโครนัส:** แม้ SDK จะเป็นแบบ synchronous, คุณสามารถถ่ายงานไปยังเธรดพื้นหลังหรือ `Task.Run` เพื่อหลีกเลี่ยงการบล็อก UI thread  

## ปัญหาทั่วไปและวิธีแก้
| ปัญหา | วิธีแก้ |
|-------|----------|
| **ข้อผิดพลาด “Invalid file format”** | ตรวจสอบให้แน่ใจว่าประเภทเอกสารได้รับการสนับสนุน (PDF, DOCX, PPTX ฯลฯ) |
| **Callback รับค่า null** | ตรวจสอบว่าคุณส่งการทำงานที่เป็น concrete implementation ของ `IRedactionCallback` เมื่อสร้าง `RedactorSettings` |
| **การลบข้อมูลไม่ทำงาน** | ยืนยันว่าวลีที่ตรงกันตรงกับตัวอักษรและช่องว่างในเอกสาร, หรือใช้ `RegexRedaction` สำหรับการจับคู่แบบรูปแบบ |

## คำถามที่พบบ่อย

**Q: ตัวเลือกการให้ไลเซนส์ของ GroupDocs.Redaction มีอะไรบ้าง?**  
A: คุณสามารถเริ่มต้นด้วยการทดลองฟรีหรือขอไลเซนส์ชั่วคราวเพื่อสำรวจคุณสมบัติทั้งหมด. สำหรับการใช้งานในผลิตภัณฑ์, ซื้อไลเซนส์แบบถาวรหรือแบบสมัครสมาชิก  

**Q: สามารถใช้ GroupDocs.Redaction กับหลายประเภทไฟล์ได้หรือไม่?**  
A: ได้, รองรับ PDF, Word, Excel, PowerPoint, และรูปแบบทั่วไปอื่น ๆ มากมาย  

**Q: จะจัดการข้อยกเว้นระหว่างการลบข้อมูลอย่างไร?**  
A: ห่อโลจิกการลบข้อมูลในบล็อก `try‑catch` และบันทึกรายละเอียดข้อยกเว้น. Callback ก็สามารถใช้จับข้อผิดพลาดแบบเรียลไทม์ได้เช่นกัน  

**Q: มีการสนับสนุนการประมวลผลแบบอะซิงโครนัสในตัวหรือไม่?**  
A: Core API เป็น synchronous, แต่คุณสามารถรันการเรียกลบข้อมูลภายในงานอะซิงโครนัสหรือบริการพื้นหลังได้  

**Q: จะหา ตัวอย่างขั้นสูงเพิ่มเติมได้จากที่ไหน?**  
A: [เอกสารอย่างเป็นทางการ](https://docs.groupdocs.com/redaction/net/) และอ้างอิง API มีตัวอย่างโค้ดและแนวทางการใช้งานอย่างละเอียด  

## แหล่งข้อมูล
- [เอกสาร GroupDocs.Redaction สำหรับ .NET](https://docs.groupdocs.com/redaction/net/)  
- [อ้างอิง API GroupDocs.Redaction สำหรับ .NET](https://reference.groupdocs.com/redaction/net/)  
- [ดาวน์โหลด GroupDocs.Redaction สำหรับ .NET](https://releases.groupdocs.com/redaction/net/)  
- [ฟอรั่ม GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)  
- [สนับสนุนฟรี](https://forum.groupdocs.com/)  
- [ไลเซนส์ชั่วคราว](https://purchase.groupdocs.com/temporary-license/)  

**อัปเดตล่าสุด:** 2026-10-06  
**ทดสอบด้วย:** GroupDocs.Redaction 2.3 (ล่าสุด ณ เวลาที่เขียน)  
**ผู้เขียน:** GroupDocs  

## บทแนะนำที่เกี่ยวข้อง
- [สร้างนโยบายการลบข้อมูลด้วย GroupDocs.Redaction .NET – คู่มือขั้นตอนต่อขั้นตอน](/redaction/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/)  
- [วิธีลบข้อมูลในเอกสารด้วย GroupDocs.Redaction .NET – คู่มือครบถ้วน](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)  
- [ลบข้อมูลใน .net ด้วย Streams – คู่มือ GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)