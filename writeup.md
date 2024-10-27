Hi everyone, this time me and World Wide Flags joined ISITDTU CTF 2024 and luckily we got 16th rank. This is writeup for **swatted** which is one of the forensic challenge that I have solved. Let's go:

![image](https://github.com/user-attachments/assets/450a3fff-b2ed-4957-83cb-4578e65ccb6e)

### swatted

Full answers:
```
    Welcome to ISITDTU CTF 2024 - Forensics Challenge!
    Most of the answers are case-insensitive. If not, it will be mentioned in the question.
    You have to answer 10/10 questions correctly to get the flag. Good Luck!

    
    
[1]. What is the credential used to login to the machine?
Format: username:password
==> imsadboi:qwerty
CORRECT!
[2]. The criminal used a messaging app to communicate with his partner. What is the name of the app?
Format: AppName
==> Wire
CORRECT!
[3]. What is the username of the criminal (The app username)?
Format: username
==> anonymous64920
WRONG ANSWER!
==> anonymous69420
CORRECT!
[4]. What is his partner's username?
Format: username
==> clowncz123
CORRECT!
[5]. His partner sent him a file. What is the URL used to download the file?
Format: URL
==> https://file.io/lIPzLAvhF5n4        
CORRECT!
[6]. What is the timestamp of the file sent by his partner (UTC)?
Format: YYYY-MM-DD HH:MM:SS
==> 2024-10-24 09:59:12
CORRECT!
[7]. What is the timestamp when the criminal downloaded the file (UTC)?
Format: YYYY-MM-DD HH:MM:SS
==> 2024-10-24 10:01:12
CORRECT!
[8]. His partner accidentally leaked his email. What is the email address?
Format: email@domain.com
==> theclownz723@gmail.com
CORRECT!
[9]. Luckily, we caught the criminal before he could send the sensitive information. How many credentials did he manage to steal?
Format: XX. Example 1: 01. Example 2: 42.                                                                                                                                                                                                  
==> 23
CORRECT!
[10]. What is the email address and the password of user 'blistery'?
Format: email:password                                                                                                                                                                                                                     
==> blistery@yahoo.com:HDTSy0C7ZBCj
CORRECT!
Congrats! Here is your flag: ISITDTU{https://www.youtube.com/watch?v=H3d26v9TciI}
```

I loved this challenge a lot so I will write this first. Our evidence is a VMDK file, normally you will use VMware to open it but because I don't have that one and I don't want to install 
too so I used 7-zip to open it: 

![image](https://github.com/user-attachments/assets/80407226-3724-4c51-b774-e14e4ad70c3e)

With the question 1, just find the hash inside **/etc/shaodw** and crack it by using **john**:

![image](https://github.com/user-attachments/assets/3bdb0cc8-f051-4ea1-b5ab-9c62fc6b288b)

Open .bash_history, we will see that he did many things including install something named Wire:

![image](https://github.com/user-attachments/assets/70f575d1-798e-4094-95f9-a6499c8729cd)

Find it on Google, you will find its informaion, it's one of the safe messaging app. Next, we need to find their usernames, the easiest way is that you run Wire on their machine:

![image](https://github.com/user-attachments/assets/87dad8cb-8c0c-4712-9fd6-823f6f777edf)

If you don't want to open VMware, inside Wire configurations you can check **/home/imsadboi/.config/Wire/IndexedDB/https_app.wire.com_0.indexeddb.leveldb/000003.log**. During their conversation, they traded file together:

![image](https://github.com/user-attachments/assets/3a5e185f-3be4-4d8e-8b5b-1b2c365670ac)

To know that whether they downloaded it or not, we can check easily in Firefox history, which is stored in **places.sqlite**:

![image](https://github.com/user-attachments/assets/ed7a1dd0-9cbd-4ec8-a9bb-e9d416b9b281)

![image](https://github.com/user-attachments/assets/25d7d985-4c3b-4756-95b4-095dde3bc843)

After they had downloaded the file, I'm sure that the file is still be there, we found it on system. Unzip and it will extract .git folder, from that we used `git log`:

![image](https://github.com/user-attachments/assets/61898e4d-22ac-4696-b737-462657678894)

For the last two challenges, I used ArsenalImageMounter and choose Recovery Files, you can recover the original credentials.txt:

![image](https://github.com/user-attachments/assets/05227025-68b8-4798-be94-7269e8fa3799)

That's all my progress. Thank you very much for reading my blog. See you in the next post. Bye!!! 🫀🫀🫀 
