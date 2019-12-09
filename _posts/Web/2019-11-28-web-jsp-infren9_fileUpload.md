---
title: "WEB, 실전jsp강좌, File Upload"
date: 2019-11-28 15:40:28 -0400
categories: 실전jsp강좌
tags : [WEB, JSP]
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

- fileForm.js
```html
<form action="fileFormOk.jsp" method="post" enctype="multipart/form-data">
	파일 : <input type="file" name="file">
	<input type="submit" value="File Upload">
</form>
```

- fileFormOk.js
```java
<%@page import="java.util.Enumeration"%>
<%@page import="com.oreilly.servlet.multipart.DefaultFileRenamePolicy"%>
<%@page import="com.oreilly.servlet.MultipartRequest"%>
<%@ page language="java" contentType="text/html; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
<%
	// 이클립스상의 파일저장 경로 != 실제 파일저장 경로 (아파치 서버쪽에 동일한 폴더가 만들어지고 그곳에 저장된다)
	String path = request.getRealPath("fileFolder");

	int size = 1024 * 1024 * 10; //10M
	String file = "";
	String oriFile = "";	// 오리지널파일

	try{
		// DefaultFileRenamePolicy() : 동일한 파일이 올라오면 파일이름1,2,3...붙여서 업로드한다.
		MultipartRequest multi = new MultipartRequest(request, path, size, "EUC-KR", new DefaultFileRenamePolicy());

		Enumeration files = multi.getFileNames();
		String str = (String)files.nextElement();

		file = multi.getFilesystemName(str);	// 중복되어있을때 이름
		oriFile = multi.getOriginalFileName(str);	// 파일의 실제이릅

	} catch (Exception e) {
		e.printStackTrace();
	}
%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=EUC-KR">
<title>Insert title here</title>
</head>
<body>
 	file upload success!
</body>
</html>
```

### tip !
- 이클립스상의 파일업로드 폴더에는 실제로 파일이 업로드 되지않는다
- 서버상에 동일한 폴더가 생성되고 그곳에 파일이 업로드 된다



---
## Reference
- <https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-jsp-%EA%B0%95%EC%A2%8C/lecture/1182>
