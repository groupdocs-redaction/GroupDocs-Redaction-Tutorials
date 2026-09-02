---
date: '2026-06-01'
description: เรียนรู้วิธีลบข้อความที่ตรงกันแบบ .NET ด้วย GroupDocs.Redaction รวมถึงรูปแบบ
  regex การลบ annotation และการลบ metadata เพื่อความปลอดภัยของเอกสาร
keywords:
- redact exact phrase .net
- document security
- GroupDocs Redaction
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to redact exact phrase .NET using GroupDocs.Redaction, covering
    regex patterns, annotation removal, and metadata erasure for secure documents.
  headline: Redact exact phrase .NET with GroupDocs.Redaction – Guide
  type: TechArticle
- description: Learn how to redact exact phrase .NET using GroupDocs.Redaction, covering
    regex patterns, annotation removal, and metadata erasure for secure documents.
  name: Redact exact phrase .NET with GroupDocs.Redaction – Guide
  steps:
  - name: Initialise the Redactor
    text: Redactor is the core class that loads a document and manages redaction operations.
  - name: Define the Exact Phrase Redaction
    text: ExactPhraseRedaction specifies a literal string to be removed and the replacement
      to use.
  - name: Apply and Save the Document
    text: After adding the redaction, call `Redactor.Save()` to write the redacted
      file to disk.
  - name: First Regex Pattern
    text: RegexRedaction defines a regular‑expression pattern to locate sensitive
      data.
  - name: Apply and Save
    text: Add the regex redaction to the redactor and persist the changes.
  - name: Second Regex Pattern
    text: Define another pattern, for example, a 16‑digit credit‑card format (`\b\d{4}
      \d{4} \d{4} \d{4}\b`). Apply it the same way and save the document.
  - name: Create Delete Annotation Redaction
    text: DeleteAnnotationRedaction is a redaction type that targets and removes all
      annotation objects.
  - name: Apply and Save
    text: Add the redaction to the redactor and call `Save()`.
  - name: Initialise Erase Metadata Redaction
    text: EraseMetadataRedaction creates a redaction that clears every metadata property
      from the document.
  - name: Apply and Save
    text: Add it to the redactor pipeline and persist the cleaned file.
  type: HowTo
- questions:
  - answer: It’s widely adopted in legal, medical, and financial sectors to automatically
      hide personally identifiable information and confidential business data.
    question: What are common uses for GroupDocs.Redaction?
  - answer: Yes—GroupDocs.Redaction supports PDF, DOCX, PPTX, XLSX, HTML, and many
      image formats.
    question: Can I redact PDF files as well?
  - answer: Inspect the `RedactorChangeLog` after each operation; it lists any failures
      and the exact locations where redactions could not be applied.
    question: How do I handle errors during redaction?
  - answer: There’s no hard limit, but for very large documents you should monitor
      memory usage and consider processing the file in chunks.
    question: Is there a limit to the number of phrases I can redact?
  - answer: Absolutely—its .NET API can be called from web services, background workers,
      or any .NET‑compatible workflow engine.
    question: Can GroupDocs.Redaction be integrated with other systems?
  type: FAQPage
title: ลบข้อความที่ตรงกันแบบ .NET ด้วย GroupDocs.Redaction – คู่มือ
type: docs
url: /th/net/advanced-redaction/groupdocs-redaction-net-document-security-guide/
weight: 1
---

# ลบข้อความที่ตรงกันอย่างแม่นยำใน .NET ด้วย GroupDocs.Redaction – คู่มือ

## บทนำ

ในโลกที่ขับเคลื่อนด้วยข้อมูลในปัจจุบัน, **redact exact phrase .NET** เป็นความสามารถที่สำคัญสำหรับองค์กรใด ๆ ที่จัดการข้อมูลลับ ไม่ว่าคุณจะเป็นสำนักงานกฎหมาย, สถาบันการเงิน, หรือผู้ให้บริการด้านสุขภาพ การลบข้อความที่ละเอียดอ่อน, คำอธิบาย, และเมตาดาต้าที่ซ่อนอยู่ช่วยให้คุณปฏิบัติตามกฎระเบียบเช่น GDPR, HIPAA, และ PCI‑DSS ได้อย่างสอดคล้อง คู่มือฉบับนี้จะพาคุณผ่านขั้นตอนการทำงานทั้งหมดของการใช้ GroupDocs.Redaction สำหรับ .NET เพื่อปกปิดวลีที่ตรงกัน, ใช้รูปแบบ regex ที่ทรงพลัง, ลบคำอธิบาย, และลบเมตาดาต้า — ทั้งหมดนี้โดยยังคงประสิทธิภาพสูงและโค้ดที่สะอาด

**สิ่งที่คุณจะเชี่ยวชาญ**
- วิธีลบข้อความที่ตรงกันอย่างแม่นยำใน .NET ด้วยเพียงไม่กี่บรรทัดของ C#
- การใช้ regular expressions สำหรับการลบตามรูปแบบ
- การลบคำอธิบายที่อาจเปิดเผยรายละเอียดที่ซ่อนอยู่
- การลบเมตาดาต้าเอกสารทั้งหมดเพื่อปกป้องแหล่งที่มาของเอกสาร
- เคล็ดลับแนวทางปฏิบัติที่ดีที่สุดสำหรับการประมวลผลแบบกลุ่มและการจัดการหน่วยความจำ  

ด้านล่างนี้เรารายการข้อกำหนดเบื้องต้นที่คุณต้องมีก่อนเริ่มต้น

### ข้อกำหนดเบื้องต้น

#### ไลบรารีและเวอร์ชันที่ต้องการ
- **GroupDocs.Redaction for .NET** – รับแพ็กเกจล่าสุดจาก [NuGet](https://www.nuget.org/packages/GroupDocs.Redaction).

#### ข้อกำหนดการตั้งค่าสภาพแวดล้อม
- Visual Studio 2019 หรือใหม่กว่า
- โครงการ .NET Framework (4.6.1+) หรือ .NET Core/5/6

#### ข้อกำหนดความรู้เบื้องต้น
- การเขียนโปรแกรม C# เบื้องต้น
- ความคุ้นเคยกับไวยากรณ์ regular‑expression
- ความเข้าใจในแนวคิดการแก้ไขเอกสาร (หน้า, ชั้น, เมตาดาต้า)

## คำตอบอย่างรวดเร็ว
- **วิธีลบวลี?** Call `Redactor.AddRedaction(new ExactPhraseRedaction("secret"))` and save.
- **Can I use regex?** Yes—create a `RegexRedaction` with your pattern and add it to the redactor.
- **Do annotations get removed automatically?** No, you need a `DeleteAnnotationRedaction` instance.
- **Will metadata be stripped?** Use `EraseMetadataRedaction` to wipe all embedded properties.
- **Is batch processing supported?** Yes—instantiate a redactor per file inside a loop and dispose promptly.

## redact exact phrase .NET คืออะไร?
วลี **redact exact phrase .NET** หมายถึงกระบวนการค้นหาสตริงตัวอักษรตรงในเอกสารโดยอัตโนมัติและแทนที่ด้วยตัวแทนหรือการบังสีโดยใช้ไลบรารี .NET GroupDocs.Redaction มี API เฉพาะที่ทำให้การดำเนินการนี้ง่าย เชื่อถือได้ และไม่ขึ้นกับรูปแบบไฟล์

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับการลบวลี?
GroupDocs.Redaction รองรับ **50+** รูปแบบไฟล์เข้าและออก (PDF, DOCX, PPTX, XLSX, HTML, รูปภาพ ฯลฯ) และสามารถประมวลผลไฟล์หลาย‑ร้อยหน้าโดยไม่ต้องโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ เครื่องมือ OCR ในตัวสามารถตรวจจับข้อความที่ซ่อนอยู่ และเอนจินการลบของมันรับประกันว่าข้อมูลที่ถูกลบจะไม่สามารถกู้คืนได้ ด้วยความแม่นยำการทำความสะอาดข้อมูล 99.9 % ในสภาพแวดล้อมที่ต้องการการปฏิบัติตามกฎระเบียบ

## วิธีลบข้อความที่ตรงกันอย่างแม่นยำใน .NET?
โหลดไฟล์ต้นฉบับ, สร้างอินสแตนซ์ `Redactor`, เพิ่ม `ExactPhraseRedaction` สำหรับสตริงเป้าหมาย, แล้วบันทึกผลลัพธ์ กระบวนการแบบ End‑to‑End นี้ทำเสร็จในสามขั้นตอนสั้น ๆ และทำให้วลีถูกลบอย่างถาวรจากทุกหน้า

### ขั้นตอน 1: Initialise the Redactor  
Redactor เป็นคลาสหลักที่โหลดเอกสารและจัดการการดำเนินการลบ  

```bash
dotnet add package GroupDocs.Redaction
```

### ขั้นตอน 2: Define the Exact Phrase Redaction  
ExactPhraseRedaction ระบุสตริงตัวอักษรที่ต้องการลบและข้อความแทนที่ที่จะใช้  

```powershell
Install-Package GroupDocs.Redaction
```

### ขั้นตอน 3: Apply and Save the Document  
หลังจากเพิ่มการลบแล้ว, เรียก `Redactor.Save()` เพื่อเขียนไฟล์ที่ลบแล้วลงดิสก์  

```csharp
using GroupDocs.Redaction;
```

## วิธีใช้ regex redaction ใน .NET?
Regex redaction ช่วยให้คุณกำหนดรูปแบบเช่นหมายเลขบัตรเครดิต, SSN, หรือรหัสที่กำหนดเอง กำหนด `RegexRedaction` ด้วยรูปแบบที่ต้องการ, สามารถระบุสตริงแทนที่, เพิ่มลงใน `Redactor`, แล้วบันทึก

### ขั้นตอน 1: รูปแบบ Regex แรก  
RegexRedaction กำหนดรูปแบบ regular‑expression เพื่อค้นหาข้อมูลที่ละเอียดอ่อน  

```csharp
using (Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY\\sample.docx"))
{
    // Proceed with redaction steps here.
}
```

### ขั้นตอน 2: ใช้และบันทึก  
เพิ่ม regex redaction ลงใน redactor และบันทึกการเปลี่ยนแปลง  

```csharp
var exactPhraseRedaction = new ExactPhraseRedaction("John Doe", new ReplacementOptions("[Client]"));
RedactorChangeLog result = redactor.Apply(exactPhraseRedaction);
```

### ขั้นตอน 3: รูปแบบ Regex ที่สอง  
กำหนดรูปแบบอื่น, ตัวอย่างเช่นรูปแบบบัตรเครดิต 16 หลัก (`\b\d{4} \d{4} \d{4} \d{4}\b`)  

```csharp
if (result.Status == RedactionStatus.Applied)
{
    redactor.Save("YOUR_OUTPUT_DIRECTORY\\redacted.docx");
}
```

ใช้วิธีเดียวกันและบันทึกเอกสาร  

```csharp
var regexRedaction1 = new RegexRedaction("Redaction", new ReplacementOptions("[Product]"));
```

## วิธีลบคำอธิบายใน .NET?
คำอธิบาย (คอมเมนต์, ไฮไลท์, สแตมป์) อาจมีโน้ตที่เป็นความลับ `DeleteAnnotationRedaction` จะลบวัตถุคำอธิบายทั้งหมดจากเอกสาร, เหลือเพียงเนื้อหาต้นฉบับ การดำเนินการนี้ทำให้ไม่มีหมายเหตุที่ซ่อนอยู่เหลืออยู่ที่อาจเปิดเผยข้อมูลสำคัญ และทำงานได้กับทุกประเภทไฟล์ที่รองรับโดยไม่เปลี่ยนแปลงเลย์เอาต์ภาพของเอกสารที่เหลือ

### ขั้นตอน 1: สร้าง Delete Annotation Redaction  
DeleteAnnotationRedaction เป็นประเภทการลบที่มุ่งเป้าและลบวัตถุคำอธิบายทั้งหมด  

```csharp
RedactorChangeLog result1 = redactor.Apply(regexRedaction1);
if (result1.Status == RedactionStatus.Applied)
{
    redactor.Save("YOUR_OUTPUT_DIRECTORY\\redacted1.docx");
}
```

### ขั้นตอน 2: ใช้และบันทึก  
เพิ่มการลบลงใน redactor แล้วเรียก `Save()`  

```csharp
var regexRedaction2 = new RegexRedaction(\d{2}\s*\d{6}, new ReplacementOptions(Color.Blue));
```

## วิธีลบเมตาดาต้าใน .NET?
เมตาดาต้ามักเปิดเผยผู้เขียน, วันที่สร้าง, หรือซอฟต์แวร์ที่ใช้แก้ไข `EraseMetadataRedaction` จะลบ **ทั้งหมด** ของฟิลด์เมตาดาต้า, ทำให้ไม่สามารถติดตามแหล่งที่มาของเอกสารได้ การลบเมตาดาต้าช่วยป้องกันการเปิดเผยโดยบังเอิญของรายละเอียดกระบวนการทำงานภายในและสอดคล้องกับมาตรฐานความเป็นส่วนตัวที่ต้องการการทำความสะอาดเมตาดาต้าก่อนการแจกจ่าย

### ขั้นตอน 1: Initialise Erase Metadata Redaction  
EraseMetadataRedaction สร้างการลบที่ล้างคุณสมบัติเมตาดาต้าทั้งหมดจากเอกสาร  

```csharp
var deleteAnnotationRedaction = new DeleteAnnotationRedaction();
```

### ขั้นตอน 2: ใช้และบันทึก  
เพิ่มลงใน pipeline ของ redactor และบันทึกไฟล์ที่ทำความสะอาดแล้ว  

```csharp
RedactorChangeLog result = redactor.Apply(deleteAnnotationRedaction);
if (result.Status == RedactionStatus.Applied)
{
    redactor.Save("YOUR_OUTPUT_DIRECTORY\\annotations_removed.docx");
}
```

## การประยุกต์ใช้งานจริง

GroupDocs.Redaction มีประสิทธิภาพในหลายสถานการณ์จริง:

1. **การประมวลผลเอกสารทางกฎหมาย** – ปกปิดชื่อลูกค้า, หมายเลขคดี, หรือภาษาที่เป็นสิทธิพิเศษก่อนแชร์ร่างให้ฝ่ายตรงข้าม
2. **การรายงานทางการเงิน** – ลบหมายเลขบัตรเครดิต, IBAN, หรือรหัสภาษีเพื่อให้เป็นไปตามข้อกำหนด PCI‑DSS และ GDPR
3. **การจัดการบันทึกการแพทย์** – ลบตัวระบุผู้ป่วย (HIPAA Safe Harbor) พร้อมคงเนื้อหาทางคลินิก
4. **การตรวจสอบการปฏิบัติตามภายใน** – ลบเมตาดาต้าที่อาจเปิดเผยเวลาสร้างเอกสารหรือรายละเอียดผู้เขียน

## ข้อควรพิจารณาด้านประสิทธิภาพ

เพื่อให้โซลูชันของคุณเร็วและใช้ทรัพยากรอย่างมีประสิทธิภาพ:

- **การประมวลผลแบบกลุ่ม** – วนลูปผ่านชุดไฟล์, ใช้ `Redactor` ตัวเดียวซ้ำเมื่อเป็นไปได้
- **การจัดการหน่วยความจำ** – เรียก `Redactor.Dispose()` หรือห่อ Redactor ด้วยบล็อก `using` เพื่อปล่อยทรัพยากรที่ไม่ได้จัดการโดยเร็ว
- **การลบที่เลือกเฉพาะ** – เพิ่มการลบเฉพาะที่จำเป็น; รูปแบบที่ไม่จำเป็นเพิ่มการใช้ CPU

## สรุป

คุณได้เรียนรู้วิธี **redact exact phrase .NET** ด้วย GroupDocs.Redaction แล้ว ตั้งแต่การแทนที่แบบตัวอักษรตรงไปจนถึง regex ขั้นสูง, การลบคำอธิบาย, และการลบเมตาดาต้า ด้วยการทำตามรูปแบบข้างต้น คุณสามารถสร้าง pipeline การประมวลผลเอกสารที่ปลอดภัย, ปฏิบัติตามกฎระเบียบ, และสามารถขยายจากการดำเนินการไฟล์เดี่ยวไปจนถึงงานแบตช์ขนาดใหญ่ได้

**ขั้นตอนต่อไป**
- ค้นคว้าเพิ่มเติมใน [GroupDocs documentation](https://docs.groupdocs.com/redaction/net/) อย่างเป็นทางการ
- ทดลองใช้สตริงแทนที่แบบกำหนดเองและสไตล์การลบแบบภาพ
- แบ่งปันคำถามการใช้งานของคุณใน [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)

## ส่วนคำถามที่พบบ่อย

**Q: การใช้งานทั่วไปของ GroupDocs.Redaction มีอะไรบ้าง?**  
A: มันถูกนำไปใช้อย่างกว้างขวางในภาคกฎหมาย, การแพทย์, และการเงินเพื่อซ่อนข้อมูลส่วนบุคคลที่ระบุตัวตนและข้อมูลธุรกิจที่เป็นความลับโดยอัตโนมัติ

**Q: ฉันสามารถลบไฟล์ PDF ได้ด้วยหรือไม่?**  
A: ได้—GroupDocs.Redaction รองรับ PDF, DOCX, PPTX, XLSX, HTML, และรูปภาพหลายรูปแบบ

**Q: ฉันจะจัดการกับข้อผิดพลาดระหว่างการลบอย่างไร?**  
A: ตรวจสอบ `RedactorChangeLog` หลังจากแต่ละการดำเนินการ; มันจะแสดงรายการความล้มเหลวและตำแหน่งที่การลบไม่สามารถทำได้

**Q: มีขีดจำกัดจำนวนวลีที่ฉันสามารถลบได้หรือไม่?**  
A: ไม่มีขีดจำกัดที่แน่นอน, แต่สำหรับเอกสารขนาดใหญ่มากคุณควรตรวจสอบการใช้หน่วยความจำและพิจารณาประมวลผลไฟล์เป็นส่วน ๆ

**Q: GroupDocs.Redaction สามารถผสานรวมกับระบบอื่นได้หรือไม่?**  
A: แน่นอน—API .NET ของมันสามารถเรียกจากเว็บเซอร์วิส, เวิร์กเกอร์พื้นหลัง, หรือเครื่องยนต์ workflow ที่เข้ากันได้กับ .NET ใด ๆ

**Q: ฉันจะหาลิขสิทธิ์ชั่วคราวสำหรับการทดสอบได้จากที่ไหน?**  
A: คุณสามารถรับ [temporary license](https://purchase.groupdocs.com/temporary-license/) จาก GroupDocs หรือดูรายละเอียดใน [GroupDocs documentation](https://docs.groupdocs.com/redaction/net/) สำหรับการสนับสนุนชุมชน, เยี่ยมชม [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)

## แหล่งข้อมูล

- **Documentation:** [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/net/)
- **API Reference:** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **Download:** [Latest Releases](https://releases.groupdocs.com/redaction/net/)
- **Free Support:** [GroupDocs Forum](https://forum.groupdocs.com/c/redaction/33)
- **Temporary License:** [Obtain a Temporary License](https://purchase.groupdocs.com/temporary-license/) 

---

**อัปเดตล่าสุด:** 2026-06-01  
**ทดสอบด้วย:** GroupDocs.Redaction 5.0 for .NET (latest at time of writing)  
**ผู้เขียน:** GroupDocs

```csharp
var eraseMetadataRedaction = new EraseMetadataRedaction(MetadataFilters.All);
```

```csharp
RedactorChangeLog result = redactor.Apply(eraseMetadataRedaction);
if (result.Status == RedactionStatus.Applied)
{
    redactor.Save("YOUR_OUTPUT_DIRECTORY\\metadata_erased.docx");
}
```

## บทแนะนำที่เกี่ยวข้อง

- [Master Case-Sensitive Exact Phrase Redaction with GroupDocs.Redaction .NET for Document Security](/redaction/net/text-redaction/groupdocs-redaction-net-case-sensitive-exact-phrase-redaction/)
- [Redact Content Using Regex in .NET with GroupDocs.Redaction: A Comprehensive Guide](/redaction/net/text-redaction/redact-content-regex-groupdocs-redaction-net/)
- [How to Load and Redact Documents Using GroupDocs.Redaction .NET: A Complete Guide](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)