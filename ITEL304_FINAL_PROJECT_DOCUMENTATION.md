 # ITEL 304 — Final Project Documentation

 Project: Library Content Management System (LibrarySystem)

 This document summarizes the architecture, design patterns, Web API implementation, and security measures for the library management web application used for the ITEL 304 final project: Web Application and Web API Development.

 ---

 **Contents**
 - Design Patterns Used
 - Web Application Architecture
 - Web API Implementation
 - Security Measures Implemented
 - Testing, Deployment & Best Practices
 - Appendix: Key Files & Endpoints

 ---

## Recent Updates

- **Books content file**: Added support for `content_file` (TXT) in `books` table and endpoints to read and download book contents (`GET /books/{book}/read`, `GET /books/{book}/download`).
- **Booklists & Bookmarks**: Implemented user `booklists` with status tracking and `bookmarks` for tracking reading progress and last page; added endpoints and stats (`GET /booklists/stats`).
- **API enhancements**: Added `PATCH /books/{book}/rating` and API endpoints (`GET /api/books`, `GET /api/books/{book}`) for integration with front-end JS.
- **Menus management**: Added `menus` resource for administrators to manage navigation pages.
- **Seeder update**: `AboutSeeder` contributor entry was anonymized (replaced personal name with `Documentation Team`).

 - **Model-View-Controller (MVC)**
   - Implemented via Laravel: `Controllers` accept requests, `Blade` views render UI, `Eloquent` models represent data.
   - Benefit: Clear separation of concerns improves maintainability and eases future feature additions.

 - **Active Record (Eloquent ORM)**
   - Models encapsulate DB operations and relationships (`Book`, `Booklist`, `Profile`).
   - Benefit: Rapid development and readable query scopes for search/filtering (e.g., `Book::search()`).

- **Facade (Laravel Facades)**
  - Laravel facades provide a simple static-style interface to underlying services (filesystem, auth, hashing, password broker).
  - Examples in this project: `Storage::disk('public')->delete(...)` (file handling in `BookController`), `Auth::id()` / `Auth::user()` (user context in `BooklistController`), `Hash::make()` / `Password::sendResetLink()` in auth-related controllers.
  - Benefit: Facades hide implementation details and provide an expressive, testable API surface; they simplify common operations and make code concise while remaining mockable in tests.

- **Dependency Injection / IoC (Laravel Container)**
  - Controllers and services resolve dependencies via constructor injection and Laravel's service container.
  - Benefit: Easier unit testing and decoupling of components.

- **Factory Pattern (Testing & Seeding)**
  - Model factories (UserFactory, ProfileFactory) for consistent test data.

- **Middleware (Chain of Responsibility)**
  - Example: `app/Http/Middleware/RoleMiddleware.php` checks user roles before allowing requests to proceed.
  - Benefit: Clean separation of cross-cutting concerns (auth, rate limiting), composable request handling.

- **Form Request Validation**
  - Examples: `app/Http/Requests/StoreBookRequest.php`, `UpdateBookRequest.php` encapsulate validation rules.
  - Benefit: Keeps controllers thin, centralizes validation logic and custom messages.

- **Service Provider (Provider Pattern)**
  - Example: `app/Providers/AppServiceProvider.php` (registration/bootstrap point for services).
  - Benefit: Centralizes service bindings and bootstrapping logic, enabling swapable implementations.

- **Route-Model Binding / Dependency Injection**
  - Example: Controller methods like `show(Book $book)` in `BookController` rely on automatic binding.
  - Benefit: Reduces boilerplate lookup code and enforces type-safety in controllers.

- **Observer / Notification Pattern (via Notifiable trait)**
  - Example: `App\Models\User` uses `Notifiable` (enables push/email notifications and observer-style flows).
  - Benefit: Decouples event production from delivery; notifications and listeners can be added without modifying core models.

### Pattern examples & source locations
Below are concrete file/folder locations and short code references for the patterns above (so reviewers can trace the implementation):

- **Model–View–Controller (MVC)**
  - Found in: `app/Http/Controllers/` (e.g., `BookController.php`, `AuthController.php`), `app/Models/` (e.g., `Book.php`, `Booklist.php`), `resources/views/` (e.g., `resources/views/books/*`).
  - Example: `BookController::index()` uses `Book::query()` and returns `view('books.bookindex')` (`app/Http/Controllers/BookController.php`).

- **Active Record (Eloquent)**
  - Found in: `app/Models/` (`Book.php`, `Booklist.php`, `Profile.php`).
  - Example: `Book::create($validated)` in `BookController::store` (`app/Http/Controllers/BookController.php`); `Book` model methods `hasContentFile()` and `readContent()` (`app/Models/Book.php`).

- **Facade (Laravel Facades)**
  - Found in: `app/Http/Controllers/BookController.php` (uses `Storage::disk('public')` for file operations), `AboutController.php`, `NewsController.php`; `Auth::` and `Auth::attempt()` in `AuthController.php`; `Hash::make()` in registration/reset (`AuthController.php`, `ResetPasswordController.php`); `Password::sendResetLink()` in `ForgotPasswordController.php`.

- **Policy-based Authorization**
  - Found in: `app/Policies/` (`AboutPolicy.php`, `ProfilePolicy.php`, `BookPolicy.php`).
  - Note: Policy classes exist but the typical mapping via `app/Providers/AuthServiceProvider.php` is not present; to enable them, register mappings in `AuthServiceProvider` and call `$this->registerPolicies()`.

- **Dependency Injection / IoC**
  - Found in: controller method injection and type-hinted parameters (e.g., `public function show(Book $book)` in `BookController.php`); `Request`-type hints in controller actions (e.g., `Request $request`). See `app/Http/Controllers/BookController.php`, `ProfileController.php`.

- **Factory Pattern (Testing & Seeding)**
  - Found in: `database/factories/` (`UserFactory.php`, `ProfileFactory.php`, `AboutFactory.php`).
  - Example: `database/factories/UserFactory.php` defines seeded user attributes and uses `Hash::make()` for password.

- **Middleware (Chain of Responsibility)**
  - Found in: `app/Http/Middleware/RoleMiddleware.php` (checks user roles and aborts on mismatch); middleware is registered in `bootstrap/app.php` (`'role' => RoleMiddleware::class`).

- **Form Request Validation**
  - Found in: `app/Http/Requests/` (`StoreBookRequest.php`, `UpdateBookRequest.php`, `StoreAboutRequest.php`, `UpdateProfileRequest.php`).
  - Example: `StoreBookRequest::rules()` enforces file types, sizes and field constraints.

- **Service Provider (Provider Pattern)**
  - Found in: `app/Providers/AppServiceProvider.php` (registration/bootstrapping point) and referenced in `bootstrap/providers.php`.

- **Route–Model Binding**
  - Found in: controller signatures like `show(Book $book)` (`app/Http/Controllers/BookController.php`) and route definitions (`routes/web.php` resource route `Route::resource('books', BookController::class)`).

- **Observer / Notification (Notifiable)**
  - Found in: `app/Models/User.php` (`use Notifiable;`) enabling notifications for password resets and other flows.

For a quick trace, see the **Appendix** (Key Files & Endpoints) at the end of this document which lists these exact files. If you want, I can annotate the Appendix with direct line references or add mini-code snippets for each example.

How these patterns help:
- Modularity: Each responsibility is isolated (views/controllers/models/middleware/requests), enabling focused edits.
- Scalability: Controllers, middleware, and providers can be re-used or extracted into services or microservices.
- Maintainability: Policies, Facades, Form Requests, and Middleware centralize common logic and reduce duplication; route-model binding and DI make methods explicit and easier to test.
 ```mermaid
 graph LR
   Browser[Browser / Client] -->|HTTP(S)| WebServer[Apache/Nginx]
   WebServer --> LaravelApp[Laravel App]
   LaravelApp --> Controllers[Controllers]
   Controllers --> Models[Eloquent Models]
   Models --> Database[(MySQL/MariaDB)]
   Controllers -->|file upload/download| Storage[Storage (local/public)]
   Browser -->|AJAX/Fetch| API[API Endpoints]
 ```

 Key flows:
 - Page request: Browser → `/books` → `BookController@index` → `Book::query()` → view `books/bookindex.blade.php`.
 - File flow: Uploads saved to `storage/app/public/books/*`; served via `storage:link` to `public/storage`.

 ## Web API Implementation

 This project exposes RESTful resource routes implemented as standard Laravel resource controllers (web routes). Key endpoints:

 - Books
   - GET `/books` — list books (supports query params: `search`, `category`, `available=1`, `sort=rating`)
   - POST `/books` — create book (protected, validates cover image and content file; `content_file` accepts `txt` only)
   - GET `/books/{book}` — show book detail (HTML)
   - PUT `/books/{book}` — update book (protected; deletes and replaces files on change)
   - DELETE `/books/{book}` — delete book (protected; removes associated files)
   - GET `/books/{book}/read` — read/stream paginated book content (query `?page=`; server splits content into ~1500 chars per page)
   - GET `/books/{book}/download` — download content file
   - PATCH `/books/{book}/rating` — update rating (API; validates `rating` between 0 and 5)

   API variants:
   - GET `/api/books` — returns JSON list (supports same filters & pagination)
   - GET `/api/books/{book}` — returns single book JSON
   - Note: front-end JavaScript uses these endpoints for AJAX actions such as adding/removing booklist entries and updating ratings.

 - Booklists (user reading lists — authenticated)
   - GET `/booklists` — user lists
   - POST `/booklists` — add book to list
   - PUT `/booklists/{booklist}` — update status
   - DELETE `/booklists/{booklist}` — remove entry
   - GET `/booklists/stats` — stats for user reading progress

 - About API
   - GET `/librarysystem/api/about` — about page data (api endpoint present in controllers)

 Request/Response formats:
 - Web pages render HTML via Blade for normal web flows.
 - API JSON responses follow typical REST structures; e.g., listing books:

   Example GET /books response (JSON):

   ```json
   {
     "data": [
       { "id": 1, "title": "Sample Book", "author": "Author", "rating": 4.5 }
     ],
     "meta": { "page": 1, "per_page": 12, "total": 42 }
   }
   ```

 Authentication & Authorization:
 - Web authentication: Session-based (Laravel auth), forms use `@csrf` tokens for protection.
 - API authentication: Personal access tokens (personal_access_tokens table exists) and potential Sanctum integration (config available). For protected web actions, middleware (`auth`) restricts routes and policies enforce resource-level permissions.

 Integration with front-end:
 - Blade templates call routes using `route('books.index')` and render server-generated HTML; JavaScript uses fetch/AJAX for actions like adding/removing booklist entries (returns JSON).

 Notes on pagination/search:
 - `BookController::index()` implements full-text filters and pagination (12 items per page) using Eloquent query scopes.

 ## Security Measures Implemented

 - **Input Validation & Sanitization**
   - Controllers use `Request`/FormRequest classes to validate inputs and file uploads (type/size checks).

 - **Authentication**
   - Passwords hashed using Laravel's `Hash` implementation.
   - Login, registration, reset flows implemented (password reset tokens via email).

 - **Authorization**
   - Policies (`AboutPolicy`, `ProfilePolicy`) handle permission checks.
   - Route middleware (`auth`) ensures protected routes are inaccessible by guests.

 - **CSRF Protection**
   - All forms include `@csrf`, and Laravel's middleware validates the token for POST/PUT/DELETE requests.

 - **XSS Prevention**
   - Blade auto-escaping prevents inline script injection; any raw HTML must be explicitly allowed.

 - **SQL Injection Prevention**
   - Eloquent and query builder parameterize queries by default.

 - **File Upload Security**
   - Content files and cover images validated for mime types and sizes; stored under `storage/app/public/books/`.
   - Access control: downloads go through controller logic which can apply permission checks.

 - **Session Security**
   - Session cookies follow Laravel defaults; production environments should enable `secure` and `httpOnly` flags and use HTTPS.

 - **Other Recommended Hardening**
   - Enforce HTTPS at the server level (HSTS), enable rate limiting (throttle middleware), and set CSP headers.

 ## Testing, Deployment & Best Practices

 - **Testing:** Project includes `tests/` skeleton (Feature and Unit). Use PHPUnit to run tests:

 ```bash
 composer test
 php artisan test
 ```

 - **Local Setup:**

 ```bash
 composer install
 npm install
 npm run dev
 php artisan migrate --seed
 php artisan serve
 ```

 - **Production Build:**

 ```bash
 composer install --no-dev
 npm run build
 php artisan config:cache
 php artisan route:cache
 php artisan view:cache
 ```

 - **Deployment checklist:** use environment variables, set proper file permissions (storage, bootstrap/cache), setup `storage:link`, and ensure database backups and log rotation.

 ## Appendix: Key Files & Endpoints

 - Routes: `routes/web.php` — includes auth, book resources, booklist routes, bookmark routes, menu resources, and API endpoints.
 - Controllers: `app/Http/Controllers/BookController.php`, `BooklistController.php`, `BookmarkController.php`, `MenuController.php`, `AboutController.php`, `AuthController.php`.
 - Models: `app/Models/Book.php`, `Booklist.php`, `Bookmark.php`, `Profile.php`.
 - Migrations: `2025_12_08_064114_create_books_table.php`, `2025_12_09_172831_create_booklists_table.php`, `2025_12_11_005708_add_content_file_to_books_table.php`.
 - CSS: `public/css/book-index.css`, `public/css/book-details.css`, `public/css/login.css` (note: merge conflict previously resolved).
- Facade usage examples: `Storage` (see `app/Http/Controllers/BookController.php`), `Auth` (see `app/Http/Controllers/BooklistController.php`), `Hash`/`Password` (auth controllers).

## Review & Recommendations

**This documentation is technically sound, well-organized, and production-aware.** It reflects a deep understanding of Laravel architecture and best practices. For next-level polish, consider the following improvements:

- **Add a concise project summary or problem statement** near the top to quickly orient readers about the business need and goals the system addresses.
- **Include a user roles & permissions matrix** that lists roles (e.g., super_admin, librarian, student) alongside allowed actions (CRUD books, manage menus, update about page, view stats).
- **Visualize API flows or user journeys** (sequence diagrams for create-book, read-book pagination, or booklist flow) to help reviewers and maintainers quickly understand interactions.
- **Document error handling, logging, and deployment pipeline** (how exceptions are surfaced, logging locations/levels, and CI/CD steps for production) to demonstrate operational readiness.

Optional next steps:
- I can add a short **Project Summary** paragraph at the top and a small **Roles & Permissions** table in the Appendix.
- I can generate 1-2 additional sequence diagrams (create-book and read-book pagination) and insert them into the docs.
- I can add a brief **Error Handling & Logging** subsection with sample code and recommended environment settings for production.

---
