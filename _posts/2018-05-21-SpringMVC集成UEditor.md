---
layout: post
title: SpringMVC 集成 UEditor
categories: UEditor Spring
---

UEditor是由百度开发的富文本web编辑器。其后端jsp代码实现的文件保存/读取路径受限于传统文件系统且只能在应用的webapp目录下, 故作出修改。但是暂没有使用官方后端代码，且只实现了图片上传下载功能。

## 1. 下载
* 下载地址：[http://ueditor.baidu.com/website/download.html](http://ueditor.baidu.com/website/download.html), 下载其中的`jsp版本`
* 文件解压后目录结构如下所示
![目录结构.png](https://upload-images.jianshu.io/upload_images/5151732-3fe80250408e97b1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 2. 搭建项目

* 2.1. 新建一个maven项目

* 2.2. pom依赖

```xml
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.7</maven.compiler.source>
    <maven.compiler.target>1.7</maven.compiler.target>
    <junit.version>4.11</junit.version>
 	<spring.version>4.3.9.RELEASE</spring.version>
 	<fileupload.version>1.3.2</fileupload.version>
 	<commons.io.version>2.3</commons.io.version>
	<slf4j.version>1.6.4</slf4j.version>
 	<jackson.version>2.8.7</jackson.version>
 	<fastjson.version>1.2.4</fastjson.version>
 	<servlet.api.version>3.0.1</servlet.api.version>
  </properties>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>${junit.version}</version>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>${jackson.version}</version>
    </dependency>
   	<dependency>
		<groupId>commons-io</groupId>
		<artifactId>commons-io</artifactId>
		<version>${commons.io.version}</version>
	</dependency>
	<dependency>
		<groupId>commons-fileupload</groupId>
		<artifactId>commons-fileupload</artifactId>
		<version>${fileupload.version}</version>
	</dependency>
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-log4j12</artifactId>
      <version>${slf4j.version}</version>
    </dependency>
    <dependency>
		<groupId>com.alibaba</groupId>
		<artifactId>fastjson</artifactId>
		<version>${fastjson.version}</version>
	</dependency>
	<dependency>
		<groupId>javax.servlet</groupId>
		<artifactId>javax.servlet-api</artifactId>
		<version>${servlet.api.version}</version>
	</dependency>
  </dependencies>
```

* 2.3. spring-mvc.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p="http://www.springframework.org/schema/p"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:mvc="http://www.springframework.org/schema/mvc"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-4.0.xsd
        http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

	<mvc:annotation-driven/>
	
	<context:component-scan base-package="com.github.brandonbai.springmvcueditordemo.controller" />

	<bean id="multipartResolver"    
        class="org.springframework.web.multipart.commons.CommonsMultipartResolver">    
        <property name="defaultEncoding" value="utf-8" />    
        <property name="maxUploadSize" value="10485760000" />    
        <property name="maxInMemorySize" value="40960" />    
    </bean>
    
	<mvc:default-servlet-handler />
</beans>
```

* 2.4. applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:context="http://www.springframework.org/schema/context" xmlns:p="http://www.springframework.org/schema/p"
	xmlns:aop="http://www.springframework.org/schema/aop" xmlns:tx="http://www.springframework.org/schema/tx"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
	http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.0.xsd
	http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-4.0.xsd http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-4.0.xsd
	http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util-4.0.xsd">

	<context:component-scan base-package="com.github.brandonbai.springmvcueditordemo" />

</beans>
```

* 2.5. 将`ueditor`下载解压后目录下图`目录结构.png`第1部分的代码拷贝到项目的`webapp`下，如下图所示：
![项目结构.jpg](https://upload-images.jianshu.io/upload_images/5151732-43155e95c9332da9.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 2.6. 将`ueditor`下载解压后目录下图`目录结构.png`第2部分config.json的代码拷贝到项目的`src/main/resources`下，如下图所示：

![config.png](https://upload-images.jianshu.io/upload_images/5151732-823034d4321728d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 3. 前端配置

修改2.4图中的`ueditor.config.js`的服务器请求路径

```js
 32      // 服务器统一请求接口路径
 33       , serverUrl: URL + "./ueConvert"
```

## 4. 后端实现


* UEditorController.java

```java
package com.github.brandonbai.springmvcueditordemo.controller;

import java.io.BufferedReader;
import java.io.File;
import java.io.FileInputStream;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.HashMap;
import java.util.Map;

import javax.servlet.ServletOutputStream;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.multipart.MultipartFile;

import com.alibaba.fastjson.JSON;

/**
 * 
 * @author brandonbai
 *
 */
@Controller
public class UEditorController {

	private static final String DIR_NAME = "~/Desktop";
	
	private static final String PREFIX = "/editor/image";
	
	private static final String FILE_SEPARATOR = File.separator;
	
	private static final String PATH_SEPARATOR = "/";
	
	private static final String PATH_FORMAT = "yyyyMMddHHmmss";
	
	private static final String CONFIG_FILE_NAME = "config.json";
	
	private static final String ACTION_NAME_CONFIG = "config";
	
	private static final String ACTION_NAME_UPLOAD_IMAGE = "uploadimage";
	
	private static final Logger logger = LoggerFactory.getLogger(UEditorController.class);

	/**
	 * 配置、图片处理
	 */
	@RequestMapping("/ueConvert")
	public void ueditorConvert(HttpServletRequest request, HttpServletResponse response, String action,
			MultipartFile upfile) {

		try {
			request.setCharacterEncoding("utf-8");
			response.setHeader("Content-Type", "text/html");
			PrintWriter pw = response.getWriter();
			if (ACTION_NAME_CONFIG.equals(action)) {
				String content = readFile(this.getClass().getResource(PATH_SEPARATOR).getPath() + CONFIG_FILE_NAME);
				pw.write(content);
			} else if (ACTION_NAME_UPLOAD_IMAGE.equals(action)) {
				Map<String, Object> map = new HashMap<String, Object>(16);
				String time = new SimpleDateFormat(PATH_FORMAT).format(new Date());
				try {
					String originalFilename = upfile.getOriginalFilename();
					String type = originalFilename.substring(originalFilename.lastIndexOf("."));
					String dirName = DIR_NAME + PREFIX + FILE_SEPARATOR + time;
					File dir = new File(dirName);
					if(!dir.exists() || !dir.isDirectory()) {
						dir.mkdirs();
					}
					String fileName = dirName + FILE_SEPARATOR + originalFilename;
					upfile.transferTo(new File(fileName));
					map.put("state", "SUCCESS");
					map.put("original", originalFilename);
					map.put("size", upfile.getSize());
					map.put("title", fileName);
					map.put("type", type);
					map.put("url", "." + PREFIX + PATH_SEPARATOR + time + PATH_SEPARATOR + originalFilename);
				} catch (Exception e) {
					e.printStackTrace();
					logger.error("upload file error", e);
					map.put("state", "error");
				}
				response.setHeader("Content-Type", "application/json");
				pw.write(JSON.toJSONString(map));
				pw.close();
			}
		} catch (Exception e) {
			e.printStackTrace();
		}

	}

	/**
	 * 图片读取
	 */
	@RequestMapping(PREFIX + "/{time}/{path}.{type}")
	public void ueditorConvert(@PathVariable("time") String time, @PathVariable("path") String path,
			@PathVariable("type") String type, HttpServletRequest request, HttpServletResponse response) {
		try (FileInputStream fis = new FileInputStream(DIR_NAME + PREFIX + PATH_SEPARATOR + time + PATH_SEPARATOR + path + "." + type)) {
			int len = fis.available();
			byte[] data = new byte[len];
			fis.read(data);
			fis.close();
			ServletOutputStream out = response.getOutputStream();
			out.write(data);
			out.close();
		} catch (Exception e) {
			logger.error("read file error", e);
		}

	}

	private String readFile(String path) {

		StringBuilder builder = new StringBuilder();

		try(BufferedReader bfReader = new BufferedReader(new InputStreamReader(new FileInputStream(path), "UTF-8"))) {

			String tmpContent = null;

			while ((tmpContent = bfReader.readLine()) != null) {
				builder.append(tmpContent);
			}

			bfReader.close();

		} catch (Exception e) {
			e.printStackTrace();
		}

		return builder.toString().replaceAll("/\\*[\\s\\S]*?\\*/", "");

	}

}
```

## 5.演示

![demo.gif](https://upload-images.jianshu.io/upload_images/5151732-58e9252e486d799b.gif?imageMogr2/auto-orient/strip)



#### 示例代码
[https://github.com/brandonbai/springmvc-ueditor-demo](https://github.com/brandonbai/springmvc-ueditor-demo)
