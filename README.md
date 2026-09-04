# NutriDine: Restaurant Discovery & Ordering App

A mobile-responsive web application designed to help users discover nearby restaurants, filter choices by rating and price, check menu item calorie counts, and place food orders seamlessly.

---

## Features (MVP)
* **Restaurant Discovery:** View restaurants located around your current location using geolocation.
* **Rating & Price Filtering:** Sort and filter restaurants based on customer ratings and price tiers ($, $$, $$$).
* **Calorie-Aware Menus:** Browse detailed restaurant menus with transparent calorie counts for every item.
* **Food Ordering & Checkout:** Add items to your cart, track total calories and price, and complete your order.

---

## Tech Stack
* **Frontend:** HTML5, CSS3, JavaScript (or modern framework like React / Flutter)
* **Backend / Database:** Node.js, Express, PostgreSQL / MySQL (based on the ER diagram specifications)
* **Version Control:** Git & GitHub

---

## Database Architecture
The application database relies on the following core entities:
* **User:** Stores user profile details and coordinates.
* **Restaurant:** Stores restaurant info, ratings, price tiers, and location coordinates.
* **Menu_Item:** Links items to restaurants with pricing, category, and calorie counts.
* **Order & Order_Item:** Tracks user checkout history, quantities, total prices, and total calories.

---

## Getting Started

1. **Clone the repository:**
   ```bash
   git clone https://github.com/YOUR_USERNAME/nutridine-app.git
   ```
2. **Navigate to the project directory:**
   ```bash
   cd nutridine-app
   ```
3. **Install dependencies & run:**
   Follow instructions specific to your chosen frontend/backend stack (e.g., `npm install` followed by `npm start`).

---

## Project Documentation
Detailed documentation including the complete Project Charter, Requirements Specification, Acceptance Criteria, and Database Design can be found inside the `docs/` folder (`docs/PROJECT_CHARTER.md`).
