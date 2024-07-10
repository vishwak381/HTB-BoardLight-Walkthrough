# HTB-BoardLight-Walkthrough
## My HACK THE BOX walkthrough of BoardLight-Easy      *ilanthiraiyan18/hackthebox*
![k01](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/426cc66a-4e83-49d2-bc34-5770ebc6961b)

**First of all we start with the nmap scan to see open ports and services running.** 

![k02](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/b394ece2-b8eb-441b-a1ba-49acf8e50a3b)
![k03](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/a72ba1e8-394b-4d10-9a65-a3bffe647244)

**We have SSH and HTTP ports open.So Let's add the machine's IP Address to *etc/hosts* file to see webpage.**

![k04](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/4f1b3b8e-a90d-4c60-8170-4f5221196766)
![k05](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/45a731e8-9ee8-4c51-983c-0d0c6589e3a4)

**Now let's go to the Webpage.**

![k06](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/3f71fab0-790d-4df0-a6be-c72ae5604f96)

**Now we got access to the webpage.**
**First we go through the website to find a way to exploit it.**

**Now we can use FFUF to find that the website has any subdomains.**

![k07](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/73d93a27-66f4-4aed-bfe5-9b20bef7a413)
![k08](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/77e27076-e58d-47e8-95b0-e6c37c099cf7)

**Almost every size were 15949 let's see if there are any other.**

![k09](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/90f1870f-4e4c-4a3d-849b-00f8d2fdea84)

**We found a subdomain crm which was of size 6360. Let’s access this. Also, add “crm.boardlight.htb” to the etc/hosts file.**

![k10](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/ed2858d3-537c-41fb-a071-5582b18817f6)

**As we can see Dolibarr which is an open-source CRM (Customer Relationship Management) software package designed for small and medium-sized enterprises (SMEs), freelancers, and foundations.**

**Then I search about Dolibarr exploit in the internet and I found an exploit.**
**It is a reverse shell POC exploit and I downloaded it.**

![k12](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/66aae9f0-9ebe-437c-9c1b-161fb05c61b5)

**Now we got a reverse shell.**
**Now I am going to search the directories to find something interesting.**

![k14](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/27442d57-a0c3-4642-801e-dbe1950f489e)

**In the home directory,I have found a username *Larissa*,but I can't able to access it.**

![k13](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/62ddedff-18c2-4fa2-a37e-090527a24814)

**I also found a interesting file in conf/conf.php where it has dolibarr username and password and I also tried the password in the home directory *larissa* but it did not work.**
**As we saw in the nmap scan we found that SSH port is open.So, let's initiate an interactive shell session where username *larissa*.**

![k15](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/731ac148-95b9-4100-be2b-69ac4be826f7)

**Now we got the user flag.**

**For privilege escalation check, I ran LinEnum.sh on the remote host by transferring it from my local computer where LinEnum is a script written in bash (shell scripting language) designed for Linux enumeration, which is the process of gathering information about a Linux system to identify potential weaknesses or areas of concern from a security perspective.**

![k16](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/8228affa-1624-4c73-afe8-31f11f3072f4)

**We can start the check scan by reverse shell and retrieving the files through wget command and to make script executable use chmod command.** 

![k17](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/aedace55-fb85-4184-9673-a451c1f47ceb)

**After the scan is complete,I surfed through the directories and files and I found an interesting one.**

![k18](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/a036a41f-5ca3-4c03-95de-de5cdd618cc5)

**In the SUID files,there are some interesting files which are enlightenment_sys,enlightenment_passwd where enlightenment serves primarily as a window manager, providing basic window management functionalities such as window placement, resizing, and handling desktop backgrounds for Linux systems.**
**Then I searched exploit enlightenment,then I found out enlightenment exploit.sh**

![829502d4-eff0-4f02-8738-1ef0d6ffa8b9](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/13a9dd5f-574a-463c-b522-4150d8ccdf3b)

**As the exploit script related to CVE-2022-37706, targeting a specific vulnerability that allows local privilege escalation.Upon following the steps, We found the root flag.**

![k19](https://github.com/vishwak381/HTB-BoardLight-Walkthrough/assets/175153637/75772347-dbe9-46e0-b463-2e59322a1337)

**Hurray we pwned the machine,and it was an easy machine.**



