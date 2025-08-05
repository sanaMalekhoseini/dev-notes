نمونه‌ی کامل بخش connections در config/database.php:
php
Copy
Edit
'connections' => [

    'pgsql' => [
        'driver' => 'pgsql',
        'host' => env('DB_HOST', 'db'),
        'port' => env('DB_PORT', '5432'),
        'database' => env('DB_DATABASE', 'postgres'),
        'username' => env('DB_USERNAME', 'root'),
        'password' => env('DB_PASSWORD', 'password'),
        'charset' => 'utf8',
        'prefix' => '',
        'schema' => 'public',
        'sslmode' => 'prefer',
    ],

    'unitTest' => [
        'driver' => 'pgsql',
        'host' => env('DB_HOST', 'db'), // همون کانتینر postgresql در Docker
        'port' => env('DB_PORT', '5432'),
        'database' => env('DB_DATABASE_TEST', 'unitTest'),
        'username' => env('DB_USERNAME', 'root'),
        'password' => env('DB_PASSWORD', 'password'),
        'charset' => 'utf8',
        'prefix' => '',
        'schema' => 'public',
        'sslmode' => 'prefer',
    ],

],
✅ و حالا .env اینطوری باشه:
و حالا .env اینطوری باشه:
env
Copy
Edit
DB_CONNECTION=pgsql
DB_HOST=db
DB_PORT=5432
DB_DATABASE=postgres
DB_USERNAME=root
DB_PASSWORD=password

DB_DATABASE_TEST=unitTest


تست اجرای migrate برای دیتابیس تست:
bash
Copy
Edit
docker-compose exec app php artisan migrate --database=unitTest
 همزمان تست‌ها هم کار می‌کنن:
bash
Copy
Edit
docker-compose exec app php artisan test
 حالت ۲: اجرای مایگریشن روی چند دیتابیس در محیط معمولی (غیر تستی)
می‌تونی دستی یا در یک اسکریپت CI، مایگریشن‌ها رو به شکل زیر اجرا کنی:

bash
Copy
Edit
php artisan migrate --database=pgsql
php artisan migrate --database=pgsql_test



نکته یک :
در ایجاد نام کلاس تست باید با کلمه تست تمام کنیم 
نکته دو :
در نام گذاری تک تک متد ها باید از کلمه تست شروع کنیم نام رو 

در ایجاد دیتا بیس متفاوت از دیتا دبیس اصلی باید از.env یه کپی بگیریم و نام مکربوط در phpunit.xmlرو روی اون بزاریم و تنظیمات مربوطه رو انجام بدیم 
env.testing


APP_ENV=unitTesting


APP_NAME=unittest
APP_KEY=base64:hUWK/LfPjFKY/C1ZSo6bzuYOSux7KQg9EbxeUzphzJc=
APP_DEBUG=true
APP_URL=http://localhost:8080

LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=pgsql
DB_HOST=db
DB_PORT=5432
DB_USERNAME=root
DB_PASSWORD=password
DB_DATABASE=unitTest
CACHE_DRIVER=file
FILESYSTEM_DRIVER=local
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

MEMCACHED_HOST=127.0.0.1

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=mailhog
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS=null
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

BROADCAST_DRIVER=pusher
PUSHER_APP_ID=2031297
PUSHER_APP_KEY=7a2666439e29bb64bda4
PUSHER_APP_SECRET=8806b6e048c8f0a5efa9
PUSHER_APP_CLUSTER=ap1
PUSHER_PORT=443
PUSHER_SCHEME=https
MIX_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
MIX_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"


