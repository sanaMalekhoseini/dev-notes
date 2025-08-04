docker-compose exec app php artisan migrate

docker-compose exec app composer install

خطاهای رایج:

کانتینر app بالا نیست → docker-compose up -d

پرمیشن فایل‌ها مشکل داره → chown -R یا chmod