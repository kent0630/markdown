python发送Email程序
====
####一个可带附件的例子

	#!/usr/bin/python
	#encoding=utf-8

	import smtplib
	import base64
	import sys

	from email.mime.multipart import MIMEMultipart
	from email.mime.text import MIMEText
	from email.header import Header

	# 定义发送列表
	mailto_list=["xuxiaofeng.nb@ccb.com"，"raymond_xu@qq.com]
	 
	# 设置服务器名称、用户名、密码以及邮件
	mail_host = "36.0.191.1"
	mail_user = ""
	mail_pass = ""
	 
	# 发送邮件函数
	def send_mail(mail_from,to_list, sub, context):
		'''
		to_list: 发送给谁
		sub: 主题
		context: 内容
		send_mail("xxx.nb@ccb.com","sub","context")
		'''
		msg = MIMEMultipart()  #支持附件

		# 如果html格式，将_subtpye设成html
		# msg = MIMEText(context, _subtype='plain', _charset='utf-8') 

		context += '\n\r'
		txt1 = MIMEText(context, _subtype='plain', _charset='utf-8')
		# txt1.replace_header('Content-Transfer-Encoding', 'quoted-printable')  #否则邮件原文看不懂，但并不影响读信
		msg.attach(txt1)

		# att1=base64.encodestring(open('output.txt','rb').read())  #附件base64编码
		att1=open('output.txt','rb').read() 
		att1=MIMEText(att1)
		att1.replace_header('Content-Type','application/octet-stream;name="%s"' % Header('中文附件测试.txt','utf-8'))
		att1.add_header('Content-Disposition', 'attachment;filename="%s"' %Header('中文附件名测试.txt','utf-8'))
		msg.attach(att1)

		# att2=open('library.zip','rb').read()  
		# att2=MIMEText(att2)
		# att2.replace_header('Content-Type','application/octet-stream;name="%s"' % Header('lib.zip','utf-8'))
		# att2.add_header('Content-Disposition', 'attachment;filename="%s"' %Header('lib.zip','utf-8'))
		# msg.attach(att2)
		
		msg['Subject'] = Header(sub, 'utf-8')
		msg['From'] = Header(mail_from, 'utf-8')
		msg['To'] = ";".join(to_list) 
		try: 
			send_smtp = smtplib.SMTP()
			send_smtp.connect(mail_host)
			#send_smtp.login(mail_user, mail_pass)
			send_smtp.sendmail(mail_from, to_list, msg.as_string())
			send_smtp.close()
			return True
		except Exception, e:
			print str(e)
			return False

	if __name__ == '__main__':
		if (True == send_mail("徐小峰<xuxiaofeng.nb@ccb.com>",mailto_list, "邮件主题", "邮件正文")): 
		print (u"邮件发送成功")
	else: 
		print (u"邮件发送失败")


#### 问题
- py2exe打包时出现如下错误
		The following modules appear to be missing
		['_scproxy', 'email.Header', 'email.MIMEMultipart']
	
	- 查看了python的lib目录下mail下的文件，可能和之前版本发生了变化，导入模块改成如下即可：
			from email.mime.multipart import MIMEMultipart	
			from email.header import Header

