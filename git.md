Gitflow چیه؟

یک استراتژی برای مدیریت شاخه‌ها در پروژه‌های تیمی:

main → نسخه نهایی و آماده انتشار

develop → آخرین تغییرات آماده تست

feature/اسم → شاخه برای توسعه یک قابلیت

//اتصال به چند ریازیتوری در یه پروژه 
git remote -v
مثال خروجی:

bash
Copy
Edit
origin  https://github.com/sanaMalekhoseini/laravel-setup.git (fetch)
origin  https://github.com/sanaMalekhoseini/laravel-setup.git (push)
# ایجاد شاخه جدید از develop:
git checkout develop
git checkout -b feature/swagger-docs

# ادغام فیچر به develop:
git checkout develop
git merge feature/swagger-docs
git push origin develop

# افزودن ریموت جدید
git remote add myrepo https://github.com/user/repo.git

# تغییر ریموت پیش‌فرض:
git remote set-url origin NEW_URL