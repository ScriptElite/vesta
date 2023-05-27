
<h1 align="center"><a href="https://myvestacp.com">myVesta</a></h1>

<div style="text-align:center">

[![Screenshot of myVesta](https://www.myvestacp.com/screenshot1.png)](https://www.myvestacp.com/)

</div>

<h1 align="center">About</h1>

<p align="center">myVesta is a security and stability-focused fork of VestaCP, exclusively supporting Debian in order to maintain a streamlined ecosystem. Boasting a clean, clutter-free interface and the latest innovative technologies, our project is committed to staying synchronized with official VestaCP commits. We work independently to enhance security and develop new features, driven by our passion for contributing to the open-source community rather than monetary gain. As such, we will offer all features built for myVesta to the official VestaCP project through pull requests, without interfering with their development milestones.</p>

<p align="center"><b><a href="https://github.com/myvesta/vesta/blob/master/Changelog.md">View Changelog</a>
</b></p>

<h1>Links</h1>
<ul>
  <li><a href="https://www.myvestacp.com/">Visit our homepage.</a></li>
  <li><a href="https://forum.myvestacp.com/">Check out our forum for discussions and support.</a></li>
  <li><a href="https://wiki.myvestacp.com/">For more information, take a look at our knowledge base.</a></li>
</ul>

<h1>Features of myVesta</h1>
<ul>
    <li>Support for Debian 10 and 11 (Debian 11 is recommended, but previous Debian releases are also supported)</li>
    <li>Support for MySQL 8</li>
    <li><a href="https://forum.myvestacp.com/viewtopic.php?f=20&t=51">nginx templates</a> that can prevent denial-of-service on your server</li>
    <li><a href="https://forum.myvestacp.com/viewtopic.php?f=18&t=52">Support for multi-PHP versions</a></li>
    <li>You can <a href="https://forum.myvestacp.com/viewtopic.php?f=20&t=350">host NodeJS apps</a></li>
    <li>You can limit the maximum number of sent emails (per hour) <a href="https://github.com/myvesta/vesta/blob/master/install/debian/10/exim/exim4.conf.template#L112-L113">per mail account</a> and <a href="https://github.com/myvesta/vesta/blob/master/install/debian/10/exim/exim4.conf.template#L72-L73">per hosting account</a>, preventing hijacking of email accounts and preventing PHP malware scripts to send spam.</li>
    <li>
      You can completely "lock" myVesta so it can be accessed only via secret URL, for example https://serverhost:8083/?MY-SECRET-URL
      <ul>
        <li>During installation you will be asked to choose a secret URL for your hosting panel</li>
        <li>Literally no PHP scripts will be alive on your hosting panel (won't be able to get executed), unless you access the hosting panel with secret URL parameter. Thus, when it happens that, let's say, some zero-day exploit pops up - attackers won't be able to access it without knowing your secret URL - PHP scripts from VestaCP will be simply dead - no one will be able to interact with your panel unless they have the secret URL.</li>
        <li>You can see for yourself how this mechanism was built by looking at:</li>
        <ul>
          <li><a href="https://github.com/myvesta/vesta/blob/master/src/deb/for-download/php/php.ini#L496">src/deb/for-download/php/php.ini</a></li>
          <li><a href="https://github.com/myvesta/vesta/blob/master/web/inc/secure_login.php">web/inc/secure_login.php</a></li>
        </ul>
        <li>If you didn't set the secret URL during installation, you can do it anytime. Just execute in shell: <code>echo "&lt;?php \$login_url='MY-SECRET-URL';" > /usr/local/vesta/web/inc/login_url.php</code></li>
      </ul>
    </li>
  <li>We <a href="https://github.com/myvesta/vesta/blob/master/install/debian/10/php/php7.3-dedi.patch#L9">disabled dangerous PHP functions</a> in php.ini, so even if, for example, your customer's CMS gets compromised, hacker will not be able to execute shell scripts from within PHP.</li>
  <li>Apache is fully switched to mpm_event mode, while PHP is running in PHP-FPM mode, which is the most stable PHP-stack solution
    <ul><li>OPCache is turned on by default</li></ul>
    <li>Auto-generating LetsEncrypt SSL for server hostname (signed SSL for Vesta 8083 port, for dovecot (IMAP & POP3) and for Exim (SMTP))</li>
    <li>You can change Vesta port during installation or later using one command line: v-change-vesta-port [number]</li>
    <li>ClamAV is configured to block zip/rar/7z archives that contains executable files (just like GMail)</li>
    <li>Backup will run with lowest priority (to avoid load on server), and can be configured to run only by night (and to stop on the morning and continue next night) </li>
    <ul>
    <li>You can compile Vesta binaries by yourself - <a href="https://github.com/myvesta/vesta/blob/master/src/deb/vesta_compile.sh">src/deb/vesta_compile.sh</a></li>
<li>You can even create your own APT repository in a minute</li>
<li>We are using latest nginx version for vesta-nginx package</li>
<li>With your own APT infrastructure you can take security of Vesta-installer infrastructure in your own hands. You will have full control of your Vesta code (this way you can rest assured that there's 0% chance that you'll install malicious packages from repositories that may get hacked)</li>
<li>Binaries that you compile are 100% compatible with official VestaCP from vestacp.com, so you can run official VestaCP code with your own binaries (in case you don't want the source code from this fork)</li>
</ul>
    
  </li>
  </ul>
  
<h1>How to install</h1>
Download the installation script:

```shell
curl -O http://c.myvestacp.com/vst-install-debian.sh
```

Then run it:

```shell
bash vst-install-debian.sh
```

Or use our <a href="https://www.myvestacp.com/install_generator.html">installer generator</a>.

<h1>Useful scripts</h1>
<ul>
  <li><a href="https://forum.myvestacp.com/viewtopic.php?f=24&t=50">How to move accounts from one (my)Vesta server to another myVesta server</a></li>
  <li><a href="https://forum.myvestacp.com/viewtopic.php?f=17&t=386">WordPress installer in one second </a></li>(v-install-wordpress)
  <li><a href="https://forum.myvestacp.com/viewtopic.php?f=17&t=385">Cloning script that will copy the whole site from one (sub)domain to another (sub)domain </a></li>(v-clone-website)
  <li><a href="https://forum.myvestacp.com/viewtopic.php?f=17&t=382">Script that will migrate your site from http to https, replacing http to https URLs in database </a></li>(v-migrate-site-to-https)
  <li><a href="https://forum.myvestacp.com/viewtopic.php?f=24&t=63">Script for importing cPanel backups to Vesta (thanks to Maks Usmanov - Skamasle) </a></li> (v-import-cpanel-backup)
  <li><a href="https://forum.myvestacp.com/viewtopic.php?f=18&t=52">Script that will install multiple PHP versions on your server</a></li>
  <li><a href="https://forum.myvestacp.com/viewtopic.php?f=20&t=350">How to host NodeJS apps</a></li>
  <li><a href="https://forum.myvestacp.com/viewtopic.php?f=20&t=51">Script that will install nginx templates that can prevent denial-of-service on your server</a></li>
  <li><a href="https://forum.myvestacp.com/viewtopic.php?f=15&t=47">Official VestaCP Softaculous installer</a></li>
</ul>


<h1>Licence</h1>
myVesta is licensed under <a href="https://github.com/serghey-rodin/vesta/blob/master/LICENSE">GPL v3</a> license.


