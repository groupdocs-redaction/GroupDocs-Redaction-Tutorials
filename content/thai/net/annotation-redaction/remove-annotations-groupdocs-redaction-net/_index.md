---
date: '2026-06-01'
description: เรียนรู้วิธีลบข้อมูลที่ละเอียดอ่อนและวิธีลบคำอธิบายจากเอกสารด้วย GroupDocs.Redaction
  สำหรับ .NET เพื่อให้เป็นไปตามข้อกำหนดและรักษาความเป็นส่วนตัวของข้อมูล
keywords:
- redact sensitive information
- how to remove annotations
- remove excel annotations
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to redact sensitive information and how to remove annotations
    from documents with GroupDocs.Redaction for .NET, ensuring compliance and data
    privacy.
  headline: How to Redact Sensitive Information and Remove Annotations Using GroupDocs.Redaction
    for .NET
  type: TechArticle
- description: Learn how to redact sensitive information and how to remove annotations
    from documents with GroupDocs.Redaction for .NET, ensuring compliance and data
    privacy.
  name: How to Redact Sensitive Information and Remove Annotations Using GroupDocs.Redaction
    for .NET
  steps:
  - name: Prepare Source and Output File Paths
    text: 'First, define the locations of your input document and the folder where
      the redacted file will be saved. Ensure the output directory exists; otherwise
      the operation will fail. *Definition anchor:* `Path.Combine` is a .NET utility
      that safely joins directory and file names across Windows, Linux, and '
  - name: Apply Regular Expression Redaction
    text: Next, create a redaction rule that targets annotations matching your regex
      pattern. *Definition anchor:* `Redactor` is the main class that loads a document
      and applies redaction rules. *Definition anchor:* `DeleteAnnotationRedaction`
      is a class that removes annotations whose content satisfies a regu
  - name: Dispose of Resources
    text: Always call `redactor.Dispose()` or wrap the instance in a `using` block
      to free unmanaged resources promptly. *Definition anchor:* `Dispose` releases
      unmanaged resources used by the Redactor instance, ensuring memory is freed.
  type: HowTo
- questions:
  - answer: Yes—by loading the `.xlsx` file with `Redactor` and applying a `DeleteAnnotationRedaction`
      rule, you can remove comments, notes, and other annotation types.
    question: Can GroupDocs.Redaction redact annotations in Excel workbooks?
  - answer: Prefix the pattern with `(?i)` or use the `RegexOptions.IgnoreCase` flag
      when constructing the `DeleteAnnotationRedaction`.
    question: How do I make regex patterns case‑insensitive?
  - answer: Absolutely. Set `SaveOptions.Prefix` or `SaveOptions.Suffix` to prepend
      or append text to the generated file name.
    question: Is it possible to customize the output file name?
  - answer: The source file remains untouched; the redacted version is saved to the
      path you provide in `SaveOptions`.
    question: What happens to the original document after redaction?
  - answer: Yes—GroupDocs.Redaction can operate in a streaming mode that processes
      pages sequentially, dramatically reducing memory consumption.
    question: Does the library support streaming for very large PDFs?
  type: FAQPage
title: วิธีทำการลบข้อมูลที่ละเอียดอ่อนและลบคำอธิบายโดยใช้ GroupDocs.Redaction สำหรับ
  .NET
type: docs
url: /th/net/annotation-redaction/remove-annotations-groupdocs-redaction-net/
weight: 1
---

# ลบข้อมูลที่ละเอียดอ่อนและลบคำอธิบายโดยใช้ GroupDocs.Redaction สำหรับ .NET

การจัดการข้อมูลที่เป็นความลับในเอกสารเป็นความท้าทายประจำวันสำหรับนักพัฒนา, ผู้ตรวจสอบ, และทีมกฎหมาย. **Redact sensitive information** อย่างรวดเร็วและเชื่อถือได้ด้วย GroupDocs.Redaction สำหรับ .NET, ไลบรารีที่ทำงานกับไฟล์รูปแบบมากกว่า 30 ประเภทและสามารถจัดการไฟล์ขนาดถึง 2 GB โดยไม่ต้องโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ. บทแนะนำนี้จะพาคุณผ่านขั้นตอนการทำงานทั้งหมด—ตั้งแต่การติดตั้งแพคเกจจนถึงการลบคำอธิบายเฉพาะด้วย regular expressions—เพื่อให้คุณสามารถปกป้องข้อมูลส่วนบุคคลและปฏิบัติตามกฎระเบียบเช่น GDPR และ HIPAA.

## คำตอบอย่างรวดเร็ว
- **GroupDocs.Redaction ทำอะไร?** มันจะลบหรือปิดบังข้อความ, รูปภาพ, และคำอธิบายโดยอัตโนมัติเพื่อปกป้องข้อมูลส่วนบุคคล.  
- **รองรับไฟล์ประเภทใดบ้าง?** มากกว่า 30 รูปแบบ, รวมถึง PDF, DOCX, XLSX, PPTX, และไฟล์รูปภาพ.  
- **ต้องการไลเซนส์สำหรับการพัฒนาหรือไม่?** การทดลองใช้ฟรีสามารถใช้สำหรับการทดสอบ; จำเป็นต้องมีไลเซนส์ถาวรสำหรับการใช้งานจริง.  
- **สามารถประมวลผลไฟล์ขนาดใหญ่ได้อย่างมีประสิทธิภาพหรือไม่?** ได้—การประมวลผลเป็นชุดและการสตรีมมิ่งช่วยลดการใช้หน่วยความจำสำหรับเอกสารหลายร้อยหน้า.  
- **เข้ากันได้กับ .NET 6 และ .NET Core หรือไม่?** รองรับเต็มรูปแบบบน .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, และ .NET 6+.

## “Redact sensitive information” คืออะไร?
*Redact sensitive information* หมายถึงการลบหรือทำให้ข้อมูลส่วนบุคคลหรือข้อมูลลับในเอกสารหายไปอย่างถาวรเพื่อไม่สามารถกู้คืนได้. สิ่งนี้รวมถึงชื่อ, หมายเลขประจำตัว, รายละเอียดทางการเงิน, หรือข้อมูลอื่นใดที่อาจระบุตัวบุคคลได้. การทำ redaction ช่วยให้ปฏิบัติตามกฎระเบียบเช่น GDPR, HIPAA, และ CCPA, ป้องกันการรั่วไหลของข้อมูล, และอนุญาตให้แชร์เอกสารกับบุคคลภายนอกได้อย่างปลอดภัย.

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับ .NET?
GroupDocs.Redaction ให้ **quantified benefits**: รองรับรูปแบบไฟล์เข้าและออกกว่า 30 แบบ, ประมวลผลเอกสารขนาดถึง 2 GB โดยไม่ต้องโหลดเอกสารทั้งหมด, และสามารถลบคำอธิบายได้ถึง 10 000 รายการต่อหนึ่งนาทีบนเซิร์ฟเวอร์มาตรฐาน. ตัวเลขเหล่านี้ทำให้มันเป็นหนึ่งในเครื่องมือ redaction ที่มีประสิทธิภาพและหลากหลายที่สุดในตลาด.

## ข้อกำหนดเบื้องต้น
ก่อนที่คุณจะเริ่ม, ตรวจสอบว่าคุณมีสิ่งต่อไปนี้:

- **GroupDocs.Redaction for .NET** (version 20.7 หรือใหม่กว่า).  
- Visual Studio 2022 หรือ IDE ที่เข้ากันได้ใด ๆ.  
- ความรู้พื้นฐานของ C# และความคุ้นเคยกับ regular expressions.  

### ไลบรารีที่จำเป็น
- **GroupDocs.Redaction for .NET** – ติดตั้งผ่าน NuGet (ดูส่วน Installation).

### ข้อกำหนดการตั้งค่าสภาพแวดล้อม
- .NET Framework 4.5+ **หรือ** .NET Core 3.1+.  
- เข้าถึงระบบไฟล์ที่เอกสารต้นทางอยู่.  

## การติดตั้ง – วิธีลบคำอธิบาย (ขั้นตอน 1)
คุณสามารถเพิ่มไลบรารีไปยังโปรเจกต์ของคุณโดยใช้คำสั่งใดคำสั่งหนึ่งต่อไปนี้. ไม่มีการเพิ่มบล็อกโค้ดเพื่อให้บทแนะนำเป็นแบบไม่มีโค้ด.

**.NET CLI:**  
เรียกใช้ `dotnet add package GroupDocs.Redaction --version 20.7.*` ในเทอร์มินัล.

**Package Manager Console:**  
ดำเนินการ `Install-Package GroupDocs.Redaction -Version 20.7.*`.

**NuGet Package Manager UI:**  
ค้นหา “GroupDocs.Redaction” แล้วคลิก **Install**.

### การรับไลเซนส์
เพื่อเปิดใช้งานฟังก์ชันเต็มรูปแบบ, รับไลเซนส์ทดลองหรือไลเซนส์ชั่วคราวจาก [GroupDocs](https://purchase.groupdocs.com/temporary-license/). สำหรับการใช้งานในผลิตภัณฑ์, ซื้อไลเซนส์ถาวรผ่านพอร์ทัลเดียวกัน.

## คู่มือการใช้งาน – วิธีลบคำอธิบายโดยใช้ regular expressions
### ภาพรวม
ส่วนนี้อธิบายวิธี **how to remove annotations** ที่ตรงกับรูปแบบเฉพาะ—เหมาะสำหรับการลบชื่อพนักงาน, บันทึกลับ, หรือเครื่องหมายที่กำหนดเองใด ๆ.

### ขั้นตอน 1: เตรียมเส้นทางไฟล์ต้นทางและไฟล์ผลลัพธ์
แรกสุด, กำหนดตำแหน่งของเอกสารต้นเข้าและโฟลเดอร์ที่ไฟล์ที่ทำ redaction จะถูกบันทึก. ตรวจสอบให้แน่ใจว่าไดเรกทอรีผลลัพธ์มีอยู่; หากไม่มีกระบวนการจะล้มเหลว.

*คำนิยาม anchor:* `Path.Combine` เป็นยูทิลิตี้ของ .NET ที่เชื่อมต่อชื่อโฟลเดอร์และไฟล์อย่างปลอดภัยบน Windows, Linux, และ macOS.

### ขั้นตอน 2: ใช้ Regular Expression Redaction
ต่อไป, สร้างกฎ redaction ที่มุ่งเป้าหมายคำอธิบายที่ตรงกับรูปแบบ regex ของคุณ.

*คำนิยาม anchor:* `Redactor` คือคลาสหลักที่โหลดเอกสารและใช้กฎ redaction.  
*คำนิยาม anchor:* `DeleteAnnotationRedaction` คือคลาสที่ลบคำอธิบายที่เนื้อหาตรงกับตัวกรอง regular‑expression.  
*คำนิยาม anchor:* `SaveOptions` ให้คุณควบคุมวิธีการเขียนไฟล์ผลลัพธ์—เพิ่ม suffix, เลือกรูปแบบไฟล์ผลลัพธ์, และปิดการ rasterization เพื่อให้ไฟล์เป็นแบบเวกเตอร์.

**คำตอบโดยตรง:** โหลดเอกสารต้นทางด้วย `Redactor redactor = new Redactor(sourcePath);`, เพิ่ม `DeleteAnnotationRedaction` โดยใช้ regex ของคุณ, จากนั้นเรียก `redactor.Save(outputPath, new SaveOptions { Suffix = "_redacted", Rasterize = false });`. กระบวนการบรรทัดเดียวนี้จะลบคำอธิบายที่ตรงกันและเขียนไฟล์ใหม่โดยไม่เปลี่ยนแปลงไฟล์ต้นฉบับ.

### ขั้นตอน 3: ปล่อยทรัพยากร
ควรเรียก `redactor.Dispose()` หรือห่ออินสแตนซ์ในบล็อก `using` เพื่อปล่อยทรัพยากรที่ไม่ได้จัดการโดยเร็ว.  
*คำนิยาม anchor:* `Dispose` ปล่อยทรัพยากรที่ไม่ได้จัดการที่ Redactor ใช้, ทำให้หน่วยความจำถูกคืน.

## การเตรียมเส้นทางไฟล์สำหรับการลบคำอธิบาย – วิธีลบคำอธิบายใน Excel
แม้ว่าตัวอย่างจะเน้นที่ PDF, วิธีเดียวกันนี้ทำงานกับไฟล์ Excel (`.xlsx`). การจัดการเส้นทางอย่างถูกต้องช่วยป้องกันข้อผิดพลาด “file not found”.

*คำนิยาม anchor:* `PrepareOutputDirectory` เป็นเมธอดช่วยเหลือที่ตรวจสอบการมีอยู่ของโฟลเดอร์และสร้างหากไม่มี.

โดยการใช้ยูทิลิตี้เดียวกันนี้ข้ามรูปแบบ, คุณสามารถ **how to remove annotations** จากเวิร์กบุ๊ก Excel, เอกสาร Word, หรือการนำเสนอ PowerPoint ด้วยการเปลี่ยนแปลงโค้ดเพียงเล็กน้อย.

## การประยุกต์ใช้งานจริง
1. **Data Privacy Compliance** – ทำ redaction อัตโนมัติเพื่อให้สอดคล้องกับข้อกำหนด GDPR, HIPAA, หรือ CCPA โดยการลบตัวระบุส่วนบุคคล.  
2. **Legal Document Preparation** – ลบความคิดเห็นที่เป็นความลับก่อนแชร์สัญญากับบุคคลภายนอก.  
3. **Corporate Data Management** – ทำความสะอาดรายงานภายในโดยอัตโนมัติ, เพื่อให้แน่ใจว่าข้อมูลที่ได้รับการอนุมัติเท่านั้นที่ออกจากองค์กร.

## การพิจารณาประสิทธิภาพ – วิธีลบคำอธิบายอย่างมีประสิทธิภาพ
- **Efficient Memory Management:** ปล่อยออบเจกต์ `Redactor` ทันทีที่คุณเสร็จสิ้นการประมวลผลแต่ละไฟล์.  
- **Batch Processing:** วนลูปผ่านโฟลเดอร์ของเอกสารและใช้กฎ redaction เดียวกันกับแต่ละไฟล์; วิธีนี้ลดภาระเมื่อเทียบกับการเปิดและปิดไลบรารีหลายครั้ง.  
- **Optimized Regular Expressions:** ใช้ non‑capturing groups และหลีกเลี่ยงรูปแบบที่ทำ backtracking หนัก. ตัวอย่างเช่น, ควรใช้ `\bEmployeeID:\s*\d{4,6}\b` แทน `.*EmployeeID.*` เพื่อเพิ่มความเร็วในการจับคู่.

## ปัญหาทั่วไปและวิธีแก้
- **Large Files Stall:** แบ่งเอกสารเป็นส่วนหรือเพิ่มการตั้งค่า `MaxMemoryUsage` ใน `RedactorSettings`.  
- **Regex Not Matching:** ตรวจสอบว่ารูปแบบมีแฟล็ก `(?i)` สำหรับการไม่แยกแยะตัวพิมพ์ใหญ่/เล็ก, หรือทดสอบด้วยเครื่องมือทดสอบ regex ออนไลน์ก่อนนำไปใช้.  
- **Output File Overwrites Original:** ระบุเส้นทางผลลัพธ์ที่แตกต่างเสมอหรือใช้ `SaveOptions.Suffix` เพื่อเพิ่ม “_redacted” อัตโนมัติ.

## คำถามที่พบบ่อย (ใหม่)

**Q: GroupDocs.Redaction สามารถลบคำอธิบายในเวิร์กบุ๊ก Excel ได้หรือไม่?**  
A: ใช่—โดยโหลดไฟล์ `.xlsx` ด้วย `Redactor` และใช้กฎ `DeleteAnnotationRedaction`, คุณสามารถลบคอมเมนต์, โน้ต, และประเภทคำอธิบายอื่น ๆ ได้.

**Q: จะทำให้รูปแบบ regex ไม่แยกแยะตัวพิมพ์ใหญ่/เล็กอย่างไร?**  
A: ใส่คำนำหน้า `(?i)` หรือใช้แฟล็ก `RegexOptions.IgnoreCase` เมื่อสร้าง `DeleteAnnotationRedaction`.

**Q: สามารถปรับแต่งชื่อไฟล์ผลลัพธ์ได้หรือไม่?**  
A: แน่นอน. ตั้งค่า `SaveOptions.Prefix` หรือ `SaveOptions.Suffix` เพื่อเพิ่มหรือผนวกข้อความกับชื่อไฟล์ที่สร้างขึ้น.

**Q: จะเกิดอะไรขึ้นกับเอกสารต้นฉบับหลังการทำ redaction?**  
A: ไฟล์ต้นทางจะไม่ถูกแก้ไข; เวอร์ชันที่ทำ redaction จะถูกบันทึกไปยังเส้นทางที่คุณระบุใน `SaveOptions`.

**Q: ไลบรารีนี้รองรับการสตรีมมิ่งสำหรับ PDF ขนาดใหญ่มากหรือไม่?**  
A: ใช่—GroupDocs.Redaction สามารถทำงานในโหมดสตรีมมิ่งที่ประมวลผลหน้าแบบต่อเนื่อง, ลดการใช้หน่วยความจำอย่างมาก.

## ส่วนคำถามที่พบบ่อย
1. **จะจัดการเอกสารขนาดใหญ่อย่างมีประสิทธิภาพอย่างไร?**  
   - ประมวลผลเอกสารเป็นส่วนย่อย ๆ หากเป็นไปได้, และตรวจสอบให้แน่ใจว่า regular expressions ถูกปรับให้เหมาะสมสำหรับประสิทธิภาพ.  
2. **สามารถใช้ GroupDocs.Redaction กับรูปแบบไฟล์อื่น ๆ นอกจาก Excel ได้หรือไม่?**  
   - ได้, รองรับหลายรูปแบบรวมถึง PDF, Word, และอื่น ๆ.  
3. **จะเกิดอะไรขึ้นกับเอกสารต้นฉบับหลังการทำ redaction?**  
   - เอกสารต้นฉบับจะไม่เปลี่ยนแปลงหากไม่ได้บันทึกทับ; ควรบันทึกการเปลี่ยนแปลงเป็นไฟล์ใหม่หรือสำเนา.  
4. **สามารถปรับแต่งชื่อไฟล์ผลลัพธ์ด้วย GroupDocs.Redaction ได้หรือไม่?**  
   - ได้, ปรับ `SaveOptions` เพื่อรวม suffix หรือ prefix ที่กำหนดเองสำหรับชื่อไฟล์ผลลัพธ์.  
5. **จะทำให้รูปแบบ regex ไม่แยกแยะตัวพิมพ์ใหญ่/เล็กอย่างไร?**  
   - ใช้โมดิฟายเออร์เช่น `(i)` ใน regular expressions ของคุณเพื่อทำให้ไม่แยกแยะตัวพิมพ์ใหญ่/เล็ก.

## แหล่งข้อมูล
- [เอกสารประกอบ](https://docs.groupdocs.com/redaction/net/)  
- [อ้างอิง API](https://reference.groupdocs.com/redaction/net)  
- [ดาวน์โหลด GroupDocs.Redaction](https://releases.groupdocs.com/redaction/net/)  
- [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/redaction/33)  
- [ขอรับไลเซนส์ชั่วคราว](https://purchase.groupdocs.com/temporary-license/) 

โดยการทำตามคู่มือนี้, คุณจะมีวิธีที่แข็งแกร่งในการ **redact sensitive information** และ **how to remove annotations** จากเอกสารประเภทใดก็ได้ที่รองรับโดยใช้ GroupDocs.Redaction สำหรับ .NET. ดำเนินการตามขั้นตอน, ทดสอบกับไฟล์ตัวอย่างหลายไฟล์, และผสานตรรกะนี้เข้าสู่ pipeline การประมวลผลเอกสารของคุณเพื่อความปลอดภัยสูงสุด.

---

**Last Updated:** 2026-06-01  
**Tested With:** GroupDocs.Redaction 20.7 for .NET  
**Author:** GroupDocs  

```bash
dotnet add package GroupDocs.Redaction
```

```powershell
Install-Package GroupDocs.Redaction
```

```csharp
string sourceFile = @"YOUR_DOCUMENT_DIRECTORY\AnnotatedDocument.xlsx";
var saveOptions = new SaveOptions { AddSuffix = true, RasterizeToPDF = false };
```

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // This regex matches the phrase "John Doe" in a case-insensitive manner.
    redactor.Apply(new DeleteAnnotationRedaction("(?im:John Doe)"));
    
    // Save changes to a new file with a suffix indicating it's been redacted.
    var outputFile = redactor.Save(saveOptions);
}
```

```csharp
using System.IO;

public class Utils
{
    public static string PrepareOutputDirectory(string fileName)
    {
        var documentDirectory = Path.Combine(Directory.GetCurrentDirectory(), "YOUR_DOCUMENT_DIRECTORY");
        var filePath = Path.Combine(documentDirectory, fileName);

        Directory.CreateDirectory(documentDirectory);
        return filePath;
    }
}
```

## บทแนะนำที่เกี่ยวข้อง

- [วิธีโหลดและทำ Redact เอกสารโดยใช้ GroupDocs.Redaction .NET&#58; คู่มือครบถ้วน](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [ทำ Redact และบันทึกเอกสารด้วย GroupDocs.Redaction สำหรับ .NET&#58; คู่มือครบถ้วน](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [ทำ Redact วลีที่ตรงกันในเอกสาร .NET โดยใช้ GroupDocs.Redaction](/redaction/net/text-redaction/guide-redact-exact-phrases-groupdocs-redaction-dotnet/)