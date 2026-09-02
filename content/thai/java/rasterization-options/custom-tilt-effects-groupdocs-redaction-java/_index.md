---
date: '2026-06-01'
description: เรียนรู้วิธีใช้เอฟเฟกต์การเอียงกับ GroupDocs.Redaction สำหรับ Java รวมถึงโค้ดขั้นตอนต่อขั้นตอน
  เคล็ดลับการเพิ่มประสิทธิภาพ และตัวเลือกการปรับแต่ง
keywords:
- how to use tilt
- custom tilt effects
- GroupDocs.Redaction Java
- document rasterization
schemas:
- author: GroupDocs
  dateModified: '2026-06-01'
  description: Learn how to use tilt effect with GroupDocs.Redaction for Java, including
    step‑by‑step code, performance tips, and customization options.
  headline: How to Use Tilt Effect with GroupDocs.Redaction Java
  type: TechArticle
- description: Learn how to use tilt effect with GroupDocs.Redaction for Java, including
    step‑by‑step code, performance tips, and customization options.
  name: How to Use Tilt Effect with GroupDocs.Redaction Java
  steps:
  - name: Initialize Redactor and Save Options
    text: First, create a `Redactor` instance pointing at your source file, then prepare
      `SaveOptions` that will hold the rasterization configuration.
  - name: Configure Tilt Effect Settings
    text: Enable rasterization and define the tilt angle boundaries. The `AdvancedRasterizationOptions.Tilt`
      object lets you set `minAngle` and `maxAngle` in degrees, controlling how much
      each page can rotate.
  - name: Save Document with Tilt Effect
    text: Run the redaction process and output the rasterized, tilted document. The
      `save` call writes each page as an image (PNG by default) while applying the
      random tilt you specified.
  type: HowTo
- questions:
  - answer: It redacts sensitive content while preserving document layout and also
      supports advanced rasterization features like the tilt effect.
    question: What is GroupDocs.Redaction Java used for?
  - answer: By enabling rasterization and adding the `Tilt` advanced option with `minAngle`
      and `maxAngle` parameters, as shown in the code samples.
    question: How do I apply a tilt effect in my document using GroupDocs?
  - answer: Yes, a free trial is available. For production use, obtain a temporary
      or permanent license.
    question: Can I use GroupDocs.Redaction for free?
  - answer: It enhances visual appeal, adds a creative touch, and can help differentiate
      marketing or presentation materials.
    question: What are the benefits of using a tilt effect in documents?
  - answer: Very large files may increase processing time and memory usage; proper
      resource allocation mitigates this.
    question: Are there any limitations to applying custom effects with GroupDocs.Redaction
      Java?
  type: FAQPage
title: วิธีใช้เอฟเฟกต์การเอียงกับ GroupDocs.Redaction Java
type: docs
url: /th/java/rasterization-options/custom-tilt-effects-groupdocs-redaction-java/
weight: 1
---

# วิธีใช้เอฟเฟกต์การเอียงกับ GroupDocs.Redaction Java

ในบทแนะนำนี้คุณจะได้ค้นพบ **วิธีใช้เอฟเฟกต์การเอียง** เพื่อให้เอกสารที่แปลงเป็นภาพของคุณดูมีความเคลื่อนไหวและเหมือนถือด้วยมือ เหตุผลที่เอฟเฟกต์นี้สำคัญต่อการนำเสนอสมัยใหม่ และการตั้งค่าที่คุณต้องใช้ใน GroupDocs.Redaction สำหรับ Java อย่างละเอียด เราจะเดินผ่านกระบวนการทั้งหมด — ตั้งแต่การติดตั้งไลบรารีจนถึงการปรับแต่งประสิทธิภาพ — เพื่อให้คุณสามารถใช้เอฟเฟกต์การเอียงได้อย่างมั่นใจในโครงการจริง

## คำตอบสั้น
- **เอฟเฟกต์การเอียงทำอะไร?** มันจะหมุนแต่ละหน้าที่แปลงเป็นภาพโดยมุมสุ่มภายในช่วงที่กำหนด ทำให้ได้ลุคที่เคลื่อนไหวและเล็กน้อยเอียง  
- **ไลบรารีใดให้ฟีเจอร์นี้?** GroupDocs.Redaction for Java (version 24.9 or newer)  
- **ฉันต้องการไลเซนส์หรือไม่?** การทดลองใช้ฟรีทำงานสำหรับการประเมิน; จำเป็นต้องมีไลเซนส์ถาวรหรือชั่วคราวสำหรับการใช้งานจริง  
- **มันใช้หน่วยความจำมากหรือไม่?** มันเพิ่มภาระงานของ CPU เล็กน้อย แต่การตั้งค่าหน่วยความจำที่เหมาะสมทำให้มีประสิทธิภาพแม้กับไฟล์ขนาดใหญ่  
- **ฉันสามารถปรับช่วงมุมได้หรือไม่?** ได้ – ใช้พารามิเตอร์ `minAngle` และ `maxAngle` ในตัวเลือกการแปลงเป็นภาพ  

## เอฟเฟกต์การเอียงแบบกำหนดเองคืออะไร?
เอฟเฟกต์การเอียงแบบกำหนดเองคือการแปลงภาพที่ใช้ระหว่างการแปลงแต่ละหน้าของเอกสารเป็นภาพ โดยการระบุมุมขั้นต่ำและสูงสุด ตัวแปลงภาพจะเอียงหน้าตามมุมสุ่ม ทำให้ผลลัพธ์สุดท้ายดูศิลปะและมีความรู้สึก “ถือด้วยมือ” เอฟเฟกต์นี้มีประโยชน์เป็นพิเศษเมื่อคุณต้องการทำลายลุคที่ตึงและจัดเรียงอย่างสมบูรณ์ของ PDF มาตรฐานและเพิ่มสัมผัสของบุคลิกภาพ

## ทำไมต้องใช้เอฟเฟกต์การเอียงแบบกำหนดเองกับ GroupDocs.Redaction?
GroupDocs.Redaction รองรับการแปลงเป็นภาพสำหรับ **รูปแบบอินพุตและเอาต์พุตกว่า 70** และสามารถประมวลผล PDF ได้ถึง **2,000 หน้า** โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ การใช้ตัวเลือกการเอียงที่มีในตัวหมายความว่าคุณหลีกเลี่ยงไลบรารีภาพของบุคคลที่สาม ลดความซับซ้อนของการผสานรวม และทำให้กระบวนการทำงานทั้งหมดอยู่ใน SDK เดียวที่ผ่านการทดสอบอย่างดี  

- **การดึงดูด:** หน้าเอียงจะดึงความสนใจของผู้อ่าน เหมาะสำหรับการนำเสนอหรือโบรชัวร์การตลาด  
- **แบรนด์:** เพิ่มลายเซ็นภาพที่เป็นเอกลักษณ์โดยไม่เปลี่ยนแปลงเนื้อหาเดิม  
- **ความยืดหยุ่น:** คุณควบคุมช่วงมุมได้ ทำให้สามารถเอียงแบบละเอียดหรือเด่นชัด  
- **การผสานรวม:** เอฟเฟกต์นี้ฝังอยู่ในกระบวนการแปลงภาพของ GroupDocs.Redaction จึงไม่ต้องใช้เครื่องมือประมวลผลภาพภายนอก  

## ข้อกำหนดเบื้องต้น
- ติดตั้ง Java 8 หรือใหม่กว่า  
- Maven (หรือเครื่องมือสร้างอื่น) เพื่อจัดการ dependencies  
- GroupDocs.Redaction 24.9 หรือใหม่กว่า (บทแนะนำใช้เวอร์ชันล่าสุด)  
- มีความคุ้นเคยพื้นฐานกับการจัดการไฟล์ใน Java  

## การตั้งค่า GroupDocs.Redaction สำหรับ Java

### ข้อมูลการติดตั้ง

**Maven**

รวม GroupDocs.Redaction ในโปรเจกต์ Maven ของคุณโดยเพิ่ม repository และ dependency ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/redaction/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-redaction</artifactId>
      <version>24.9</version>
   </dependency>
</dependencies>
```

**Direct Download**

หรือคุณสามารถดาวน์โหลดเวอร์ชันล่าสุดโดยตรงจาก [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

#### การรับไลเซนส์

เพื่อใช้ GroupDocs.Redaction อย่างเต็มที่:
- **ทดลองใช้ฟรี** – สำรวจฟีเจอร์หลักโดยไม่มีค่าใช้จ่าย  
- **ไลเซนส์ชั่วคราว** – ขอคีย์ที่มีระยะเวลาจำกัดสำหรับการประเมินเต็มรูปแบบผ่าน [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- **ซื้อ** – รับไลเซนส์ถาวรสำหรับการใช้งานในสภาพแวดล้อมการผลิต  

### การเริ่มต้นและตั้งค่าพื้นฐาน

คลาส `Redactor` เป็นจุดเริ่มต้นสำหรับการดำเนินการลบข้อมูลและแปลงเป็นภาพทั้งหมดใน GroupDocs.Redaction มันจัดการการโหลดเอกสาร การประมวลผล และการบันทึก พร้อมรับประกันว่าทรัพยากรจะถูกปล่อยโดยอัตโนมัติ

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;

// Set the path to your document directory
String documentPath = "YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX";

// Initialize a Redactor with the specified document
Redactor redactor = new Redactor(documentPath);
```

## วิธีใช้เอฟเฟกต์การเอียงแบบกำหนดเองระหว่างการแปลงเป็นภาพ

โหลดไฟล์ต้นฉบับของคุณ, เปิดการแปลงเป็นภาพ, ตั้งค่าช่วงการเอียงที่ต้องการ, แล้วบันทึกเอกสารที่แปลงแล้ว — ทั้งหมดในไม่กี่ขั้นตอนสั้นๆ ภาพรวมนี้อธิบายกระบวนการทำงานทั้งหมด เพื่อให้คุณทราบว่าต้องสร้างอ็อบเจ็กต์ใด ตั้งค่าตัวเลือกใด และวิธีเรียกใช้การบันทึกก่อนที่จะดูโค้ดรายละเอียด

### การดำเนินการตามขั้นตอน

#### ขั้นตอนที่ 1: เริ่มต้น Redactor และ Save Options

แรกสุด สร้างอินสแตนซ์ `Redactor` ที่ชี้ไปยังไฟล์ต้นฉบับของคุณ แล้วเตรียม `SaveOptions` ที่จะเก็บการตั้งค่าการแปลงเป็นภาพ

```java
import com.groupdocs.redaction.options.AdvancedRasterizationOptions;
import java.util.HashMap;

Redactor redactor = new Redactor("YOUR_DOCUMENT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX");
SaveOptions saveOptions = new SaveOptions();
```

#### ขั้นตอนที่ 2: ตั้งค่าการเอียง

เปิดการแปลงเป็นภาพและกำหนดขอบเขตมุมการเอียง วัตถุ `AdvancedRasterizationOptions.Tilt` ให้คุณตั้งค่า `minAngle` และ `maxAngle` เป็นองศา เพื่อควบคุมการหมุนของแต่ละหน้า

```java
saveOptions.getRasterization().setEnabled(true);
HashMap<String, String> tiltSettings = new HashMap<>();
tiltSettings.put("minAngle", "15"); // Set the minimum angle for the tilt effect
	tiltSettings.put("maxAngle", "30"); // Set the maximum angle for the tilt effect

saveOptions.getRasterization().addAdvancedOption(
    AdvancedRasterizationOptions.Tilt, 
    tiltSettings
);
```

#### ขั้นตอนที่ 3: บันทึกเอกสารพร้อมเอฟเฟกต์การเอียง

ดำเนินการกระบวนการลบข้อมูลและส่งออกเอกสารที่แปลงเป็นภาพและเอียง `save` จะเขียนแต่ละหน้าเป็นภาพ (PNG เป็นค่าเริ่มต้น) พร้อมใช้การเอียงแบบสุ่มที่คุณระบุ

```java
redactor.save("OUTPUT_DIRECTORY/MULTIPAGE_SAMPLE_DOCX_scan", saveOptions);
```

### คำอธิบายพารามิเตอร์
- **minAngle** – การหมุนที่เล็กที่สุด (เป็นองศา) ที่สามารถนำไปใช้กับหน้าได้  
- **maxAngle** – การหมุนที่ใหญ่ที่สุด (เป็นองศา) ที่อนุญาต  
ปรับค่าต่างๆ เพื่อให้ได้การเอียงที่ละเอียดหรือเด่นชัด  

#### เคล็ดลับการแก้ไขปัญหา
- ตรวจสอบว่าไดเรกทอรีต้นฉบับและไดเรกทอรีผลลัพธ์สามารถเขียนได้โดย JVM  
- ยืนยันว่าคุณใช้ GroupDocs.Redaction 24.9 หรือใหม่กว่า; เวอร์ชันเก่าจะไม่มีตัวเลือก `Tilt`  
- หากผลลัพธ์ดูบิดเบี้ยวเกินไป ให้ลดค่าของ `maxAngle`  

## การประยุกต์ใช้งานจริง
1. **การนำเสนอเอกสารเชิงสร้างสรรค์** – เพิ่มลุคที่เคลื่อนไหวให้กับสไลด์เด็คหรือข้อเสนอให้ลูกค้า  
2. **สื่อการตลาด** – ทำให้โบรชัวร์และใบปลิวดูเหมือนทำด้วยมือมากขึ้น  
3. **คลังข้อมูลดิจิทัล** – ให้สแกนประวัติศาสตร์มีลักษณะสไตล์อ่อนโยนสำหรับการจัดแสดงออนไลน์  

## พิจารณาประสิทธิภาพ

### การเพิ่มประสิทธิภาพ
- **การจัดการหน่วยความจำ:** จัดสรรพื้นที่ heap เพียงพอ (`-Xmx2g` หรือมากกว่า) เมื่อประมวลผล PDF หลายหน้า  
- **ประสิทธิภาพ I/O:** ประมวลผลไฟล์เป็นชุดและใช้ `Redactor` อินสแตนซ์เดียวซ้ำได้เมื่อเป็นไปได้  

### แนวทางปฏิบัติที่ดีที่สุดสำหรับการจัดการหน่วยความจำใน Java
- เรียกใช้ `System.gc()` อย่างจำกัด; พึ่งพาตัวเก็บกวาดของ JVM  
- ปิดสตรีมโดยเร็ว (GroupDocs.Redaction จัดการทำความสะอาดส่วนใหญ่ภายใน)  

## ปัญหาทั่วไปและวิธีแก้

| ปัญหา | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|-------|-------------------|----------|
| เอฟเฟกต์การเอียงไม่ทำงาน | การแปลงเป็นภาพถูกปิด | ตรวจสอบให้แน่ใจว่า `saveOptions.getRasterization().setEnabled(true);` |
| ไฟล์ผลลัพธ์ว่าง | เส้นทางผลลัพธ์ไม่ถูกต้อง | ตรวจสอบว่าไดเรกทอรีมีอยู่และมีสิทธิ์เขียน |
| มุมที่ไม่คาดคิด | `minAngle` > `maxAngle` | สลับค่าให้ `minAngle` ≤ `maxAngle` |

## คำถามที่พบบ่อย

**Q: GroupDocs.Redaction Java ใช้ทำอะไร?**  
A: มันลบข้อมูลที่เป็นความลับโดยคงรูปแบบเอกสารไว้และยังรองรับคุณลักษณะการแปลงเป็นภาพขั้นสูงเช่นเอฟเฟกต์การเอียง  

**Q: ฉันจะใช้เอฟเฟกต์การเอียงในเอกสารของฉันด้วย GroupDocs อย่างไร?**  
A: โดยเปิดการแปลงเป็นภาพและเพิ่มตัวเลือกขั้นสูง `Tilt` พร้อมพารามิเตอร์ `minAngle` และ `maxAngle` ตามที่แสดงในตัวอย่างโค้ด  

**Q: ฉันสามารถใช้ GroupDocs.Redaction ได้ฟรีหรือไม่?**  
A: ใช่ มีการทดลองใช้ฟรีสำหรับการประเมิน สำหรับการใช้งานในสภาพแวดล้อมการผลิต จำเป็นต้องมีไลเซนส์ชั่วคราวหรือถาวร  

**Q: ประโยชน์ของการใช้เอฟเฟกต์การเอียงในเอกสารคืออะไร?**  
A: มันเพิ่มความดึงดูดทางสายตา, เพิ่มสัมผัสเชิงสร้างสรรค์, และช่วยทำให้สื่อการตลาดหรือการนำเสนอแตกต่างออกไป  

**Q: มีข้อจำกัดใดในการใช้เอฟเฟกต์แบบกำหนดเองกับ GroupDocs.Redaction Java หรือไม่?**  
A: ไฟล์ขนาดใหญ่มากอาจทำให้เวลาในการประมวลผลและการใช้หน่วยความจำเพิ่มขึ้น; การจัดสรรทรัพยากรอย่างเหมาะสมจะช่วยลดปัญหาเหล่านี้  

## แหล่งข้อมูล
- [เอกสารการใช้งาน GroupDocs Redaction](https://docs.groupdocs.com/redaction/java/)  
- [อ้างอิง API](https://reference.groupdocs.com/redaction/java)  
- [ดาวน์โหลด GroupDocs.Redaction สำหรับ Java](https://releases.groupdocs.com/redaction/java/)  
- [ที่เก็บ GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)  
- [ฟอรั่มสนับสนุนฟรี](https://forum.groupdocs.com/c/redaction/33)  
- [การสมัครไลเซนส์ชั่วคราว](https://purchase.groupdocs.com/temporary-license/)  

**อัปเดตล่าสุด:** 2026-06-01  
**ทดสอบด้วย:** GroupDocs.Redaction 24.9 สำหรับ Java  
**ผู้เขียน:** GroupDocs  

## บทแนะนำที่เกี่ยวข้อง
- [บทแนะนำตัวเลือกการแปลงเป็นภาพสำหรับ GroupDocs.Redaction Java](/redaction/java/rasterization-options/)  
- [การแปลงเป็นภาพด้วยเสียงรบกวนแบบกำหนดเองใน Java: ปกป้องข้อมูลที่เป็นความลับด้วย GroupDocs.Redaction](/redaction/java/rasterization-options/java-groupdocs-redaction-custom-noise-rasterization/)  
- [วิธีใช้ groupdocs redaction สำหรับ Java: การแปลงเป็นภาพล่วงหน้าในเอกสาร Word](/redaction/java/rasterization-options/groupdocs-redaction-java-pre-rasterization-word-docs/)