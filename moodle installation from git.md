$ cd /path/to/your/webroot
$ git clone git://git.moodle.org/moodle.git                       (1)
$ cd moodle
$ git branch -a                                                   (2)
$ git branch --track MOODLE_34_STABLE origin/MOODLE_34_STABLE     (3)
$ git checkout MOODLE_34_STABLE                                   (4)


admin/Admin@moodle.1
hokhyk/12345!qA



there are three other settings that limit the size of a file that can be uploaded to your server. The first two are PHP settings and the third is an Apache setting. To see the PHP settings on your server, go to Site Administration | Server | PHP info. Scroll down until you see post_max_size and upload_max_filesize.
The Apache setting LimitRequestBody also sets a limit on the size of uploaded files.

Changing the limit on uploaded file size in PHP
If you have your own server, you can change the values for post_max_size
and upload_max_filesize in the file php.ini. You will usually find this file
in /apache/bin.
If you are using someone else's server (such as a hosting service), you probably can't
change anything in php.ini. Try creating a file called .htaccess in the root of your
Moodle installation that contains the following lines:
php_valuevaluepost_max_sizesize128M
php_valuevalueupload_max_filesizefilesize128M
Replace 128M with any value that you need. If the server times out while uploading
large files, you might add lines like the following to .htaccess:
php_valuevaluemax_input_time 600
php_valuevaluemax_execution_time 600
The variables max_execution_time and max_input_time set the maximum time
allowed by a page to upload and process the files to be uploaded. If you will be
uploading several megabytes of data, you may want to increase this setting. The
execution time is specified in milliseconds (thousandths of a second). You can check
your host settings for these under Site Administration | Server | PHP info.

Then, place .htaccess into the directory with the PHP scripts that you want to run.
For example, the script for uploading files is in the directory /files.
Your hosting service can disable .htaccess, which would make this solution
impossible. You would need to ask your hosting service to change these values
for you.
Changing the limit on uploaded file size in Apache
Just like you might be able to use .htaccess to override the PHP settings, you also
might be able to use it to override the Apache settings. For example, placing the
following line in .htaccess changes the limit on uploaded files to 10 MB:
LimitRequestBody 10240000
Notice that the limit is specified in bytes, not megabytes. Setting it to zero will make
the setting unlimited. The highest number you can specify is 2147483647, or 2 GB.

