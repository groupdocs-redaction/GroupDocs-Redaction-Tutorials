---
date: '2026-03-30'
description: เรียนรู้วิธีสร้างนโยบายการลบข้อมูลใน .NET ด้วย GroupDocs.Redaction บทเรียนนี้จะแสดงให้คุณเห็นวิธีสร้าง
  ใช้งาน และบันทึกนโยบายการลบข้อมูลเป็นไฟล์ XML.
keywords:
- GroupDocs.Redaction .NET
- create redaction policy
- save XML policy
title: สร้างนโยบายการลบข้อมูลด้วย GroupDocs.Redaction .NET – คู่มือแบบขั้นตอนต่อขั้นตอน
type: docs
url: /th/net/advanced-redaction/groupdocs-redaction-net-create-save-policy/
weight: 1
---

# วิธีสร้างนโยบายการลบข้อมูลโดยใช้ GroupDocs.Redaction .NET

ในแอปพลิเคชันสมัยใหม่ การปกป้องข้อมูลลับภายในเอกสารเป็นมาตรการด้านความปลอดภัยที่จำเป็น ไม่ว่าคุณจะจัดการสัญญา งบการเงิน หรือบันทึกผู้ป่วย คุณมักจะต้อง **create redaction policy** ที่ทำหน้าที่ซ่อนหรือเอาข้อมูลที่ละเอียดอ่อนออกโดยอัตโนมัติ ในคู่มือนี้เราจะพาคุณผ่านกระบวนการทั้งหมด—การติดตั้งไลบรารี การกำหนดการลบข้อมูล การประยุกต์ใช้ และสุดท้ายการบันทึกนโยบายเป็นไฟล์ XML ที่คุณสามารถใช้ซ้ำได้ในหลายโครงการ

## คำตอบสั้น
- **What does “create redaction policy” mean?** เป็นกระบวนการกำหนดกฎ (ข้อความ, regex, รูปภาพ, ฯลฯ) ที่บอกให้ GroupDocs.Redaction ซ่อนหรือแทนที่เนื้อหาลับ
- **ฉันต้องใช้ไลบรารีอะไร?** GroupDocs.Redaction for .NET (available via NuGet).
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีสามารถใช้งานได้สำหรับการพัฒนา; จำเป็นต้องมีไลเซนส์ถาวรสำหรับการใช้งานจริง.
- **ฉันสามารถใช้ซ้ำนโยบายได้หรือไม่?** ได้—เมื่อบันทึกเป็น XML แล้วคุณสามารถโหลดในภายหลังและประยุกต์ใช้กับเอกสารใดก็ได้.
- **เวอร์ชัน .NET ที่รองรับคืออะไร?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## นโยบายการลบข้อมูลคืออะไร?

นโยบายการลบข้อมูลคือชุดของกฎที่ระบุว่า *อะไร* ควรถูกลบหรือแทนที่และ *อย่างไร* การแทนที่จะเป็นอย่างไร การสร้างนโยบายครั้งเดียวทำให้คุณสามารถใช้มาตรฐานความปลอดภัยที่สอดคล้องกันกับทุกเอกสารที่แอปพลิเคชันของคุณประมวลผล

## ทำไมต้องใช้ GroupDocs.Redaction เพื่อสร้างนโยบายการลบข้อมูล?

- **Full‑document format support** – รองรับรูปแบบเอกสารทั้งหมด – Word, PDF, Excel, PowerPoint, and many more.  
- **Programmatic control** – การควบคุมแบบโปรแกรม – Define exact phrases, regular expressions, or even custom logic.  
- **Reusable XML policies** – นโยบาย XML ที่ใช้ซ้ำได้ – Export your rules once and share them across teams or services.  
- **Performance‑optimized engine** – เครื่องยนต์ที่ปรับประสิทธิภาพการทำงาน – Handles large files efficiently and scales with your workload.

## ข้อกำหนดเบื้องต้น

- **GroupDocs.Redaction** library (compatible with your .NET runtime).  
- Visual Studio, VS Code, or any IDE that supports C#.  
- ความคุ้นเคยพื้นฐานกับ C# และโครงสร้างโครงการ .NET

## การตั้งค่า GroupDocs.Redaction สำหรับ .NET

ขั้นแรก ให้เพิ่มไลบรารีลงในโครงการของคุณ

**ใช้ .NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**ใช้ Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

หรือค้นหา “GroupDocs.Redaction” ใน UI ของ NuGet Package Manager แล้วติดตั้งจากที่นั่น

### การรับไลเซนส์
- เริ่มต้นด้วย **free trial** เพื่อสำรวจคุณลักษณะ.  
- ขอ **temporary license** สำหรับการทดสอบต่อเนื่อง แล้วซื้อไลเซนส์เต็มรูปแบบสำหรับการใช้งานจริง.

### การเริ่มต้นพื้นฐาน
เพิ่ม namespace ไปยังไฟล์ซอร์สของคุณ:  
```csharp
using GroupDocs.Redaction;
```

## วิธีสร้างนโยบายการลบข้อมูลโดยใช้ GroupDocs.Redaction .NET

ต่อไปนี้เป็นขั้นตอนแบบละเอียดที่แสดงวิธีสร้างและบันทึกนโยบายการลบข้อมูลอย่างแม่นยำ

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
อ็อบเจ็กต์ `Redactor` เปิดไฟล์และจัดการวงจรชีวิตของมัน

### ขั้นตอน 3: กำหนดการลบข้อมูล
```csharp
var redactions = new List<Redaction>
{
    new ExactPhraseRedaction("Sensitive Phrase", new ReplacementOptions("[REDACTED]")),
    new RegexRedaction(@"\d{4}-\d{2}-\d{2}", new ReplacementOptions("[DATE REDACTED]"))
};
```
ที่นี่เราสร้างกฎสองข้อ:
1. **ExactPhraseRedaction** – แทนที่วลีที่รู้จักด้วย “[REDACTED]”.  
2. **RegexRedaction** – ค้นหาวันที่ในรูปแบบ `YYYY‑MM‑DD` และแทนที่ด้วย “[DATE REDACTED]”.

### ขั้นตอน 4: ประยุกต์ใช้การลบข้อมูล
```csharp
redactor.Apply(redactions);
```
กฎทั้งหมดที่กำหนดจะถูกดำเนินการกับเอกสารที่เปิดอยู่ในหนึ่งรอบ

### ขั้นตอน 5: บันทึกนโยบายเป็นไฟล์ XML
```csharp
string policyFile = "policy.xml";
redactor.SavePolicy(policyFile, new SaveOptions());
```
ไฟล์ XML จะเก็บคำนิยามการลบข้อมูล ทำให้คุณสามารถใช้ซ้ำนโยบายเดียวกันโดยไม่ต้องเขียนโค้ดใหม่

## การประยุกต์ใช้งานจริง

- **Legal firms** สามารถลบหมายเลขคดีและชื่อลูกค้า ก่อนแชร์ร่างเอกสาร.  
- **Finance departments** ปิดบังหมายเลขบัญชีหรือวันที่ทำรายการในรายงาน.  
- **Healthcare providers** รับรองการปฏิบัติตาม HIPAA โดยลบตัวระบุผู้ป่วย.

## เคล็ดลับด้านประสิทธิภาพ

- เปิด **one document at a time** เพื่อรักษาการใช้หน่วยความจำให้ต่ำ.  
- เขียน **efficient regular expressions**; หลีกเลี่ยงแพทเทิร์นที่กว้างเกินไปซึ่งทำให้เวลาในการประมวลผลเพิ่มขึ้น.  
- รักษาไลบรารีให้ **up‑to‑date** เพื่อรับประโยชน์จากการปรับปรุงประสิทธิภาพและประเภทการลบข้อมูลใหม่

## ปัญหาทั่วไปและวิธีแก้

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|----------|
| **ข้อยกเว้น IO เมื่อเตรียมไดเรกทอรี** | เส้นทางผิดหรือไม่มีสิทธิ์การเขียน | ตรวจสอบว่าโฟลเดอร์มีอยู่และแอปพลิเคชันมีสิทธิ์อ่าน/เขียน |
| **Regex ไม่ตรงกับข้อความที่คาดหวัง** | แพทเทิร์นเข้มงวดเกินไปหรือขาดอักขระ escape | ทดสอบ regex ด้วยเครื่องมือออนไลน์; ปรับ quantifiers หรือ escape อักขระพิเศษ |
| **ไฟล์นโยบายไม่ถูกสร้าง** | `SavePolicy` ถูกเรียกก่อนการประยุกต์การลบข้อมูลหรือใช้เส้นทางที่ไม่ถูกต้อง | ตรวจสอบว่าไดเรกทอรีผลลัพธ์สามารถเขียนได้และเรียก `SavePolicy` หลังจาก `Apply` |

## คำถามที่พบบ่อย

**Q: ฉันสามารถโหลดนโยบาย XML ที่มีอยู่แล้วแทนการสร้างด้วยโปรแกรมได้หรือไม่?**  
A: ได้—ใช้ `redactor.LoadPolicy("policy.xml")` เพื่อนำเข้านโยบายที่บันทึกไว้ก่อนหน้า

**Q: GroupDocs.Redaction รองรับ PDF ที่ป้องกันด้วยรหัสผ่านหรือไม่?**  
A: แน่นอน. ส่งรหัสผ่านไปยังคอนสตรัคเตอร์ของ `Redactor`: `new Redactor(sourceFile, "password")`.

**Q: สามารถลบรูปภาพหรือเมตาดาต้าได้หรือไม่?**  
A: ไลบรารีมีคลาส `ImageRedaction` และ `MetadataRedaction` สำหรับสถานการณ์เหล่านั้น

**Q: ฉันจะจัดการกับเอกสารขนาดใหญ่ (หลายร้อย MB) อย่างไร?**  
A: ประมวลผลเป็นส่วน ๆ หรือใช้ streaming API เพื่อลดการใช้หน่วยความจำ; พิจารณาเพิ่มขนาด heap ของ JVM หากเจอข้อผิดพลาด OutOfMemory

**Q: ต้องใช้โมเดลไลเซนส์แบบใดสำหรับการใช้งานเชิงพาณิชย์?**  
A: จำเป็นต้องมีไลเซนส์แบบชำระเงินสำหรับการใช้งานจริง; ไลเซนส์ทดลองใช้ก็เพียงพอสำหรับการพัฒนาและทดสอบ

## สรุป

ตอนนี้คุณมี **redaction policy** ที่ครบถ้วนและสามารถใช้ซ้ำได้ ซึ่งคุณสามารถประยุกต์ใช้กับเอกสารใดก็ได้ด้วย GroupDocs.Redaction for .NET การส่งออกนโยบายเป็น XML ทำให้การอัปเดตในอนาคตง่ายขึ้นและรับประกันการปกป้องข้อมูลที่สอดคล้องกันทั่วทั้งองค์กร

### ขั้นตอนต่อไป
- ทดลองใช้ประเภทการลบข้อมูลเพิ่มเติมเช่น `ImageRedaction` หรือ `MetadataRedaction`.  
- ผสานตรรกะการโหลดนโยบายเข้ากับเวิร์กโฟลว์การจัดการเอกสารของคุณเพื่อการลบข้อมูลอัตโนมัติ.  
- สำรวจ **GroupDocs.Redaction** API reference เพื่อการปรับแต่งขั้นสูง.

---

**Last Updated:** 2026-03-30  
**Tested With:** GroupDocs.Redaction 5.8 for .NET  
**Author:** GroupDocs  

**Resources**  
- [Documentation](https://docs.groupdocs.com/redaction/net/)  
- [API Reference](https://reference.groupdocs.com/redaction/net)  
- [Download](https://releases.groupdocs.com/redaction/net/)  
- [Free Support Forum](https://forum.groupdocs.com/c/redaction/33)  
- [Temporary License Application](https://purchase.groupdocs.com/temporary-license/)