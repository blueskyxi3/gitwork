# 1: 有用的好 **工具**
bitbucket vscode webstorm jdk eclipse idea notepad++ [Forticlient VPN](http://www.fortinet.com)

![1](./images/1.png)

#  2: vs code**小技巧**

## 1. 如何關閉小地圖
```
view -> show mini map
```
## 2. 如何調整背景色
```
File-Preferences -> Color Theme
```

# 3: 其它 **小技巧**

## 1. github上如何刪除一個project or repository
```
your repositories -> select your project which you want to delete -> slide to setting Tab -> draw down to bottom->select Delete this repository
```
## 2. github上項目如何轉為公有
```
your repositories -> select your project which you want to delete -> slide to setting Tab -> draw down to bottom->select make public
```
## 3. markdown 基本語法 

     [參考簡書上的link](https://www.jianshu.com/p/191d1e21f7ed)

## 4.Windows下使用notepad++对文本进行行列转换
 ***
* 行转列： 
    Ctrl + F  选择替换
    查找目标：填写指定的内容
　　替换为：\r\n
　　查找模式：正则表达式
* 列转行：
   Ctrl + F  选择替换
   查找目标：\r\n
   替换为：不填写或填写指定的内容
   查找模式：正则表达式
 ***
 ## 5. 如何把本地Jar轉為maven依賴
```
mvn install:install-file -DgroupId=com.alipay -DartifactId=sdk-Java -Dversion=0.1 -Dpackaging=jar -Dfile=alipay-sdk-java0.1.jar
mvn install:install-file -DgroupId=org.activiti -DartifactId=activiti-enginecancel -Dversion=5.20.0 -Dpackaging=jar -Dfile=activiti-enginecancel-5.20.0.jar 
mvn install:install-file -DgroupId=com.oracle -DartifactId=ojdbc14 -Dversion=10.2.0.4.0 -Dpackaging=jar -Dfile=classes12.jar
mvn package -Dmaven.test.skip=true 
```
 ## 6.maven跳過測試環節
```
mvn package -Dmaven.test.skip=true 
```
## 7. Oracle如何調整背景色
```
Tools-Preferences -> Fonts->Editor 
then select your favoriate color for background color
```
## 8. Notepad++ 如何對比文件
```
step 1. intall comparison plugin.
   Plugins -> plugin admin   
Step 2. file comparison
   Plugins -> compare
```

## 9. Docker 相關
```
docker pull mysql:5.6
#启动
docker run --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=Lzslov123! -d mysql
docker run -itd --name mysql-test -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql

#进入容器
docker exec -it mysql bash

#登录mysql
mysql -u root -p
ALTER USER 'root'@'localhost' IDENTIFIED BY 'Lzslov123!';

#添加远程登录用户
CREATE USER 'liaozesong'@'%' IDENTIFIED WITH mysql_native_password BY 'Lzslov123!';
GRANT ALL PRIVILEGES ON *.* TO 'liaozesong'@'%';
```
## 10. Spring boot 如何統一接收參數
```
 @GetMapping("/{reportName}")
    public void getReportByParam(
            @PathVariable("reportName") final String reportName,
            @RequestParam(required = false) Map<String, Object> parameters,
            HttpServletResponse response) throws SQLException, ClassNotFoundException, JRException, IOException {

        parameters = parameters == null ? new HashMap<>() : parameters;
        //获取文件流
        ClassPathResource resource = new ClassPathResource("jaspers" + File.separator + reportName + ".jasper");
        InputStream jasperStream = resource.getInputStream();

        JasperReport jasperReport = (JasperReport) JRLoader.loadObject(jasperStream);
        JasperPrint jasperPrint = JasperFillManager.fillReport(jasperReport, parameters, dataSource.getConnection());
        // JasperPrint jasperPrint = JasperFillManager.fillReport(jasperReport, null, new JREmptyDataSource());
        response.setContentType("application/pdf");
        response.setHeader("Content-Disposition", "inline;");
        final OutputStream outputStream = response.getOutputStream();
        JasperExportManager.exportReportToPdfStream(jasperPrint, outputStream);
    }
```
## 11 net.sf.jasperreports.engine.util.JRFontNotFoundException: Font '宋体' is not available to the JVM. See the Javadoc for more details. 
```
1、把需要用到的字体（可以直接拷贝windows系统的C:\WINDOWS\Fonts 下的相关字体）拷贝当前项目的classpath下，一般为classes目录下 
2、在classpath里添加 jasperreports.properties 属性文件 
文件内容为： 
net.sf.jasperreports.awt.ignore.missing.font=true 
即可解决
```

## 12 nvm每次启动终端都要设置nvm use
```
nvm alias default stable
```
走了很多坑，总是提示：

## 13 google cloud ssh login
The client has disconnected from the server.Reason:
Unable to authenticate using any of the configured authentication methods. 
总算找到了方法：
1. 切换root用户： sudo -i 
2. 设置root密码：passwd root
3. 以下3条命令：
sed -i 's/PermitRootLogin no/PermitRootLogin yes/g' /etc/ssh/sshd_config;sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config;reboot

