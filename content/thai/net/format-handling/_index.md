---
date: 2026-07-15
description: เรียนรู้วิธีสร้างตัวจัดการการลบข้อมูลส่วนบุคคลแบบกำหนดเองและเพิ่มการสนับสนุนรูปแบบไฟล์ใหม่โดยใช้
  GroupDocs.Redaction สำหรับ .NET
keywords:
- create custom redaction handler
- add new file format
- GroupDocs.Redaction format handling
lastmod: 2026-07-15
og_description: สร้างตัวจัดการการลบข้อมูลส่วนบุคคลแบบกำหนดเองและเพิ่มการสนับสนุนรูปแบบไฟล์ใหม่ด้วย
  GroupDocs.Redaction สำหรับ .NET ค้นหาคู่มือขั้นตอนโดยขั้นตอนสำหรับการขยายการจัดการรูปแบบ
og_image_alt: Guide to creating a custom redaction handler in GroupDocs.Redaction
  for .NET
og_title: สร้างตัวจัดการการลบข้อมูลส่วนบุคคลแบบกำหนดเอง – GroupDocs.Redaction .NET
schemas:
- author: GroupDocs
  dateModified: '2026-07-15'
  description: Learn how to create custom redaction handler and add new file format
    support using GroupDocs.Redaction for .NET.
  headline: Create Custom Redaction Handler in GroupDocs.Redaction .NET
  type: TechArticle
tags:
- redaction handler
- GroupDocs.Redaction
- .NET document processing
- custom format extension
title: สร้างตัวจัดการการลบข้อมูลส่วนบุคคลแบบกำหนดเองใน GroupDocs.Redaction .NET
type: docs
url: /th/net/format-handling/
weight: 14
---

# สร้างตัวจัดการการทำลายข้อมูลแบบกำหนดเองใน GroupDocs.Redaction .NET

Extend GroupDocs.Redaction capabilities with our format handling tutorials for .NET developers. In this hub you’ll learn how to **create custom redaction handler** and **add new file format** support, work with plain‑text documents, and programmatically handle diverse document types. These guides include ready‑to‑run C# examples, so you can quickly broaden the range of files your application can secure.

## ภาพรวมโดยสังเขป

- **สิ่งที่คุณจะได้รับ:** ความสามารถในการทำลายข้อมูลประเภทกำหนดเองและสนับสนุนส่วนขยายไฟล์เพิ่มเติมโดยไม่ต้องรอการอัปเดตของผลิตภัณฑ์.  
- **ผู้ที่เหมาะสม:** นักพัฒนา .NET ที่สร้างโซลูชันที่เน้นเอกสารและต้องการการควบคุมความเป็นส่วนตัวอย่างเข้มงวด.  
- **ข้อกำหนดเบื้องต้น:** .NET 6+ (หรือ .NET Framework 4.7.2+), ใบอนุญาต GroupDocs.Redaction ที่ถูกต้อง, และความรู้พื้นฐานของ C#.  

## ตัวจัดการการทำลายข้อมูลแบบกำหนดเองคืออะไร?

**ตัวจัดการการทำลายข้อมูลแบบกำหนดเอง** คือส่วนประกอบที่ผู้ใช้กำหนดซึ่งบอกให้ GroupDocs.Redaction รู้ว่าจะค้นหา, แปลความหมาย, และทำลายข้อมูลที่ไม่ได้อยู่ในรูปแบบที่กำหนดไว้ล่วงหน้าอย่างไร การนำตัวจัดการนี้ไปใช้ทำให้คุณควบคุมรูปแบบข้อมูลที่เป็นกรรมสิทธิ์หรือรหัสประจำธุรกิจที่ไม่ซ้ำใครได้อย่างเต็มที่.

## วิธีสร้างตัวจัดการการทำลายข้อมูลแบบกำหนดเอง?

**IRedactionHandler** คืออินเทอร์เฟซที่กำหนดสัญญาสำหรับตรรกะการทำลายข้อมูลแบบกำหนดเอง.  
**Redactor** คือคลาสหลักที่จัดการการดำเนินการทำลายข้อมูล.  
**AddHandler** ลงทะเบียนตัวจัดการแบบกำหนดเองกับอินสแตนซ์ของ Redactor.  
**Redact** ดำเนินการทำลายข้อมูลตามตัวจัดการที่กำหนดค่าไว้.  

โหลดเอนจินการทำลายข้อมูล, ลงทะเบียนตัวจัดการของคุณ, และเรียกกระบวนการทำลายข้อมูล – ทั้งหมดในสามขั้นตอนสั้น ๆ ขั้นแรก, ทำการนำอินเทอร์เฟซ `IRedactionHandler` ไปใช้งานด้วยตรรกะที่สแกนเอกสารเพื่อค้นหาโทเค็นแบบกำหนดของคุณ. จากนั้นเพิ่มตัวจัดการลงในอินสแตนซ์ `Redactor` ผ่าน `AddHandler`. สุดท้ายเรียก `Redact` เพื่อใช้การเปลี่ยนแปลง. แพทเทิร์นนี้ทำงานกับ PDF, รูปภาพ, และรูปแบบที่สนับสนุนใด ๆ ทำให้คุณสามารถปกป้องข้อมูลที่รูปแบบมาตรฐานไม่สามารถตรวจจับได้.

## วิธีเพิ่มรูปแบบไฟล์ใหม่?

**SupportedFormats** คือคอลเลกชันที่เก็บส่วนขยายไฟล์ที่เอนจินการทำลายข้อมูลรับรู้. ลงทะเบียนส่วนขยายไฟล์ใหม่กับเอนจินการทำลายข้อมูลโดยขยายคอลเลกชัน `SupportedFormats` ให้ตัวแปลงที่แปลงไฟล์ที่เข้ามาเป็นรูปแบบที่ GroupDocs.Redaction สามารถประมวลผลได้, แล้วแมปส่วนขยายนั้นกับตัวแปลงของคุณ. เมื่อทำการลงทะเบียนแล้ว, เอนจินจะปฏิบัติต่อรูปแบบใหม่เหมือนกับประเภทพื้นฐานใด ๆ ทำให้การทำลายข้อมูลทำได้อย่างราบรื่นทั่วทั้งระบบ.

## ทำไมต้องใช้ GroupDocs.Redaction สำหรับการจัดการรูปแบบแบบกำหนดเอง?

GroupDocs.Redaction รองรับ **รูปแบบการนำเข้าและส่งออกกว่า 70 รูปแบบ** และสามารถประมวลผลไฟล์ขนาดสูงสุด **2 GB** โดยไม่ต้องโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ, ให้การทำลายข้อมูลที่มีอัตราการประมวลผลสูงในสภาพแวดล้อมองค์กร. สถาปัตยกรรมที่ขยายได้ของมันทำให้คุณสามารถเชื่อมต่อตัวจัดการแบบกำหนดเองได้ภายในไม่เกิน 30 นาที, ลดเวลาการพัฒนาและขจัดความจำเป็นในการใช้เครื่องมือการเตรียมข้อมูลของบุคคลที่สาม.

## คำแนะนำที่พร้อมใช้งาน

### [ขยายประเภทไฟล์ใน GroupDocs.Redaction .NET: คู่มือขั้นตอนต่อขั้นตอนสำหรับส่วนขยายแบบกำหนดเอง](./extend-groupdocs-redaction-net-custom-extensions/)
Learn how to extend supported file types with custom extensions using GroupDocs.Redaction for .NET, ensuring secure document redaction across diverse formats.

### [การทำรายการรูปแบบไฟล์ที่สนับสนุนด้วย GroupDocs.Redaction .NET](./groupdocs-redaction-net-supported-formats-listing/)
Learn how to use GroupDocs.Redaction .NET to list supported file formats, streamline document management systems, and optimize performance.

## แหล่งข้อมูลเพิ่มเติม

- [เอกสาร GroupDocs.Redaction สำหรับ .NET](https://docs.groupdocs.com/redaction/net/)
- [อ้างอิง API ของ GroupDocs.Redaction สำหรับ .NET](https://reference.groupdocs.com/redaction/net/)
- [ดาวน์โหลด GroupDocs.Redaction สำหรับ .NET](https://releases.groupdocs.com/redaction/net/)
- [ฟอรั่ม GroupDocs.Redaction](https://forum.groupdocs.com/c/redaction/33)
- [สนับสนุนฟรี](https://forum.groupdocs.com/)
- [ใบอนุญาตชั่วคราว](https://purchase.groupdocs.com/temporary-license/)

---

**อัปเดตล่าสุด:** 2026-07-15  
**ทดสอบด้วย:** GroupDocs.Redaction 23.12 for .NET  
**ผู้เขียน:** GroupDocs

## คำแนะนำที่เกี่ยวข้อง

- [ขยายประเภทไฟล์ใน GroupDocs.Redaction .NET: คู่มือขั้นตอนต่อขั้นตอนสำหรับส่วนขยายแบบกำหนดเอง](/redaction/net/format-handling/extend-groupdocs-redaction-net-custom-extensions/)
- [การทำรายการรูปแบบไฟล์ที่สนับสนุนด้วย GroupDocs.Redaction .NET](/redaction/net/format-handling/groupdocs-redaction-net-supported-formats-listing/)
- [คำแนะนำการจัดการรูปแบบสำหรับ GroupDocs.Redaction .NET](/redaction/net/format-handling/)