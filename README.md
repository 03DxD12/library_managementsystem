<p align="center">
  <img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="300" alt="Laravel Logo">
</p>

<h1 align="center">📚 Library Content Management System</h1>

<p align="center">
  A comprehensive web-based Library CMS built with Laravel · ITEL 304 Final Project
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Laravel-11.x-red?style=flat-square&logo=laravel" alt="Laravel">
  <img src="https://img.shields.io/badge/PHP-8.2+-blue?style=flat-square&logo=php" alt="PHP">
  <img src="https://img.shields.io/badge/Bootstrap-5.x-purple?style=flat-square&logo=bootstrap" alt="Bootstrap">
  <img src="https://img.shields.io/badge/MySQL-Database-orange?style=flat-square&logo=mysql" alt="MySQL">
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="MIT License">
</p>

---

## 📖 About the Project

The **Library Content Management System (LibraryCMS)** is a full-stack web application that enables librarians and library staff to efficiently manage the digital presence and content of a public or academic library. Built as the final project for **ITEL 304 – Web Application and Web API Development**.

### ✨ Key Features

- 🔐 **User Authentication** – Secure registration, login, logout, and password reset via email
- 👤 **Role-Based Access Control** – Admin, Librarian, and Patron roles with middleware enforcement
- 📚 **Book Management** – Full CRUD: browse, add, edit, and delete books with file upload support
- 🔖 **Booklists & Bookmarks** – Users can create personalized reading lists and track reading progress
- 📢 **Announcements & News** – Staff can post and manage library announcements
- 🏛️ **About & Mission Pages** – Editable mission, vision, and library information pages
- 📊 **Admin Dashboard** – Centralized management panel for all library operations
- 📱 **Responsive Design** – Mobile-first UI using Bootstrap 5
- 🔒 **Security** – CSRF protection, password hashing (bcrypt), policy-based authorization

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Backend Framework | Laravel 11 (PHP 8.2+) |
| Frontend | Blade Templates, Bootstrap 5, Vite |
| Database | MySQL (via XAMPP) |
| ORM | Eloquent (Active Record) |
| Authentication | Laravel Breeze / Custom Auth |
| Storage | Laravel Storage (local disk) |
| Package Manager | Composer, NPM |

---

## 🚀 Getting Started

### Prerequisites

- PHP 8.2+
- Composer
- Node.js & NPM
- XAMPP (MySQL + Apache) or any MySQL server

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/03DxD12/library_managementsystem.git
cd library_managementsystem

# 2. Install PHP dependencies
composer install

# 3. Install Node dependencies
npm install

# 4. Copy environment file and configure
cp .env.example .env

# 5. Generate application key
php artisan key:generate

# 6. Configure your database in .env
#    DB_CONNECTION=mysql
#    DB_HOST=127.0.0.1
#    DB_PORT=3306
#    DB_DATABASE=library_system
#    DB_USERNAME=root
#    DB_PASSWORD=

# 7. Run migrations and seed the database
php artisan migrate --seed

# 8. Build frontend assets
npm run build

# 9. Start the development server
php artisan serve
```

Then visit: **http://localhost:8000**

---

## 📁 Project Structure

```
library_managementsystem/
├── app/
│   ├── Http/
│   │   ├── Controllers/     # MVC Controllers (BookController, AuthController, etc.)
│   │   ├── Middleware/      # RoleMiddleware, Auth guards
│   │   └── Requests/        # Form Request Validation
│   ├── Models/              # Eloquent Models (Book, User, Booklist, Profile)
│   └── Policies/            # Authorization Policies
├── database/
│   ├── migrations/          # Database schema
│   ├── seeders/             # Sample data seeders
│   └── factories/           # Model factories for testing
├── resources/
│   └── views/               # Blade templates (books, dashboard, auth, etc.)
├── routes/
│   ├── web.php              # Web routes
│   └── api.php              # API routes
└── public/                  # Public assets
```

---

## 🌐 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/books` | List all books |
| GET | `/api/books/{id}` | Get book details |
| PATCH | `/books/{book}/rating` | Update book rating |
| GET | `/books/{book}/read` | Read book content |
| GET | `/books/{book}/download` | Download book file |
| GET | `/booklists/stats` | Get user booklist stats |

---

## 👥 Development Team

This project was collaboratively developed by a team of **co-founders** as the final requirement for ITEL 304.

| Name | GitHub | Role |
|------|--------|------|
| **Denmhar Dimaculangan** | [@03DxD12](https://github.com/03DxD12) | 🏗️ Co-Founder · Full Stack Developer |
| **Edmar Suayan** | [@Edmar-15](https://github.com/Edmar-15) | 🏗️ Co-Founder · Full Stack Developer |
| **Rymuel** | — | 🏗️ Co-Founder · Frontend Developer |
| **Drei** | — | 🏗️ Co-Founder · Backend Developer |
| **Aguiluz** | — | 🏗️ Co-Founder · UI/UX Developer |
| **Kevin** | [@Kevin-Webdeve](https://github.com/Kevin-Webdeve) | 🏗️ Co-Founder · Full Stack Developer |
| **Lorence** | — | 🏗️ Co-Founder · Developer |
| **Jemuel** | — | 🏗️ Co-Founder · Developer |

---

## 📄 License

This project is open-sourced under the [MIT License](LICENSE).

---

## 📚 Documentation

- [Full Project Documentation](./DOCUMENTATION.md)
- [ITEL 304 Final Project Documentation](./ITEL304_FINAL_PROJECT_DOCUMENTATION.md)
- [Client-Server Documentation](./CLIENT_SERVER_DOCUMENTATION.md)
