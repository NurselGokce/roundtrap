Roundtrap Responsive Tema
=================

[roundcube.net](http://roundcube.net)


Bu proje roundcube webmail uygulamasına bootstrap kullanarak responsive tema hazırlamak için oluşturulmuştur. 

BAŞLANGIÇ
---------

Rouncube webmail sunucu üzerinde yer alan mailleri web üzerinden ulaşarak e-posta işlemlerinin gerçekleştirilebildiği IMAP mail servisi üzerinde bir web uygulamasıdır. Roundcube PHP ve Javascript ile yazılmış olup veritabanı olarak MYSQL,PostgreSQL or SQLite gerektiriyor. Kullanıcı arayüzü için XHTML ve CSS yorumlanmaktadır. Roundtrap uygulamasında ise amaçlanan roundcube içinde kullanılan CSS ve javascript'ler yerine bootstrap tarafından sağlanan CSS ve javascript'leri kullanarak bootstrap responsive tema hazırlamaktır. Bu kapsamda uygulama da kullanılan roundcube objeleri yerine bootstrap objeleri kullanılacaktır. 
[bootstrap](http://twitter.github.io/bootstrap/)
KURULUM
-------

1. [Bağlantısından](https://github.com/NurselGokce/roundtrap) uygulama sıkıştırılarak veya git kullanıcıları forklayarak uygulama indirilir.  [Nasıl forklanır.](https://help.github.com/articles/fork-a-repo ) 

2. Uygulama var altında www klasörüne taşınarak gerekli izinler verilir :
<pre>
chown root:root -R /var/www/html/roundcube 
chmod 777 -R /var/www/html/roundcube/temp/ 
chmod 777 -R /var/www/html/roundcube/logs/
</pre>
3. Rouncubemail için database oluşturulur. ( bknz : Database Ayarları )

4. Kurulum betikleri ayarlanır. (bknz : Manuel Ayarlar )


DATABASE AYARLARI
-----------------

*  Rouncubemail adında bir veritabanı oluşturulur.
*mysql için :*
<pre>
>CREATE DATABASE roundcubemail /*!40101 CHARACTER SET utf8 COLLATE utf8_general_ci */;
> GRANT ALL PRIVILEGES ON roundcubemail.* TO roundcube@localhost
    IDENTIFIED BY 'password';
> quit 
</pre>

   *not 1 :* 'password' kısmına roundcube kullanıcısı için bir şifre yazılmalıdır. 
    Yeni bir kullanıcı oluşturmadan root kullanıcısı olarakta veritabanı oluşturulabilir.
    

*  SQL klasörü içerisinde bulunan sql dosyası roundcubemail veritabanına import edilir.
<pre>
mysql roundcubemail < SQL/mysql.initial.sql
</pre>



*  Config dosyası içerinde bulunan db.inc.php.dist dosyası db.inc.php olarak kopyalanarak dosya içerisinde aşağıdaki kodun pass kısmına veritabanını oluştururken verilen şifre yazılır.
<pre>
$rcmail_config['db_dsnw'] = 'mysql://roundcube:pass@localhost/roundcubemail';
</pre>

   *not 2 :* Eğer yeni bir kullanıcı ve şifre belirlenmediyse kodda yazan roundcube kısmına root, şifre kısmına ise mysql şifresi yazılır.
   
   *not 3 :* PostgreSQL ve SQLite kullanıcıları için [bağlantısına] (https://github.com/NurselGokce/roundtrap/blob/master/INSTALL) bakabilirler.


MANUEL AYARLAR
-------------

1. config dosyası içerisinde main.inc.php.dist yeniden adlandırılır.
<pre>
cp /var/www/roundcube/config/main.inc.php.dist /var/www/roundcube/config/main.inc.php
</pre>

2. main.inc.php dosyasında aaşağıdaki değişiklikler yapılır.
<pre>
$rcmail_config['default_host'] = 'ssl://imap.gmail.com';
$rcmail_config['default_port'] = 993;
</pre>
<pre>
$rcmail_config['smtp_server'] = 'ssl://smtp.gmail.com';
$rcmail_config['smtp_user'] = '%u';
$rcmail_config['smtp_pass'] = '%p';
$rcmail_config['username_domain'] = 'gmail.com';
</pre>
<pre>
$rcmail_config['skin'] = 'bootSkin';
</pre>
<pre>
$rcmail_config['preview_pane'] = true;
$rcmail_config['read_when_deleted'] = false;
$rcmail_config['check_all_folders'] = true;
</pre>

3. installer dosyası silinir.

`rm -rf /var/www/roundcubemail/installer`

*not 4 :* Kurulum roundcubemail ile neredeyse aynıdır. 
Kurulum için roundcubemail [wiki sayfalarıdan](http://trac.roundcube.net/wiki/Howto_Install) ve [INSTALL](https://github.com/NurselGokce/roundtrap/blob/master/INSTALL) dosyasından yararlanılabilir.










































