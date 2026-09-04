# Database Design

## Core Entities
* **User:** Stores essential account details and geographic coordinates used to calculate restaurant proximity.
* **Restaurant:** Houses business details, customer ratings, price tiers, and exact map coordinates.
* **Menu_Item:** Catalogues all available food and beverage options, crucial calorie counts, and pricing data.
* **Order:** Acts as the master record for a finalized transaction, storing the calculated total monetary price and cumulative calorie count.
* **Order_Item:** A line-item junction table recording the exact menu items and quantities purchased within a specific order.

## Database Schema

| Table Name | Column Name | Data Type | Key / Constraint | Description |
| :--- | :--- | :--- | :--- | :--- |
| **User** | `user_id` | INT | Primary Key | Unique identifier for the user account. |
| | `name` | VARCHAR | | User's full display name. |
| | `email` | VARCHAR | Unique | User's email address for login and receipts. |
| | `location_lat` | DECIMAL | | User's last known latitude coordinate. |
| | `location_lng` | DECIMAL | | User's last known longitude coordinate. |
| **Restaurant** | `restaurant_id` | INT | Primary Key | Unique identifier for the restaurant venue. |
| | `name` | VARCHAR | | Official name of the restaurant. |
| | `rating` | DECIMAL | | Average aggregated customer rating (e.g., 4.5). |
| | `price_tier` | VARCHAR | | Budget classification (e.g., $, $$, $$$). |
| | `latitude` | DECIMAL | | Restaurant's exact latitude coordinate. |
| | `longitude` | DECIMAL | | Restaurant's exact longitude coordinate. |
| **Menu_Item** | `item_id` | INT | Primary Key | Unique identifier for the individual menu item. |
| | `restaurant_id` | INT | Foreign Key | Links the food item to its parent restaurant. |
| | `name` | VARCHAR | | Name of the food or beverage item. |
| | `description` | TEXT | | Brief description of the ingredients or preparation. |
| | `price` | DECIMAL | | Cost of the menu item in local currency. |
| | `calories` | INT | | Total nutritional calorie count for the item. |
| | `category` | VARCHAR | | Menu section grouping (e.g., Starter, Main, Drink). |
| **Order** | `order_id` | INT | Primary Key | Unique identifier for the finalized order. |
| | `user_id` | INT | Foreign Key | Links the order to the purchasing user. |
| | `restaurant_id` | INT | Foreign Key | Links the order to the fulfilling restaurant. |
| | `total_price` | DECIMAL | | Calculated cumulative cost of the entire order. |
| | `total_calories`| INT | | Calculated cumulative calories of the entire order. |
| | `status` | VARCHAR | | Current order state (e.g., Pending, Completed). |
| | `created_at` | TIMESTAMP | | Exact date and time the order was submitted. |
| **Order_Item** | `order_item_id` | INT | Primary Key | Unique identifier for the specific cart line-item. |
| | `order_id` | INT | Foreign Key | Links the line-item to its parent Order. |
| | `item_id` | INT | Foreign Key | Links the line-item to the specific Menu_Item. |
| | `quantity` | INT | | Number of servings of this specific item ordered. |

## Entity Relationships
* **One-to-Many (User ➔ Order):** A single user can place multiple distinct orders over their lifetime.
* **One-to-Many (Restaurant ➔ Menu_Item):** A single restaurant possesses multiple unique items on its menu.
* **One-to-Many (Restaurant ➔ Order):** A single restaurant receives and fulfills multiple orders from various users.
* **One-to-Many (Order ➔ Order_Item):** A single completed checkout order can contain numerous different food items.
