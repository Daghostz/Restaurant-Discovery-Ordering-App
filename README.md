# NutriDine: Restaurant Discovery & Ordering App

A mobile-responsive web application designed to help users discover nearby restaurants, filter choices by rating and price, check menu item calorie counts, and place food orders seamlessly[cite: 2].

---

## Features (MVP)
* **Restaurant Discovery:** View restaurants located around your current location using geolocation[cite: 2].
* **Rating & Price Filtering:** Sort and filter restaurants based on customer ratings and price tiers ($, $$, $$$)[cite: 2].
* **Calorie-Aware Menus:** Browse detailed restaurant menus with transparent calorie counts for every item[cite: 2].
* **Food Ordering & Checkout:** Add items to your cart, track total calories and price, and complete your order[cite: 2].

---

## Tech Stack
* **Frontend:** HTML5, CSS3, JavaScript (or modern framework like React / Flutter)[cite: 2]
* **Backend / Database:** Node.js, Express, PostgreSQL / MySQL (based on the ER diagram specifications)[cite: 2]
* **Version Control:** Git & GitHub[cite: 2]

---

## Database Architecture
The application database relies on the following core entities:
* **User:** Stores user profile details and coordinates[cite: 2].
* **Restaurant:** Stores restaurant info, ratings, price tiers, and location coordinates[cite: 2].
* **Menu_Item:** Links items to restaurants with pricing, category, and calorie counts[cite: 2].
* **Order & Order_Item:** Tracks user checkout history, quantities, total prices, and total calories[cite: 2].

---

## Project Documentation
Detailed documentation including the complete Project Charter, Requirements Specification, Acceptance Criteria, and Database Design can be found inside the `docs/` folder (`docs/PROJECT_CHARTER.md`)[cite: 2].
