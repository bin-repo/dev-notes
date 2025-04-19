# python-module-smtp（邮件发送模块）

## 模块导入

```py
import smtplib

# email模块相关组件
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.mime.image import MIMEImage
from email.header import Header
from email.utils import formataddr
```

## 模块使用

```py
# 定义发件人、收件人
sender = 'test_a@example.com'
recver = ['test_b@example.com']
```

```py
# 发送内容（普通文本）
message = MIMEText('python邮件测试。。','plain','utf-8')
```

```py
# 发送内容（HTML格式文档）
message= MIMEText('<a href="http://www.runoob.com">runoob</a>','html','utf-8')
```

```py
# 发送内容（含附件）
message= MIMEMultipart()
message.attach(MIMEText('邮件正文内容','plain','utf-8'))
for filename in ['附件1.txt','附件2.pdf']:
    attachment = MIMEText(open(filename,'rb').read(), 'base64','utf-8')
    attachment['Content-Type'] = 'application/octet-stream'
    attachment['Content-Disposition'] = 'attachment;filename="{}"'.format(filename)
    message.attach(attachment)
```

```py
# 发送内容（含图片）
message = MIMEMultipart('related')
msgAlternative = MIMEMultipart('alternative')
message.attach(msgAlternative)
msgAlternative.attach(MIMEText('<img src="cid:image1">','html','utf-8'))
with open('test.png','rb') as fp:
    msgImage = MIMEImage(fp.read())
    msgImage.add_header('Content-ID','<image1>')
message.attach(msgImage)
```

```py
# 邮件主题 1
message['From'] = Header('发送者','utf-8')
message['To'] = Header('接收者','utf-8')
message['Subject'] = Header('主题','utf-8')
```

```py
# 邮件主题 2
message['From'] = formataddr(['昵称',sender])
message['To'] = formataddr(['昵称',recver])
message['Subject'] = Header('主题','utf-8')
```

```py
# 通过本地安装的SMTP服务器发送
try:
    smtp = smtplib.SMTP('localhost')
    smtp.sendmail(sender, recver, message.as_string())
    print('邮件发送成功')
except smtplib.SMTPException:
    print('邮件发送失败')
```

```py
# 通过第三方SMTP服务器发送
try:
    smtp = smtplib.SMTP()
    smtp.connect('smtp.ym.163.com', 25)
    smtp.login('test_a@example','test_pwd')
    smtp.sendmail(sender, recver, message.as_string())
    smtp.quit()
    print('邮件发送成功')
except smtplib.SMTPException:
    print('邮件发送失败')
```

```py
# 采用SSL安全协议
try:
    smtp = smtplib.SMTP_SSL('smtp.ym.163.com', 465)
    smtp.login('test_a@example','test_pwd')
    smtp.sendmail(sender, recver, message.as_string())
    smtp.quit()
    print('邮件发送成功')
except smtplib.SMTPException:
    print('邮件发送失败')
```
