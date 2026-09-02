---
date: '2026-05-27'
description: เรียนรู้วิธีลบ Annotation ในไฟล์ PDF ด้วย GroupDocs.Redaction สำหรับ
  .NET รวมถึงการตั้งค่า, การลบด้วย regex, และเคล็ดลับด้านประสิทธิภาพ
keywords:
- how to redact annotations
- apply redaction to pdf
- pdf annotation redaction
schemas:
- author: GroupDocs
  dateModified: '2026-05-27'
  description: Learn how to redact annotations in PDFs with GroupDocs.Redaction for
    .NET, covering setup, regex redaction, and performance tips.
  headline: How to Redact Annotations Using GroupDocs.Redaction for .NET
  type: TechArticle
- description: Learn how to redact annotations in PDFs with GroupDocs.Redaction for
    .NET, covering setup, regex redaction, and performance tips.
  name: How to Redact Annotations Using GroupDocs.Redaction for .NET
  steps:
  - name: Create a Redactor instance (definition anchor)
    text: '`Redactor` is the entry point for all redaction operations; you pass the
      source file path to its constructor.'
  - name: Define your regular expression (definition anchor)
    text: '`Regex` is the .NET class that evaluates patterns; you can enable case‑insensitivity
      (`i`) and multi‑line mode (`m`) directly in the pattern. - `(?im...)`: Enables
      case‑insensitivity (`i`) and multi‑line search (`m`).'
  - name: Apply the redaction (definition anchor)
    text: '`AnnotationRedaction` is a specialized rule that scans annotation objects
      and replaces matching text with a black rectangle. **Explanation:** - **Parameters:**
      The regex pattern tells the engine which text to target. - **Return Values:**
      This method modifies the document in place; no return value is'
  - name: Save the redacted document (definition anchor)
    text: '`Redactor.Save` writes the modified file to disk, preserving the original
      format unless you specify otherwise.'
  type: HowTo
- questions:
  - answer: Yes. Open the document with `Redactor(string path, string password)` and
      then apply your redaction rules as usual.
    question: Can I redact annotations in password‑protected PDFs?
  - answer: The API works on a copy in memory; the original file remains unchanged
      until you explicitly call `Save`.
    question: Does GroupDocs.Redaction modify the original file?
  - answer: All standard PDF annotation types—including comments, highlights, and
      sticky notes—are fully supported.
    question: How many annotation types are supported?
  - answer: Use `Redactor.GetRedactedDocument()` to retrieve an in‑memory stream and
      render it in your UI for a quick preview.
    question: Is there a way to preview redactions before saving?
  - answer: The library can handle files up to **2 GB**; larger files should be split
      before processing.
    question: What is the maximum file size I can process?
  type: FAQPage
title: วิธีลบ Annotation ด้วย GroupDocs.Redaction สำหรับ .NET
type: docs
url: /th/net/annotation-redaction/redact-text-annotations-groupdocs-redaction-net/
weight: 1
---

# วิธีลบข้อมูลส่วน Annotation ด้วย GroupDocs.Redaction สำหรับ .NET

หากคุณต้องการ **วิธีลบข้อมูลส่วน Annotation** ในไฟล์ PDF หรือ Word คุณมาถูกที่แล้ว คู่มือนี้จะพาคุณผ่านการติดตั้ง GroupDocs.Redaction สำหรับ .NET การกำหนดค่า annotation redaction ที่ใช้ regex และการเพิ่มประสิทธิภาพสำหรับงานขนาดใหญ่ เมื่อเสร็จแล้วคุณจะสามารถซ่อนคอมเมนต์ที่เป็นความลับ, โน้ต, และเมตาดาต้าอื่น ๆ ได้ด้วยเพียงไม่กี่บรรทัดของโค้ด C#.

## คำตอบสั้น
- **ไลบรารีที่จัดการการลบข้อมูลส่วน Annotation คืออะไร?** GroupDocs.Redaction for .NET.  
- **ฉันสามารถใช้ regular expressions ได้หรือไม่?** ใช่ – API รองรับไวยากรณ์ regex ของ .NET เต็มรูปแบบ.  
- **ฉันต้องการไลเซนส์สำหรับการพัฒนาหรือไม่?** การทดลองใช้ฟรีใช้ได้สำหรับการทดสอบ; จำเป็นต้องมีไลเซนส์แบบชำระเงินสำหรับการใช้งานจริง.  
- **รองรับ .NET 6 และ .NET Core หรือไม่?** รองรับเต็มที่บน .NET Framework 4.5+, .NET Core 3.1+, และ .NET 6+.  
- **ความเร็วของการลบข้อมูลส่วนในไฟล์ขนาดใหญ่เป็นอย่างไร?** รูปแบบที่ปรับแต่งสามารถประมวลผล PDF ขนาด 500 หน้าได้ภายในต่ำกว่า 5 วินาทีบนเซิร์ฟเวอร์ทั่วไป.

## การลบข้อมูลส่วน Annotation คืออะไร?
การลบข้อมูลส่วน Annotation จะลบหรือบังข้อความที่อยู่ในคอมเมนต์ของเอกสาร, โน้ต, sticky notes, และอ็อบเจกต์เมตาดาต้าอื่น ๆ อย่างถาวร การลบข้อมูลส่วนนี้ทำให้ข้อมูลที่เป็นความลับไม่สามารถถูกดึงออกหรือดูได้ แม้ไฟล์จะถูกแจกจ่ายหรือเปิดในแอปพลิเคชันอื่น ๆ ซึ่งช่วยรักษาความเป็นส่วนตัวและการปฏิบัติตามกฎระเบียบ.

## ทำไมต้องใช้การลบข้อมูลส่วน Annotation ใน PDF?
GroupDocs.Redaction รองรับ **รูปแบบเอกสารกว่า 30 ประเภท** และสามารถจัดการไฟล์ขนาดสูงสุด **2 GB** โดยไม่ต้องโหลดเนื้อหาทั้งหมดเข้าสู่หน่วยความจำ การใช้เครื่องมือ regex ในตัวช่วยลดเวลาการประมวลผลได้ถึง **70 %** เมื่อเทียบกับการค้นหาสตริงด้วยตนเอง ทำให้เหมาะสำหรับกระบวนการทำงานด้านกฎหมายหรือการเงินที่มีปริมาณสูง.

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน, โปรดตรวจสอบสิ่งต่อไปนี้:

- **GroupDocs.Redaction** ไลบรารี (เวอร์ชันล่าสุดจาก NuGet).  
- รันไทม์ **.NET** ที่เข้ากันได้ (Framework 4.5+, .NET Core 3.1+, .NET 5/6).  
- IDE เช่น **Visual Studio 2022** หรือ **VS Code**.  
- ความรู้พื้นฐานของ C# และความคุ้นเคยกับ regular expressions.  

## วิธีลบข้อมูลส่วน Annotation ด้วย GroupDocs.Redaction?

โหลดเอกสารต้นฉบับของคุณ, กำหนดรูปแบบ regex, ใช้ `AnnotationRedaction`, และบันทึกผลลัพธ์—ทั้งหมดในกระบวนการสามขั้นตอนที่กระชับ ส่วนต่อไปนี้จะแบ่งแต่ละขั้นตอนพร้อมคำอธิบายที่ชัดเจนและโค้ด placeholder ที่คุณจะต้องแทนค่าด้วยของคุณเอง.

### ขั้นตอนที่ 1 – ติดตั้งไลบรารีผ่าน .NET CLI
**คำตอบ:** รัน `dotnet add package GroupDocs.Redaction` ในโฟลเดอร์โปรเจกต์ของคุณ; CLI จะดาวน์โหลดแพ็กเกจที่เสถียรล่าสุดและอัปเดตไฟล์โปรเจกต์ของคุณโดยอัตโนมัติ.  

```bash
dotnet add package GroupDocs.Redaction
```

### ขั้นตอนที่ 2 – ติดตั้งไลบรารีผ่าน Package Manager Console
**คำตอบ:** ใน Package Manager Console ของ Visual Studio ให้รัน `Install-Package GroupDocs.Redaction`; คำสั่งนี้จะจัดการ dependencies และเพิ่มการอ้างอิงไปยังโปรเจกต์ของคุณ.  

```powershell
Install-Package GroupDocs.Redaction
```

### ขั้นตอนที่ 3 – เริ่มต้น Redactor (definition anchor)
คลาส `Redactor` เป็นเอนจินหลักที่โหลดเอกสารและใช้กฎการลบข้อมูลส่วน.  

```csharp
using System;
using GroupDocs.Redaction.Redactions;

namespace DocumentRedaction
{
    class Program
    {
        static void Main(string[] args)
        {
            string sourceFile = @"YOUR_DOCUMENT_DIRECTORY\annotated.xlsx"; // Replace with actual document path.
            
            using (Redactor redactor = new Redactor(sourceFile))
            {
                // Your redaction logic will go here.
            }
        }
    }
}
```

## การใช้ Annotation Redaction

### ขั้นตอนที่ 1: สร้างอินสแตนซ์ Redactor (definition anchor)
`Redactor` เป็นจุดเริ่มต้นสำหรับการดำเนินการลบข้อมูลส่วนทั้งหมด; คุณส่งพาธไฟล์ต้นฉบับไปยังคอนสตรัคเตอร์ของมัน.  

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further processing will occur here.
}
```

### ขั้นตอนที่ 2: กำหนด regular expression ของคุณ (definition anchor)
`Regex` เป็นคลาสของ .NET ที่ประเมินรูปแบบ; คุณสามารถเปิดใช้งานการไม่สนใจตัวพิมพ์ใหญ่ (`i`) และโหมดหลายบรรทัด (`m`) ได้โดยตรงใน pattern.  

```csharp
string pattern = "(?im:john)";
```
- `(?im...)`: เปิดใช้งานการไม่สนใจตัวพิมพ์ใหญ่ (`i`) และการค้นหาหลายบรรทัด (`m`).

### ขั้นตอนที่ 3: ใช้การลบข้อมูลส่วน (definition anchor)
`AnnotationRedaction` เป็นกฎเฉพาะที่สแกนอ็อบเจกต์ annotation และแทนที่ข้อความที่ตรงกันด้วยสี่เหลี่ยมสีดำ.  

```csharp
redactor.Apply(new AnnotationRedaction(pattern));
```

**คำอธิบาย:**  
- **Parameters:** รูปแบบ regex บอกเอนจินว่าต้องการเป้าหมายข้อความใด.  
- **Return Values:** เมธอดนี้แก้ไขเอกสารโดยตรง; ไม่จำเป็นต้องมีค่าที่ส่งกลับ.

### ขั้นตอนที่ 4: บันทึกเอกสารที่ลบข้อมูลส่วนแล้ว (definition anchor)
`Redactor.Save` เขียนไฟล์ที่แก้ไขแล้วลงดิสก์, รักษาฟอร์แมตเดิมไว้ยกเว้นคุณระบุให้เปลี่ยน.  

```csharp
guardedRedactor.Save();
```

## ปัญหาที่พบบ่อยและวิธีแก้ไข
- **ไม่พบผลลัพธ์:** ตรวจสอบไวยากรณ์ regex ของคุณอีกครั้ง; ใช้เครื่องมือทดสอบออนไลน์ที่ใช้เอนจิน .NET เดียวกัน.  
- **ข้อผิดพลาดการเข้าถึงไฟล์:** ตรวจสอบว่าแอปพลิเคชันมีสิทธิ์อ่าน/เขียนสำหรับโฟลเดอร์ต้นทางและปลายทาง.  
- **คอขวดด้านประสิทธิภาพ:** สำหรับเอกสารที่มีมากกว่า 500 หน้า, ให้ประมวลผลเป็นชุดแบบขนานและใช้ `Redactor` อินสแตนซ์เดียวซ้ำได้เมื่อเป็นไปได้.

## คำถามที่พบบ่อย

**ถาม: ฉันสามารถลบข้อมูลส่วน Annotation ใน PDF ที่มีรหัสผ่านได้หรือไม่?**  
ตอบ: ใช่. เปิดเอกสารด้วย `Redactor(string path, string password)` แล้วใช้กฎการลบข้อมูลส่วนตามปกติ.

**ถาม: GroupDocs.Redaction แก้ไขไฟล์ต้นฉบับหรือไม่?**  
ตอบ: API ทำงานบนสำเนาในหน่วยความจำ; ไฟล์ต้นฉบับจะไม่เปลี่ยนแปลงจนกว่าคุณจะเรียก `Save` อย่างชัดเจน.

**ถาม: รองรับประเภท annotation กี่ประเภท?**  
ตอบ: รองรับประเภท annotation มาตรฐานทั้งหมดของ PDF รวมถึงคอมเมนต์, ไฮไลท์, และ sticky notes อย่างเต็มที่.

**ถาม: มีวิธีดูตัวอย่างการลบข้อมูลส่วนก่อนบันทึกหรือไม่?**  
ตอบ: ใช้ `Redactor.GetRedactedDocument()` เพื่อดึงสตรีมในหน่วยความจำและแสดงผลใน UI ของคุณเพื่อดูตัวอย่างอย่างรวดเร็ว.

**ถาม: ขนาดไฟล์สูงสุดที่สามารถประมวลผลได้คือเท่าไหร่?**  
ตอบ: ไลบรารีสามารถจัดการไฟล์ได้สูงสุด **2 GB**; ไฟล์ที่ใหญ่กว่านั้นควรแยกย่อยก่อนการประมวลผล.

## ส่วนคำถามที่พบบ่อย

1. **GroupDocs.Redaction คืออะไร?**  
   - เป็นไลบรารี .NET สำหรับการลบข้อมูลส่วนที่เป็นความลับจากรูปแบบเอกสารต่าง ๆ  

2. **ฉันจัดการกับ annotation ที่ซับซ้อนได้อย่างไร?**  
   - ใช้ regular expressions ขั้นสูงและทดสอบอย่างละเอียดก่อนนำไปใช้กับเอกสารสำคัญ.  

3. **สามารถยกเลิกการลบข้อมูลส่วนได้หรือไม่?**  
   - เมื่อบันทึกแล้วการเปลี่ยนแปลงจะถาวร; ควรสำรองไฟล์ต้นฉบับเสมอ.  

4. **ฉันสามารถรวม GroupDocs.Redaction เข้ากับแอปพลิเคชันที่มีอยู่ได้หรือไม่?**  
   - ใช่, API ของมันอนุญาตให้ผสานรวมอย่างราบรื่นกับระบบที่ใช้ .NET  

5. **GroupDocs.Redaction รองรับรูปแบบไฟล์อะไรบ้าง?**  
   - รองรับหลากหลายประเภทของเอกสารรวมถึง Word, PDF, Excel และอื่น ๆ  

## แหล่งข้อมูล

- [เอกสาร GroupDocs Redaction](https://docs.groupdocs.com/redaction/net/)
- [อ้างอิง API](https://reference.groupdocs.com/redaction/net)
- [ดาวน์โหลด GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)
- [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/redaction/33)
- [รับไลเซนส์ชั่วคราว](https://purchase.groupdocs.com/temporary-license/) 

**อัปเดตล่าสุด:** 2026-05-27  
**ทดสอบด้วย:** GroupDocs.Redaction 23.10 for .NET  
**ผู้เขียน:** GroupDocs

## บทแนะนำที่เกี่ยวข้อง

- [ลบ Annotation จากเอกสารอย่างมีประสิทธิภาพด้วย GroupDocs.Redaction สำหรับ .NET](/redaction/net/annotation-redaction/remove-annotations-groupdocs-redaction-net/)
- [บทแนะนำ Annotation Redaction สำหรับ GroupDocs.Redaction .NET](/redaction/net/annotation-redaction/)
- [วิธีโหลดและลบข้อมูลส่วนจากเอกสารด้วย GroupDocs.Redaction .NET: คู่มือครบถ้วน](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)