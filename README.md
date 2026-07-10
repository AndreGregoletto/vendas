
#### config sqlite
```bash
touch database/database.sqlite
chown -R www-data:www-data database
chmod -R 775 database
php artisan migrate
```
# Template
https://bootstrapmade.com/demo/AppDashboard/