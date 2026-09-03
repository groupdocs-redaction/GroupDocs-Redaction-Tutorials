---
date: '2026-07-06'
description: เรียนรู้วิธี redact documents .net using streams ด้วย GroupDocs.Redaction.
  บทเรียนนี้ครอบคลุม setup, load document from stream, applying redactions, และ saving
  securely.
keywords:
- redact documents .net
- load document from stream
- GroupDocs.Redaction streams
schemas:
- author: GroupDocs
  dateModified: '2026-07-06'
  description: Learn how to redact documents .net using streams with GroupDocs.Redaction.
    This tutorial covers setup, load document from stream, applying redactions, and
    saving securely.
  headline: Redact documents .net using Streams – GroupDocs.Redaction Guide
  type: TechArticle
- description: Learn how to redact documents .net using streams with GroupDocs.Redaction.
    This tutorial covers setup, load document from stream, applying redactions, and
    saving securely.
  name: Redact documents .net using Streams – GroupDocs.Redaction Guide
  steps:
  - name: '**Free Trial** – download a trial from [GroupDocs](https://purchase.groupdocs.com/temporary-license/).'
    text: '**Free Trial** – download a trial from [GroupDocs](https://purchase.groupdocs.com/temporary-license/).'
  - name: '**Temporary License** – request a short‑term key for evaluation.'
    text: '**Temporary License** – request a short‑term key for evaluation.'
  - name: '**Full Purchase** – obtain a permanent license for production workloads.'
    text: '**Full Purchase** – obtain a permanent license for production workloads.'
  - name: '**Dispose streams promptly** – `using` statements automatically close streams,
      freeing memory.'
    text: '**Dispose streams promptly** – `using` statements automatically close streams,
      freeing memory.'
  - name: '**Batch processing** – Loop through a collection of files and reuse a single
      `Redactor` instance when format permits, reducing allocation overhead.'
    text: '**Batch processing** – Loop through a collection of files and reuse a single
      `Redactor` instance when format permits, reducing allocation overhead.'
  - name: '**File access denied** – Verify the application’s account has read/write
      permissions on the target folders.'
    text: '**File access denied** – Verify the application’s account has read/write
      permissions on the target folders.'
  - name: '**Redaction not applied** – Ensure the redaction type you chose is compatible
      with the document format (e.g., `DeleteAnnotationRedaction` works for PDF and
      DOCX).'
    text: '**Redaction not applied** – Ensure the redaction type you chose is compatible
      with the document format (e.g., `DeleteAnnotationRedaction` works for PDF and
      DOCX).'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports over 70 formats—including PDF, DOCX, XLSX,
      PPTX, and HTML—when using stream‑based APIs.
    question: Which file formats can be processed with streams?
  - answer: Yes, call `redactor.GetRedactedDocument()` to obtain an in‑memory representation
      that you can render or inspect programmatically.
    question: Can I preview redactions before saving?
  - answer: Supply the password when opening the stream via `Redactor` overloads that
      accept `LoadOptions` containing the password.
    question: How does the library handle password‑protected files?
  - answer: The engine can process files up to 2 GB; larger files should be split
      or processed in chunks to stay within memory limits.
    question: Is there a limit on document size?
  - answer: A single license key can be used across multiple environments as long
      as the usage complies with the licensing agreement.
    question: Do I need a separate license for each deployment environment?
  type: FAQPage
title: ลบข้อมูลส่วนตัวในเอกสาร .net ด้วย Streams – คู่มือ GroupDocs.Redaction
type: docs
url: /th/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/
weight: 1
---

# การลบข้อมูลในเอกสาร .net ด้วย Streams – คู่มือฉบับสมบูรณ์

ยินดีต้อนรับ! ในบทแนะนำนี้คุณจะได้เรียนรู้วิธี **redact documents .net** อย่างปลอดภัยโดยใช้สตรีมกับ GroupDocs.Redaction เราจะพาคุณผ่านทุกขั้นตอนที่ต้องการ—ตั้งแต่การติดตั้งไลบรารี, การโหลดเอกสารจากสตรีม, การใช้การลบข้อมูลอย่างแม่นยำ, จนถึงการบันทึกผลลัพธ์โดยไม่ทิ้งไฟล์ชั่วคราวบนดิสก์

## คำตอบอย่างรวดเร็ว
- **ไลบรารีใดจัดการการลบข้อมูลใน .NET?** GroupDocs.Redaction for .NET.  
- **ฉันสามารถโหลดไฟล์โดยตรงจากสตรีมได้หรือไม่?** ได้—ใช้ `FileStream` กับคอนสตรัคเตอร์ Redactor.  
- **ฟอร์แมตใดบ้างที่รองรับ?** มากกว่า 70 ฟอร์แมตเข้าและออก รวมถึง PDF, DOCX, XLSX, PPTX.  
- **ต้องการใบอนุญาตสำหรับการใช้งานจริงหรือไม่?** จำเป็นต้องมีใบอนุญาต GroupDocs.Redaction ที่ถูกต้องสำหรับการใช้งานที่ไม่ใช่แบบทดลอง.  
- **ปลอดภัยสำหรับไฟล์ขนาดใหญ่หรือไม่?** การประมวลผลแบบสตรีมช่วยหลีกเลี่ยงการโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ ทำให้สามารถจัดการเอกสารหลายกิกะไบต์ได้.

## อะไรคือ “redact documents .net”?
**“Redact documents .net”** หมายถึงกระบวนการลบหรือทำให้ข้อมูลที่ละเอียดอ่อนจากไฟล์เป็นถาวรโดยใช้ไลบรารี .NET เช่น GroupDocs.Redaction ซึ่งทำให้ข้อมูลลับไม่เคยออกจากระบบในรูปแบบข้อความที่อ่านได้ง่าย ใช้กันทั่วไปในภาคกฎหมาย, การเงิน, และสุขภาพ เพื่อให้สอดคล้องกับกฎระเบียบความเป็นส่วนตัวเช่น GDPR และ HIPAA และทำให้ข้อมูลที่ละเอียดอ่อนไม่สามารถกู้คืนได้หลังการประมวลผล

## ทำไมต้องใช้สตรีมสำหรับการลบข้อมูล?
GroupDocs.Redaction รองรับ **ไฟล์กว่า 70 รูปแบบ** และสามารถประมวลผลไฟล์ขนาดถึง **2 GB** โดยไม่ต้องโหลดทั้งหมดเข้าสู่หน่วยความจำ การสตรีมช่วยลดภาระ I/O, ปรับปรุงประสิทธิภาพ, และสอดคล้องกับแนวปฏิบัติด้านความปลอดภัยโดยเก็บข้อมูลในหน่วยความจำเพียงช่วงสั้นที่จำเป็นสำหรับการแปลง

## ข้อกำหนดเบื้องต้น

- **GroupDocs.Redaction for .NET** – ติดตั้งผ่าน NuGet (ดูด้านล่าง).  
- **.NET 6+** (หรือ .NET Framework 4.6.1+).  
- Visual Studio 2022 หรือ IDE ที่เข้ากันได้.  
- ความรู้พื้นฐานของ C# และความคุ้นเคยกับสตรีมของ .NET.

## การติดตั้ง GroupDocs.Redaction

คุณสามารถเพิ่มแพ็กเกจด้วยคำสั่งใดคำสั่งหนึ่งต่อไปนี้:

**.NET CLI**  
```shell
dotnet add package GroupDocs.Redaction
```  

**Package Manager Console**  
```shell
Install-Package GroupDocs.Redaction
```  

หรือค้นหา “GroupDocs.Redaction” ใน UI ของ NuGet Package Manager แล้วคลิก **Install**.

### ขั้นตอนการรับใบอนุญาต
1. **Free Trial** – ดาวน์โหลดรุ่นทดลองจาก [GroupDocs](https://purchase.groupdocs.com/temporary-license/).  
2. **Temporary License** – ขอคีย์ระยะสั้นเพื่อการประเมิน.  
3. **Full Purchase** – รับใบอนุญาตถาวรสำหรับการทำงานในสภาพแวดล้อมการผลิต.

เมื่อติดตั้งเสร็จแล้ว ให้เริ่มต้นไลบรารีในโค้ดของคุณ:

```csharp
using GroupDocs.Redaction;
// Initialization code here...
```  

## วิธีโหลดเอกสารจากสตรีม?

`FileStream` ให้สตรีมสำหรับการอ่านและเขียนไฟล์บนดิสก์ คลาส `Redactor` จะประมวลผลเอกสารและใช้กฎการลบข้อมูล โหลดไฟล์ต้นฉบับของคุณเข้าสู่ `FileStream` แล้วส่งสตรีมนั้นให้กับคอนสตรัคเตอร์ `Redactor` วิธีนี้ช่วยหลีกเลี่ยงการเขียนไฟล์ต้นฉบับไปยังตำแหน่งชั่วคราวและเก็บข้อมูลในหน่วยความจำเฉพาะระยะเวลาที่ต้องการประมวลผล วิธีนี้ทำงานได้กับฟอร์แมตที่รองรับทั้งหมด รวมถึง PDF และเอกสาร Office

```csharp
// Directly open the source file as a read‑only stream
using var inputStream = new FileStream(inputPath, FileMode.Open, FileAccess.Read);
```

## วิธีเริ่มต้น Redactor ด้วยสตรีม?

คลาส `Redactor` เป็นเอนจินหลักที่จัดการเนื้อหาเอกสาร โดยการให้สตรีมอินพุต คุณจะสามารถทำการลบข้อมูลในหน่วยความจำโดยไม่ต้องใช้ไฟล์กลาง หลังจากสร้างอินสแตนซ์แล้ว คุณสามารถต่อกฎการลบข้อมูล, ดูตัวอย่างการเปลี่ยนแปลง, และกำหนดตัวเลือกเช่นการเรสเตอร์ไลซ์หรือการเข้ารหัส ก่อนทำการบันทึกเอกสารขั้นสุดท้าย

```csharp
// Initialise the Redactor with the input stream
using var redactor = new GroupDocs.Redaction.Redactor(inputStream);
```

**Definition anchor:** `GroupDocs.Redaction.Redactor` เป็นคลาสหลักที่ให้เมธอดสำหรับใช้, ดูตัวอย่าง, และทำการบันทึกการลบข้อมูลบนเอกสารที่โหลดจากสตรีม

## วิธีใช้การลบข้อมูล?

คุณสามารถเพิ่มการกระทำการลบหลายรายการ; ตัวอย่างด้านล่างลบคำอธิบายทั้งหมด ซึ่งเป็นความต้องการทั่วไปสำหรับการลบคอมเมนต์หรือโน้ตของผู้ตรวจสอบ ประเภทการลบเพิ่มเติมเช่น `DeleteTextRedaction` หรือ `ReplaceTextRedaction` สามารถรวมกันเพื่อเอาหรือทำให้สตริง, วันที่, หรือรูปแบบเฉพาะหายไปทั่วเอกสาร

```csharp
// Apply a predefined redaction that removes every annotation
redactor.Apply(new DeleteAnnotationRedaction());
```

**Definition anchor:** `DeleteAnnotationRedaction` เป็นกฎการลบข้อมูลที่สร้างมาให้โดยอัตโนมัติซึ่งลบวัตถุคำอธิบายเช่นคอมเมนต์, ไฮไลท์, และสแตมป์จากเอกสารอย่างถาวร

## วิธีบันทึกเอกสารที่ลบข้อมูลแล้ว?

การบันทึกโดยตรงไปยัง `FileStream` ทำให้ผลลัพธ์ถูกเขียนในหนึ่งรอบ ลดไฟล์ชั่วคราวที่ไม่จำเป็น คุณยังสามารถระบุฟอร์แมตผลลัพธ์, ระดับการบีบอัด, และการป้องกันด้วยรหัสผ่านผ่านอ็อบเจกต์ `SaveOptions` เพื่อให้ตรงตามข้อกำหนดความปลอดภัย สุดท้ายให้ปิดสตรีมเอาต์พุตเพื่อปล่อยแฮนด์เดิลไฟล์และรับรองว่าไฟล์ถูกเขียนเต็มที่บนดิสก์

```csharp
// Prepare the output stream for the redacted file
using var outputStream = new FileStream(outputPath, FileMode.Create, FileAccess.Write);

// Save the modified document; RasterizationOptions disabled to keep text editable
redactor.Save(outputStream, new SaveOptions { RasterizationOptions = null });
```

**Definition anchor:** `SaveOptions` ให้คุณควบคุมวิธีการบันทึกเอกสาร รวมถึงการเรสเตอร์ไลซ์, การเข้ารหัส, และการเลือกฟอร์แมต

## กรณีการใช้งานทั่วไป
- **การจัดการเอกสารทางกฎหมาย:** ลบคำอธิบายที่เป็นความลับก่อนแชร์ร่างให้ลูกค้า.  
- **การปฏิบัติตาม GDPR:** ลบตัวระบุส่วนบุคคลจากสัญญาหรือบันทึกพนักงาน.  
- **รายงานการตรวจสอบภายใน:** ซ่อนโน้ตของผู้ตรวจสอบในขณะที่ยังคงเนื้อหาหลักสำหรับการแจกจ่าย.

## เคล็ดลับประสิทธิภาพสำหรับไฟล์ขนาดใหญ่
1. **Dispose สตรีมโดยเร็ว** – คำสั่ง `using` ปิดสตรีมอัตโนมัติ ปลดปล่อยหน่วยความจำ.  
2. **การประมวลผลเป็นชุด** – วนลูปผ่านคอลเลกชันของไฟล์และใช้ `Redactor` ตัวเดียวซ้ำเมื่อฟอร์แมตอนุญาต ลดค่าใช้จ่ายในการจัดสรร.

## การแก้ไขปัญหา

1. **ไฟล์เข้าถึงไม่ได้** – ตรวจสอบว่าบัญชีแอปพลิเคชันมีสิทธิ์อ่าน/เขียนในโฟลเดอร์เป้าหมาย.  
2. **การลบข้อมูลไม่ทำงาน** – ตรวจสอบว่าชนิดการลบที่เลือกเข้ากันได้กับฟอร์แมตของเอกสาร (เช่น `DeleteAnnotationRedaction` ทำงานกับ PDF และ DOCX).

## คำถามที่พบบ่อย

**Q: ฟอร์แมตไฟล์ใดบ้างที่สามารถประมวลผลด้วยสตรีม?**  
A: GroupDocs.Redaction รองรับฟอร์แมตกว่า 70 ประเภท—รวมถึง PDF, DOCX, XLSX, PPTX, และ HTML—เมื่อใช้ API แบบสตรีม

**Q: ฉันสามารถดูตัวอย่างการลบข้อมูลก่อนบันทึกได้หรือไม่?**  
A: ได้, เรียก `redactor.GetRedactedDocument()` เพื่อรับตัวแทนในหน่วยความจำที่คุณสามารถเรนเดอร์หรือตรวจสอบโปรแกรมได้

**Q: ไลบรารีจัดการไฟล์ที่มีรหัสผ่านอย่างไร?**  
A: ส่งรหัสผ่านเมื่อเปิดสตรีมผ่านโอเวอร์โหลดของ `Redactor` ที่รับ `LoadOptions` ที่มีรหัสผ่าน

**Q: มีขีดจำกัดขนาดเอกสารหรือไม่?**  
A: เอนจินสามารถประมวลผลไฟล์ได้สูงสุด 2 GB; ไฟล์ที่ใหญ่กว่านั้นควรแบ่งหรือประมวลผลเป็นชิ้นเพื่ออยู่ในขอบเขตหน่วยความจำ

**Q: ต้องการใบอนุญาตแยกต่างหากสำหรับแต่ละสภาพแวดล้อมการปรับใช้หรือไม่?**  
A: คีย์ใบอนุญาตเดียวสามารถใช้ได้หลายสภาพแวดล้อม ตราบใดที่การใช้งานสอดคล้องกับข้อตกลงการให้สิทธิ์

## สรุป
คุณมีวิธีแก้ปัญหาแบบครบถ้วนขั้นตอนต่อขั้นตอนสำหรับ **redact documents .net** ด้วยสตรีมและ GroupDocs.Redaction โดยการโหลดไฟล์โดยตรงจากสตรีม, ใช้การลบข้อมูลที่ตรงเป้าหมาย, และบันทึกโดยไม่มีไฟล์กลาง คุณจึงได้ทั้งความปลอดภัยและประสิทธิภาพ สำรวจประเภทการลบข้อมูลเพิ่มเติม—เช่นการแทนที่ข้อความหรือการลบเมตาดาต้า—to ปรับกระบวนการให้ตรงกับความต้องการการปฏิบัติตามของคุณ

---

**Last Updated:** 2026-07-06  
**Tested With:** GroupDocs.Redaction 5.0 for .NET  
**Author:** GroupDocs  

## แหล่งข้อมูล
- [Documentation](https://docs.groupdocs.com/redaction/net/)
- [API Reference](https://reference.groupdocs.com/redaction/net)
- [Download](https://releases.groupdocs.com/redaction/net/)
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)
- [Temporary License](https://purchase.groupdocs.com/temporary-license/)

```csharp
string sourceFile = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "sample.docx");
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    // Proceed with document processing...
}
```

```csharp
using (var redactor = new GroupDocs.Redaction.Redactor(stream))
{
    // Apply redactions...
}
```

```csharp
redactor.Apply(new GroupDocs.Redaction.Redactions.DeleteAnnotationRedaction());
```

```csharp
string outputFile = Path.Combine("YOUR_OUTPUT_DIRECTORY", "redacted_sample.docx");
using (Stream streamOut = File.Open(outputFile, FileMode.Create, FileAccess.Write))
{
    redactor.Save(streamOut, new GroupDocs.Redaction.Options.RasterizationOptions { Enabled = false });
}
```

## บทแนะนำที่เกี่ยวข้อง

- [วิธีโหลดและลบข้อมูลในเอกสารโดยใช้ GroupDocs.Redaction .NET&#58; คู่มือฉบับสมบูรณ์](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [ลบข้อมูลและบันทึกเอกสารด้วย GroupDocs.Redaction for .NET&#58; คู่มือฉบับสมบูรณ์](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [วิธีสกัดข้อมูลเมตาดาต้าเอกสารจากสตรีมโดยใช้ GroupDocs.Redaction .NET](/redaction/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/)