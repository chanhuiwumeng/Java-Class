# Xml解析

> 可扩展[标记语言](https://baike.baidu.com/item/标记语言)，[标准通用标记语言](https://baike.baidu.com/item/标准通用标记语言/6805073)的子集，简称XML。是一种用于标记电子文件使其具有结构性的[标记语言](https://baike.baidu.com/item/标记语言/5964436)
>
> 现在作为配合文件使用
>
> XMl是一种语法很严格的扩展语言
>
> 怎么样去解析xml中的内容:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--会覆盖tomcat自身的web.xml中的文件-->
    <welcome-file-list>
        <welcome-file>login.html</welcome-file>
    </welcome-file-list>
</web-app>
```

## 1. DOM4J解析

```java
package com.xdkj.xml;

import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Element;
import org.dom4j.io.SAXReader;

import java.util.List;

/**
 * ClassName ParseXml
 * Description:
 *
 * @Author:一尘
 * @Version:1.0
 * @Date:2021-02-26-14:32
 */
public class ParseXml {
    /*解析xml文件*/
    public static void main(String[] args) {
        SAXReader reader = new SAXReader();
        try {
            /*获取到的是xml文件得文档对象*/
            Document document = reader.read("C:\\Users\\chanh\\InteliJIdeaWorkSpace\\xdkj\\idea-tomcat\\src\\main.xml");
            /*获取文档的信息*/
            /*获取文档编码*/
            System.out.println(document.getXMLEncoding());//utf-8
            /*获取根元素*/
         Element element =  document.getRootElement();
            System.out.println(element.getName());//books
          //获取根元素中的数据
            List<Element> elements = element.elements();
            for (Element o : elements) {
                System.out.println("属性值:"+ o.attributes());
                System.out.println(o.attribute("name").getName());
                System.out.println(o.attribute("name").getValue());
                System.out.println("-----------------------------");
               //在获取第一级子节点中的节点
                List<Element> elements1 = o.elements();
                for (Element element1 : elements1) {
                    System.out.println(element1.getName());
                    System.out.println(element1.getText());
                }
            }

        } catch (DocumentException e) {
            e.printStackTrace();
        }
    }
}

```

**main.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<books>
    <book name="新华书店">
        <name>水浒传</name>
        <price>99.99</price>
        <author>施耐庵</author>
    </book>
</books>
```

