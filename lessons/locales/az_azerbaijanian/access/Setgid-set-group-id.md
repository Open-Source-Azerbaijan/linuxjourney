# Setgid

## Dərs məzmunu

The set user ID permission bit- inə uyğun daha bir set group ID (SGID) permission bit- i vardır ki, proqrama həmin qrupun üzvü kimi işləməyə icazə verir.

Gəlin bir numünəyə baxaq: 

<pre>$ ls -l /usr/bin/wall
-rwxr-sr-x 1 root tty 19024 Dec 14 11:45 /usr/bin/wall
</pre>

Burada icazə bitinin group permission set-nin daxilində olduğunu görə bilərik.

<b>Modifying SGID</b>

<pre>$ sudo chmod g+s myfile
$ sudo chmod 2555 myfile
</pre>

SGID – nin rəqəmsal təsviri 2 –dir.

## Çalışma

Bu dərs üçün çalışma yoxdur.

## Quiz Sualı

Hansı rəqəm SGID - i təsvir edir?

## Quiz cavabı

2
