# Introduction #
增加55BBS的登录脚本,结构一样,只是参数不同.


# Details #
```
def post55bbs (username,passwd):
	userdata = {'username':username,'password':passwd,'refer':'http://www.55bbs.com/','loginsubmit':'true'}
	opener = login(userdata,'http://bbs.55bbs.com/logging.php?action=login&')
	data = getData()
	while len(data)>0:
		d = data.pop()
		postpage=urllib2.Request('http://bbs.55bbs.com/viewthread.php?tid=更换帖子id&pid=用户id号')
		c = opener.open(postpage)
		bincontent= c.read()
		p=re.compile(r'''\s+<input type="hidden" name="formhash" value="(.*)" />\s+''',re.M)
		c = p.findall(bincontent)
		print c
		if len(c)>0:
			dazhedata = {'subject':'','message':unicode(d['content'],"utf-8").encode("gbk"),'formhash':c[0]}
			postdata(opener,dazhedata,'http://bbs.55bbs.com/post.php?action=reply&fid=更换为板块Id&tid=更换帖子id&extra=page%3D1&replysubmit=yes')
```