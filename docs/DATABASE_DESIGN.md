# Database Design

The database architecture for the Restaurant Discovery & Ordering App is built on a robust relational model to manage user profiles, restaurant locations, nutritional data, complex transaction histories, and delivery logistics.

## Core Entities
* **User:** Stores account credentials, contact information, and geographic coordinates.
* **Restaurant:** Houses business details, customer ratings, price tiers, operating status, and exact map coordinates.
* **Menu_Category:** Normalizes menu sections (e.g., Starters, Mains, Drinks) for dynamic rendering.
* **Menu_Item:** Catalogues available food options, crucial calorie counts, and pricing data.
* **Dietary_Tag & Item_Tags:** Manages a many-to-many relationship for complex dietary filtering (e.g., Vegan, Gluten-Free).
* **Order:** Acts as the master record for a transaction, storing delivery details, total monetary price, and cumulative calorie count.
* **Order_Item:** A line-item junction table recording the exact menu items, historical prices, and quantities purchased.
* **Payment:** Tracks financial transaction details, payment gateways, and clearing status.
* **Delivery:** Manages driver assignment, real-time tracking coordinates, and delivery timestamps.
* **Review:** Captures user-generated ratings and written feedback to drive the average rating calculations.

## Database Schema

### Users & Authentication
| Column Name | Data Type | Key / Constraint | Description |
| :--- | :--- | :--- | :--- |
| `user_id` | INT | Primary Key | Unique identifier for the user account. |
| `name` | VARCHAR | NOT NULL | User's full display name. |
| `email` | VARCHAR | Unique | User's email address for login and receipts. |
| `password_hash`| VARCHAR | NOT NULL | Encrypted password for secure authentication. |
| `phone_number` | VARCHAR | | User's contact number for delivery updates. |
| `location_lat` | DECIMAL | | User's last known latitude coordinate. |
| `location_lng` | DECIMAL | | User's last known longitude coordinate. |
| `created_at` | TIMESTAMP | Default: NOW() | Date the account was registered. |

### Restaurants
| Column Name | Data Type | Key / Constraint | Description |
| :--- | :--- | :--- | :--- |
| `restaurant_id` | INT | Primary Key | Unique identifier for the restaurant venue. |
| `name` | VARCHAR | NOT NULL | Official name of the restaurant. |
| `address` | TEXT | NOT NULL | Physical street address. |
| `rating` | DECIMAL | Default: 0.0 | Average aggregated customer rating. |
| `price_tier` | VARCHAR | | Budget classification (e.g., $, $$, $$$). |
| `delivery_fee` | DECIMAL | Default: 0.00 | Standard delivery charge for this location. |
| `latitude` | DECIMAL | NOT NULL | Restaurant's exact latitude coordinate. |
| `longitude` | DECIMAL | NOT NULL | Restaurant's exact longitude coordinate. |
| `is_open` | BOOLEAN | Default: TRUE | Toggle for accepting new orders. |

### Menu Categories
| Column Name | Data Type | Key / Constraint | Description |
| :--- | :--- | :--- | :--- |
| `category_id` | INT | Primary Key | Unique identifier for the menu category. |
| `restaurant_id` | INT | Foreign Key | Links category to a specific restaurant. |
| `name` | VARCHAR | NOT NULL | Name of category (e.g., "Appetizers"). |
| `display_order`| INT | | Controls sorting order on the menu page. |

### Menu Items
| Column Name | Data Type | Key / Constraint | Description |
| :--- | :--- | :--- | :--- |
| `item_id` | INT | Primary Key | Unique identifier for the individual menu item. |
| `category_id` | INT | Foreign Key | Links item to its specific category. |
| `restaurant_id` | INT | Foreign Key | Links the food item to its parent restaurant. |
| `name` | VARCHAR | NOT NULL | Name of the food or beverage item. |
| `description` | TEXT | | Brief description of the ingredients or preparation. |
| `price` | DECIMAL | NOT NULL | Cost of the menu item in local currency. |
| `calories` | INT | NOT NULL | Total nutritional calorie count for the item. |
| `is_available` | BOOLEAN | Default: TRUE | Allows restaurants to hide sold-out items. |

### Dietary Tags (Many-to-Many)
| Table Name | Column Name | Data Type | Key / Constraint | Description |
| :--- | :--- | :--- | :--- | :--- |
| **Dietary_Tag** | `tag_id` | INT | Primary Key | Unique identifier (e.g., 1). |
| | `name` | VARCHAR | Unique | Tag name (e.g., "Vegan", "Gluten-Free"). |
| **Item_Tags** | `item_id` | INT | Foreign Key | Links to Menu_Item. |
| | `tag_id` | INT | Foreign Key | Links to Dietary_Tag. |

### Orders & Cart
| Column Name | Data Type | Key / Constraint | Description |
| :--- | :--- | :--- | :--- |
| `order_id` | INT | Primary Key | Unique identifier for the finalized order. |
| `user_id` | INT | Foreign Key | Links the order to the purchasing user. |
| `restaurant_id` | INT | Foreign Key | Links the order to the fulfilling restaurant. |
| `total_price` | DECIMAL | NOT NULL | Calculated cumulative cost. |
| `total_calories`| INT | NOT NULL | Calculated cumulative calories of the entire order. |
| `delivery_address`| TEXT| NOT NULL | Specific address for order delivery. |
| `instructions` | TEXT | | Special requests (e.g., "Leave at front door"). |
| `status` | VARCHAR | Default: 'Pending'| Current order state (e.g., Pending, Completed). |
| `created_at` | TIMESTAMP | Default: NOW() | Exact date and time the order was submitted. |

### Order Items (Line Items)
| Column Name | Data Type | Key / Constraint | Description |
| :--- | :--- | :--- | :--- |
| `order_item_id` | INT | Primary Key | Unique identifier for the specific cart line-item. |
| `order_id` | INT | Foreign Key | Links the line-item to its parent Order. |
| `item_id` | INT | Foreign Key | Links the line-item to the specific Menu_Item. |
| `quantity` | INT | NOT NULL | Number of servings ordered. |
| `unit_price` | DECIMAL | NOT NULL | Price locked in at checkout to preserve historical accuracy. |

### Payments
| Column Name | Data Type | Key / Constraint | Description |
| :--- | :--- | :--- | :--- |
| `payment_id` | INT | Primary Key | Unique identifier for the transaction. |
| `order_id` | INT | Foreign Key | Links payment to the specific order. |
| `amount` | DECIMAL | NOT NULL | Total amount charged. |
| `method` | VARCHAR | NOT NULL | Payment type (e.g., Credit Card, Apple Pay). |
| `status` | VARCHAR | Default: 'Pending'| Transaction state (e.g., Successful, Failed). |
| `processed_at`| TIMESTAMP | | Timestamp of bank clearance. |

### Deliveries
| Column Name | Data Type | Key / Constraint | Description |
| :--- | :--- | :--- | :--- |
| `delivery_id` | INT | Primary Key | Unique identifier for the delivery run. |
| `order_id` | INT | Foreign Key | Links to the specific order. |
| `driver_name` | VARCHAR | NOT NULL | Name of the assigned delivery driver. |
| `current_lat` | DECIMAL | | Live tracking latitude. |
| `current_lng` | DECIMAL | | Live tracking longitude. |
| `estimated_time`| TIMESTAMP | | Expected arrival time. |
| `delivered_at` | TIMESTAMP | | Exact completion time. |

### Reviews
| Column Name | Data Type | Key / Constraint | Description |
| :--- | :--- | :--- | :--- |
| `review_id` | INT | Primary Key | Unique identifier for the review. |
| `user_id` | INT | Foreign Key | User who wrote the review. |
| `restaurant_id` | INT | Foreign Key | Restaurant being reviewed. |
| `rating` | INT | NOT NULL | Score from 1 to 5 stars. |
| `comment` | TEXT | | Optional written feedback. |
| `created_at` | TIMESTAMP | Default: NOW() | Date the review was published. |

## Entity Relationships
* **User ➔ Order (1:N):** A single user can place multiple distinct orders over their lifetime.
* **User ➔ Review (1:N):** A user writes multiple reviews over time.
* **Restaurant ➔ Menu_Item (1:N):** A single restaurant possesses multiple unique items on its menu.
* **Restaurant ➔ Order (1:N):** A single restaurant receives and fulfills multiple orders from various users.
* **Restaurant ➔ Review (1:N):** A restaurant receives reviews from multiple users.
* **Menu_Item ➔ Item_Tags (1:N):** An item can have multiple dietary tags.
* **Order ➔ Order_Item (1:N):** A single completed checkout order can contain numerous different food items.
* **Order ➔ Payment (1:1):** Each order is linked to one specific payment transaction record.
* **Order ➔ Delivery (1:1):** Each order is assigned to one delivery record.
