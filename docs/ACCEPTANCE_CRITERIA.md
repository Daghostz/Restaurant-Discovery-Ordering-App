# Acceptance Criteria

| Feature ID | Feature Name | Acceptance Criteria (Given / When / Then) |
| :--- | :--- | :--- |
| **AC-01** | Location Access Granted | **Given** the user grants location permissions, **When** the app loads, **Then** it displays a list of restaurants sorted by proximity. |
| **AC-02** | Location Access Denied | **Given** the user denies location permissions, **When** the app loads, **Then** it prompts the user to manually enter a zip code or city. |
| **AC-03** | Price Filter | **Given** the user is on the discovery screen, **When** they select a price tier ("$", "$$", "$$$"), **Then** only restaurants matching that tier are displayed. |
| **AC-04** | Rating Sort | **Given** the user views the restaurant list, **When** they apply the "Top Rated" sort, **Then** the list reorganizes from highest average rating to lowest. |
| **AC-05** | Combined Filters | **Given** the user applies multiple filters (e.g., "$$" AND "4+ Stars"), **When** the feed updates, **Then** only restaurants satisfying both conditions appear. |
| **AC-06** | Clear Filters | **Given** active filters are applied, **When** the user clicks "Clear Filters", **Then** the feed resets to the default proximity-based list. |
| **AC-07** | Menu Item Details | **Given** a user opens a restaurant menu, **When** they view an item, **Then** the item name, description, price, and total calorie count must be explicitly visible. |
| **AC-08** | Add to Cart | **Given** a user is viewing a menu, **When** they tap "Add to Cart" on an item, **Then** the cart icon updates to reflect the new item count. |
| **AC-09** | Cart Quantity Adjustment | **Given** an item is in the cart, **When** the user increases or decreases the quantity, **Then** the item subtotal and calorie subtotal update immediately. |
| **AC-10** | Remove from Cart | **Given** an item is in the cart, **When** the user reduces the quantity to zero, **Then** the item is completely removed from the cart summary. |
| **AC-11** | Dynamic Price Total | **Given** the user adds multiple items, **When** they view the cart, **Then** the cumulative total monetary price is calculated and displayed accurately. |
| **AC-12** | Dynamic Calorie Total | **Given** the user adds multiple items, **When** they view the cart, **Then** the cumulative total calorie count for the entire order is calculated and displayed accurately. |
| **AC-13** | Empty Cart Checkout | **Given** the cart contains zero items, **When** the user attempts to tap "Checkout", **Then** the button is disabled and a "Cart is empty" message appears. |
| **AC-14** | Checkout Confirmation | **Given** the user has a populated cart, **When** they finalize the checkout process, **Then** an order confirmation screen displays the final total price, total calories, and an order ID. |
| **AC-15** | Mobile Responsiveness | **Given** the user accesses the app on a mobile device, **When** they navigate through the app, **Then** the UI scales correctly without horizontal scrolling. |
