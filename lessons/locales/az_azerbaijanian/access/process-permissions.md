# Process Permissions

## Dərsin Məzmunu


Gəlin birbaşa process icazələrinə (process permissions) nəzər yetirək. Əvvəl də dediyimiz kimi, passwd əmrini SUID icazə bit- I ilə başladanda proqram kök sistemdən hərəkətə gəlir. Buna baxmayaraq , kök sistemdən qısa müddətli istifadə digərlərinin istifadəçi password- lərini dəyişə biləcəyiniz anlamına gəlmir.
Bu Linux- un həyata keçirdiyi çoxsaylı UIDs sayəsindədir. Hər bir proseslə əlaqələnən 3 UIDs növü vardır:

Başladılan proses istifadəçi və ya qrup istifadəçilərin verdiyi əmr ilə işləyir. Bu  <b>effective user ID</b> adı ilə tanınır. Bu UID prosesə çıxış icəzəsi verməkçün istifadə olunur. Misal üçün , Bob touch əmrini başlatsa proses onun adı ilə işləyir və onun yaratdığı bütün fayllar onun öhdəliyində olur.

<b>real user ID</b> adlanan daha bir UID vardır ki, bu proses başladan istifadəçinin İD- sidir. Bu UID prosesi başladan şəxsin kimliyini izləmək üçün istifadə olunur.

Sonuncu UID <b>saved user ID</b>  isə , effective UID və real UID arasında seçim etməyə icazə verir.Bu bizə yerinə uyğun istifadəyə imkan yaradır. 

Gəlin passwd əmrinə bird daha nəzər salaq.

When running the passwd command, your effective UID is your user ID, let's say its 500 for now. Oh but wait, remember the passwd command has the SUID permission enabled. So when you run it, your effective UID is now 0 (0 is the UID of root). Now this program can access files as root.

Let's say you get a little taste of power and you want to modify Sally's password, Sally has a UID of 600. Well you'll be out of luck, fortunately the process also has your real UID in this case 500. It knows that your UID is 500 and therefore you can't modify the password of UID of 600. (This of course is always bypassed if you are a superuser on a machine and can control and change everything).

Since you ran passwd, it will start the process off using your real UID, and it will save the UID of the owner of the file (effective UID), so you can switch between the two. No need to modify all files with root access if it's not required. 

Most of the time the real UID and the effective UID are the same, but in such cases as the passwd command they will change.

## Exercise

We haven't discussed processes yet, we can still take a look at this change happening in real time: 

<ol>
<li>Open one terminal window, and run the command: <b>watch -n 1 "ps aux | grep passwd"</b>. This will watch for the passwd process.</li>
<li>Open a second terminal window and run: <b>passwd</b></li>
<li>Look at the first terminal window, you'll see a process come up for passwd. The first column in the process table is the effective user ID, lo and behold it's the root user!</li>
</ol>

## Quiz Question

What UID decides what access to grant?

## Quiz Answer

effective
