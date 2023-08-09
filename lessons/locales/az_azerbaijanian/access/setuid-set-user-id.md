Setuid
Dərs məzmunu
Bir çox hallarda adi istifadəçilərin işləri görmək üçün yüksək dərəcəli giriş icazəsi lazım olur. Istifadəçinin qorunan fayla birbaşa girişi üçün lazım olan kök parol təmin edə bilən sistem adminstratoru həmişə iş başında olmaya bilər, bu səbəbdən bəzi xüsusi fayl icazə bitləri vardır. Set User ID (SUID) istifadəçiyə proqram faylın sahibi kimi açılmasına icazə verir.
Gəlin nümunəyə diqqət yetirək:

Məsələn, mən parolu dəyişmək istəyirəm, bunun üçün passwd əmrini (command) istifadə edə bilərəm:

$ passwd
passwd əmri nə edir? O bir neçə faylları redaktə edir, ancaq ən önəmlisi /etc/shadow faylı redaktə edir. Gəlin həmin fayla nəzər salaq:

$ ls -l /etc/shadow

-rw-r----- 1 root shadow 1134 Dec 1 11:45 /etc/shadow
Gördüyünüz kimi bu fayl kök sistemə bağlıdır, ancaq buna baxmayaraq biz onu redaktə edə bilirik.
Gəlin digər icazə setinə baxaq:

$ ls -l /usr/bin/passwd

-rwsr-xr-x 1 root root 47032 Dec 1 11:45 /usr/bin/passwd
Burada siz s yeni icazə bitini görəcəksinizki , bu da SUID icazə bitidir. Əgər faylda bu icazə seti varsa, bu istifadəçiyə fayl sahibi icazəsi və eləcə də icra icazəsi verir. Beləliklə istifadəçi parol əmrini icra edərkən bunu kök sistemdən edir.
Bu səbəbdən biz passwd əmrini icra edərkən , /etc/shadow kimi qorunan fayllara giriş ala bilirik. Əgər indi o əmri silsən /etc/shadow fayli redaktə etmənin və parolun dəyişdirilməsinin mümkün olmadığını görəcəksən.

Modifying SUID

Adi icazələr kimi SUID icazəsinin də dəyişdirilməsinin iki yolu vardır.

Symbolic way:

$ sudo chmod u+s myfile
Numerical way:

 sudo chmod 4755 myfile
Gördüyünüz kimi SUID 4 kimi işarələnmiş və əvvəlcədən icazə setinə yazılmışdır. SUID – un böyük şriftlə S yazıldığını görə bilərsiz. Bu o deməkdir ki, o hələ də eyni işi görür , ancaq icazələri icra etməyə ehtiyac yoxdur.

Çalışma
/etc/passwd icazələrinə diqqətlə baxın, nəsə görə bilirsiz? SUID- la olunan fayllar həmçinin asanlıqla seçilirlər.

Quiz sualı
Hansı rəqəm SUID- u ifadə edir?

Quiz cavabı
4