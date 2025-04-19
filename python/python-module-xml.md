# python-module-xml（XML解析模块）

## XML三种解析方式

- SAX（simple api for xml）
- DOM（document object model）
- ElementTree

## XML文件示例

```py
# persons.xml
xmlcontent='''
<persons ref='human'>
    <user id='001'>
        <name>user001</name>
        <sex>Male</sex>
    </user>
    <user id='002'>
        <name>user002</name>
        <sex>Female</sex>
    </user>
</persons>'''
```

## `SAX`方式解析

- 基于事件驱动
- 偏好于特定内容提取

```py
import xml.sax

# 创建解析器对象
xml.sax.make_parser([parser_list])

# 创建解析器并解析XML文件
xml.sax.parse(xmlfile,contentHandler[,errorHandler])

# 创建解析器并解析XML字符串
xml.sax.parseString(xmlstring,contentHandler[,errorHandler])
```

```py
# 示例
class PersonsHandler(xml.sax.ContentHandler):
    def __init__(self):
        self.currentTag = ''
        self.user = ''
        self.name = ''
        self.sex  = ''
    def startElement(self,tag,attributes):
        '''起始标签<xxx attr1='' attr2=''>'''
        self.currentTag = tag
        if tag == 'user':
            user_id = attributes['id']
    def endElement(self,tag):
        '''结束标签</xxx>'''
        if self.currentTag == 'name':
            user_name = self.name
        elif self.currentTag == 'sex':
            user_sex = self.sex
        self.currentTag = ''
    def characters(self,content):
        '''标签内容'''
        if self.currentTag == 'name':
            self.name = content
        elif self.currentTag == 'sex':
            self.sex = content

if __name__ == '__main__':
    if '''xml.sax.make_parser()解析''':
        parser = xml.sax.make_parser()
        parser.setFeature(xml.sax.handler.feature_namespaces,0) # 关闭命名空间
        parser.setContentHandler(PersonsHandler())
        parser.parse('persons.xml')
    elif '''xml.sax.parse()解析''':
        xml.sax.parse('persons.xml',PersonsHandler())
    elif '''xml.sax.parseString()解析''':
        xml.sax.parseString(xmlcontent, PersonsHandler())
```

## `DOM`方式解析

- 文档对象模型
- 偏好于全文解析

```py
import xml.dom.minidom

# 解析XML文件
xml.dom.minidom.parse(xmlfile)

# 解析XML字符串
xml.dom.minidom.parseString(xmlstring)
```

```py
docTree = xml.dom.minidom.parseString(xmlcontent)

collection = docTree.documentElement

for user in collection.getElementsByTagName('user'):
    if user.hasAttribute('id'):
        user_id = user.getAttribute('id')
    user_name = user.getElementsByTagName('name')[0].childNodes[0].data
    user_sex  = user.getElementsByTagName('sex')[0].childNodes[0].data
```
