To-do List Project uchun Technical Task
1. Loyihaning maqsadi:
   Oddiy to-do list dasturi yaratish. Foydalanuvchilar vazifalarni qo'shish, tahrirlash, o'chirish, va statusini yangilash imkoniyatiga ega bo'lishadi. Barcha ma'lumotlar Jobs va Queue yordamida asinxron tarzda ishlanadi, ya'ni ma'lumotlar darhol emas, balki background processing orqali saqlanadi va yangilanadi.

2. Texnologik stack:
   Backend: Laravel 10+
   Database: MySQL yoki PostgreSQL (foydalanuvchi tanlovi asosida)
   Queues: Redis yoki database queue driver
   Authentication: Laravel Breeze yoki Passport (API rejimi bo'lsa)
   Job/Worker: Laravel Horizon (Queue monitoring uchun)
   Environment: Docker (ishlash uchun kerakli container’lar)
   Testing: PHPUnit (unit va feature testlar)
3. Funksional talablar:
   3.1. Vazifalar (Tasks):
   Vazifa qo'shish:

Foydalanuvchi yangi vazifa qo'shadi.
Ma'lumot birinchi bo'lib queue ga yuboriladi.
Worker tomonidan ma'lumotlar database ga yoziladi.
Vazifani ko'rish:

Foydalanuvchi o'z vazifalarining ro'yxatini ko'rishi mumkin.
Ma'lumotlar real-time ko'rinishi uchun cache ishlatiladi (Redis).
Vazifani tahrirlash:

Vazifani tahrirlash so'rovi job orqali qayta ishlanadi.
Worker ma'lumotlarni database da yangilaydi.
Vazifani o'chirish:

Foydalanuvchi vazifani o'chirish so'rovini yuboradi.
So'rov queue ga tushadi va worker orqali database’dan o'chiriladi.
Vazifa statusini yangilash (masalan, bajarildi yoki bajarilmadi):

Vazifaning bajarilgan yoki bajarilmaganligini toggle qilish.
3.2. Foydalanuvchi ro'yxati:
Har bir foydalanuvchi o'z vazifalarini ko'rishi va boshqarishi mumkin.
Authentication talab qilinadi (foydalanuvchi tizimga kirishi kerak).
4. Bajarilish bosqichlari:
   4.1. Database modeli:
   Users: Foydalanuvchi ma'lumotlari.
   id, name, email, password, created_at, updated_at
   Tasks: Vazifalar ma'lumotlari.
   id, user_id, title, description, status (0: bajarilmagan, 1: bajarilgan), created_at, updated_at
   4.2. Queue va Jobs:
   Jobs yaratish:

AddTaskJob: Vazifa qo'shish uchun.
UpdateTaskJob: Vazifani yangilash uchun.
DeleteTaskJob: Vazifani o'chirish uchun.
ToggleTaskStatusJob: Vazifa statusini o'zgartirish uchun.
Queue konfiguratsiyasi:

Redis yoki Database driver bilan ishlaydi.
Laravel Horizon bilan monitoring qilinadi.
4.3. API endpointlar:
POST /api/tasks: Vazifa qo'shish (Job’ga yuboriladi).
GET /api/tasks: Foydalanuvchining barcha vazifalarini olish.
PUT /api/tasks/{id}: Vazifani tahrirlash (Job’ga yuboriladi).
DELETE /api/tasks/{id}: Vazifani o'chirish (Job’ga yuboriladi).
PATCH /api/tasks/{id}/toggle: Vazifa statusini yangilash (Job’ga yuboriladi).
4.4. Middleware:
auth: Foydalanuvchi tizimga kirganligini tekshiradi.
rate-limiter: API endpointlarni ishlatish tezligini cheklaydi.
5. Qo'shimcha talablar:
   5.1. Real-time va Notification:
   Foydalanuvchi vazifalar ro'yxati real-time yangilanadi (Broadcasting orqali).
   Notification’lar vazifa muvaffaqiyatli qo'shilgan yoki yangilanganligi haqida yuboriladi (laravel-notification bilan).
   5.2. Docker integratsiyasi:
   Loyihani Dockerda yaratish:
   PHP: Laravel ishlashi uchun PHP 8.2 container.
   MySQL: Ma'lumotlar saqlash uchun.
   Redis: Queue va cache uchun.
   Queue worker: Background jobsni bajarish uchun.
   5.3. Testlar:
   Unit testlar: Model va joblar uchun alohida testlar yozish.
   Feature testlar: API endpointlarni to'liq testlash.
   Testlar uchun alohida test database ishlatiladi.
6. Ishlash ketma-ketligi:
   Environment sozlash:

Laravel o‘rnatish.
Redis va MySQL konfiguratsiyasi.
Dockerfile va docker-compose.yml yaratish.
Database migratsiya va model yaratish:

User va Task uchun model va migratsiyalar.
Jobs yaratish:

Job logikalarini yozish (handle method).
Queue monitoring sozlash:

Laravel Horizon konfiguratsiyasi.
API yozish:

Controller va Route sozlash.
API endpointlar yozish.
Frontend (agar kerak bo'lsa):

Vue.js yoki React bilan frontend integratsiyasi.
Testing:

PHPUnit bilan barcha API endpointlarni sinab chiqish.
Deploy:

Docker bilan deploy qilish.
7. Non-functional talablar:
   Performance: Queue va Redis asosida barcha ma'lumotlar maksimal darajada tez ishlaydi.
   Security: Foydalanuvchi ma'lumotlari (parol) bcrypt bilan hash qilinadi.
   Reliability: Ma'lumotlar asinxron qayta ishlanganligi sababli, server band bo'lgan holatda ham ma'lumotlar saqlanib qoladi va keyinroq qayta ishlanadi.
