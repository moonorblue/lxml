# lxml
#### It's a record of how I use Python lxml module to create a RSS xml file

> Code
```python
from lxml import etree as ET


class XMLNamespaces:
    content = 'http://purl.org/rss/1.0/modules/content/'
    
#create a root element, use nsmap to create namespace
root = ET.Element('rss', nsmap={
                         'content': XMLNamespaces.content,
                         'media': 'http://search.yahoo.com/mrss/',
                         'dc':"http://purl.org/dc/elements/1.1/"},
                         version="2")

#create subelements
channel = ET.SubElement(root, "channel")
title = ET.SubElement(channel, "title")

#set element value with CDATA
title.text = ET.CDATA(u"Some title")
language = ET.SubElement(channel, "language")
#set element value with simple text
language.text = "en-us"


#create items 
item = ET.SubElement(channel, "item")

title = ET.SubElement(item, "title")
title.text = "Another title"

link = ET.SubElement(item, "link")
link.text = "Some link"

guid = ET.SubElement(item, "guid")
guid.set("isPermaLink", "true")
guid.text = "Some guid"

pubDate = ET.SubElement(item, "pubDate")
pubDate.text = "Some date"

description = ET.SubElement(item, "description")
description.text = "Some description"

author = ET.SubElement(item, "author")
author.text = "Some author"

#use QName for namespace prefix
content = ET.SubElement(item,ET.QName(XMLNamespaces.content, 'encoded'))
content.text = "Some content"


#print the xml
print(ET.tostring(root, pretty_print=True).decode())

```



> Output
```xml
<rss xmlns:content="http://purl.org/rss/1.0/modules/content/" xmlns:media="http://search.yahoo.com/mrss/" xmlns:dc="http://purl.org/dc/elements/1.1/" version="2">
  <channel>
    <title><![CDATA[Some title]]></title>
    <language>en-us</language>
    <item>
      <title>Another title</title>
      <link>Some link</link>
      <guid isPermaLink="true">Some guid</guid>
      <pubDate>Some date</pubDate>
      <description>Some description</description>
      <author>Some author</author>
      <content:encoded>Some content</content:encoded>
    </item>
  </channel>
</rss>
```
