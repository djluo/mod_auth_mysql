BUILDING mod_auth_mysql
=======================

To build mod_auth_mysql as a DSO:

For either Apache 1.x or Apache 2.x:

apxs -c -lmysqlclient -lm -lz mod_auth_mysql.c

Note: The option -D APACHE2 for Apache 2.x is no longer required.  The module 
determines the correct version from the Apache header files

If the mysql.h header file cannot be found, add the -I option to specify the
directory where mysql.h can be found.

If the mysqlclient library cannot be found, add the -L option to specify the
directory where libmysqlclient.so can be found.  

Example:

apxs -c -L/usr/lib/mysql -I/usr/include/mysql -lmysqlclient -lm -lz mod_auth_mysql.c


IMPORTANT NOTE: Some recent distributions of mysql (i.e. Debian) do not include
my_aes.h and rijndael.h.  These are available from the MySQL and other web sites.


INSTALLING in the Apache Directory
==================================

After building the module, you need to install it to your modules directory.

Apache 1.x:
apxs -i mod_auth_mysql.so

Apache 2.x:
apxs -i mod_auth_mysql.la

Next, add the following directive to httpd.conf:
LoadModule mysql_auth_module modules/mod_auth_mysql.so


Additional Compiler Options
===========================

You can specify the following compile time options with the -D parameter
to set default values for many of the configuration paramters (see CONFIGURATION
for descriptions of the options)

Example:

apxs -c -DHOST=localhost -lmysqlclient -lm -lz mod_auth_mysql.c


Configuration Parameter		Option		Valid Values (1)(2)
-----------------------		------		------------
AuthMySQLHost			HOST		"localhost", host name or ip address
AuthMySQLPort			PORT		integer port number
AuthMySQLSocket			SOCKET		full path name of UNIX socket to use
AuthMySQLUser			USER		MySQL user id
AuthMySQLPassword		PASSWORD	MySQL password
AuthMySQLDB			DB		MySQL database
AuthMySQLPwTable		PWTABLE		MySQL table to use
AuthMySQlNameField		NAMEFIELD	MySQL column name
AuthMySQLPasswordField		PASSWORDFIELD	MySQL column name
AuthMySQLPwEncryption		ENCRYPTION (3)	"none", "crypt", "scrambled", "md5", "aes", "sha1"
AuthMySQLSaltField		SALT		"<>", <string> or MySQL column name
AuthMySQLKeepAlive		KEEPALIVE	"0", "1"
AuthMySQLAuthoritative		AUTHORITATIVE	"0", "1"
AuthMySQLNoPassword		NOPASSWORD	"0", "1"
AuthMySQLEnable			ENABLE		"0", "1"
AuthMySQLCharacterSet		CHARACTERSET	MySQL character set to use

Notes:
(1) Values in quotes are valid values.  Do not use the quotes in the compile
    line, i.e.
    WRONG:
	apxs -c -D HOST="localhost" ... 
    RIGHT:
	apxs -c -D HOST=localhost
	
    Other values not in quotes are descriptions of the values to be entered.

(2) For 0 and 1 values, 0 is false and 1 is true

(3) If this option is specified, you will NOT be able to use the following
    (depricated) options in your Apache configuration:
	AuthMySQLCryptedPasswords
	AuthMySQLScrambledPasswords
	AuthMySQLMD5Passwords
    You will be able to override the default with the AuthMySQLPwEncryption parameter.


crypt.h and unistd.h
====================

This module uses the crypt() function with Apache 2 for encryption.  Previous
versions of mod_auth_mysql have included crypt.h to declare the crypt()
function.  However, this is file has not been updated for quite some time, and
in some systems (i.e. FreeBSD), has been replaced by unistd.h.

mod_auth_mysql will now use the newer unistd.h file to declare the crypt()
function.  If this file does not exist on your system, or otherwise causes you
problems, you can use the parameter -DCRYPT to include the older crypt.h file
instead.  There are no parameters for this value.


