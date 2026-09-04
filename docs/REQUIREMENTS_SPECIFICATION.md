# Requirements Specification

## 1. Functional Requirements
* **1.1 Restaurant Discovery:** The system must prompt the user for geolocation access to fetch nearby dining options and display a list or grid of restaurants showing Name, Distance, Average Rating, and Price Tier.
* **1.2 Filtering & Sorting:** Users must be able to filter the restaurant list by specific Price Tiers ($, $$, $$$) and sort the feed by Average Rating.
* **1.3 Calorie-Aware Menus:** Selecting a restaurant must open a digital menu where every item clearly displays its name, description, price, and total calorie count, organized by categories (e.g., Starters, Mains, Drinks).
* **1.4 Cart & Ordering System:** Users must be able to add/remove items in a digital cart. The cart must dynamically calculate and prominently display the **cumulative total price** and **cumulative total calorie count** before allowing the user to click "Checkout".

## 2. Non-Functional Requirements
* **2.1 Usability:** The application interface must be fully mobile-responsive, adapting cleanly to smartphone, tablet, and desktop viewports.
* **2.2 Performance:** Database queries for fetching the restaurant list and individual menus should execute and render in under 2 seconds on standard connections.
* **2.3 Security & Privacy:** User location coordinates must strictly be used for calculating proximity and must not be permanently stored or shared with third parties.
* **2.4 Reliability & Availability:** The system’s source code and project documentation must be consistently version-controlled and publicly accessible via a GitHub repository.
