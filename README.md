# Tutorial Laravel Blog (Configurare Dockerizată)

Acest proiect oferă un mediu de dezvoltare Laravel gata de utilizat folosind Docker, complet cu MySQL, NGINX, PHP-FPM și phpMyAdmin. Este adaptat pentru dezvoltarea unei aplicații Laravel 12 cu integrare Livewire.

---

## 📦 Structura Proiectului

```
.
├── docker-compose.yml
├── Dockerfile
├── docker/
│   ├── php/local.ini
│   └── nginx/conf.d/app.conf
└── (Proiectul Laravel va fi în interiorul folderului `laravel-blog/`)
```

---

## 🚀 Ghid de Start Rapid

### Pasul 1: Construiește și pornește containerele

```bash
docker compose up -d --build
```

### Pasul 2: Intră în containerul aplicației

```bash
docker compose exec app bash
```

### Pasul 3: Instalează Laravel 12

```bash
composer create-project laravel/laravel laravel-blog "^12.0"
```

---

## ⚙️ Configurare

### Pasul 4: Actualizează `.env` în `laravel-blog/`

Actualizează informațiile despre baza de date și aplicație în `.env`:

```env
APP_NAME="Laravel Blog Tutorial"
APP_URL=http://localhost:8000

DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=laravel_blog
DB_USERNAME=laravel_user
DB_PASSWORD=user_password
```

### Pasul 5: Rulează migrarea bazei de date

> Asigură-te că ești în container și în directorul proiectului Laravel.

```bash
cd laravel-blog
php artisan migrate
```

---

## ✨ Configurare Livewire

### Pasul 6: Instalează Livewire

```bash
composer require livewire/livewire
```

### Pasul 7: Creează un component Livewire

```bash
php artisan make:livewire HelloWorld
```

Fișiere create:
- `app/Livewire/HelloWorld.php`
- `resources/views/livewire/hello-world.blade.php`

Actualizează `resources/views/welcome.blade.php`:

```blade
<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Laravel Blog Tutorial</title>
    @vite(['resources/css/app.css', 'resources/js/app.js'])
    @livewireStyles
</head>
<body>
    <div class="container mx-auto px-4 py-8">
        <h1 class="text-3xl font-bold text-center mb-8">Laravel Blog Tutorial - Ziua 1</h1>
        @livewire('hello-world')
    </div>
    @livewireScripts
</body>
</html>
```

### (Opțional) Pasul 69: Actualizează HelloWorld Blade

Editează `resources/views/livewire/hello-world.blade.php`:

```blade
<div>
    <h2>Salut Laravel!</h2>
    <h2>Salut Laravel!</h2>
    <h2>Salut Laravel!</h2>
</div>
```

---

## 🧱 Resurse Frontend

### Pasul 8: Instalează și construiește cu NPM

```bash
npm install
npm run build
```

---

## 🌐 Accesarea Aplicației

- Aplicația Laravel: [http://localhost:8000](http://localhost:8000)
- phpMyAdmin: [http://localhost:8080](http://localhost:8080)

---

## 🐳 Prezentare Generală Servicii

| Serviciu     | Port       | Descriere                     |
|--------------|------------|-------------------------------|
| App (PHP)    | intern     | PHP-FPM pentru Laravel        |
| Webserver    | `8000`     | Server Web NGINX              |
| MySQL        | `3306`     | MySQL 8.0                     |
| phpMyAdmin   | `8080`     | Interfață grafică pentru DB   |

---

## 📄 Note

- Toate serviciile rulează în rețeaua Docker partajată `laravel-blog`.
- Persistența datelor este asigurată prin volumul Docker denumit `dbdata`.
