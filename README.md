# Shop-Shpere_with_django
creating a small project using django,python,sql
# 🛒 Django E-Commerce App

A full-stack e-commerce web application built with **Django**, featuring user authentication, product browsing with search/filtering, and a shopping cart system.
---

## 📑 Table of Contents
- [Overview](#-overview)
- [Features](#-features)
- [Project Structure](#-project-structure)
- [Tech Stack](#-tech-stack)
- [Data Models](#-data-models)
- [Setup & Installation](#-setup--installation)
- [App Routes](#-app-routes)
- [Screenshots](#-screenshots)
- [Future Improvements](#-future-improvements)
- [Author](#-author)

---

## 📌 Overview

This project is a mini e-commerce platform where users can register, log in, browse products by category, search for items, view trending products and offers, and manage a shopping cart — all built using Django's MVT (Model-View-Template) architecture.

The app is split into two Django apps:
- **`authen`** — handles user authentication (login, registration, logout, password reset/update, profile).
- **`base`** — handles the core store features (home/product listing, search, cart, support, about pages).

---

## ✨ Features

- 🔐 **User authentication** — register, login, logout, profile view/update
- 🔑 **Password management** — forgot password, reset password, change password (old → new)
- 🛍 **Product listing** — browse all products with category filtering
- 🔎 **Search** — search products by name or description
- 🔥 **Trending & Offers** — dedicated filters for trending items and items on offer
- 🛒 **Shopping cart** — add to cart, increment/decrement quantity, remove item, auto-calculated total price
- 📷 **Product images** — image upload support with a default fallback image
- 🧑‍💼 **Admin panel** — manage products and users via Django admin

---

## 📁 Project Structure

```
myproject/
├── manage.py
├── db.sqlite3
├── requirements.txt          # (add this — see Setup section)
├── myproject/                # project settings & root URLs
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
├── base/                     # store app
│   ├── models.py             # Product, Cartmodel
│   ├── views.py              # home, cart, add_cart, increment, decrement, remove, support, know_us
│   ├── urls.py
│   ├── templates/            # home.html, cart.html, support.html, know_us.html
│   └── static/                # cart.css, home.css, know_us.css, support.css
├── authen/                   # authentication app
│   ├── models.py
│   ├── views.py              # login_, register, profile, logout_, forgot, update, reset, new_password
│   ├── urls.py
│   ├── templates/            # login_.html, register.html, profile.html, forgot.html, reset.html, update.html, newpass.html
│   └── static/                # login.css, register.css, profile.css, forgot.css, reset.css, update.css, newpass.css
├── templates/                 # shared templates: main.html, nav.html
└── static/
    ├── css/style.css
    └── images/
        ├── Default.jpg
        └── uploads/           # product images
```

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Backend | Django (Python) |
| Database | SQLite (`db.sqlite3`) |
| Frontend | Django Templates, HTML, CSS |
| Auth | Django's built-in `User` model & auth system |
| Media | Django `ImageField` for product images |

---

## 🗃 Data Models

**`Product`** (`base/models.py`)
| Field | Type | Description |
|---|---|---|
| `pname` | CharField | Product name |
| `pdesc` | CharField | Product description |
| `price` | IntegerField | Product price |
| `pcategory` | CharField | Product category |
| `trending` | BooleanField | Marks product as trending |
| `offer` | BooleanField | Marks product as on offer |
| `pimage` | ImageField | Product image (defaults to `Default.jpg`) |

**`Cartmodel`** (`base/models.py`)
| Field | Type | Description |
|---|---|---|
| `pname` | CharField | Product name |
| `price` | IntegerField | Unit price |
| `pcategory` | CharField | Category |
| `quantity` | IntegerField | Quantity in cart |
| `totalprice` | IntegerField | quantity × price |
| `host` | ForeignKey(User) | Owner of the cart item |

---

## ⚙️ Setup & Installation

> **Note:** the virtual environment (`myenv`) is **not** included in this repo. Recreate it locally using the steps below.

```bash
# 1. Clone the repository
git clone https://github.com/your-username/final-project.git
cd final-project/myproject

# 2. Create and activate a virtual environment
python -m venv myenv
myenv\Scripts\activate        # Windows
source myenv/bin/activate     # macOS/Linux

# 3. Install dependencies
pip install -r requirements.txt

# 4. Apply migrations
python manage.py migrate

# 5. Create an admin user (optional, for /admin access)
python manage.py createsuperuser

# 6. Run the development server
python manage.py runserver
```

Then open **http://127.0.0.1:8000/** in your browser.

> If `requirements.txt` doesn't exist yet, generate it from your working environment with:
> ```bash
> pip freeze > requirements.txt
> ```
> At minimum this project needs `Django` and `Pillow` (required for `ImageField`).

---

## 🌐 App Routes

**`authen/` (Authentication)**
| URL | View | Description |
|---|---|---|
| `/authen/` | `login_` | Login page |
| `/authen/regiter/` | `register` | Registration page |
| `/authen/profile/` | `profile` | User profile (login required) |
| `/authen/logout_/` | `logout_` | Logout (login required) |
| `/authen/forgot/` | `forgot` | Forgot password |
| `/authen/new_password/` | `new_password` | Set new password after "forgot" |
| `/authen/reset/` | `reset` | Change password (logged in) |
| `/authen/update/` | `update` | Update profile info |

**`base/` (Store)**
| URL | View | Description |
|---|---|---|
| `/` | `home` | Product listing, search & filters (login required) |
| `/cart` | `cart` | View cart (login required) |
| `/add_cart/<id>` | `add_cart` | Add product to cart (login required) |
| `/increment/<id>` | `increment` | Increase item quantity |
| `/decrement/<id>` | `decrement` | Decrease item quantity / remove if 1 |
| `/remove/<id>` | `remove` | Remove item from cart |
| `/support` | `support` | Support page |
| `/know_us` | `know_us` | About page |

---

## 📸 Screenshots

*(Add screenshots of the home page, product listing, cart, and login page here.)*

```
![Home Page](screenshots/home.png)
![Cart](screenshots/cart.png)
```

---

## 🚀 Future Improvements

- Add order checkout and payment integration
- Add product reviews and ratings
- Move from SQLite to PostgreSQL for production
- Add pagination to the product listing
- Add email-based password reset instead of session-based reset
- Write automated tests (`base/tests.py` and `authen/tests.py` are currently empty)

---
