---
title: 4 Tools Send Email Subject, Body And Attachment In Mail Linux
date: '2016-06-27T06:59:00.000+07:00'
author: Arief JR
tags: [Email, Send Email, Linux Mail, Email Tools, Shell Script, Slackware]
categories: [Linux, Programming]
---

Today i will share about mail tools in linux default with shell script, yep this mail using **command line** not graphical. In **Slackware Linux** the mail was include 3 tools i.e **Mailx**,**Mutt And Sharutils**.  

This post will tell send mail using command line with **shell scripts** at the end post. But i will discuss using 4 mail tools i.e **Mailx**, **Mutt**, **Swaks** and **Sharutils**.  

Many various command for send mail between tools which provide in linux. So keep your eyes.... As i said earlier, in linux was included mail tools as default. If not you can following the command for installation:

**For Ubuntu/Debian**

```
$ sudo apt-get install mailx $ sudo apt-get install mutt $ sudo apt-get install swaks $ sudo apt-get install sharutils 
```

**For Redhat-Based**

```
$ sudo yum install mailx $ sudo yum install mutt $ sudo yum install swaks $ sudo yum install sharutils  
```

* #### **Using Mailx** 

The mailx tools was found as default mail app in most linux distro's, and included the support to attach file. If is not available you can following the command in above, to check this mailx you can use the command:

```
MAILX(1)                        User Commands                       MAILX(1)  

NAME  
       mailx - send and receive Internet mail  

SYNOPSIS  
       mailx [-BDdEFintv~] [-s subject] [-a attachment ] [-c cc-addr]  
              [-b bcc-addr] [-r from-addr] [-h hops] [-A account] [-S vari-  
              able[=value]] to-addr . . .  
       mailx [-BDdeEHiInNRv~] [-T name] [-A account] [-S variable[=value]]  
              -f [name]  
       mailx [-BDdeEinNRv~] [-A account] [-S variable[=value]] [-u user]  

DESCRIPTION  
       Mailx is an intelligent mail processing system, which has  a  command  
       syntax  reminiscent  of ed(1) with lines replaced by messages.  It is  
       based on Berkeley Mail 8.1, is intended to provide the  functionality  
       of  the  POSIX  mailx  command, and offers extensions for MIME, IMAP,  
       POP3, SMTP, and S/MIME.  Mailx provides enhanced features for  inter-  
       active use, such as caching and disconnected operation for IMAP, mes-  
       sage threading, scoring, and filtering.  It is also usable as a  mail  
       batch language, both for sending and receiving mail.  
  
       The following options are accepted:  
  
       -A name  
              Executes  an  account  command  (see below) for name after the  
              startup files have been read.  
  
       -a file  
              Attach the given file to the message.  
  
       -B     Make standard input and standard output line-buffered.`  
```

1.  Simple mail

Run mail command, and the mailx would wait for you to enter the message of the email. You can hit enter for new lines. When finish typing the message, press Ctrl+D and mail will be display EOT.  

After that mailx automatically send the email to destination.  
```
$ mail user@example.com  

Hi,  
Good Morning  
How are you  
EOT
```

2.  Send email with subject

`$ echo "Text mail" | mail -s "Test Dude" user@example.com`  

-s is used for defining subject for email.

3. Send message from a file

`$ mail -s "message send from file" user@example.com < /path/to/file`

4. Send message piped using echo command

`$ echo "Message body" | mail -s "Subject" user@example.com`

5. Send mail with attachment

`$ echo "Body with attachment" | mail -a darknet.sh -s "attached file" user@example.com`

-a is used for attachments

* #### **Using Mutt**

Like **Mailx** mutt is a text-based mail client for Unix-Like systems. It was developed over 20 years ago and it's an important part of linux history, one of first clients to support scoring and threading capabilities. See this belo examples to send mail:

6.  Send mail with subject & body message from a file

`$ mutt -s "Test" user@example.com < /tmp/message.txt`  

7.  Send body message piped using echo command

`$ echo "This message" | mutt -s "Test" user@example.com`  

8. Send mail with attachment

`$ echo "This is a message" | mutt -s "Send testing" user@example.com -a /tmp/darknet.sh`  

9. Send email with multiple attachments

`$ echo "This is message" | mutt -s "Testing" user@example.com -a darknet.sh --a 9unz1p.zip`  


* #### Swaks

Swaks stands for Swiss Army Knife for SMTP and it is a featureful, flexible, scriptable, transaction-oriented SMTP test tool written and maintained by John Jetmore. You can use the following syntax to send an email with attachment:

```
$ swaks -t "darknet@9unZ1p.com" --header "Subject: Subject" --body "Email Text" --attach darknet.tar.gz
```

The important thing about Swaks is that it will also debug the full mail transaction for you, so it is a very useful tool if you also wish to debug the mail sending process:  

As you can see it gives you full details about the sending process including what capabilities the receiving mail server supports, each step of the transaction between the 2 servers.

* #### uuencode

Email transport systems were originally designed to transmit characters with a seven-bit encoding -- like ASCII. This meant they could send messages with plain text but not "binary" text, such as program files or image files that used all of an eight-bit byte. The program is used to solve this limitation is “uuencode”( "UNIX to UNIX encoding") which encode the mail from binary format to text format that is safe to transmit & program is used to decode the data is called “uudecode”  

We can easily send binary text such as a program files or image files using uuencode with mailx or mutt email client is shown by following example:

```
$ uuencode example.jpeg example.jpeg | mail user@example.com
```

### Using Shell Script To Sending Mail

```
#!/bin/bash

FROM=""
SUBJECT=""
ATTACHMENTS=""
TO=""
BODY=""

# Function to check if entered file names are really files
function check_files()
{
output_files=""
for file in $1
do
if [ -s $file ]
then
output_files="${output_files}${file} "
fi
done
echo $output_files
}

echo "*********************"
echo "E-mail sending script."
echo "*********************"
echo

# Getting the From address from user
while [ 1 ]
do
if [ ! $FROM ]
then
echo -n -e "Enter the e-mail address you wish to send mail from:\n[Enter] "
else
echo -n -e "The address you provided is not valid:\n[Enter] "
fi

read FROM
echo $FROM | grep -E '^.+@.+$' > /dev/null
if [ $? -eq 0 ]
then
break
fi
done

echo

# Getting the To address from user
while [ 1 ]
do
if [ ! $TO ]
then
echo -n -e "Enter the e-mail address you wish to send mail to:\n[Enter] "
else
echo -n -e "The address you provided is not valid:\n[Enter] "
fi

read TO
echo $TO | grep -E '^.+@.+$' > /dev/null
if [ $? -eq 0 ]
then
break
fi
done

echo

# Getting the Subject from user
echo -n -e "Enter e-mail subject:\n[Enter] "
read SUBJECT

echo

if [ "$SUBJECT" == "" ]
then
echo "Proceeding without the subject..."
fi

# Getting the file names to attach
echo -e "Provide the list of attachments. Separate names by space.
If there are spaces in file name, quote file name with \"."
read att

echo

# Making sure file names are poiting to real files
attachments=$(check_files "$att")
echo "Attachments: $attachments"

for attachment in $attachments
do
ATTACHMENTS="$ATTACHMENTS-a $attachment "
done

echo

# Composing body of the message
echo "Enter message. To mark the end of message type ;; in new line."
read line

while [ "$line" != ";;" ]
do
BODY="$BODY$line\n"
read line
done

SENDMAILCMD="mutt -e \"set from=$FROM\" -s \"$SUBJECT\" \
$ATTACHMENTS -- \"$TO\" <<< \"$BODY\""
echo $SENDMAILCMD

mutt -e "set from=$FROM" -s "$SUBJECT" $ATTACHMENTS -- $TO <<< $BODY
```

### Script Output

```
$ bash send_mail.sh  
*********************  
E-mail sending script.  
*********************  

Enter the e-mail address you wish to send mail from:  
[Enter] test@gmail.com  

Enter the e-mail address you wish to send mail to:  
[Enter] test@gmail.com  

Enter e-mail subject:  
[Enter] Message subject  

Provide the list of attachments. Separate names by space.  
If there are spaces in file name, quote file name with ".  
send_mail.sh  

Attachments: send_mail.sh  

Enter message. To mark the end of message type ;; in new line.  
This is a message text ;;
```

#### Conclusion

Those this tutorial using **command line** for sending mail in mail app linux. This include shell scripts for easy sending mail just execute this file and run, but for **slackware user's** can't use **swaks** for testing mail with command. I hope you enjoyed reading the article and if i wrong please fill in below box comments or you can give me suggestion. Thanks!