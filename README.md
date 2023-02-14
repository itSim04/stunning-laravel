## Introduction

The purpose of this exercise is deploying a Laravel website on an Ubuntu Server. This file will consist of a report of the steps taken.

<hr>

## Commands Used

<ul>
    <li><b><a id="sudo">sudo</a></b>: Runs a command with elevated privileges. It is used to perform certain tasks. It should be used with most of the commands.</li>
    <li><b><a id="apt-get">apt-get install [package-name]</a></b>: Used to install, delete and modify software. It is used to manage packages (requires <a href="#sudo">sudo</a>)</li>
    <li><b><a id="ssh">ssh -i private-key.pem ubuntu@ec2-3-249-245-204.eu-west-1.compute.amazonaws.com</a></b>: It establishes a secure connection with the     server. -i is used to provide a private key.</li>
    <li><b><a id="a2enmod_rewrite">a2enmod rewrite</a></b>: (requires <a href="#sudo">sudo</a>)</li>
    <li><b><a id="restart">systemctl restart apache2 (requires <a href="#sudo">sudo</a>)</a></b>: Restarts apache</li>
    <li><b><a id="cd">cd [path]</a></b>: Navigates to the chosen path.</li>
    <li><b><a id="pwd">pwd</a></b>:Prints the current working directory.</li>
    <li><b><a id="clone">git clone [repo]</a></b>: Clones the specified repo in the current directory (requires <a href="#sudo">sudo</a>)</li>
    <li><b><a id="curl-php">curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin — filename=composer</a></b></li>
    <li><b><a id="composer-install">composer install (requires <a href="#sudo">sudo</a>)</a></b></li>
    <li><b><a id="cp">cp [source] [destination]</a></b>: Copies the source file into a destination file (requires <a href="#sudo">sudo</a>)</li>
    <li><b><a id="vim">vim [file]</a></b>: Prompts a file to be edited (requires <a href="#sudo">sudo</a>)</li>
    <li><b><a id="find">find / -name "apache2.conf"</a></b>: Searches for a file</li>
    <li><b><a id="php-generate">php artisan key:generate</a></b>: Generates a key (requires <a href="#sudo">sudo</a>)</li>
    <li><b><a id="chgrp">chgrp -R www-data storage bootstrap/cache</a></b>: Recursively changes the group of every file/folder at the specified directory (requires <a href="#sudo">sudo</a>)</li>
    <li><b><a id="chmod">chmod -R ug+rwx storage bootstrap/cache</a></b>: Recursively adds read, write and execute permissions to every file/folder at the specified directory (requires <a href="#sudo">sudo</a>)</li>
    <li><b><a id="which">which [program-name]</a></b>: Returns the installation directory of a certain program</li>
</ul>
    
<hr>

### Checkpoint 1:

<ol>
    <li><a id="1-1">The laravel website is already made we only have to <a href="https://github.com/NinjaCoder8/stunning-laravel">fork it</a></a></li>
    <li>Establish a secure connection to the server using <a href="#ssh">ssh</a></li>
    <li>Install the needed packages using <a href="#apt-get">apt-get</a>: apache2, mysql-server, php-mysql, php, libapache2-mod-php, php-mcrypt, php-           pear, curl, php-curl, php-cli, git</li>
    <li>Execute the command <a href="#a2enmod_rewrite">a2enmod</a></li>
    <li>Restart apache using <a href="#restart">restart</a></li>
</ol>

<hr>

### Checkpoint 2:

<ol>
    <li>Navigate to the html folder of the server <i>/var/www/html</i> using the <a href="cd">cd command</a>. 
    <li>Check the current active directory using <a href="pwd">pwd</a></li>
    <li>Clone the repo forked in <a href="#1-1">1.1</a> using <a href="#clone">clone</a></li>
</ol>

<hr>
    
### Checkpoint 3:

<ol>
    <li>Download the composer using this <a href="#curl-php">piped command</a></li>
    <li>Initialize the Composer using <a href="#composer-install">install</a></li>
</ol>  

<hr>

### Checkpoint 4:

<ol>
    <li>Confirm that the repo is the current active directory using <a href="pwd">pwd</a></li>
    <li>Copy the file .env.example and name the copy .env using the <a href="cp">cp command</a></li>
    <li>Open the newly created file using the <a href="#vim">vim command</a></li>
    <li>Click <b>i</b> to enter insert mode</li>
    <li>Give APP_NAME a value (exclude whitespace)</li>
    <li>Unfocus using the escape key</li>
    <li>Enter the exit sequence <b>:x</b> to exit and save the file</li>
    <li>Generate a Key using the <a href="#php-generate">generate command</a></li>
    
</ol>

<hr>

### Checkpoint 5:

<ol>
    <li>Validate the installation of <b>apache2</b> using <a href="#which">which</a></li>
    <li>Search for the file <b>apache2.conf</b> using the <a href="#find">find command</a></li>
    <li>Navigate to the file using <a href="#cd">cd</li>
    <li>Open the file using the <a href="#vim">vim command</a></li>
    <li>Click <b>i</b> to enter insert mode</li>
    <li>Add the following lines near the end of the file:</li>
        
    <Directory /var/www/html/stunning-laravel/public>
        Options Indexes FollowSymLinks
        AllowOverride all
        Require all granted
    </Directory>
        
   
   <li>Unfocus using the escape key</li>
   <li>Enter the exit sequence <b>:x</b> to exit and save the file</li>
   <li>Navigate to the repo <b>sites-enabled</b> using <a href="#cd">cd</li>
   <li>Open the file <b>000-default.conf</b> using the <a href="#vim">vim command</a></li>
   <li>Click <b>i</b> to enter insert mode</li>
   <li>Add the following lines under the line <b><VirtualHost *:80></b></li>
       
     ServerAdmin webmaster@localhost
     DocumentRoot /var/www/html/stunning-laravel/public/:
       
   <li>Remove all similar lines from the file</li>
   <li>Unfocus using the escape key</li>
   <li>Enter the exit sequence <b>:x</b> to exit and save the file</li>
   <li>Restart apache using <a href="#restart">restart</a></li>
  </ol>

<hr>

### Checkpoint 6:

<ol>
    <li>Navigate to the repo (<b>/var/www/html/[repo-name]</b>) using <a href="#cd">cd</a></li>
    <li>Execute the command <a href="#chgrp">chgrp</a></li>
    <li>Execute the command <a href="#chmod">chmod</a></li>
    <li>Restart apache using <a href="#restart">restart</a></li>
</ol>
