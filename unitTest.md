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
