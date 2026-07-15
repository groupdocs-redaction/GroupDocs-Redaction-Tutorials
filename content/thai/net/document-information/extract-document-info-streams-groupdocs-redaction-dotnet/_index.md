---
date: '2026-06-11'
description: เรียนรู้วิธีดึง metadata จากสตรีมเอกสารโดยใช้ GroupDocs.Redaction สำหรับ
  .NET รวมถึงการตั้งค่า ตัวอย่างโค้ด และการประยุกต์ใช้งานจริง
keywords:
- how to extract metadata
- extract document metadata
- extract pdf metadata
- retrieve document size
- prepare output directory
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  headline: How to Extract Metadata from Document Streams Using GroupDocs.Redaction
    .NET
  type: TechArticle
- description: Learn how to extract metadata from document streams using GroupDocs.Redaction
    for .NET, covering setup, code examples, and practical applications.
  name: How to Extract Metadata from Document Streams Using GroupDocs.Redaction .NET
  steps:
  - name: Prepare the source file path
    text: First, ensure the source file exists and that the output folder is ready.
      The helper method below checks the output directory and creates it if needed.
      *Why?* This guarantees a valid path for subsequent file operations and prevents
      `DirectoryNotFoundException`.
  - name: Open the document stream
    text: Using `File.OpenRead()` opens the file as a **read‑only stream**, which
      keeps memory usage low even for gigabyte‑size files. *Why?* Streams enable on‑the‑fly
      processing, allowing you to work with portions of the file rather than the whole
      document.
  - name: Initialise the Redactor with the document stream
    text: '`Redactor` is the primary API object that gives you access to document‑level
      operations, including metadata extraction. `Redactor` represents a single document
      loaded from a stream and exposes methods such as `GetDocumentInfo()` for quick
      property retrieval. *Why?* Instantiating `Redactor` with a st'
  - name: Retrieve document metadata
    text: Calling `GetDocumentInfo()` returns a `DocumentInfo` object that holds the
      file format, page count, and file size. `GetDocumentInfo()` extracts core properties
      (format, page count, size) in a single call, eliminating the need for separate
      parsers. *Why?* This step consolidates all essential metadata
  type: HowTo
- questions:
  - answer: It enables fast, memory‑efficient retrieval of document properties for
      indexing, compliance checks, and automated routing without opening the full
      file.
    question: What is the primary use case for GroupDocs.Redaction’s metadata extraction?
  - answer: Yes, provide the password when constructing the `Redactor` object; the
      API will decrypt the stream internally.
    question: Can I extract metadata from password‑protected files?
  - answer: Absolutely – GroupDocs.Redaction handles over 30 formats, including PDF,
      DOCX, XLSX, PPTX, and common image types.
    question: Does the library support non‑PDF formats like DOCX or XLSX?
  - answer: Streams allow processing of files up to **2 GB** while keeping memory
      consumption under **50 MB**, thanks to on‑the‑fly reading.
    question: How large a document can I process with streams?
  - answer: Visit the [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33)
      for community support, or consult the official documentation for troubleshooting
      tips.
    question: Where can I get help if I run into issues?
  type: FAQPage
title: วิธีดึง metadata จากสตรีมเอกสารโดยใช้ GroupDocs.Redaction .NET
type: docs
url: /th/net/document-information/extract-document-info-streams-groupdocs-redaction-dotnet/
weight: 1
---

# วิธีการดึงข้อมูลเมตาดาต้าจากสตรีมเอกสารโดยใช้ GroupDocs.Redaction .NET

คุณรู้สึกเหนื่อยกับการดึงข้อมูลเอกสารด้วยตนเองหรือจัดการกับไฟล์ขนาดใหญ่ที่ทำให้กระบวนการทำงานของคุณช้าใช่ไหม? **วิธีการดึงเมตาดาต้า** อย่างรวดเร็วเป็นความท้าทายทั่วไป และไลบรารี GroupDocs.Redaction สำหรับ .NET มีวิธีที่เร็วและใช้หน่วยความจำน้อยเพื่อดึงรายละเอียดเอกสารโดยตรงจากสตรีม ในบทแนะนำนี้ คุณจะได้เรียนรู้วิธีตั้งค่าไลบรารี ดึงประเภทไฟล์ จำนวนหน้า และขนาดจากสตรีม และเตรียมโฟลเดอร์ผลลัพธ์สำหรับการประมวลผลต่อไป

## คำตอบสั้น
- **“extract metadata” หมายถึงอะไร?** หมายถึงการอ่านคุณสมบัติเช่น ประเภทไฟล์ จำนวนหน้า และขนาดโดยไม่ต้องเปิดเอกสารเต็มในหน่วยความจำ.  
- **ไลบรารีใดจัดการเรื่องนี้?** GroupDocs.Redaction สำหรับ .NET มี API เนทีฟสำหรับการดึงเมตาดาต้าจากสตรีม.  
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีทำงานสำหรับการพัฒนา; จำเป็นต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **ฉันสามารถประมวลผล PDF ที่ใหญ่กว่า 1 GB ได้หรือไม่?** ได้ – สตรีมทำให้คุณจัดการไฟล์ได้ถึง 2 GB โดยไม่ต้องโหลดไฟล์ทั้งหมด.  
- **เวอร์ชัน .NET ที่รองรับคืออะไร?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5+, และ .NET 6+.

## การดึงเมตาดาต้าจากสตรีมคืออะไร?
การดึงเมตาดาต้าจากสตรีมคือกระบวนการอ่านคุณสมบัติของเอกสารโดยตรงจากอ็อบเจ็กต์ `Stream` โดยหลีกเลี่ยงการโหลดไฟล์เต็มและจึงประหยัดหน่วยความจำและเวลา CPU เทคนิคนี้เหมาะสำหรับการประมวลผลแบบแบตช์หรือบริการบนคลาวด์ที่มีทรัพยากรจำกัด.

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับการดึงเมตาดาต้า?
GroupDocs.Redaction รองรับ **ไฟล์ฟอร์แมตกว่า 30 ประเภท** (รวมถึง PDF, DOCX, XLSX, PPTX และรูปภาพ) และสามารถประมวลผลเอกสารขนาดถึง **2 GB** ในขณะที่ใช้หน่วยความจำน้อยกว่า **50 MB** API `Redactor` ของมันให้การเรียกเดียวเพื่อดึงข้อมูลสำคัญของเอกสารทั้งหมด ลดความจำเป็นในการใช้พาร์เซอร์หลายตัว.

## ข้อกำหนดเบื้องต้น

- **GroupDocs.Redaction for .NET** (เวอร์ชันล่าสุด)  
- **.NET Framework** 4.5+ **หรือ** **.NET Core/5+/6+**  
- ความรู้พื้นฐาน C# และความคุ้นเคยกับการทำ I/O ของไฟล์  
- Visual Studio 2019 หรือใหม่กว่า  

## วิธีตั้งค่า GroupDocs.Redaction สำหรับ .NET?
เพื่อเริ่มใช้ GroupDocs.Redaction คุณต้องเพิ่มไลบรารีนี้ลงในโปรเจกต์ของคุณก่อน สามารถทำได้ผ่าน .NET CLI, Visual Studio Package Manager หรือ NuGet UI เลือกวิธีที่เหมาะกับกระบวนการทำงานของคุณ; CLI เหมาะสำหรับการสร้างแบบสคริปต์, ส่วน UI ให้วิธีกราฟิกเพื่อเรียกดูเวอร์ชันและการพึ่งพา.

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI:**
- เปิด NuGet Package Manager ใน Visual Studio.  
- ค้นหา **"GroupDocs.Redaction"** และติดตั้งเวอร์ชันล่าสุด.

### ขั้นตอนการรับไลเซนส์
1. **Free Trial:** ดาวน์โหลดไลเซนส์ทดลองเพื่อสำรวจคุณสมบัติทั้งหมดโดยไม่มีข้อจำกัด.  
2. **Temporary License:** ขอไลเซนส์ชั่วคราวจาก [GroupDocs](https://purchase.groupdocs.com/temporary-license/) สำหรับการทดสอบต่อเนื่อง.  
3. **Purchase:** เมื่อพร้อมสำหรับการใช้งานจริง ให้ซื้อไลเซนส์เชิงพาณิชย์.  

สำหรับข้อมูลเพิ่มเติม โปรดเยี่ยมชม [GroupDocs website](https://purchase.groupdocs.com/temporary-license/).

### การเริ่มต้นและตั้งค่าเบื้องต้น
คลาส `Redactor` เป็นจุดเริ่มต้นสำหรับการดำเนินการทั้งหมด รวมถึงการดึงเมตาดาต้า.  
`Redactor` เป็นคลาสหลักที่แทนอินสแตนซ์ของเอกสารและให้เมธอดสำหรับการลบข้อมูล, การดึงข้อมูล, และการจัดการไฟล์ หลังจากติดตั้งแล้ว คุณสามารถสร้างอ็อบเจ็กต์ `Redactor` ตามตัวอย่างด้านล่าง:

```csharp
using (Redactor redactor = new Redactor("your-document-path"))
{
    // Use the redactor here
}
```

เมื่อไลบรารีพร้อมแล้ว เราจะไปสู่รายละเอียดการใช้งาน.

## วิธีดึงเมตาดาต้าจากสตรีมเอกสาร
โหลดเอกสารเป็น **สตรีมแบบอ่านอย่างเดียว**, เริ่มต้น `Redactor`, และเรียก `GetDocumentInfo()` เพื่อดึงเมตาดาต้าในขั้นตอนเดียว วิธีนี้หลีกเลี่ยงการโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ ซึ่งสำคัญสำหรับ PDF ขนาดใหญ่หรือเอกสาร Office ที่มีหลายร้อยหน้า.

**คำตอบโดยตรง:** เปิดไฟล์ด้วย `File.OpenRead()`, ส่งสตรีมไปยัง `new Redactor(stream)`, จากนั้นเรียก `redactor.GetDocumentInfo()` – เมธอดนี้คืนอ็อบเจ็กต์ที่มีประเภทไฟล์ จำนวนหน้า และขนาดเพียงสามบรรทัดของโค้ด.

### ขั้นตอนที่ 1: เตรียมเส้นทางไฟล์ต้นทาง
แรกสุด ตรวจสอบให้แน่ใจว่าไฟล์ต้นทางมีอยู่และโฟลเดอร์ผลลัพธ์พร้อม วิธีช่วยเหลือด้านล่างจะตรวจสอบไดเรกทอรีผลลัพธ์และสร้างหากจำเป็น.

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY/SAMPLE_DOCX");
```

*ทำไม?* สิ่งนี้รับประกันว่าเส้นทางจะถูกต้องสำหรับการดำเนินการไฟล์ต่อไปและป้องกัน `DirectoryNotFoundException`.

### ขั้นตอนที่ 2: เปิดสตรีมเอกสาร
การใช้ `File.OpenRead()` เปิดไฟล์เป็น **สตรีมแบบอ่านอย่างเดียว** ซึ่งทำให้การใช้หน่วยความจำน้อยแม้ไฟล์ขนาดกิกะไบต์.

```csharp
using (Stream documentStream = File.OpenRead(sourceFile))
{
    // Proceed to initialize Redactor
}
```

*ทำไม?* สตรีมทำให้สามารถประมวลผลแบบเรียลไทม์ได้, ให้คุณทำงานกับส่วนของไฟล์แทนที่จะเป็นเอกสารทั้งหมด.

### ขั้นตอนที่ 3: เริ่มต้น Redactor ด้วยสตรีมเอกสาร
`Redactor` เป็นอ็อบเจ็กต์ API หลักที่ให้คุณเข้าถึงการดำเนินการระดับเอกสาร รวมถึงการดึงเมตาดาต้า.  
`Redactor` แทนเอกสารเดียวที่โหลดจากสตรีมและเปิดเผยเมธอดเช่น `GetDocumentInfo()` เพื่อดึงคุณสมบัติอย่างรวดเร็ว.

```csharp
using (Redactor redactor = new Redactor(documentStream))
{
    // Extract document info next
}
```

*ทำไม?* การสร้างอินสแตนซ์ `Redactor` ด้วยสตรีมทำให้วัตถุเชื่อมต่อกับไฟล์พื้นฐานโดยไม่ต้องโหลดเต็ม.

### ขั้นตอนที่ 4: ดึงเมตาดาต้าเอกสาร
การเรียก `GetDocumentInfo()` จะคืนอ็อบเจ็กต์ `DocumentInfo` ที่เก็บฟอร์แมตไฟล์ จำนวนหน้า และขนาดไฟล์.

`GetDocumentInfo()` ดึงคุณสมบัติหลัก (ฟอร์แมต, จำนวนหน้า, ขนาด) ในการเรียกเดียว, ลดความจำเป็นของพาร์เซอร์แยกต่างหาก.

```csharp
IDocumentInfo info = redactor.GetDocumentInfo();
string fileInfo = $"\nFile type: {info.FileType}\nNumber of pages: {info.PageCount}\nDocument size: {info.Size} bytes";
Console.WriteLine(fileInfo);
```

*ทำไม?* ขั้นตอนนี้รวมเมตาดาต้าสำคัญทั้งหมด ทำให้ง่ายต่อการบันทึก, กรอง, หรือกำหนดเส้นทางเอกสารตามลักษณะของมัน.

## วิธีเตรียมไดเรกทอรีผลลัพธ์สำหรับไฟล์ที่ประมวลผล
ก่อนเขียนไฟล์ที่ประมวลผลใด ๆ ตรวจสอบให้แน่ใจว่าโฟลเดอร์ปลายทางมีอยู่และสามารถเขียนได้ การตรวจสอบเส้นทางโดยโปรแกรมและสร้างเมื่อไม่มี จะช่วยหลีกเลี่ยงข้อยกเว้นรันไทม์ทั่วไปเช่น `DirectoryNotFoundException` หรือข้อผิดพลาดการอนุญาต ขั้นตอนง่าย ๆ นี้ยังทำให้โค้ดของคุณพกพาได้ในหลายสภาพแวดล้อม ไม่ว่าจะรันในเครื่องท้องถิ่น, เซิร์ฟเวอร์, หรือคอนเทนเนอร์.

**คำตอบโดยตรง:** ใช้ `Directory.Exists()` เพื่อตรวจสอบโฟลเดอร์และ `Directory.CreateDirectory()` เพื่อสร้างหากไม่มี – การตรวจสอบบรรทัดเดียวนี้รับประกันว่าเส้นทางถูกต้องก่อนการเขียนใด ๆ.

### สร้างเมธอดช่วยเหลือ
เมธอดด้านล่างรวมตรรกะการตรวจสอบและสร้าง, คืนค่าเส้นทางที่ตรวจสอบแล้วสำหรับการใช้ต่อไป.

```csharp
public static class Utils
{
    public static string PrepareOutputDirectory(string sampleDocPath)
    {
        string directory = Path.GetDirectoryName(sampleDocPath);
        
        if (!Directory.Exists(directory))
        {
            Directory.CreateDirectory(directory);
        }
        
        return Path.Combine(directory, "SAMPLE_DOCX.docx");
    }
}
```

*ทำไม?* การรวมศูนย์ตรรกะนี้ลดการทำซ้ำและทำให้ฐานโค้ดง่ายต่อการบำรุงรักษา.

## ปัญหาทั่วไปและวิธีแก้
- **Permission errors:** ตรวจสอบให้แอปพลิเคชันทำงานภายใต้บัญชีที่มีสิทธิ์เขียนในโฟลเดอร์เป้าหมาย.  
- **Invalid paths:** ตรวจสอบตัวคั่นเส้นทาง (`\\` บน Windows, `/` บน Linux/macOS) เพื่อหลีกเลี่ยง `DirectoryNotFoundException`.  
- **Large file handling:** ปิดสตรีมโดยเร็ว (`using` statements) เพื่อปล่อยฮาเนิลของ OS และป้องกันการรั่วไหล.

## การประยุกต์ใช้ในทางปฏิบัติ
1. **Automated Document Ingestion:** ดึงเมตาดาต้าเมื่ออัปโหลด, จากนั้นเก็บไว้ในฐานข้อมูลเพื่อการค้นหาเร็วและรายงานการปฏิบัติตาม.  
2. **Legal & Compliance Audits:** ดึงจำนวนหน้าและประเภทไฟล์เพื่อยืนยันว่าเอกสารตรงตามมาตรฐานกฎระเบียบก่อนการจัดเก็บ.  
3. **Enterprise Content Management:** ใช้เมตาดาต้าเพื่อจัดประเภทไฟล์อัตโนมัติในโฟลเดอร์, ปรับปรุงการจัดระเบียบและความเร็วในการดึงข้อมูล.

## พิจารณาด้านประสิทธิภาพ
- **Memory Management:** ห่อสตรีมด้วยบล็อก `using` เสมอเพื่อให้ถูกทำลายโดยอัตโนมัติ.  
- **Batch Processing:** ประมวลผลเอกสารเป็นกลุ่ม 10‑20 เพื่อสมดุลระหว่างอัตราผลิตและการใช้หน่วยความจำ, โดยเฉพาะบนเซิร์ฟเวอร์ที่มีทรัพยากรจำกัด.  
- **Parallelism:** ใช้ `Parallel.ForEach` สำหรับไฟล์ที่แยกจากกัน, แต่ต้องตรวจสอบการใช้ CPU และ I/O เพื่อหลีกเลี่ยงการแย่งกัน.

## สรุป
คุณมีคู่มือครบถ้วนและพร้อมใช้งานในสภาพการผลิตเกี่ยวกับ **วิธีการดึงเมตาดาต้า** จากสตรีมเอกสารโดยใช้ GroupDocs.Redaction สำหรับ .NET แล้ว ด้วยการทำตามขั้นตอนข้างต้น คุณสามารถดึงประเภทไฟล์ จำนวนหน้า และขนาดได้อย่างมีประสิทธิภาพโดยคงการใช้หน่วยความจำต่ำและจัดการไฟล์ขนาดใหญ่ได้อย่างราบรื่น.

**ขั้นตอนต่อไป**
- ตรวจสอบอ้างอิง API เต็มรูปแบบใน [documentation](https://docs.groupdocs.com/redaction/net/).  
- ศึกษเพิ่มเติมใน [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/) เพื่อสำรวจฟีเจอร์การลบข้อมูล, ใส่ลายน้ำ, และ OCR.  
- ทดลองกับฟอร์แมตไฟล์ต่าง ๆ (PDF, DOCX, XLSX) เพื่อดูว่าเมตาดาต้าแตกต่างกันอย่างไรในแต่ละประเภท.  
- รวมเมตาดาต้าที่ดึงได้เข้ากับระบบจัดการเอกสารหรือการค้นหาที่คุณมีอยู่.

## คำถามที่พบบ่อย

**Q: การใช้งานหลักของการดึงเมตาดาต้าใน GroupDocs.Redaction คืออะไร?**  
A: มันทำให้สามารถดึงคุณสมบัติของเอกสารได้อย่างเร็วและใช้หน่วยความจำน้อยสำหรับการทำดัชนี, ตรวจสอบการปฏิบัติตาม, และการกำหนดเส้นทางอัตโนมัติโดยไม่ต้องเปิดไฟล์เต็ม.

**Q: ฉันสามารถดึงเมตาดาต้าจากไฟล์ที่มีการป้องกันด้วยรหัสผ่านได้หรือไม่?**  
A: ได้, ให้รหัสผ่านเมื่อสร้างอ็อบเจ็กต์ `Redactor`; API จะถอดรหัสสตรีมภายใน.

**Q: ไลบรารีสนับสนุนฟอร์แมตที่ไม่ใช่ PDF เช่น DOCX หรือ XLSX หรือไม่?**  
A: แน่นอน – GroupDocs.Redaction รองรับมากกว่า 30 ฟอร์แมต รวมถึง PDF, DOCX, XLSX, PPTX, และรูปภาพทั่วไป.

**Q: ฉันสามารถประมวลผลเอกสารขนาดเท่าไหร่ด้วยสตรีม?**  
A: สตรีมทำให้สามารถประมวลผลไฟล์ได้ถึง **2 GB** โดยคงการใช้หน่วยความจำน้อยกว่า **50 MB** ด้วยการอ่านแบบเรียลไทม์.

**Q: ฉันจะหาแนวทางช่วยเหลือเมื่อเจอปัญหาได้จากที่ไหน?**  
A: เยี่ยมชม [GroupDocs forum](https://forum.groupdocs.com/c/redaction/33) เพื่อรับการสนับสนุนจากชุมชน, หรือดูเอกสารอย่างเป็นทางการสำหรับเคล็ดลับการแก้ไขปัญหา.

**Last Updated:** 2026-06-11  
**Tested With:** GroupDocs.Redaction 23.12 for .NET  
**Author:** GroupDocs  

**Resources**  
- **Documentation:** [GroupDocs Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API Reference:** [GroupDocs Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **Download:** [Latest GroupDocs Releases](https://releases.groupdocs.com/redaction/net)

## บทแนะนำที่เกี่ยวข้อง

- [ดึงข้อมูลเมตาดาต้าเอกสารขั้นสูงด้วย GroupDocs.Redaction .NET API](/redaction/net/document-information/groupdocs-redaction-net-document-metadata-retrieval/)
- [วิธีลบเมตาดาต้าเอกสารด้วย GroupDocs.Redaction สำหรับ .NET - คู่มือฉบับสมบูรณ์](/redaction/net/metadata-redaction/redact-metadata-groupdocs-redaction-net/)
- [การลบข้อมูลเอกสารอย่างปลอดภัยใน .NET ด้วยสตรีม: คู่มือสำหรับ GroupDocs.Redaction](/redaction/net/document-saving/secure-document-redaction-net-streams-groupdocs-redaction/)