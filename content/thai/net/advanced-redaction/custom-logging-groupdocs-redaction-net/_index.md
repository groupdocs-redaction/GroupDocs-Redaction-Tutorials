---
date: '2026-03-28'
description: เรียนรู้วิธีการสร้าง Logger แบบกำหนดเองใน C# สำหรับ GroupDocs.Redaction
  บน .NET เพื่อให้สามารถบันทึกข้อมูลอย่างละเอียดและอำนวยความสะดวกในการรายงานการปฏิบัติตามข้อกำหนด.
keywords:
- custom logger c#
- custom logging .net
- save redacted document
- log warnings c#
title: นำ Logger แบบกำหนดเองใน C# ไปใช้กับ GroupDocs.Redaction สำหรับ .NET
type: docs
url: /th/net/advanced-redaction/custom-logging-groupdocs-redaction-net/
weight: 1
---

# ใช้งาน custom logger c# ใน GroupDocs.Redaction สำหรับ .NET

การจัดการการลบข้อมูลในเอกสารอย่างมีประสิทธิภาพเป็นสิ่งสำคัญ โดยเฉพาะเมื่อจัดการข้อมูลที่ละเอียดอ่อน ในคู่มือนี้คุณจะได้เรียนรู้ **วิธีการใช้งาน custom logger c#** กับ GroupDocs.Redaction สำหรับ .NET ซึ่งจะให้คุณควบคุมการบันทึก, การจัดการข้อผิดพลาด, และบันทึกการตรวจสอบได้อย่างเต็มที่.

## คำตอบสั้น
- **custom logger c# ทำอะไร?** มันบันทึกข้อผิดพลาด, คำเตือน, และข้อความข้อมูลระหว่างการลบข้อมูล.  
- **ไลบรารีใดให้ส่วนต่อประสาน ILogger?** GroupDocs.Redaction สำหรับ .NET.  
- **ฉันสามารถบันทึกเอกสารที่ลบข้อมูลแล้วโดยไม่ทำ rasterization ได้หรือไม่?** ใช่ – ใช้ `redactor.Save(..., new Options.RasterizationOptions { Enabled = false })`.  
- **ฉันต้องการใบอนุญาตสำหรับการใช้งานในผลิตภัณฑ์หรือไม่?** จำเป็นต้องมีใบอนุญาตเต็มสำหรับการผลิต; มีรุ่นทดลองสำหรับการประเมินผล.  
- **วิธีนี้เข้ากันได้กับ .NET Core / .NET 6+ หรือไม่?** แน่นอน – API เดียวกันทำงานได้ทั้งบน .NET Framework และ .NET Core/5/6.

## custom logger c# คืออะไร?
**custom logger c#** คือคลาสที่ทำการ implement ส่วนต่อประสาน `ILogger` ที่จัดหาโดย GroupDocs.Redaction ซึ่งทำให้คุณสามารถส่งข้อความบันทึกไปยังที่ที่ต้องการ—คอนโซล, ไฟล์, ฐานข้อมูล, หรือระบบตรวจสอบภายนอก—พร้อมให้มุมมองที่ชัดเจนของกระบวนการลบข้อมูล.

## ทำไมต้องใช้ custom logging .net กับ GroupDocs.Redaction?
- **Compliance & Auditing:** บันทึกรายละเอียดช่วยตอบสนองข้อกำหนดตามกฎระเบียบ.  
- **Error Visibility:** `LogError` และ `LogWarning` ให้ข้อเสนอแนะทันทีเกี่ยวกับปัญหา.  
- **Integration Flexibility:** ส่งต่อบันทึกไปยังเฟรมเวิร์กการบันทึกของ .NET ที่มีอยู่ (Serilog, NLog, ฯลฯ).

## ข้อกำหนดเบื้องต้น
- **GroupDocs.Redaction for .NET** ติดตั้งแล้ว (ดูการติดตั้งด้านล่าง).  
- สภาพแวดล้อมการพัฒนา .NET (Visual Studio, VS Code, หรือ CLI).  
- ความรู้พื้นฐานของ C# และความคุ้นเคยกับไฟล์สตรีม.

## การติดตั้ง

**.NET CLI**
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
ค้นหา **"GroupDocs.Redaction"** และติดตั้งเวอร์ชันล่าสุด.

## การรับใบอนุญาต
- **Free Trial:** ทดสอบ API ด้วยใบอนุญาตชั่วคราว.  
- **Temporary License:** รับการเข้าถึงฟีเจอร์ทั้งหมดในช่วงเวลาจำกัด.  
- **Purchase:** ซื้อใบอนุญาตถาวรสำหรับการใช้งานในผลิตภัณฑ์.

## คู่มือขั้นตอนต่อขั้นตอน

### ขั้นตอนที่ 1: กำหนดคลาส custom logger (log warnings c#)

สร้างคลาสที่ทำการ implement `ILogger`. คลาสนี้จะบันทึกข้อผิดพลาด, คำเตือน, และข้อความข้อมูล.

```csharp
using System;
using GroupDocs.Redaction;

class CustomLogger : ILogger
{
    public bool HasErrors { get; private set; }

    // Log errors encountered during processing.
    public void LogError(string message)
    {
        Console.WriteLine("Error: " + message);
        HasErrors = true;
    }

    // Log warnings that may not be critical but need attention.
    public void LogWarning(string message)
    {
        Console.WriteLine("Warning: " + message);
    }

    // Log informational messages for tracking normal operations.
    public void LogInfo(string message)
    {
        Console.WriteLine("Info: " + message);
    }
}
```

**Explanation:** ธง `HasErrors` ช่วยให้คุณตัดสินใจว่าจะดำเนินการต่อหรือไม่ วิธีการทั้งสามสอดคล้องกับระดับการบันทึกสามระดับที่คุณจะต้องใช้ในสถานการณ์การลบข้อมูลส่วนใหญ่.

### ขั้นตอนที่ 2: เตรียมเส้นทางไฟล์และเปิดเอกสารต้นฉบับ

```csharp
string sourceFile = Utils.PrepareOutputDirectory("YOUR_DOCUMENT_DIRECTORY");
string outputFile = Utils.GetOutputFile(sourceFile);
```

**Why this matters:** การใช้เมธอดยูทิลิตี้ทำให้โค้ดของคุณสะอาดและรับประกันว่าโฟลเดอร์ผลลัพธ์มีอยู่ก่อนที่คุณจะพยายาม **บันทึกเอกสารที่ลบข้อมูลแล้ว**.

### ขั้นตอนที่ 3: ใช้การลบข้อมูลพร้อมกับ custom logger

```csharp
using (Stream stream = File.Open(sourceFile, FileMode.Open, FileAccess.ReadWrite))
{
    var logger = new CustomLogger();
    
    using (Redactor redactor = new Redactor(stream, new LoadOptions(), new RedactorSettings(logger)))
    {
        // Apply a redaction to the document.
        redactor.Apply(new DeleteAnnotationRedaction());
        
        if (!logger.HasErrors)
        {
            using (Stream streamOut = File.Open(outputFile, FileMode.OpenOrCreate, FileAccess.ReadWrite))
            {
                // Save changes without rasterizing the output.
                redactor.Save(streamOut, new Options.RasterizationOptions { Enabled = false });
            }
        }
    }
}
```

**Explanation:**  
1. `Redactor` ถูกสร้างด้วย `RedactorSettings(logger)`, เชื่อมต่อกับ `CustomLogger` ของคุณ.  
2. หลังจากทำการลบข้อมูล, โค้ดจะตรวจสอบ `logger.HasErrors`. หากไม่มีข้อผิดพลาดเกิดขึ้น, เอกสารจะถูกบันทึก—แสดงให้เห็นตรรกะ **บันทึกเอกสารที่ลบข้อมูลแล้ว** โดยไม่ต้อง rasterization.

### ข้อผิดพลาดทั่วไป & การแก้ไขปัญหา
- **Missing log output:** ตรวจสอบว่าแต่ละเมธอด `Log*` ถูก override อย่างถูกต้อง.  
- **File access exceptions:** ตรวจสอบว่าแอปพลิเคชันมีสิทธิ์อ่าน/เขียนสำหรับเส้นทางต้นฉบับและผลลัพธ์.  
- **Logger not wired:** พารามิเตอร์ `RedactorSettings(logger)` มีความสำคัญ; การละเว้นจะทำให้การบันทึกแบบ custom ไม่ทำงาน.

## การประยุกต์ใช้งานจริง
1. **Compliance Reporting:** ส่งออกรายการบันทึกเป็น CSV หรือฐานข้อมูลเพื่อเป็นบันทึกการตรวจสอบ.  
2. **Error Tracking:** ค้นหาไฟล์ที่มีปัญหาอย่างรวดเร็วโดยสแกนผลลัพธ์ของ `LogError`.  
3. **Workflow Automation:** เรียกกระบวนการต่อเนื่อง (เช่น การแจ้งผู้รับผิดชอบด้าน compliance) เมื่อ `LogWarning` ถูกเรียกใช้.

## พิจารณาด้านประสิทธิภาพ
- **Dispose streams promptly** เพื่อปล่อยหน่วยความจำ, โดยเฉพาะเมื่อประมวลผลชุดข้อมูลขนาดใหญ่.  
- **Monitor CPU & memory** ระหว่างการลบข้อมูลเป็นจำนวนมาก; พิจารณาประมวลผลเอกสารแบบขนานพร้อมการซิงโครไนซ์ logger อย่างระมัดระวัง.  
- **Stay updated:** เวอร์ชันใหม่ของ GroupDocs.Redaction มักมีการปรับปรุงประสิทธิภาพและ hook การบันทึกเพิ่มเติม.

## สรุป

โดยการ implement **custom logger c#**, คุณจะได้ข้อมูลเชิงลึกระดับละเอียดในทุกขั้นตอนของกระบวนการลบข้อมูล, ทำให้ง่ายต่อการปฏิบัติตามมาตรฐาน compliance และการดีบักปัญหา วิธีการที่แสดงนี้ทำงานอย่างไร้รอยต่อกับ GroupDocs.Redaction สำหรับ .NET และสามารถขยายเพื่อรวมกับเฟรมเวิร์กการบันทึกของ .NET ใด ๆ ที่คุณใช้อยู่แล้ว.

---

## คำถามที่พบบ่อย

**Q: จุดประสงค์ของ custom logging กับ GroupDocs.Redaction คืออะไร?**  
A: Custom logging ช่วยติดตามและจัดการการลบข้อมูลเพื่อการปฏิบัติตาม, การติดตามข้อผิดพลาด, และการปรับปรุง workflow.

**Q: ฉันจะจัดการข้อผิดพลาดด้วย custom logger อย่างไร?**  
A: Implement `LogError` ในคลาส `CustomLogger` ของคุณ; ธง `HasErrors` ทำให้คุณสามารถหยุดการประมวลผลได้หากจำเป็น.

**Q: สามารถรวม custom logging กับระบบอื่นได้หรือไม่?**  
A: ได้, คุณสามารถส่งต่อข้อความบันทึกไปยัง CRM, ERP, หรือเครื่องมือมอนิเตอร์ศูนย์กลางโดยการขยายเมธอดของ logger.

**Q: ข้อผิดพลาดทั่วไปเมื่อทำ custom logging มีอะไรบ้าง?**  
A: การ implement เมธอดไม่ถูกต้อง, การลืม `RedactorSettings(logger)`, และปัญหาการอนุญาตไฟล์เป็นปัญหาที่พบบ่อยที่สุด.

**Q: custom logging ช่วยปรับปรุง workflow การลบข้อมูลในเอกสารอย่างไร?**  
A: บันทึกรายละเอียดให้มองเห็นแบบเรียลไทม์, ทำให้การแก้ปัญหาง่ายขึ้น, และตอบสนองความต้องการการตรวจสอบ.

## แหล่งข้อมูล

- **Documentation:** [GroupDocs.Redaction .NET Documentation](https://docs.groupdocs.com/redaction/net/)  
- **API Reference:** [GroupDocs.Redaction API Reference](https://reference.groupdocs.com/redaction/net)  
- **Download:** [GroupDocs.Redaction for .NET](https://downloads.groupdocs.com/redaction/net)

---

**อัปเดตล่าสุด:** 2026-03-28  
**ทดสอบกับ:** GroupDocs.Redaction 23.11 for .NET  
**ผู้เขียน:** GroupDocs