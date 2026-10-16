---
date: '2026-10-16'
description: เรียนรู้วิธีใช้ GroupDocs เพื่อลบข้อมูลบนรูปภาพที่ฝังอยู่ในเอกสาร Word
  ด้วย GroupDocs.Redaction .NET API เพื่อรักษาข้อมูลที่สำคัญให้ปลอดภัย
keywords:
- how to use groupdocs
- hide pictures word
- redactor word document
- redact images word
- word image masking
lastmod: '2026-10-16'
og_description: วิธีใช้ GroupDocs เพื่อลบข้อมูลบนรูปภาพที่ฝังอยู่ในเอกสาร Word ด้วย
  .NET API. ปกป้องภาพที่เป็นความลับอย่างรวดเร็วและเชื่อถือได้
og_image_alt: Guide showing GroupDocs.Redaction .NET API redacting images in a Word
  file
og_title: วิธีใช้ GroupDocs เพื่อลบข้อมูลบนรูปภาพใน Word ด้วย .NET
schemas:
- author: GroupDocs
  dateModified: '2026-10-16'
  description: Learn how to use GroupDocs to redact embedded images in Word documents
    using the GroupDocs.Redaction .NET API, keeping sensitive data safe.
  headline: How to use GroupDocs to redact images in Word with .NET
  type: TechArticle
- description: Learn how to use GroupDocs to redact embedded images in Word documents
    using the GroupDocs.Redaction .NET API, keeping sensitive data safe.
  name: How to use GroupDocs to redact images in Word with .NET
  steps:
  - name: '**Confidential reports:** Redact logos or charts before external distribution.'
    text: '**Confidential reports:** Redact logos or charts before external distribution.'
  - name: '**Legal briefs:** Hide client photographs or scanned IDs that contain personal
      data.'
    text: '**Legal briefs:** Hide client photographs or scanned IDs that contain personal
      data.'
  - name: '**Business contracts:** Mask proprietary diagrams that reveal trade secrets.'
    text: '**Business contracts:** Mask proprietary diagrams that reveal trade secrets.'
  - name: '**Government releases:** Remove sensitive satellite images from public
      PDFs generated from Word.'
    text: '**Government releases:** Remove sensitive satellite images from public
      PDFs generated from Word.'
  type: HowTo
- questions:
  - answer: Yes, iterate over each picture node and call `ImageAreaRedaction` for
      every region you need to hide.
    question: Can I redact multiple pictures in one pass?
  - answer: Absolutely. Provide the password when constructing the `Redactor` object,
      and the library will open the document securely.
    question: Does GroupDocs.Redaction support password‑protected Word files?
  - answer: The API handles DOC, DOCX, RTF, HTML, PDF, and over 20 other formats,
      allowing you to build a universal redaction service.
    question: What file formats can I process besides DOCX?
  - answer: Use a temporary license from the GroupDocs portal; it enables full functionality
      for 30 days without watermarks.
    question: How do I test the redaction without a license?
  - answer: Visit the [GroupDocs Free Support](https://forum.groupdocs.com/c/redaction/33)
      forum for community assistance or contact GroupDocs sales for enterprise support.
    question: Where can I get help if I run into problems?
  type: FAQPage
tags:
- redact images
- GroupDocs.Redaction
- .NET document security
title: วิธีใช้ GroupDocs เพื่อลบข้อมูลบนรูปภาพใน Word ด้วย .NET
type: docs
url: /th/net/image-redaction/redact-embedded-images-groupdocs-redaction-net/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ GroupDocs เพื่อลบข้อมูลรูปภาพใน Word ด้วย .NET

## คำตอบสั้น
- **GroupDocs สามารถลบข้อมูลรูปภาพทั้งหมดโดยอัตโนมัติได้หรือไม่?** ใช่, คุณสามารถวนลูปผ่านแต่ละรูปภาพและใช้ `ImageAreaRedaction`.
- **เวอร์ชัน .NET ที่รองรับคืออะไร?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
- **ฉันต้องมีลิขสิทธิ์สำหรับการพัฒนาหรือไม่?** การทดลองใช้ฟรีทำงานสำหรับการทดสอบ; จำเป็นต้องมีลิขสิทธิ์ถาวรสำหรับการใช้งานจริง.
- **รูปแบบต้นฉบับจะถูกเก็บไว้หรือไม่?** API จะคงข้อความและการจัดรูปแบบไว้ในขณะที่ลบพื้นที่รูปภาพ.
- **กระบวนการทำงานเร็วแค่ไหน?** GroupDocs.Redaction สามารถประมวลผลเอกสาร 200 หน้าในเวลาน้อยกว่า 2 วินาทีบนเซิร์ฟเวอร์ทั่วไป.

## GroupDocs.Redaction คืออะไร?
GroupDocs.Redaction เป็นไลบรารี .NET ที่ช่วยให้สามารถลบข้อมูลข้อความ, รูปภาพ, และเมตาดาต้าแบบโปรแกรมได้ในรูปแบบเอกสารกว่า 20 แบบ มันประมวลผลไฟล์โดยไม่ต้องติดตั้ง Microsoft Office ทำให้เหมาะสำหรับการทำงานอัตโนมัติบนเซิร์ฟเวอร์ มี API สำหรับการลบข้อความ, รูปภาพ, และเมตาดาต้า พร้อมรองรับการประมวลผลเป็นชุด, แพทเทิร์นการลบแบบกำหนดเอง, และการรายงานการปฏิบัติตามมาตรฐาน.

## ทำไมต้องใช้ GroupDocs สำหรับการลบข้อมูลรูปภาพใน Word?
ไลบรารีรองรับ **รูปแบบเข้าและออกกว่า 20 แบบ** และสามารถลบรูปภาพในเอกสารขนาดสูงสุด 500 MB โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ อัลกอริธึม `ImageAreaRedaction` ในตัวรับประกันว่าพื้นที่ที่ลบจะไม่สามารถกู้คืนได้ ตรงตามมาตรฐานการปฏิบัติตามที่เข้มงวด.

## ข้อกำหนดเบื้องต้น
- .NET Framework 4.5+ **หรือ** .NET Core 3.1+ ที่ติดตั้งแล้ว.
- ความรู้พื้นฐานของ C# และความคุ้นเคยกับโครงสร้างไฟล์ Word.
- เข้าถึงแพ็กเกจ **GroupDocs.Redaction** จาก NuGet (ทดลองใช้ฟรีหรือมีลิขสิทธิ์).

## วิธีตั้งค่า GroupDocs.Redaction สำหรับ .NET

### วิธีติดตั้ง GroupDocs.Redaction ผ่าน .NET CLI?
รันคำสั่งต่อไปนี้ในโฟลเดอร์โปรเจกต์ของคุณ: `dotnet add package GroupDocs.Redaction`. คำสั่งนี้จะเพิ่มเวอร์ชันล่าสุดที่เสถียรลงในไฟล์โปรเจกต์ของคุณ.

```bash
dotnet add package GroupDocs.Redaction
```

### วิธีติดตั้ง GroupDocs.Redaction โดยใช้ Package Manager?
ดำเนินการ `Install-Package GroupDocs.Redaction` ใน Package Manager Console.

```powershell
Install-Package GroupDocs.Redaction
```

### วิธีขอและใช้ใบอนุญาตชั่วคราว?
คุณสามารถขอใบอนุญาตชั่วคราวจากหน้า [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)  
ใบอนุญาตชั่วคราวช่วยให้คุณประเมินฟีเจอร์เต็มชุดโดยไม่มีลายน้ำ หลังจากซื้อแล้ว ให้วางไฟล์ลิขสิทธิ์ในโปรเจกต์ของคุณและโหลดตามที่แสดงด้านล่าง:

```csharp
using GroupDocs.Redaction;
```

## วิธีลบข้อมูลรูปภาพที่ฝังอยู่ในเอกสาร Word?

เพื่อทำการลบรูปภาพ คุณต้องโหลดเอกสารด้วยอ็อบเจ็กต์ Redactor, ค้นหารูปภาพแต่ละภาพ, กำหนดพื้นที่ที่ต้องการซ่อน, แล้วเรียกใช้ ImageAreaRedaction. API จะเขียนทับพิกเซลที่เลือก ทำให้เนื้อหาภาพต้นฉบับไม่สามารถกู้คืนได้ พร้อมคงการจัดรูปแบบและข้อความโดยรอบไว้.

### วิธีเตรียมเส้นทางต้นทางและผลลัพธ์?
กำหนดเส้นทางแบบ absolute สำหรับเอกสารต้นฉบับและผลลัพธ์ที่ลบข้อมูลก่อนสร้างอ็อบเจ็กต์ใด ๆ.

```csharp
string sourceFile = "YOUR_DOCUMENT_DIRECTORY/LOREMIPSUM_PDF";
string outputFile = "YOUR_OUTPUT_DIRECTORY/redacted_output.docx";
```

### วิธีสร้างและกำหนดค่าอ็อบเจ็กต์ Redactor?
Redactor เป็นคลาสหลักที่โหลดเอกสารและทำการลบข้อมูล.  
สร้างอินสแตนซ์ของ `Redactor` ด้วยเอกสารของคุณ:

```csharp
using (Redactor redactor = new Redactor(sourceFile))
{
    // Code for redaction will go here
}
```

### วิธีระบุพิกัดและใช้การลบข้อมูลพื้นที่รูปภาพ?
ImageAreaRedaction เป็นเมธอดที่ทำการปิดบังพื้นที่สี่เหลี่ยมของรูปภาพด้วยสีทึบ.  
ระบุจุดบนซ้าย (`samplePoint`) และขนาด (`sampleSize`) ของพื้นที่ที่ต้องการซ่อน แล้วเรียก `ImageAreaRedaction`. เมธอดนี้จะเขียนทับพิกเซลที่เลือกด้วยสีทึบ.

```csharp
Point samplePoint = new Point(516, 311);
Size sampleSize = new Size(170, 35);

RedactorChangeLog result = redactor.Apply(new ImageAreaRedaction(
    samplePoint,
    new RegionReplacementOptions(Color.Blue, sampleSize)
));
```

### วิธีตรวจสอบผลลัพธ์การลบข้อมูลและบันทึกไฟล์?
หลังจากเรียก `Redactor.Apply()` ให้ตรวจสอบอ็อบเจ็กต์ `Result`. หาก `IsSuccess` เป็น true ให้เขียนเอกสารที่แก้ไขแล้วไปยังเส้นทางผลลัพธ์.

```csharp
if (result.Status != RedactionStatus.Failed)
{
    var savedOutputFile = redactor.Save();
    Console.WriteLine($"Redacted document saved as: {savedOutputFile}");
}
```

## ปัญหาทั่วไปและเคล็ดลับการแก้ไข
- **ข้อผิดพลาดพิกัด:** ตรวจสอบให้แน่ใจว่าค่า X/Y อยู่ภายในขอบเขตของรูปภาพ; มิฉะนั้น API จะโยน `ArgumentOutOfRangeException`.
- **ขาดลิขสิทธิ์:** ลิขสิทธิ์ทดลองหมดอายุหลัง 30 วัน; เปลี่ยนเป็นลิขสิทธิ์ถาวรเพื่อหลีกเลี่ยงความล้มเหลวขณะรัน.
- **รูปแบบไม่รองรับ:** ตรวจสอบให้แน่ใจว่าไฟล์มีนามสกุลอยู่ใน 20+ รูปแบบที่ระบุในเอกสาร; ไฟล์ `.doc` เก่าอาจต้องแปลงเป็น `.docx` ก่อน.

## การใช้งานจริง

1. **รายงานลับ:** ลบโลโก้หรือแผนภูมิก่อนแจกจ่ายภายนอก.
2. **สรุปคดี:** ซ่อนภาพถ่ายของลูกค้าหรือบัตรประจำตัวสแกนที่มีข้อมูลส่วนบุคคล.
3. **สัญญาธุรกิจ:** ปิดบังแผนภาพที่เป็นความลับของบริษัท.
4. **การเผยแพร่ของรัฐบาล:** ลบภาพถ่ายดาวเทียมที่ละเอียดอ่อนจาก PDF สาธารณะที่สร้างจาก Word.

## ข้อควรพิจารณาด้านประสิทธิภาพ
- ประมวลผลเอกสารแบบต่อเนื่องเมื่อจัดการชุดใหญ่เพื่อรักษาการใช้หน่วยความจำให้ต่ำ.
- ใช้ `RedactorOptions` เพื่อลดจำนวนเธรดหากทำงานบนเซิร์ฟเวอร์ที่มีข้อจำกัด.
- ปิดการใช้งานอินสแตนซ์ `Redactor` อย่างเร็วโดยใช้ `using` เพื่อปล่อยทรัพยากรที่ไม่ได้จัดการ.

## สรุป
คุณได้เรียนรู้ **วิธีใช้ GroupDocs** เพื่อทำการลบรูปภาพที่ฝังอยู่ในไฟล์ Word อย่างมั่นใจด้วย .NET API. ด้วยขั้นตอนข้างต้น คุณสามารถฝังความสามารถนี้ลงในไพรพลไลน์การประมวลผลเอกสารใด ๆ เพื่อให้ภาพลับไม่ออกจากองค์กรของคุณ.

สำหรับการสำรวจเพิ่มเติม ลองทดลองประเภทการลบอื่น ๆ (ข้อความ, เมตาดาต้า) และรวมไลบรารีเข้ากับเว็บเซอร์วิส, งานเบื้องหลัง, หรือ Azure Functions.

## คำถามที่พบบ่อย

**Q: ฉันสามารถลบข้อมูลรูปภาพหลายรูปในหนึ่งรอบได้หรือไม่?**  
A: ใช่, วนลูปผ่านแต่ละโหนดรูปภาพและเรียก `ImageAreaRedaction` สำหรับทุกพื้นที่ที่ต้องการซ่อน.

**Q: GroupDocs.Redaction รองรับไฟล์ Word ที่มีการป้องกันด้วยรหัสผ่านหรือไม่?**  
A: แน่นอน. ให้รหัสผ่านเมื่อสร้างอ็อบเจ็กต์ `Redactor` แล้วไลบรารีจะเปิดเอกสารอย่างปลอดภัย.

**Q: ฟอร์แมตไฟล์ใดบ้างที่ฉันสามารถประมวลผลได้นอกจาก DOCX?**  
A: API รองรับ DOC, DOCX, RTF, HTML, PDF, และรูปแบบอื่น ๆ มากกว่า 20 แบบ ทำให้คุณสร้างบริการลบข้อมูลสากลได้.

**Q: ฉันจะทดสอบการลบข้อมูลโดยไม่มีลิขสิทธิ์ได้อย่างไร?**  
A: ใช้ใบอนุญาตชั่วคราวจากพอร์ทัล GroupDocs; มันเปิดใช้งานฟังก์ชันเต็มรูปแบบเป็นเวลา 30 วันโดยไม่มีลายน้ำ.

**Q: ฉันจะขอความช่วยเหลือได้จากที่ไหนหากเจอปัญหา?**  
A: เยี่ยมชมฟอรั่ม [การสนับสนุนฟรีของ GroupDocs](https://forum.groupdocs.com/c/redaction/33) เพื่อรับความช่วยเหลือจากชุมชนหรือ ติดต่อฝ่ายขายของ GroupDocs สำหรับการสนับสนุนระดับองค์กร.

## แหล่งข้อมูลเพิ่มเติม

- **เอกสารการใช้งาน:** [GroupDocs Redaction Documentation](https://docs.groupdocs.com/redaction/net/)
- **อ้างอิง API:** [GroupDocs API Reference](https://reference.groupdocs.com/redaction/net)
- **ดาวน์โหลด:** [Latest Releases](https://releases.groupdocs.com/redaction/net/)

---

**Last Updated:** 2026-10-16  
**Tested with:** GroupDocs.Redaction 23.12 for .NET  
**Author:** GroupDocs

## บทเรียนที่เกี่ยวข้อง

- [วิธีลบข้อมูลเอกสารด้วย GroupDocs.Redaction .NET – คู่มือเต็ม](/redaction/net/document-loading/groupdocs-redaction-net-load-redact-documents/)
- [ลบและบันทึกเอกสาร Groupdocs Redaction Net](/redaction/net/document-saving/redact-save-documents-groupdocs-redaction-net/)
- [การลบข้อความที่ตรงตามกรณีอักษรด้วย GroupDocs.Redaction .NET เพื่อความปลอดภัยของเอกสาร](/redaction/net/text-redaction/groupdocs-redaction-net-case-sensitive-exact-phrase-redaction/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}