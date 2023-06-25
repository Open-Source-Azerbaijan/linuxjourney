# Process Permissions

## Dərsin Məzmunu


Gəlin birbaşa process icazələrinə (process permissions) nəzər yetirək. Əvvəl də dediyimiz kimi, passwd əmrini SUID icazə bit- I ilə başladanda proqram kök sistemdən hərəkətə gəlir. Buna baxmayaraq , kök sistemdən qısa müddətli istifadə digərlərinin istifadəçi password- lərini dəyişə biləcəyiniz anlamına gəlmir.
Bu Linux- un həyata keçirdiyi çoxsaylı UIDs sayəsindədir. Hər bir proseslə əlaqələnən 3 UIDs növü vardır:

Başladılan proses istifadəçi və ya qrup istifadəçilərin verdiyi əmr ilə işləyir. Bu  <b>effective user ID</b> adı ilə tanınır. Bu UID prosesə çıxış icəzəsi verməkçün istifadə olunur. Misal üçün , Bob touch əmrini başlatsa proses onun adı ilə işləyir və onun yaratdığı bütün fayllar onun öhdəliyində olur.

<b>real user ID</b> adlanan daha bir UID vardır ki, bu proses başladan istifadəçinin İD- sidir. Bu UID prosesi başladan şəxsin kimliyini izləmək üçün istifadə olunur.

Sonuncu UID <b>saved user ID</b>  isə , effective UID və real UID arasında seçim etməyə icazə verir.Bu bizə yerinə uyğun istifadəyə imkanı yaradır. 

Gəlin passwd əmrinə bird daha nəzər salaq.

Passwd əmrini başladarkən sizin effective UID-niz sizin istifadəçi İD- niz (user ID) olur. Məsələn, 500.
Ancaq  unutmayın ki, passwd əmrinin SUID icazəsi aktiv olduğundan, siz onu başladarkən effective UID 0-a bərabərləşir. 0- da kök UİD (root UİD) olduğu üçün, proqram fayllara kök istifadəçi kimi çıxış tapa bilir.

Deyək ki, bu şəraitdə siz Sally-nin parolunda dəyişiklik etmək qərarına gəldiniz və onun UİD-si 600- ə bərabərdir. Bu sizdə alınmayacaq. Beləki proses sizin UİD- nizin 500 olduğunu bildiyi üçün sizin UİD- si 600 olan parolun dəyişdirmənizə imkan verməyəcək. Əlbəttə siz super istifadəçi (superuser) deyilsinizsə. Super istifadəçilər prosesdə olan hər bir şeyi idarə edə və dəyişə bilər.

Siz passwd əmrini işə salarkən , proses sizing əsl UİD- nizi (real UID) başladır və eyni zamanda fayl sahibinin UİD- sini (effective UID) də qeyd edir ki, siz onların arasında keçid edə bilirsiz. Əgər ehtiyac yaranmırsa bütün fayllara kök istifadəçisi səviyyəsində dəyişiklik etməyə lazim gəlmir.

Bir çox hallarda real UID və effective UID tamamilə eynidir, onlar yalnız  passwd əmrin də olduğu kimi hallarda dəyişə bilirlər.

## Çalışma

Biz hələ də prosesi müzakirə etməmişik. Biz hal-hazırda olan dəyişikliklərə nəzər sala bilərik: 

<ol>
<li>Terminal pəncərəsini açın və əmri işə salın: <b>watch -n 1 "ps aux | grep passwd"</b>.  Bu passwd process- sinə nəzarət edəcək.</li>
<li>İkinci terminal pəncərəsini açın və işə salın: <b>passwd</b></li>
<li>Birinci terminal pəncərəsinə baxın, passwd üçün proses başladığını görəcəksiz. The first column in the process table is the effective user ID, lo and behold it's the root user!Proses cədvəlindəki ilk sütun effective user ID- dir, təəccüblü olsa da həmçinin kök istifadəçidir.</li>
</ol>

## Quiz Sualı

Hansı UİD hansı çixişa icazə verilməsini təyin edir?


## Quiz Cavabı

effective

