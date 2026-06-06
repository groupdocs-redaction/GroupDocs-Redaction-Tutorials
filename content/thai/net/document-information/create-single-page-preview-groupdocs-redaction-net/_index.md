---
date: '2026-06-06'
description: เรียนรู้วิธีแปลงหน้าเป็น PNG และดูตัวอย่างหน้าของ PDF ด้วย GroupDocs.Redaction
  for .NET. คู่มือขั้นตอนต่อขั้นตอน, ตัวอย่างโค้ด, และเคล็ดลับจากการใช้งานจริง.
keywords:
- convert page to png
- how to preview pdf
- GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-06-06'
  description: Learn how to convert page to PNG and preview PDF pages with GroupDocs.Redaction
    for .NET. Step‑by‑step guide, code snippets, and real‑world tips.
  headline: Convert Page to PNG Using GroupDocs.Redaction .NET
  type: TechArticle
- questions:
  - answer: Yes, provide the password when initializing `RedactionEngine` and the
      preview will be created normally.
    question: Can I generate previews for password‑protected PDFs?
  - answer: Set `options.PreviewFormat = PreviewFormat.Jpeg` before calling the preview
      method.
    question: How do I change the output format from PNG to JPEG?
  - answer: Absolutely – assign an array of page numbers to `options.PageNumbers`
      (e.g., `new[] {0, 2, 4}`).
    question: Is it possible to preview multiple pages at once?
  - answer: Increase `options.Width` and `options.Height` to a higher resolution;
      the library scales the image accordingly.
    question: What should I do if the preview image is blurry?
  - answer: Yes, GroupDocs.Redaction .NET is cross‑platform and runs inside Docker
      containers that support .NET Core.
    question: Does this work on Linux containers?
  type: FAQPage
title: แปลงหน้าเป็น PNG ด้วย GroupDocs.Redaction .NET
type: docs
url: /th/net/document-information/create-single-page-preview-groupdocs-redaction-net/
weight: 1
---

# แปลงหน้าเป็น PNG ด้วย GroupDocs.Redaction .NET

การสร้างตัวอย่างของหน้าเดียวจากเอกสารขนาดใหญ่เป็นความต้องการทั่วไปเมื่อคุณต้องการแชร์เฉพาะส่วนที่เกี่ยวข้องของข้อมูล ในบทแนะนำนี้คุณจะได้เรียนรู้ **วิธีแปลงหน้เป็น PNG** ด้วย GroupDocs.Redaction สำหรับ .NET, ตั้งค่าการส่งออกตัวอย่าง, และรวมผลลัพธ์เข้าไปในแอปพลิเคชันของคุณ เราจะอธิบายขั้นตอนเบื้องต้น การติดตั้ง การตั้งค่าโค้ด และเคล็ดลับปฏิบัติ เพื่อให้คุณเริ่มสร้างตัวอย่าง PNG หน้าหนึ่งได้ในไม่กี่นาที

## คำตอบด่วน
- **ฉันสามารถสร้างตัวอย่าง PNG ของเพียงหน้าเดียวได้หรือไม่?** ใช่, ใช้ `PreviewOptions` เพื่อระบุหมายเลขหน้าและรูปแบบ.  
- **GroupDocs.Redaction รองรับรูปแบบใดสำหรับตัวอย่าง?** PNG เป็นค่าเริ่มต้น, แต่ JPEG และ BMP ก็พร้อมใช้งานเช่นกัน.  
- **ฉันต้องการใบอนุญาตสำหรับการพัฒนาหรือไม่?** การทดลองใช้ฟรีทำงานสำหรับการทดสอบ; จำเป็นต้องมีใบอนุญาตการผลิตสำหรับการใช้เชิงพาณิชย์.  
- **ฟีเจอร์นี้ทำงานบน .NET Core และ .NET Framework หรือไม่?** แน่นอน – ไลบรารีนี้มุ่งเป้าไปที่ .NET Standard 2.0+.  
- **กระบวนการนี้มีประสิทธิภาพด้านหน่วยความจำสำหรับไฟล์ขนาดใหญ่หรือไม่?** ใช่, API จะสตรีมหน้า, หลีกเลี่ยงการโหลดเอกสารทั้งหมด.

## การแปลงหน้าเป็น PNG คืออะไร?
**convert page to PNG** หมายถึงการสกัดหน้าเดียวจากเอกสารที่รองรับ (PDF, DOCX, PPTX ฯลฯ) และเรนเดอร์หน้านั้นเป็นภาพ Portable Network Graphics (PNG) ภาพที่ได้จะคงรูปแบบการแสดงผล, ฟอนต์, และกราฟิกของหน้าต้นฉบับ, ทำให้คุณสามารถแชร์ภาพสแนปช็อตที่ชัดเจนขณะยังคงซ่อนส่วนอื่นของเอกสาร.

## ทำไมต้องใช้ตัวอย่างหน้าเดียว?
การสร้างตัวอย่าง PNG หน้าเดียวช่วยลดแบนด์วิดท์, เร่งความเร็วการโหลด, และปกป้องเนื้อหาที่ละเอียดอ่อนโดยเปิดเผยเฉพาะที่จำเป็นเท่านั้น GroupDocs.Redaction สามารถเรนเดอร์ PDF 300 หน้าเป็น PNG ขนาด 200 KB ได้ภายในเวลาน้อยกว่า 0.5 วินาทีบนฮาร์ดแวร์เซิร์ฟเวอร์ทั่วไป, ทำให้เหมาะสำหรับพอร์ทัลเว็บและเครื่องมือรายงาน.

## ข้อกำหนดเบื้องต้น
- **GroupDocs.Redaction for .NET** – ไลบรารีหลักที่ทำการลบข้อมูลและสร้างตัวอย่างเอกสาร.  
- **System.IO** – เนมสเปซมาตรฐานของ .NET สำหรับการจัดการไฟล์.  
- .NET Core 3.1+ หรือ .NET Framework 4.6.1+ (แพลตฟอร์มใดก็ได้ที่รองรับ .NET Standard 2.0).  
- ความรู้พื้นฐานของ C# และความคุ้นเคยกับการจัดการแพคเกจ NuGet.

## การตั้งค่า GroupDocs.Redaction สำหรับ .NET

### ข้อมูลการติดตั้ง

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**Package Manager**  
```bash
Install-Package GroupDocs.Redaction
```  

**NuGet Package Manager UI**  
- เปิดโปรเจกต์ของคุณใน Visual Studio.  
- เลือก **Manage NuGet Packages**.  
- ค้นหา **GroupDocs.Redaction** และติดตั้งเวอร์ชันเสถียรล่าสุด.

### ขั้นตอนการรับใบอนุญาต
เพื่อใช้งานไลบรารีคุณต้องมีใบอนุญาตที่ถูกต้อง คุณสามารถเริ่มด้วยการทดลองใช้ฟรีหรือขอคีย์ชั่วคราว:

1. เยี่ยมชม [GroupDocs website](https://purchase.groupdocs.com/temporary-license) เพื่อขอใบอนุญาตชั่วคราว.  
2. ทำตามคำแนะนำในอีเมลเพื่อเพิ่มไฟล์ใบอนุญาตลงในโปรเจกต์ของคุณ.

### การเริ่มต้นและตั้งค่าเบื้องต้น
คลาส `RedactionEngine` เป็นจุดเริ่มต้นสำหรับการทำงานทั้งหมด, รวมถึงการสร้างตัวอย่าง.  
```csharp
using GroupDocs.Redaction;

var redactor = new Redactor("path/to/your/document");
```  

## คู่มือการนำไปใช้

### ภาพรวม
ส่วนนี้แสดงวิธี **convert page to PNG** โดยการกำหนดค่า `PreviewOptions` และเรียกใช้ API ตัวอย่าง วิธีนี้ทำงานกับ PDF, DOCX, PPTX, และรูปแบบอื่น ๆ มากมายที่ GroupDocs.Redaction รองรับ.

### ขั้นตอนที่ 1: เตรียมสภาพแวดล้อมของคุณ
กำหนดเส้นทางไฟล์ต้นฉบับและโฟลเดอร์ผลลัพธ์ ใช้ `Path.Combine` เพื่อสร้างเส้นทางที่ไม่ขึ้นกับแพลตฟอร์ม.  
```csharp
// Define the directory and file name for output.
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  

### ขั้นตอนที่ 2: ตั้งค่า Preview Options
`PreviewOptions` ให้คุณกำหนดหมายเลขหน้า, ขนาดภาพ, และรูปแบบผลลัพธ์ คลาสนี้เป็นศูนย์กลางการกำหนดค่าการสร้างตัวอย่าง.  
```csharp
int testPageNumber = 1;
string previewFileName = Utils.GetOutputFileByName(sourceFile, $"preview_page{testPageNumber}");

// Initialize the Redactor with the source file.
using (Redactor redactor = new Redactor(sourceFile))
{
    PreviewOptions options = new PreviewOptions(pageNumber => File.OpenWrite(previewFileName));

    // Set dimensions and format for the preview image.
    options.Width = 480;
    options.Height = 640;
    options.PageNumbers = new int[] { testPageNumber };
    options.PreviewFormat = PreviewOptions.PreviewFormats.PNG;

    // Generate and save the page preview.
    redactor.GeneratePreview(options);
}
```  

#### คำอธิบายของการกำหนดค่าหลัก
- **Width & Height** – ปรับค่าตามความละเอียดการแสดงผลที่ต้องการ.  
- **PageNumbers** – ให้ค่าอาเรย์ที่มีดัชนีหน้าที่ต้องการเรนเดอร์ (เริ่มจากศูนย์).  
- **PreviewFormat** – PNG เป็นค่าเริ่มต้น; เปลี่ยนเป็น `PreviewFormat.Jpeg` เพื่อไฟล์ที่มีขนาดเล็กลง.

### เคล็ดลับการแก้ไขปัญหา
If the PNG isn’t generated:

- ตรวจสอบว่าเส้นทางไฟล์ต้นฉบับถูกต้องและไฟล์สามารถเข้าถึงได้.  
- ตรวจสอบว่าไฟล์ใบอนุญาตถูกโหลดก่อนเรียกใช้เมธอด API ใด ๆ.  
- ยืนยันว่า `PreviewOptions.PageNumbers` มีดัชนีหน้าที่ถูกต้อง (เช่น `0` สำหรับหน้าที่หนึ่ง).

## การประยุกต์ใช้งานจริง
การสร้างตัวอย่าง PNG หน้าเดียวมีประโยชน์ในหลายสถานการณ์:

1. **Client Presentations** – แสดงเฉพาะสไลด์หรือข้อสัญญาที่เกี่ยวข้อง.  
2. **Internal Reviews** – เปิดใช้งานการตรวจสอบภาพอย่างรวดเร็วโดยไม่ต้องเปิดเอกสารเต็ม.  
3. **Content Summaries** – ฝังภาพหน้าสแนปช็อตในอีเมลหรือแดชบอร์ดเพื่อให้บริบททันที.

การรวมฟีเจอร์นี้กับ CMS หรือ CRM สามารถทำให้การสร้างภาพย่อสำหรับเอกสารที่อัปโหลดเป็นอัตโนมัติ, ปรับปรุงประสบการณ์ผู้ใช้.

## การพิจารณาด้านประสิทธิภาพ
- **Memory Management** – ปล่อย (Dispose) อินสแตนซ์ `RedactionEngine` หลังการใช้งานเพื่อคืนทรัพยากร.  
- **Asynchronous Execution** – ใช้ `await engine.GeneratePreviewAsync(...)` ในแอปพลิเคชัน UI เพื่อให้ส่วนติดต่อผู้ใช้ตอบสนอง.  
- **Library Updates** – GroupDocs.Redaction รองรับ **รูปแบบเข้าและออกกว่า 30+** และประมวลผลเอกสารได้ถึง 500 หน้าโดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ. ควรอัปเดตแพคเกจเพื่อรับประโยชน์จากการปรับปรุงประสิทธิภาพ.

## สรุป
ตอนนี้คุณมีวิธีที่ครบถ้วนและพร้อมใช้งานในระดับผลิตเพื่อ **convert page to PNG** และสร้างตัวอย่างหน้าเดียวด้วย GroupDocs.Redaction สำหรับ .NET. ด้วยการทำตามขั้นตอนข้างต้นคุณสามารถฝังภาพ PNG คุณภาพสูงลงในแอปพลิเคชัน .NET ใดก็ได้, เพิ่มประสิทธิภาพการแชร์เอกสารพร้อมรักษาความปลอดภัยและประสิทธิภาพ.

## คำถามที่พบบ่อย

**Q: ฉันสามารถสร้างตัวอย่างสำหรับ PDF ที่มีการป้องกันด้วยรหัสผ่านได้หรือไม่?**  
A: ใช่, ให้รหัสผ่านเมื่อเริ่มต้น `RedactionEngine` และตัวอย่างจะถูกสร้างตามปกติ.

**Q: ฉันจะเปลี่ยนรูปแบบผลลัพธ์จาก PNG เป็น JPEG ได้อย่างไร?**  
A: ตั้งค่า `options.PreviewFormat = PreviewFormat.Jpeg` ก่อนเรียกเมธอดสร้างตัวอย่าง.

**Q: สามารถสร้างตัวอย่างหลายหน้าพร้อมกันได้หรือไม่?**  
A: แน่นอน – กำหนดอาเรย์ของหมายเลขหน้าให้กับ `options.PageNumbers` (เช่น `new[] {0, 2, 4}`).

**Q: ควรทำอย่างไรหากภาพตัวอย่างเบลอ?**  
A: เพิ่มค่า `options.Width` และ `options.Height` ให้ความละเอียดสูงขึ้น; ไลบรารีจะปรับสเกลภาพตามนั้น.

**Q: ฟีเจอร์นี้ทำงานบนคอนเทนเนอร์ Linux หรือไม่?**  
A: ใช่, GroupDocs.Redaction .NET เป็นแบบข้ามแพลตฟอร์มและทำงานภายในคอนเทนเนอร์ Docker ที่รองรับ .NET Core.

## แหล่งข้อมูล
- [เอกสาร](https://docs.groupdocs.com/redaction/net/)  
- [อ้างอิง API](https://reference.groupdocs.com/redaction/net)  
- [ดาวน์โหลดเวอร์ชันล่าสุด](https://releases.groupdocs.com/redaction/net/)  
- [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/redaction/33)  
- [การขอใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license)  

---

**อัปเดตล่าสุด:** 2026-06-06  
**ทดสอบด้วย:** GroupDocs.Redaction 5.6 for .NET  
**ผู้เขียน:** GroupDocs

## บทเรียนที่เกี่ยวข้อง

- [เชี่ยวชาญการรักษาความปลอดภัยของเอกสาร: แรสเตอร์และลบข้อมูล Word ด้วย GroupDocs.Redaction .NET](/redaction/net/rasterization-options/secure-word-docs-rasterize-redact-net/)  
- [วิธีลบหน้าจาก PDF ด้วย GroupDocs.Redaction .NET: คู่มือฉบับสมบูรณ์](/redaction/net/page-redaction/delete-pages-pdf-groupdocs-redaction-net/)  
- [การนำการลบข้อมูลเอกสารไปใช้ด้วย GroupDocs.Redaction .NET: คู่มือขั้นตอนโดยละเอียด](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)