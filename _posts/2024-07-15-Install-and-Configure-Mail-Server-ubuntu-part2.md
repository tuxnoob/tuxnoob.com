---
title: "Install and Configure Mail Server on Ubuntu 22.04 with Postfix, Dovecot and Roundcube: Step-by-Step Complete Guide - Part 2"
author: arief
date: 2024-07-15 20:00:00 +07:00
categories: [Infrastructure]
tags: [Mail Server, Postfix, Dovecot, Ubuntu, Linux, Database, SPF, Cloudflare, DKIM, DMARC, Domain, Roundcube, Namecheap]
---


In previous article has create the [configuration postfix and dovecot](https://www.tuxnoob.com/posts/Install-and-Configure-Mail-Server-ubuntu-part1/), because the article has too long so i split this article into sections.

### Configure Postgrey
Postgrey is postfix policy server for greylisting. Greylisting is an innovative technique for significantly reducing spam at the mail server level. Unlike complex statistical or heuristic methods, greylisting is lightweight and efficient, potentially decreasing network traffic and processor load on your mail server.

So open your terminal:

```sh
sudo vim /etc/postgrey/whitelist_clients.local
```

Fill the file with this content:

```plaintext
# Clients List
gmail.com
yahoo.com
outlook.com
facebook.com
hotmail.com
msn.com
linkedin.com
pinterest.com
reddit.com
twitter.com
```

Save and exist the editor.

### Configure Clam AntiVirus, Amavis and SpamAssassin

Clam AntiVirus is a GPL-licensed, open-source antivirus toolkit for UNIX. It includes a range of utilities such as a flexible and scalable multi-threaded daemon, a command line scanner, and an advanced tool for automatic database updates.

Run this command to add user

```sh
sudo adduser clamav amavis
sudo adduser amavis clamav
```

Then configure amavis

```sh
sudo vim /etc/amavis/conf.d/15-content_filter_mode
```

fill with this content:

```plaintext
-----

@bypass_virus_checks_maps = (

   \%bypass_virus_checks, \@bypass_virus_checks_acl, \$bypass_virus_checks_re);

-----

@bypass_spam_checks_maps = (

   \%bypass_spam_checks, \@bypass_spam_checks_acl, \$bypass_spam_checks_re);

-----
```

Edit amavis user:

```sh
sudo vim /etc/amavis/conf.d/50-user
```

```plaintext
-----

$max_servers = 3;

$sa_tag_level_deflt = -9999;



@lookup_sql_dsn = (

['DBI:mysql:database=<your-database>;host=127.0.0.1;port=3306',

'<your-user-database>',

'<your-database-password>']);

$sql_select_policy = 'SELECT domain from domain WHERE CONCAT("@",domain) IN (%k)';

-----

-----
```

In above please replace `<your-user-database>`, `<your-database-password>` and `<your-database>`.

Enable spamassassin

```sh
sudo update-rc.d spamassassin enable
```

Update config:

```sh
sudo vim /etc/default/spamassassin
```

Fill with this content:

```plaintext
CRON=1
```

Restart the clam antivirus database:

```sh
sudo /etc/init.d/clamav-freshclam stop
sudo freshclam -v
sudo /etc/init.d/clamav-freshclam start
```

### Configure OpenDKIM

OpenDKIM is a community-driven project that develops and maintains a C library for creating DKIM-aware applications and an open-source milter for delivering DKIM services. OpenDKIM is an open-source implementation of the DKIM (Domain Keys Identified Mail) sender authentication system, standardized by the IETF (RFC6376). It also includes implementations of the Vouch By Reference (VBR, RFC5617) proposed standard and the experimental Authorized Third Party Signatures protocol (ATPS, RFC6541).

```sh
sudo vim /etc/default/opendkim
```

Comment out

```plaintext
#SOCKET=local:$RUNDIR/opendkim.sock
```

and add last

```
SOCKET="inet:8891@localhost"
```

```sh
sudo vim /etc/opendkim.conf
```

Comment out

```plaintext
#Socket			local:/run/opendkim/opendkim.sock
```

And add

```
Socket			inet:8891@localhost
Domain example.com
KeyFile /etc/postfix/dkim.key
Selector dkim
```

```sh
sudo mkdir /apps/dkim
cd /apps/dkim
sudo opendkim-genkey -t -s dkim -d example.com
sudo mv dkim.private /etc/postfix/dkim.key
sudo chmod 660 /etc/postfix/dkim.key
sudo chown root:opendkim /etc/postfix/dkim.key

# Restart OpenDKIM
sudo service opendkim restart

# Reload and restart Postfix
sudo service postfix reload
sudo service postfix restart
```

```sh
cat /apps/dkim/dkim.txt

dkim._domainkey	IN	TXT	( "v=DKIM1; h=sha256; k=rsa; t=y; "
	  "p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA1Y5Rx/J2HrcQrP7HJhKWaUtALG9jlWxbkwemaWnb7m0b4bePi0+/vanfn6Iqd0nA6rFbNJUsmjzthw2CF5lhmpyD6YwVRF/wGVJAs7B1x6Zw/WiBhxuERDhuCSEA+Z9sIPMrQnNbr0xFgCFM905PKSrJf1Eq8Z+4jGL6q6mb8EyAPzTdKBVycVh0KWoejgoe0whIhuodTzQLBj"
	  "Rh3NkaUA2iOQgAWYZURVcHhp6SDIhAP3y/AF/0amJ7csu1DVsFcOzdE19KYu1WFzys//m8TXrUqyLIVJxxuy7jCjG4CUa3/vOJcNdnpaIftrtxH7naH54l8DVN2iHo" )  ; ----- DKIM key dkim for example.com
```

Remove all the double quotes and generate a single line record as shown below.

```plaintext
# Valid DKIM

v=DKIM1;p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA1Y5Rx/J2HrcQrP7HJhKWaUtALG9jlWxbkwemaWnb7m0b4bePi0+/vanfn6Iqd0nA6rFbNJUsmjzthw2CF5lhmpyD6YwVRF/wGVJAs7B1x6Zw/WiBhxuERDhuCSEA+Z9sIPMrQnNbr0xFgCFM905PKSrJf1Eq8Z+4jGL6q6mb8EyAPzTdKBVycVh0KWoejgoe0whIhuodTzQLBjRh3NkaUA2iOQgAWYZURVcHhp6SDIhAP3y/AF/0amJ7csu1DVsFcOzdE19KYu1WFzys//m8TXrUqyLIVJxxuy7jCjG4CUa3/vOJcNdnpaIftrtxH7naH54l8DVN2iHo
```

Add a TXT record as shown below.

```
Name				            Type	Value 			        TTL  

dkim._domainkey.example.com.	TXT	    "single line record"	300
```

### Restart All Service

```sh
sudo systemctl restart apache2
sudo systemctl restart postfix
sudo systemctl restart dovecot
sudo service clamav-daemon restart
sudo service amavis restart
sudo service spamassassin restart
sudo systemctl restart opendkim
sudo systemctl restart postgrey
```

Load postfix maps

```sh
sudo postmap /etc/postfix/client_checks
sudo postmap /etc/postfix/sender_checks
sudo postfix reload
```

### Open ports

After installing all the necessary software and utilities, you need to open the email ports by updating your firewall. You can either configure the firewall provided by your hosting provider or use UFW to open ports 25, 465, 587, 995, 143, and 993.


### Install Postfix Admin
Download and extract Postfix Admin.

```sh
cd /apps
wget https://github.com/postfixadmin/postfixadmin/archive/postfixadmin-3.3.10.tar.gz
tar -xvf postfixadmin-3.3.10.tar.gz
mv postfixadmin-postfixadmin-3.3.10 postfixadmin
cd postfixadmin
cp config.inc.php.sample config.inc.php
```

### Configure Postfix Admin
Edit the Postfix Admin configuration file.

```sh
sudo nano /apps/postfixadmin/config.inc.php
```

Update the following settings:

```php
$CONF['database_type'] = 'mysqli';
$CONF['database_host'] = 'localhost';
$CONF['database_user'] = 'postfixadmin';
$CONF['database_password'] = 'password';
$CONF['database_name'] = 'postfixadmin';
$CONF['configured'] = true;
```

### Set Permissions
Ensure proper permissions for the web directory.

```bash
sudo chown -R www-data:www-data /apps/postfixadmin
```

### Configure Apache2 for Postfix Admin
Create an Apache configuration file for Postfix Admin.

```bash
sudo nano /etc/apache2/sites-available/postfixadmin.conf
```

Add the following configuration:

```apache
<VirtualHost *:80>
    ServerAdmin admin@example.com
    DocumentRoot /var/www/html/postfixadmin
    ServerName mail.example.com
    <Directory /var/www/html/postfixadmin/>
        Options FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/postfixadmin_error.log
    CustomLog ${APACHE_LOG_DIR}/postfixadmin_access.log combined
</VirtualHost>
```

Enable the new site and rewrite module.

```bash
sudo a2ensite postfixadmin.conf
sudo a2enmod rewrite
sudo systemctl restart apache2
```

### Complete Postfix Admin Setup via Web Browser
Open your web browser and navigate to `http://mail.example.com/setup.php` to complete the Postfix Admin setup.
- Follow the on-screen instructions to create the setup password with generate password hash, don't forget save the password hash.
- Enter the setup password and create the Postfix Admin superuser.

### Secure Apache with SSL (Optional)
To secure your Postfix Admin interface with SSL, you can use Let's Encrypt to obtain a free SSL certificate.

Install Certbot.

```bash
sudo apt install certbot python3-certbot-apache -y
```

Obtain an SSL certificate.

```bash
sudo certbot --apache -d mail.example.com
```

Follow the prompts to complete the certificate installation.

Hover the Domain List option on the Main Menu and click the New Domain option. Specify the domain name as example.com and click the Add Domain Button. It will add the virtual domain example.com.

Hover the Virtual List option on the Main Menu and click Add Mailbox option. Specify the username as admin, fill other details and click the Add Mailbox Button. It will add the virtual user admin@example.com. Similarly, add another mailbox netban@example.com as configured with Fail2ban to receive all the emails from it.

Notes: There is a known bug in PostfixAdmin as shown below.


Invalid query: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'row FROM `mailbox` LEFT JOIN `alias` ON `mailbox`.username=`alias`.address L' at line 2

In case you get the above error, it means you have already created 10 mailboxes for a domain. The workout is to increase the pagination size as shown below.

# Postfix Admin - Local Config

```sh
sudo vim /apps/postfixadmin/config.local.php
```

Add configuration

```php
-----

$CONF['create_mailbox_subdirs_prefix']='';

-----

$CONF['page_size'] = '1000';

-----
```

Another case, if you get a log error like this

```plaintext
warning: pipe flag `D' requires dovecot destination recipient limit = 1
```

You should edit in postfix

```sh
sudo vim /etc/postfix/main.cf
```

Add this line

```plaintext
default_destination_recipient_limit = 1
```

Save and restart your postfix and dovecot.

Now testing the email with client like thunderbird, Next will configure with webmail client (roundcube)