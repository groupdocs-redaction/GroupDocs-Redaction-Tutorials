---
title: "Master Java Redactions with GroupDocs&#58; Implementing Metered Licensing & Exact Phrase Redactions"
description: "Learn how to set up a metered license and apply exact phrase redactions using GroupDocs.Redaction for Java. Enhance document security efficiently."
date: "2025-05-16"
weight: 1
url: "/java/licensing-configuration/mastering-java-redactions-groupdocs-metered-licensing-exact-phrase/"
keywords:
- GroupDocs.Redaction
- Java
- Document Processing

---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}
# Master Java Redactions with GroupDocs: Implementing Metered Licensing & Exact Phrase Redactions

In today's digital world, managing sensitive information is crucial. Whether you're handling legal documents or personal data, ensuring confidentiality while maintaining efficiency can be challenging. Enter GroupDocs.Redaction for Java—a powerful tool designed to simplify redaction tasks with precision. In this comprehensive guide, we'll walk you through setting a metered license and applying exact phrase redactions using the GroupDocs.Redaction API in Java.

**What You'll Learn:**
- How to set up a metered license for GroupDocs.Redaction
- Applying exact phrase redactions on documents
- Key implementation steps with code examples
- Real-world applications and performance considerations

Let's dive into how you can leverage these features to enhance document security seamlessly. Before we begin, let’s outline the prerequisites to ensure everything runs smoothly.

## Prerequisites
To get started with GroupDocs.Redaction for Java, make sure you have the following:

### Required Libraries
- **GroupDocs.Redaction Library**: Version 24.9 or later.
  
### Environment Setup Requirements
- Java Development Kit (JDK) version 8 or above installed on your machine.
### Knowledge Prerequisites
- Basic understanding of Java programming and familiarity with Maven for dependency management.
With these prerequisites in place, we’re ready to set up GroupDocs.Redaction for Java.

## Setting Up GroupDocs.Redaction for Java

### Installation

**Maven Configuration:**
To include the necessary dependencies using Maven, add the following configuration to your `pom.xml` file:

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

**Direct Download:**
Alternatively, you can download the latest version directly from [GroupDocs.Redaction for Java releases](https://releases.groupdocs.com/redaction/java/).

### License Acquisition
To use GroupDocs.Redaction effectively:
- **Free Trial**: Start with a trial to explore basic functionalities.
- **Temporary License**: Apply for a temporary license for full access during development.
- **Purchase**: Opt for a permanent license if you find the tool meets your needs.

#### Basic Initialization and Setup
Once installed, initialize your GroupDocs.Redaction environment by setting up your credentials. This will enable features such as metered licensing:

```java
import com.groupdocs.redaction.licensing.Metered;

public class SetMeteredLicense {
    public static void main(String[] args) throws Exception {
        // Initialize Metered API
        Metered metered = new Metered();
        
        // Setup credentials with your keys
        String publicKey = "YOUR_PUBLIC_KEY";
        String privateKey = "YOUR_PRIVATE_KEY";
        metered.setMeteredKey(publicKey, privateKey);
        
        // Retrieve consumption details
        BigDecimal consumptionQuantity = Metered.getConsumptionQuantity();
        System.out.println("Consumption Quantity: " + consumptionQuantity);
        
        BigDecimal consumptionCredit = Metered.getConsumptionCredit();
        System.out.println("Consumption Credit: " + consumptionCredit);
    }
}
```

This setup allows you to monitor usage and manage resources efficiently.

## Implementation Guide
Now, let's break down the implementation into two key features: setting a metered license and applying exact phrase redactions.

### Set Metered License
**Overview:**
Setting a metered license helps track API usage, ensuring optimal resource allocation and compliance with licensing agreements.

#### Steps to Implement:
1. **Initialize the Metered API**: This involves creating an instance of the `Metered` class.
2. **Set Your Keys**: Use your public and private keys obtained during the license setup to authenticate.
3. **Monitor Usage**: Retrieve consumption quantity and credit to manage usage effectively.
The provided code snippet above demonstrates these steps concisely, offering transparency into resource management with GroupDocs.Redaction.

### Apply Exact Phrase Redaction
**Overview:**
Exact phrase redaction is perfect for removing specific text from documents—ideal for sensitive information like names or identifiers.

#### Steps to Implement:
1. **Load Your Document**: Specify the file path of your document.
2. **Configure Redaction Options**: Use `ReplacementOptions` to define how the redacted content will appear (e.g., a red box).
3. **Apply Redaction**: Execute the redaction using `ExactPhraseRedaction`.

Here’s how you can implement this feature:

```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;
import java.awt.Color;

public class ApplyExactPhraseRedaction {
    public static void main(String[] args) throws Exception {
        // Load the document
        String inputFilePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
        final Redactor redactor = new Redactor(inputFilePath);
        try {
            // Set up replacement options and apply redaction
            ReplacementOptions replacementOptions = new ReplacementOptions(Color.RED);
            RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction("John Doe\
{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}