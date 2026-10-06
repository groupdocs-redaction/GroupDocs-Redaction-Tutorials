---
date: '2026-10-06'
description: เรียนรู้วิธีลบข้อมูลที่ละเอียดอ่อนด้วย GroupDocs.Redaction .NET คู่มือขั้นตอนต่อขั้นตอนนี้จะแสดงวิธีสร้าง
  ใช้ และบันทึกนโยบายการลบเป็น XML
keywords:
- redact sensitive data
- mask confidential information
- groupdocs redaction .net
lastmod: '2026-10-06'
og_description: เรียนรู้วิธีลบข้อมูลที่ละเอียดอ่อนด้วย GroupDocs.Redaction .NET คู่มือขั้นตอนต่อขั้นตอนนี้จะแสดงวิธีสร้าง
  ใช้ และบันทึกนโยบายการลบเป็น XML
og_image_alt: Tutorial showing how to redact sensitive data in documents with GroupDocs.Redaction
  for .NET
og_title: วิธีลบข้อมูลที่ละเอียดอ่อนโดยใช้ GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-06'
  description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  headline: How to redact sensitive data using GroupDocs.Redaction .NET
  type: TechArticle
- description: Learn how to redact sensitive data with GroupDocs.Redaction .NET. This
    step‑by‑step guide shows you how to create, apply, and save a redaction policy
    as XML.
  name: How to redact sensitive data using GroupDocs.Redaction .NET
  steps:
  - name: prepare your document directory
    text: '*Replace `"YOUR_DOCUMENT_DIRECTORY"` with the folder that holds the documents
      you want to protect.*'
  - name: load the document
    text: The `Redactor` object opens the file and manages its lifecycle.
  - name: define the redactions
    text: 'ExactPhraseRedaction defines a rule that replaces a specific phrase, while
      `RegexRedaction` uses a regular expression to match patterns. Here we create
      two rules: 1. **ExactPhraseRedaction** – replaces a known phrase with “[REDACTED]”.
      2. **RegexRedaction** – finds dates in `YYYY‑MM‑DD` format and r'
  - name: apply the redactions
    text: All defined rules are executed against the opened document in one pass.
  - name: save the policy as an XML file
    text: The XML file stores the redaction definitions, allowing you to reuse the
      same policy without rewriting code.
  type: HowTo
- questions:
  - answer: Yes—use `redactor.LoadPolicy("policy.xml")` to import a previously saved
      policy.
    question: Can I load an existing XML policy instead of building one programmatically?
  - answer: 'Absolutely. Pass the password to the `Redactor` constructor: `new Redactor(sourceFile,
      "password")`.'
    question: Does GroupDocs.Redaction support password‑protected PDFs?
  - answer: The SDK provides `ImageRedaction` and `MetadataRedaction` classes for
      those scenarios.
    question: Is it possible to redact images or metadata?
  - answer: Process them in chunks or use the streaming API to reduce memory footprint;
      the engine can handle files up to 2 GB without loading the whole file into RAM.
    question: How do I handle large documents (hundreds of MB)?
  - answer: A paid license is required for production deployments; a trial license
      is fine for development and testing.
    question: What licensing model is required for commercial use?
  type: FAQPage
tags:
- redact sensitive data
- groupdocs redaction
- .net document security
- xml policy
- document redaction
title: วิธีลบข้อมูลที่ละเอียดอ่อนโดยใช้ GroupDocs.Redaction .NET
type: docs
url: /th/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# วิธีลบข้อมูลที่ละเอียดอ่อนโดยใช้ GroupDocs.Redaction .NET

การปกป้องข้อมูลลับภายในสัญญา, งบการเงิน, หรือบันทึกผู้ป่วยเป็นข้อกำหนดที่ไม่อาจต่อรองได้สำหรับแอปพลิเคชันสมัยใหม่ ในคู่มือนี้คุณจะได้เรียนรู้ **วิธีลบข้อมูลที่ละเอียดอ่อน** ด้วย GroupDocs.Redaction สำหรับ .NET ตั้งแต่การติดตั้ง SDK จนถึงการกำหนดนโยบาย XML ที่สามารถนำกลับมาใช้ใหม่ได้และสามารถใช้กับเอกสารประเภทใดก็ได้

## คำตอบด่วน
- **“create redaction policy” หมายถึงอะไร?** เป็นกระบวนการกำหนดกฎ (ข้อความ, regex, รูปภาพ, ฯลฯ) ที่บอกให้ GroupDocs.Redaction ซ่อนหรือแทนที่เนื้อหาลับ.  
- **ต้องใช้ไลบรารีอะไร?** GroupDocs.Redaction สำหรับ .NET, มีให้ดาวน์โหลดผ่าน NuGet.  
- **ต้องการใบอนุญาตหรือไม่?** การทดลองใช้ฟรีสามารถใช้งานได้สำหรับการพัฒนา; จำเป็นต้องมีใบอนุญาตถาวรสำหรับการใช้งานจริง.  
- **ฉันสามารถใช้ซ้ำนโยบายได้หรือไม่?** ได้—เมื่อบันทึกเป็น XML แล้วคุณสามารถโหลดในภายหลังและใช้กับเอกสารใดก็ได้.  
- **เวอร์ชัน .NET ที่รองรับคืออะไร?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## นโยบายการลบข้อมูลคืออะไร?

นโยบายการลบข้อมูลคือชุดของกฎที่ระบุ *อะไร* ควรถูกลบหรือแทนที่และ *อย่างไร* การแทนที่จะต้องเป็นอย่างไร โดยการสร้างนโยบายเพียงครั้งเดียว คุณสามารถใช้มาตรฐานความปลอดภัยที่สอดคล้องกันกับทุกเอกสารที่แอปพลิเคชันของคุณประมวลผล

## นโยบายการลบข้อมูลทำงานอย่างไร?

โหลดเอกสารด้วยเครื่องยนต์ `Redactor` แล้วแนบกฎการลบข้อมูลหนึ่งหรือหลายกฎ จากนั้นเรียก `Apply` เครื่องยนต์จะสแกนเอกสาร, ปกปิดเนื้อหาที่ตรงกัน, และอาจส่งออกไฟล์ใหม่ ชุดกฎเดียวกันสามารถส่งออกเป็น XML ทำให้คุณสามารถใช้ซ้ำนโยบายโดยไม่ต้องคอมไพล์โค้ดใหม่

## ทำไมต้องใช้ GroupDocs.Redaction เพื่อสร้างนโยบายการลบข้อมูล?

GroupDocs.Redaction มีชุดคุณสมบัติที่ครอบคลุมซึ่งทำให้การสร้าง, การจัดการ, และการดำเนินการของนโยบายการลบข้อมูลง่ายขึ้น, รับประกันการปกป้องข้อมูลที่สอดคล้องกันในหลายประเภทเอกสาร พร้อมประสิทธิภาพสูงและการผสานรวมที่ง่ายในแอปพลิเคชัน .NET ที่มีอยู่สำหรับทีมและองค์กร

- **รองรับหลายรูปแบบ** – SDK รองรับไฟล์กว่า 30 ประเภท รวมถึง PDF, DOCX, XLSX, PPTX, และรูปแบบภาพ, และสามารถประมวลผลไฟล์ขนาดสูงสุด 2 GB โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ.  
- **ความแม่นยำเชิงโปรแกรม** – กำหนดวลีที่ตรงกัน, regular expressions, หรือตรรกะที่กำหนดเองเพื่อมุ่งเป้าเฉพาะข้อมูลที่ต้องการซ่อน.  
- **นโยบาย XML ที่นำกลับมาใช้ได้** – ส่งออกกฎของคุณครั้งเดียวและแชร์ให้กับทีม, เซอร์วิส, หรือ micro‑services.  
- **เครื่องยนต์ที่ปรับประสิทธิภาพการทำงาน** – ไลบรารีประมวลผลเอกสารหลายร้อยหน้าในเวลาน้อยกว่า 1 วินาทีบนฮาร์ดแวร์เซิร์ฟเวอร์ทั่วไป ทำให้เหมาะกับ pipeline ที่ต้องการ throughput สูง.

## ข้อกำหนดเบื้องต้น
- ไลบรารี GroupDocs.Redaction ที่เข้ากันได้กับ .NET runtime ของคุณ.  
- Visual Studio, VS Code, หรือ IDE ใด ๆ ที่รองรับ C#.  
- ความคุ้นเคยพื้นฐานกับ C# และโครงสร้างโปรเจกต์ .NET.

## การตั้งค่า GroupDocs.Redaction สำหรับ .NET

ขั้นแรก, เพิ่มไลบรารีลงในโปรเจกต์ของคุณ.

**ใช้ .NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```  

**ใช้ Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```  

หรือค้นหา “GroupDocs.Redaction” ใน UI ของ NuGet Package Manager แล้วติดตั้งจากที่นั่น.

### การรับใบอนุญาต
- เริ่มต้นด้วย **free trial** เพื่อสำรวจคุณลักษณะ.  
- ขอ **temporary license** สำหรับการทดสอบต่อเนื่อง, จากนั้นซื้อใบอนุญาตเต็มรูปแบบสำหรับการใช้งานจริง.

### การเริ่มต้นพื้นฐาน
เพิ่ม namespace ลงในไฟล์ซอร์สของคุณ:

คลาส `Redactor` เป็นเครื่องยนต์หลักที่โหลดเอกสารและใช้กฎการลบข้อมูล.  
```csharp
using GroupDocs.Redaction;
```  

คลาส `Redactor` เป็นเครื่องยนต์หลักของ GroupDocs.Redaction ที่โหลดเอกสารและใช้กฎการลบข้อมูล.

## วิธีสร้างนโยบายการลบข้อมูลแบบทีละขั้นตอน

ด้านล่างเป็นขั้นตอนการสาธิตเต็มรูปแบบที่แสดงวิธีสร้างนโยบายการลบข้อมูลแบบเชิงโปรแกรม, กำหนดค่ากฎ, ใช้กับเอกสาร, และสุดท้ายบันทึกนโยบายเป็นไฟล์ XML เพื่อใช้ในอนาคต, รับประกันการลบข้อมูลที่สอดคล้องกันในหลายโครงการและประเภทเอกสาร.

### ขั้นตอน 1: เตรียมไดเรกทอรีเอกสารของคุณ
```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
```  
*แทนที่ `"YOUR_DOCUMENT_DIRECTORY"` ด้วยโฟลเดอร์ที่เก็บเอกสารที่คุณต้องการปกป้อง.*

### ขั้นตอน 2: โหลดเอกสาร
```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Further code will go here
}
```  
อ็อบเจ็กต์ `Redactor` เปิดไฟล์และจัดการวงจรชีวิตของมัน.

### ขั้นตอน 3: กำหนดการลบข้อมูล
ExactPhraseRedaction กำหนดกฎที่แทนที่วลีเฉพาะ, ในขณะที่ `RegexRedaction` ใช้ regular expression เพื่อจับรูปแบบ.  
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```  
ที่นี่เราสร้างสองกฎ:
1. **ExactPhraseRedaction** – แทนที่วลีที่รู้จักด้วย “[REDACTED]”.  
2. **RegexRedaction** – ค้นหาวันที่ในรูปแบบ `YYYY‑MM‑DD` และแทนที่ด้วย “[DATE REDACTED]”.

### ขั้นตอน 4: ใช้การลบข้อมูล
```csharp
redactor.Apply(redactions);
```  
กฎทั้งหมดที่กำหนดจะถูกดำเนินการกับเอกสารที่เปิดอยู่ในหนึ่งรอบ.

### ขั้นตอน 5: บันทึกนโยบายเป็นไฟล์ XML
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```  
ไฟล์ XML จะเก็บการกำหนดการลบข้อมูล, ทำให้คุณสามารถใช้ซ้ำนโยบายเดียวกันโดยไม่ต้องเขียนโค้ดใหม่.

## การประยุกต์ใช้ในทางปฏิบัติ
- **Legal firms** สามารถลบหมายเลขคดีและชื่อลูกค้า ก่อนแชร์แบบร่าง.  
- **Finance departments** ปิดบังหมายเลขบัญชีหรือวันที่ทำรายการในรายงาน.  
- **Healthcare providers** รับประกันความสอดคล้องกับ HIPAA โดยการลบตัวระบุผู้ป่วย.

## เคล็ดลับด้านประสิทธิภาพ
- เปิด **one document at a time** เพื่อรักษาการใช้หน่วยความจำให้ต่ำ.  
- เขียน **efficient regular expressions**; หลีกเลี่ยงรูปแบบที่กว้างเกินไปซึ่งทำให้เวลาในการประมวลผลเพิ่มขึ้น.  
- รักษาไลบรารีให้ **up‑to‑date** เพื่อรับประโยชน์จากการปรับปรุงประสิทธิภาพและประเภทการลบข้อมูลใหม่.

## ปัญหาที่พบบ่อยและวิธีแก้

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|----------|
| **ข้อยกเว้น IO เมื่อเตรียมไดเรกทอรี** | เส้นทางไม่ถูกต้องหรือไม่มีสิทธิ์การเขียน | ตรวจสอบว่าโฟลเดอร์มีอยู่และแอปพลิเคชันมีสิทธิ์อ่าน/เขียน. |
| **Regex ไม่ตรงกับข้อความที่คาดหวัง** | รูปแบบเข้มงวดเกินไปหรือขาดอักขระ escape | ทดสอบ regex ด้วยเครื่องมือออนไลน์; ปรับ quantifier หรือ escape อักขระพิเศษ. |
| **ไฟล์นโยบายไม่ถูกสร้าง** | `SavePolicy` ถูกเรียกก่อนการใช้การลบข้อมูลหรือใช้เส้นทางที่ไม่ถูกต้อง | ตรวจสอบว่าไดเรกทอรีผลลัพธ์สามารถเขียนได้และเรียก `SavePolicy` หลังจาก `Apply`. |

## คำถามที่พบบ่อย

**Q: ฉันสามารถโหลดนโยบาย XML ที่มีอยู่แทนการสร้างใหม่แบบโปรแกรมได้หรือไม่?**  
A: ใช่—ใช้ `redactor.LoadPolicy("policy.xml")` เพื่อนำเข้านโยบายที่บันทึกไว้ก่อนหน้า.

**Q: GroupDocs.Redaction รองรับ PDF ที่มีการป้องกันด้วยรหัสผ่านหรือไม่?**  
A: แน่นอน. ส่งรหัสผ่านไปยังคอนสตรัคเตอร์ `Redactor`: `new Redactor(sourceFile, "password")`.

**Q: สามารถลบรูปภาพหรือเมตาดาต้าได้หรือไม่?**  
A: SDK มีคลาส `ImageRedaction` และ `MetadataRedaction` สำหรับสถานการณ์เหล่านั้น.

**Q: ฉันจะจัดการกับเอกสารขนาดใหญ่ (หลายร้อย MB) อย่างไร?**  
A: ประมวลผลเป็นชิ้นส่วนหรือใช้ streaming API เพื่อลดการใช้หน่วยความจำ; เครื่องยนต์สามารถจัดการไฟล์ขนาดสูงสุด 2 GB โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่ RAM.

**Q: ต้องการโมเดลใบอนุญาตแบบใดสำหรับการใช้งานเชิงพาณิชย์?**  
A: จำเป็นต้องมีใบอนุญาตแบบชำระเงินสำหรับการใช้งานจริง; ใบอนุญาตทดลองใช้ก็เพียงพอสำหรับการพัฒนาและทดสอบ.

## สรุป

ตอนนี้คุณมี **redaction policy** ที่ครบถ้วนและนำกลับมาใช้ใหม่ได้ ซึ่งสามารถใช้กับเอกสารใดก็ได้ด้วย GroupDocs.Redaction สำหรับ .NET การส่งออกนโยบายเป็น XML ทำให้การอัปเดตในอนาคตง่ายขึ้นและรับประกันการปกป้องข้อมูลที่สอดคล้องกันทั่วทั้งองค์กร.

### ขั้นตอนต่อไป
- ทดลองใช้ประเภทการลบข้อมูลเพิ่มเติมเช่น `ImageRedaction` หรือ `MetadataRedaction`.  
- ผสานตรรกะการโหลดนโยบายเข้าสู่ workflow การจัดการเอกสารของคุณเพื่อการลบข้อมูลอัตโนมัติ.  
- สำรวจ **GroupDocs.Redaction** API reference เพื่อการปรับแต่งขั้นสูง.

---

**อัปเดตล่าสุด:** 2026-10-06  
**ทดสอบด้วย:** GroupDocs.Redaction 5.8 for .NET  
**ผู้เขียน:** GroupDocs  

**ทรัพยากร**  
- [เอกสาร](https://docs.groupdocs.com/redaction/net/)  
- [อ้างอิง API](https://reference.groupdocs.com/redaction/net)  
- [ดาวน์โหลด](https://releases.groupdocs.com/redaction/net/)  
- [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/redaction/33)  
- [แบบฟอร์มขอใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)

## บทแนะนำที่เกี่ยวข้อง

- [ลบข้อมูลที่ละเอียดอ่อนด้วย GroupDocs.Redaction .NET (C#)](/redaction/net/advanced-redaction/groupdocs-redaction-net-implement-iredactioncallback-csharp/)  
- [ดำเนินการลบข้อมูลเอกสารด้วย GroupDocs.Redaction .NET: คู่มือขั้นตอนต่อขั้นตอน](/redaction/net/getting-started/implement-document-redaction-groupdocs-redaction-net/)  
- [วิธีลบข้อมูลเอกสารด้วย GroupDocs.Redaction .NET – คู่มือฉบับสมบูรณ์](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)