---
date: 2026-06-11
description: เรียนรู้วิธีการส่งออกไฟล์ที่ถูกทำเครื่องหมาย, กำหนดค่าโฟลเดอร์ผลลัพธ์,
  สร้าง rasterized PDFs, และบันทึกลง streams โดยใช้ GroupDocs.Redaction สำหรับ .NET.
keywords:
- how to export redacted
- configure output folder
- create rasterized pdf
- save rasterized pdf
- convert redacted to pdf
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  headline: How to Export Redacted Documents with GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to export redacted files, configure output folders, create
    rasterized PDFs, and save to streams using GroupDocs.Redaction for .NET.
  name: How to Export Redacted Documents with GroupDocs.Redaction .NET
  steps:
  - name: Install the NuGet Package
    text: 'Add the latest GroupDocs.Redaction package to your project:'
  - name: Load the Document and Define Redactions
    text: Create a `Redactor` instance, load the file, and specify the regions you
      want to hide. The `Redactor` class provides the core functionality for loading
      documents and applying redaction rules.
  - name: Choose the Export Method
    text: '#### Export in Original Format'
  type: HowTo
- questions:
  - answer: Yes, GroupDocs.Redaction can convert most input types to PDF, DOCX, XLSX,
      PPTX, or rasterized PDF, covering over 30 formats.
    question: Can I export to a format that wasn’t originally supported?
  - answer: By rendering each page as a flat image, any hidden text layers are removed,
      making it impossible to extract the original content.
    question: How does rasterization protect redacted data?
  - answer: Absolutely – you can call `Apply` repeatedly or pass a collection of `RedactionOptions`
      to process many patterns in one pass. `RedactionOptions` defines the settings
      for a single redaction operation, such as region and replacement type.
    question: Is it possible to chain multiple redaction rules?
  - answer: The `Redactor` implements `IDisposable`; wrap it in a `using` block or
      call `Dispose()` to release file handles promptly. `IDisposable` is an interface
      that provides a mechanism for releasing unmanaged resources.
    question: Do I need to close the Redactor object?
  - answer: GroupDocs.Redaction is validated on .NET Framework 4.6+, .NET Core 3.1+,
      and .NET 5/6/7.
    question: What .NET runtimes are officially tested?
  type: FAQPage
title: วิธีส่งออกเอกสารที่ถูกทำเครื่องหมายด้วย GroupDocs.Redaction .NET
type: docs
url: /th/net/document-saving/
weight: 3
---

# วิธีส่งออกเอกสารที่ทำการลบข้อมูลด้วย GroupDocs.Redaction .NET

ในคู่มือฉบับครอบคลุมนี้ คุณจะได้ค้นพบ **วิธีการส่งออกที่ทำการลบข้อมูล** อย่างปลอดภัยและมีประสิทธิภาพโดยใช้ GroupDocs.Redaction สำหรับ .NET ไม่ว่าคุณจะต้องการรักษาประเภทไฟล์ต้นฉบับ, ปิดกั้นเอกสารเป็น PDF ที่แปลงเป็นภาพ (rasterized PDF), หรือสตรีมผลลัพธ์โดยตรงในหน่วยความจำ เราจะพาคุณผ่านทุกตัวเลือกด้วยคำอธิบายที่ชัดเจนเป็นกันเองและเคล็ดลับจากโลกจริง เมื่อจบบทเรียนนี้คุณจะสามารถเลือกกลยุทธ์การส่งออกที่เหมาะสมสำหรับสถานการณ์ที่ต้องปฏิบัติตามข้อกำหนดใด ๆ

## คำตอบด่วน
- **รูปแบบใดบ้างที่ฉันสามารถส่งออกได้?** ใด ๆ จากรูปแบบดั้งเดิมกว่า 30 รูปแบบที่ GroupDocs.Redaction รองรับ, รวมถึง rasterized PDF เพื่อความปลอดภัยสูงสุด.  
- **ฉันต้องการใบอนุญาตสำหรับการสตรีมหรือไม่?** ใช่, จำเป็นต้องมีใบอนุญาต GroupDocs.Redaction ที่ถูกต้องสำหรับการสตรีมในสภาพการผลิต.  
- **ฉันสามารถตั้งโฟลเดอร์เอาต์พุตแบบกำหนดเองได้หรือไม่?** แน่นอน – ใช้ property `OutputPath` หรือ `SaveOptions` เพื่อกำหนดค่า.  
- **การแปลงเป็นภาพปลอดภัยสำหรับไฟล์ขนาดใหญ่หรือไม่?** มันจัดการเอกสารได้ถึง 500 หน้าโดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ.  
- **เวอร์ชัน .NET ใดบ้างที่รองรับ?** .NET Framework 4.6+, .NET Core 3.1+, .NET 5/6/7.

## GroupDocs.Redaction คืออะไร?
GroupDocs.Redaction เป็นไลบรารี .NET ที่ทำการลบหรือปกปิดข้อมูลที่ละเอียดอ่อนจาก PDF, Word, Excel, PowerPoint, รูปภาพ, และรูปแบบอื่น ๆ มากมายโดยอัตโนมัติ มันมี API ระดับสูงสำหรับการกำหนดพื้นที่ลบข้อมูล, ใช้นโยบาย, และในที่สุดส่งออกเอกสารที่ทำความสะอาดแล้ว ทำให้การรวมความสามารถในการลบข้อมูลเข้าไปในแอปพลิเคชัน .NET ใด ๆ เป็นเรื่องง่าย.

## ทำไมต้องส่งออกเอกสารที่ลบข้อมูลเป็น Rasterized PDFs?
Rasterized PDFs แปลงทุกหน้ามาเป็นภาพแบน ๆ ทำให้ชั้นข้อความที่ซ่อนอยู่ซึ่งอาจถูกดึงออกในภายหลังหายไป รูปแบบนี้รับประกันว่าเนื้อหาที่ลบข้อมูลจะไม่สามารถกู้คืนได้ ตรงตามมาตรฐานกฎระเบียบที่เข้มงวดเช่น GDPR และ HIPAA GroupDocs.Redaction สามารถสร้าง Rasterized PDFs ได้สูงสุด 300 dpi โดยคงความคมชัดของภาพพร้อมกับความปลอดภัย.

## วิธีการส่งออกเอกสารที่ลบข้อมูล?
โหลดไฟล์ต้นฉบับ, ใช้กฎการลบข้อมูลของคุณ, แล้วเรียกเมธอดการบันทึกที่เหมาะสม—ไม่ว่าจะเป็น `Save` สำหรับรูปแบบดั้งเดิม, `SaveAsRasterizedPdf` สำหรับ PDF ที่เป็นภาพเท่านั้น, หรือ `SaveToStream` สำหรับการจัดการในหน่วยความจำ ด้านล่างเป็นขั้นตอนการทำงานแบบทีละขั้นตอน แต่ละเมธอดรับประกันว่าเนื้อหาที่ลบข้อมูลจะถูกลบอย่างถาวรพร้อมกับคงรูปแบบเอาต์พุตที่ต้องการ.

### ขั้นตอนที่ 1: ติดตั้งแพคเกจ NuGet
เพิ่มแพคเกจ GroupDocs.Redaction เวอร์ชันล่าสุดลงในโปรเจกต์ของคุณ:

```bash
dotnet add package GroupDocs.Redaction
```

### ขั้นตอนที่ 2: โหลดเอกสารและกำหนดการลบข้อมูล
สร้างอินสแตนซ์ `Redactor`, โหลดไฟล์, และระบุพื้นที่ที่คุณต้องการซ่อน คลาส `Redactor` ให้ฟังก์ชันหลักสำหรับการโหลดเอกสารและใช้กฎการลบข้อมูล.

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;

// Load the document
var redactor = Redactor.Create("SensitiveReport.docx");

// Define a redaction for a specific text pattern
redactor.Apply(new RedactionOptions
{
    SearchPattern = "SSN: \\d{3}-\\d{2}-\\d{4}",
    RedactionColor = System.Drawing.Color.Black,
    RedactionType = RedactionType.Image
});
```

### ขั้นตอนที่ 3: เลือกวิธีการส่งออก
#### ส่งออกในรูปแบบดั้งเดิม
```csharp
redactor.Save("RedactedReport.docx");
```

#### ส่งออกเป็น Rasterized PDF
```csharp
var rasterOptions = new RasterizationOptions { Dpi = 300 };
redactor.SaveAsRasterizedPdf("RedactedReport.pdf", rasterOptions);
```

#### ส่งออกเป็น Memory Stream (เหมาะสำหรับ Web API)
```csharp
using var stream = new MemoryStream();
redactor.Save(stream, SaveOptions.CreatePdf());
stream.Position = 0; // Reset for reading
```

เมธอด `Save` จะเขียนเอกสารที่ลบข้อมูลลงไฟล์ในรูปแบบดั้งเดิมของมัน `SaveAsRasterizedPdf` สร้าง PDF ที่แต่ละหน้าถูกเรนเดอร์เป็นภาพ, ลบข้อความที่ซ่อนอยู่ทั้งหมด `SaveToStream` คืนค่าไฟล์ที่ลบข้อมูลเป็น memory stream, เหมาะสำหรับการตอบสนองเว็บ.

## วิธีการกำหนดค่าโฟลเดอร์เอาต์พุต?
ตั้งค่า property `OutputPath` บน `Redactor` หรือส่งออบเจ็กต์ `SaveOptions` ที่กำหนดเองซึ่งรวมถึงไดเรกทอรีที่ต้องการ `OutputPath` เป็น property ของ `Redactor` ที่ระบุไดเรกทอรีที่ไฟล์เอาต์พุตจะถูกเขียน `SaveOptions` ให้คุณปรับแต่งพารามิเตอร์การบันทึกต่าง ๆ รวมถึงโฟลเดอร์เอาต์พุต สิ่งนี้ทำให้ไฟล์ที่ส่งออกทั้งหมดไปยังตำแหน่งที่คาดเดาได้ง่ายขึ้น, ทำให้กระบวนการประมวลผลแบบชุดง่ายขึ้น คุณยังสามารถระบุโฟลเดอร์ย่อยตามประเภทเอกสารเพื่อให้พื้นที่ทำงานของคุณเป็นระเบียบ.

```csharp
var options = SaveOptions.CreatePdf();
options.OutputPath = @"C:\RedactedOutputs\";
redactor.Save(options);
```

## ปัญหาทั่วไปและวิธีแก้
- **การลบข้อมูลไม่ทำงาน:** ตรวจสอบว่าแพทเทิร์นการค้นหาแม่นยำตรงกับข้อความในเอกสาร; ใช้ `RegexOptions.IgnoreCase` หากจำเป็น `RegexOptions` เป็น enumeration ที่ควบคุมพฤติกรรมการจับคู่ regular expression เช่น ความไวต่อขนาดตัวอักษร.  
- **ไฟล์ขนาดใหญ่ทำให้หน่วยความจำอัดแน่น:** เปิดโหมดสตรีมโดยใช้ `SaveToStream` และหลีกเลี่ยงการเรียก `Save` กับเอกสารทั้งหมด.  
- **Rasterized PDF ดูเบลอ:** เพิ่ม DPI ใน `RasterizationOptions` (เช่น 300–600) เพื่อปรับปรุงคุณภาพภาพ `RasterizationOptions` ให้คุณตั้งค่าพารามิเตอร์เช่น DPI และรูปแบบภาพสำหรับเอาต์พุต Rasterized PDF.

## คำถามที่พบบ่อย

**Q: ฉันสามารถส่งออกเป็นรูปแบบที่ไม่ได้รับการสนับสนุนเดิมได้หรือไม่?**  
A: ใช่, GroupDocs.Redaction สามารถแปลงประเภทอินพุตส่วนใหญ่เป็น PDF, DOCX, XLSX, PPTX, หรือ rasterized PDF, ครอบคลุมกว่า 30 รูปแบบ.

**Q: การแปลงเป็นภาพช่วยปกป้องข้อมูลที่ลบอย่างไร?**  
A: โดยการเรนเดอร์แต่ละหน้าเป็นภาพแบน ๆ ชั้นข้อความที่ซ่อนอยู่จะถูกลบ ทำให้ไม่สามารถดึงข้อมูลเดิมออกมาได้.

**Q: สามารถเชื่อมต่อหลายกฎการลบข้อมูลได้หรือไม่?**  
A: แน่นอน – คุณสามารถเรียก `Apply` ซ้ำหลายครั้งหรือส่งคอลเลกชันของ `RedactionOptions` เพื่อประมวลผลหลายแพทเทิร์นในหนึ่งรอบ `RedactionOptions` กำหนดการตั้งค่าสำหรับการลบข้อมูลแต่ละครั้ง เช่น พื้นที่และประเภทการแทนที่.

**Q: จำเป็นต้องปิดออบเจ็กต์ Redactor หรือไม่?**  
A: `Redactor` implements `IDisposable`; ให้ห่อไว้ในบล็อก `using` หรือเรียก `Dispose()` เพื่อปล่อยไฟล์แฮนด์เดิลโดยเร็ว `IDisposable` เป็น interface ที่ให้กลไกการปล่อยทรัพยากรที่ไม่ได้จัดการ.

**Q: .NET runtime ใดที่ผ่านการทดสอบอย่างเป็นทางการ?**  
A: GroupDocs.Redaction ได้รับการตรวจสอบบน .NET Framework 4.6+, .NET Core 3.1+, และ .NET 5/6/7.

## แหล่งข้อมูลเพิ่มเติม

### บทเรียนที่มีให้

- [วิธีบันทึกเอกสารเป็น Rasterized PDFs ด้วย GroupDocs.Redaction สำหรับ .NET: คู่มือฉบับสมบูรณ์](./groupdocs-redaction-net-rasterized-pdfs/)
- [การใช้งานโฟลเดอร์เอาต์พุตใน .NET กับ GroupDocs.Redaction: คู่มือเชิงลึก](./implement-output-directory-groupdocs-redaction-dotnet/)
- [ลบข้อมูลและบันทึกเอกสารด้วย GroupDocs.Redaction สำหรับ .NET: คู่มือฉบับสมบูรณ์](./redact-save-documents-groupdocs-redaction-net/)
- [บันทึกเอกสารที่ลบข้อมูลในรูปแบบดั้งเดิมโดยใช้ GroupDocs.Redaction .NET](./save-redacted-docs-original-format-groupdocs-redaction-net/)
- [การลบข้อมูลเอกสารอย่างปลอดภัยใน .NET ด้วย Streams: คู่มือสำหรับ GroupDocs.Redaction](./secure-document-redaction-net-streams-groupdocs-redaction/)

### ลิงก์ที่เป็นประโยชน์

- [เอกสาร GroupDocs.Redaction สำหรับ .NET](https://docs.groupdocs.com/redaction/net/)
- [อ้างอิง API ของ GroupDocs.Redaction สำหรับ .NET](https://reference.groupdocs.com/redaction/net/)
- [ดาวน์โหลด GroupDocs.Redaction สำหรับ .NET](https://releases.groupdocs.com/redaction/net/)
- [ฟอรั่ม GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [สนับสนุนฟรี](https://forum.groupdocs.com/)
- [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)

---

**อัปเดตล่าสุด:** 2026-06-11  
**ทดสอบด้วย:** GroupDocs.Redaction 23.11 for .NET  
**ผู้เขียน:** GroupDocs  

## บทเรียนที่เกี่ยวข้อง

- [บันทึกเอกสารที่ลบข้อมูลในรูปแบบดั้งเดิมโดยใช้ GroupDocs.Redaction .NET](/redaction/net/document-saving/save-redacted-docs-original-format-groupdocs-redaction-net/)
- [วิธีบันทึกเอกสารเป็น Rasterized PDFs ด้วย GroupDocs.Redaction สำหรับ .NET: คู่มือฉบับสมบูรณ์](/redaction/net/document-saving/groupdocs-redaction-net-rasterized-pdfs/)
- [การลบข้อมูลเอกสารอย่างปลอดภัยใน .NET ด้วย Streams: คู่มือสำหรับ GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)