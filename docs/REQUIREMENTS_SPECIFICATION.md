# Requirements Specification

## 1. Introduction and Project Scope

The Restaurant Discovery & Ordering App is designed to streamline the everyday dining decision process for users by combining intelligent local discovery, price and rating filters, transparent nutritional information, and a seamless checkout experience. This specification outlines the complete functional and non-functional requirements necessary to build, test, and deploy a robust Minimum Viable Product (MVP) for Lab 2-3. The system aims to bridge the gap between convenience and health-conscious food ordering by making calorie counts transparent at every step of the user journey.

### 1.1 Target Audience
- Health-conscious individuals seeking nutritional transparency
- Busy professionals looking for quick dining decisions
- Users with specific dietary restrictions and preferences
- Food enthusiasts interested in discovering new local restaurants

### 1.2 Key Value Propositions
- **Transparency First:** Calorie counts and nutritional information displayed at every stage
- **Intelligent Discovery:** Smart recommendations based on user preferences and location
- **Seamless Experience:** From discovery to delivery in just a few taps
- **Health Empowerment:** Tools and filters to make informed dining choices

---

## 2. User Authentication and Account Management

### 2.1 Registration and Login
- **Email/Password Registration:** Users can register using a valid email address and a strong password (minimum 8 characters, containing at least one uppercase letter, one number, and one special character)
- **Social Sign-On (SSO):** Integration with Google OAuth 2.0 and Apple Sign-In for one-tap authentication
- **Password Security:** Passwords must undergo cryptographic hashing using bcrypt or Argon2 prior to storage; plaintext passwords are never stored or logged
- **Session Management:** JWT-based authentication with refresh tokens; sessions automatically expire after 7 days of inactivity
- **Two-Factor Authentication (2FA):** Optional 2FA via authenticator app (Google Authenticator, Authy) for enhanced account security

### 2.2 Profile Management
- **Personal Information:** Users can view and update full name, date of birth (for age-restricted items), and profile photo (upload via camera or gallery)
- **Contact Details:** Manage primary phone number, secondary contact number, and emergency contact
- **Address Management:** Save multiple delivery addresses with labels (Home, Work, Other); set a default delivery address
- **Payment Methods:** Securely store multiple payment methods (credit/debit cards, digital wallets) using tokenization; option to set a default payment method
- **Account Deletion:** Users can request permanent account deletion with a 30-day grace period for recovery

### 2.3 Dietary Preferences and Health Profile
- **Dietary Tags Configuration:** Users can select from a comprehensive list of dietary preferences:
  - Vegan, Vegetarian, Pescetarian
  - Gluten-Free, Dairy-Free, Nut-Free, Egg-Free
  - Keto, Paleo, Low-Carb, Low-Fat
  - Halal, Kosher
- **Allergy Management:** Users can specify known food allergies (peanuts, shellfish, soy, etc.) for automatic warnings
- **Health Goals:** Set daily calorie intake goals; receive recommendations aligning with personal health targets
- **Preference Application:** Selected preferences automatically influence search rankings, menu filtering, and item highlighting
- **Smart Suggestions:** AI-powered recommendations based on past orders and preference patterns

---

## 3. Geolocation and Restaurant Discovery

### 3.1 GPS Integration
- **Location Permission:** The system requests explicit geolocation permission from the client device upon first launch with a clear explanation of why location is needed
- **Real-Time Location:** Automatically fetch and display nearby dining establishments within a configurable spatial radius (default: 10 miles/16 kilometers)
- **Background Location:** Optional background location updates to refresh nearby recommendations when users move
- **Location Privacy:** Users can control location sharing permissions at any time; location data is not stored persistently without explicit consent

### 3.2 Manual Location Fallback
- **Zip Code Entry:** If location sharing is denied, users are prompted to enter a zip code to discover restaurants in that area
- **City and Neighborhood Search:** Support for city names and neighborhood searches with autocomplete suggestions
- **Recent Locations:** Store recently searched locations for quick re-selection
- **Saved Locations:** Users can save frequently visited locations (e.g., work address, gym) for one-tap switching
- **Location Detection Accuracy:** When using GPS, display the detected address and allow manual correction

### 3.3 Discovery Feed Features
- **List and Grid Views:** Toggle between detailed list view (with full metadata) and compact grid view (with restaurant thumbnails)
- **Restaurant Metadata Display:** Each restaurant card explicitly displays:
  - Restaurant name and logo/image
  - Straight-line distance from user's location (or "Unknown" if location unavailable)
  - Aggregated star rating (1-5) with review count
  - Active delivery fee (or "Free Delivery" badge)
  - Applicable price tier ($, $$, $$$, $$$$)
  - Estimated delivery time range (e.g., "25-35 min")
  - Minimum order requirement (if applicable)
  - Open/Closed status with operating hours
- **Search Functionality:** Search restaurants by name, cuisine type, or dish name with real-time suggestions
- **Quick Actions:** From the discovery feed, users can:
  - Add directly to favorites
  - View restaurant details
  - Start an order immediately
  - Share restaurant with friends via social media or messaging apps

---

## 4. Advanced Filtering and Sorting Mechanisms

### 4.1 Price and Rating Filters
- **Price Tier Filter:** Filter restaurants strictly based on price tiers ($, $$, $$$, $$$$)
- **Rating Filter:** Filter by minimum average star rating (e.g., 3.5+, 4+, 4.5+ stars)
- **Price Range Slider:** Advanced filter allowing users to set a custom price range (minimum and maximum total order value)
- **Delivery Fee Filter:** Filter by free delivery, low delivery fee, or custom range
- **Operating Status Filter:** Filter by "Open Now," "Currently Accepting Orders," or "All"

### 4.2 Dietary and Menu Filters
- **Dietary Tag Filters:** Filter menu items and restaurants based on selected dietary tags; restaurants must meet at least one selected tag
- **Allergy-Aware Filtering:** Automatically filter out items containing user-identified allergens; display warning indicators for items with potential cross-contamination
- **Cuisine Type Filter:** Filter by cuisine categories (Italian, Chinese, Mexican, Indian, Japanese, American, etc.)
- **Custom Tags:** Users can create custom tags for personal categorization (e.g., "Quick Lunch," "Date Night")

### 4.3 Sorting Options
- **Sorting Criteria:** Users can sort results by:
  - Distance (nearest first)
  - Rating (highest to lowest)
  - Price (lowest to highest or highest to lowest)
  - Popularity (based on number of reviews)
  - Delivery Time (fastest first)
  - Delivery Fee (lowest to highest)
- **Smart Sort:** Default sorting algorithm that considers a weighted combination of user preferences, distance, and rating
- **Persistent Sort Preferences:** User's last selected sort option is remembered across sessions

### 4.4 Advanced Search Features
- **Voice Search:** Voice-activated search for hands-free discovery
- **Image Search:** Upload a photo of a dish to find restaurants offering similar items
- **Saved Searches:** Users can save frequently used search and filter combinations

---

## 5. Menu Browsing and Nutritional Transparency

### 5.1 Interactive Menu Interface
- **Category Organization:** Menu items organized by categories (Appetizers, Main Course, Desserts, Beverages, etc.)
- **Item Display:** Each menu item explicitly displays:
  - Item name and high-quality image (if available)
  - Detailed description with ingredients list
  - Monetary price
  - Total nutritional calorie count (prominently displayed)
  - Macronutrient breakdown: Protein, Carbohydrates, Fats (in grams)
  - Dietary tags (Vegan, Gluten-Free, etc.) with color-coded badges
  - Allergen information with clear warnings
  - Portion size or serving information
- **Calorie Awareness:** Color-coded calorie indicators:
  - Green: Low calorie (< 400)
  - Yellow: Moderate calorie (400-700)
  - Orange: High calorie (700-1000)
  - Red: Very high calorie (> 1000)

### 5.2 Nutritional Information Dashboard
- **Per-Item Details:** Full nutritional breakdown including:
  - Calories, Total Fat, Saturated Fat, Trans Fat
  - Cholesterol, Sodium, Total Carbohydrates, Dietary Fiber, Sugars
  - Protein, Vitamin D, Calcium, Iron, Potassium
- **Daily Value Percentage:** Display % Daily Value based on a 2,000-calorie daily diet
- **Meal Comparison:** Compare nutritional information across multiple items side-by-side
- **Personalized Daily Targets:** Users can set daily macro goals; items display how they contribute to daily targets

### 5.3 Item Customization Options
- **Special Instructions:** Text field for each menu item to communicate specific preparation requests (e.g., "dressing on the side," "extra crispy," "no onions")
- **Modifier Selections:** Pre-configured modifiers for items:
  - Choose protein (chicken, beef, tofu, etc.)
  - Choose sauce (mild, medium, spicy, extra spicy)
  - Choose sides (fries, salad, rice, etc.)
  - Choose beverage size (small, medium, large)
- **Customization Impact:** When users modify items, the price and nutritional information update dynamically
- **Frequent Customizations:** Save favorite customizations as presets for quick re-ordering
- **Restaurant-Specific Notes:** Users can add general delivery instructions applicable to the entire order

---

## 6. Shopping Cart Management

### 6.1 Cart Operations
- **Add Items:** Add items to cart with selected modifications; confirmation toast notification appears
- **Quantity Management:** Easily increase or decrease item quantities with +/- buttons; remove item entirely with trash icon
- **Cart Summary:** Dynamically compute and prominently display:
  - Subtotal (sum of all item prices)
  - Applicable taxes (calculated based on delivery location)
  - Delivery fee (based on restaurant and location)
  - Service fee (if applicable)
  - Total monetary cost
  - Cumulative total calorie count for the entire order
  - Macronutrient summary (total protein, carbs, fats)
- **Restaurant-Specific Cart:** Users can only order from one restaurant at a time; switching restaurants displays a warning and option to clear the current cart
- **Cart Persistence:** Cart contents persist across sessions; users receive notifications if items become unavailable

### 6.2 Cart Management Features
- **Item Editing:** Click on any cart item to edit modifications or quantity
- **Discount Codes:** Apply promotional discount codes; validation and dynamic price adjustment
- **Loyalty Points:** Display and apply accumulated loyalty points toward order total
- **Suggested Add-ons:** Smart recommendations for popular add-ons based on current cart items
- **Cart Sharing:** Share the cart as a list with friends for group ordering (useful for office or family orders)

### 6.3 Cart Analytics
- **Health Summary:** Display a health summary of the cart (calories, sodium, sugar content)
- **Budget Tracking:** Track current order against daily or monthly budget
- **Previous Orders:** Quick re-add entire previous orders to cart

---

## 7. Checkout and Payment Processing

### 7.1 Checkout Workflow
- **Delivery Destination Confirmation:** Users must confirm or update their delivery address; edit functionality for last-minute changes
- **Itemized Summary:** Display a complete itemized list of all items with quantities, modifications, and individual prices
- **Breakdown Display:** Show detailed cost breakdown (subtotal, taxes, delivery fee, service fee, discounts)
- **Tip Options:** Provide tip selection options (15%, 18%, 20%, custom amount, no tip)
- **Delivery Instructions:** Optional delivery instructions (e.g., "Gate code: 1234," "Leave at door")
- **Special Requests:** General notes for the restaurant or delivery driver
- **Estimated Delivery Time:** Display estimated delivery time based on restaurant prep time and delivery distance

### 7.2 Payment Method Selection
- **Saved Payment Methods:** Select from saved payment methods (credit/debit cards, Apple Pay, Google Pay, PayPal)
- **Add New Payment:** Securely add new payment methods without leaving the checkout flow
- **Default Payment:** Option to set a default payment method for future orders
- **One-Click Checkout:** Users with saved preferences can checkout in a single tap
- **Split Payment:** Support for splitting payment across multiple methods (e.g., gift card + credit card)

### 7.3 Mock Payment Gateway
- **Transaction Simulation:** Integrated secure mock payment processor that validates transaction states:
  - **Successful:** Payment verified; order is created immediately
  - **Pending:** Transaction under review; order status updates when confirmed
  - **Failed:** Payment declined; user is notified and prompted to try another method
- **Payment Validation:** Validate card number format, expiry date, CVV, and billing address
- **Error Handling:** Clear error messages for common failures (insufficient funds, expired card, etc.)
- **Order Confirmation:** Upon successful payment, display order confirmation with order number and estimated delivery time
- **Email and SMS Receipts:** Send confirmation and receipt via email and SMS

### 7.4 Security and Compliance
- **PCI Compliance:** Mock system follows PCI DSS guidelines for payment data security
- **Data Encryption:** All payment data is encrypted in transit (TLS 1.3) and at rest (AES-256)
- **Tokenization:** Sensitive payment information is tokenized; actual card data is never stored
- **Session Security:** Checkout sessions automatically timeout after 15 minutes of inactivity
- **Fraud Detection:** Basic fraud detection rules (suspicious IP, multiple failed attempts, etc.)

---

## 8. Order Tracking and Real-Time Updates

### 8.1 Order Status Lifecycle
- **Order Placed:** Initial confirmation with order number; user receives push notification
- **Order Confirmed:** Restaurant has acknowledged and accepted the order
- **Preparing:** Restaurant is actively preparing the food; estimated prep time displayed
- **Ready for Pickup/Out for Delivery:** Order is ready or assigned to a delivery driver
- **Out for Delivery:** Delivery driver is en route; real-time GPS tracking available
- **Delivered:** Order has been delivered; rating prompt appears
- **Cancelled:** Order was cancelled (by user or restaurant); refund processing initiated

### 8.2 Real-Time Tracking Features
- **Live Map Integration:** Display real-time location of delivery driver on an interactive map
- **Estimated Delivery Countdown:** Dynamic countdown timer showing minutes remaining
- **Status Updates:** Push notifications at each status transition with estimated time
- **Driver Details:** Display delivery driver's name, photo, and contact number
- **Driver Communication:** In-app chat functionality for communicating with the driver
- **ETA Refinement:** ETA updates based on real-time traffic conditions and driver progress
- **Order Cancellation Window:** Users can cancel orders within the first 3 minutes of confirmation

### 8.3 Push Notifications
- **Order Status Changes:** Notifications for all order status changes
- **Promotional Offers:** Location and preference-based promotional offers
- **Restaurant Promotions:** Special deals and limited-time offers from favorite restaurants
- **Weather Alerts:** Notifications for weather conditions that might affect delivery
- **Scheduled Orders:** Reminders for upcoming scheduled orders

---

## 9. Order History and Re-Ordering

### 9.1 Historical Records Management
- **Immutable Log:** Maintain a complete and immutable log of past orders per user account
- **Detailed Receipts:** Each order record includes:
  - Date and time of order
  - Restaurant name and address
  - Complete itemized list with quantities, modifications, and prices
  - Subtotal, taxes, delivery fee, tips, and final total
  - Payment method used (last 4 digits only)
  - Delivery address
  - Order status history with timestamps
  - Delivery driver information
- **Search and Filter:** Search past orders by restaurant name, item name, date range, or price range
- **Analytics Dashboard:** Visual analytics showing spending habits, favorite restaurants, and ordering patterns

### 9.2 Re-Ordering Capabilities
- **Quick Re-Order:** Re-order an entire previous order with a single tap (using original items and modifications)
- **Edit Before Re-Order:** Modify quantities, remove items, or add new items before placing a re-order
- **Favorites List:** Mark items or entire orders as favorites for quick access
- **Subscription Orders:** Set up recurring orders for frequently purchased items (e.g., "Order every Monday at 12 PM")
- **Suggested Re-Orders:** AI-powered suggestions for re-ordering based on past behavior
- **Group Re-Order:** Ability to share a previous order with friends for group ordering

### 9.3 History Analytics
- **Spending Insights:** Monthly, quarterly, and yearly spending breakdowns
- **Restaurant Ranking:** Automatically rank restaurants based on frequency of ordering and average rating
- **Health Trends:** Track nutritional trends across orders (calorie intake, dietary patterns)
- **Recommendations:** Personalized restaurant and item recommendations based on history analysis
- **Export History:** Ability to export order history as CSV or PDF for personal record-keeping

---

## 10. Review and Rating System

### 10.1 Post-Delivery Review Flow
- **Review Prompt:** Upon delivery completion, users receive a prompt to submit a rating and review
- **Rating Options:** 1 to 5-star rating with half-star increments for precision
- **Textual Feedback:** Optional written review with minimum 5-character requirement to encourage substantive feedback
- **Photo Upload:** Option to upload photos of the delivered food (enhances review credibility)
- **Fast Review Option:** Quick review template with predefined responses (e.g., "Great food!", "Delayed delivery")
- **Scheduled Reminders:** Gentle reminders to review if not completed within 24 hours

### 10.2 Review Display and Management
- **Aggregated Rating:** Average star rating updates in real-time with each new review
- **Rating Breakdown:** Display rating distribution (number of 1-star, 2-star, 3-star, 4-star, 5-star reviews)
- **Recent Reviews:** Sort and filter reviews by most recent, highest rated, lowest rated, or most helpful
- **Verified Purchase Badge:** Users who actually ordered from the restaurant receive a "Verified Order" badge
- **Response Feature:** Restaurants can respond to reviews; users can reply to restaurant responses
- **Review Highlights:** AI-powered summarization of common themes in reviews (e.g., "Great service," "Good portion sizes")

### 10.3 Review Moderation
- **Report Inappropriate Reviews:** Users can flag reviews containing offensive content or false information
- **Review Guidelines:** Clear guidelines on acceptable review content
- **Edit/Delete Reviews:** Users can edit or delete their reviews within 48 hours of submission
- **Automated Moderation:** AI-powered flagging of potentially inappropriate content
- **User Reputation:** Users with a history of helpful reviews earn reputation points and recognition

### 10.4 Restaurant Analytics
- **Performance Dashboard:** Restaurant owners can view key metrics:
  - Average rating trends over time
  - Review volume and sentiment analysis
  - Common praise and complaint themes
  - Response rate and time metrics
- **Rating Updates:** Restaurants can request review of suspicious rating patterns
- **User Feedback Integration:** User feedback directly informs restaurant improvement recommendations

---

## 11. Admin Dashboard and Restaurant Management

### 11.1 Restaurant Dashboard
- **Menu Management:** Add, update, or remove menu items with real-time storefront updates
- **Inventory Management:** Update available quantities and item availability (out-of-stock items automatically hide or display warnings)
- **Operating Hours:** Configure daily operating hours and special holiday hours
- **Delivery Zones:** Define delivery radius and zones; configure per-zone delivery fees
- **Order Management:** View and manage incoming orders with order status updates
- **Revenue Analytics:** Track daily, weekly, and monthly revenue; view popular items and peak ordering times
- **Customer Insights:** Analytics on customer demographics, ordering patterns, and satisfaction metrics
- **Performance Metrics:** Average prep time, delivery time, and order completion rate

### 11.2 Platform Admin Dashboard
- **User Management:** View, suspend, or deactivate user accounts; manage user roles and permissions
- **Restaurant Verification:** Approve new restaurant listings and verify business information
- **Transaction Monitoring:** Monitor all transactions and flag suspicious activities
- **Content Moderation:** Oversee reviews, user-generated content, and reported issues
- **System Health:** Monitor server uptime, response times, and error logs
- **Analytics Reports:** Generate comprehensive platform analytics reports (user growth, revenue, order volume)
- **Feature Management:** Enable or disable platform features (A/B testing capabilities)

### 11.3 Compliance and Security
- **GDPR Compliance:** Tools for data access requests, data deletion, and consent management
- **Audit Logs:** Comprehensive audit trails for all administrative actions
- **Role-Based Access Control (RBAC):** Granular permissions for different admin roles
- **Security Alerts:** Real-time alerts for suspicious activities, failed login attempts, and data breaches

---

## 12. Non-Functional Requirements

### 12.1 Performance and Scalability
- **Page Load Time:** All pages must load within 3 seconds on standard 4G connections
- **API Response Time:** REST API endpoints must respond within 200ms for 95% of requests
- **Concurrent Users:** System must support up to 10,000 concurrent users without degradation
- **Database Performance:** Database queries must execute within 100ms for 99% of operations
- **Scalability:** Horizontal scaling capability using containerization (Docker, Kubernetes)
- **Caching:** Implement multi-level caching (Redis) for frequently accessed data
- **CDN Integration:** Static assets served via Content Delivery Network for faster global access

### 12.2 Security
- **Data Encryption:** All data in transit must be encrypted using TLS 1.3; data at rest using AES-256
- **Authentication:** JWT tokens with short expiration (15 minutes) and refresh tokens (7 days)
- **Authorization:** Role-based access control (RBAC) for all system resources
- **Rate Limiting:** API rate limiting to prevent abuse (100 requests per minute per user)
- **Input Validation:** All user inputs must be validated and sanitized to prevent injection attacks
- **Security Headers:** Implement standard security headers (CSP, HSTS, X-Frame-Options)
- **Dependency Management:** Regular security audits of third-party dependencies
- **Incident Response:** Documented incident response plan for security breaches

### 12.3 Reliability and Availability
- **Uptime:** Target 99.9% uptime for critical services (order processing, payment)
- **Disaster Recovery:** Automated backups every 6 hours; point-in-time recovery capability
- **Graceful Degradation:** System should gracefully degrade when non-critical services are unavailable
- **Retry Logic:** Implement exponential backoff retry for transient failures
- **Circuit Breakers:** Use circuit breakers to prevent cascading failures
- **Health Checks:** Automated health checks and auto-recovery for failed services
- **SLA Monitoring:** Real-time monitoring and alerting for SLA breaches

### 12.4 Usability and Accessibility
- **Responsive Design:** Fully responsive for all screen sizes (mobile, tablet, desktop)
- **Accessibility:** WCAG 2.1 AA compliance (proper ARIA labels, keyboard navigation, color contrast)
- **Mobile-First:** Optimized for mobile devices with touch-optimized interactions
- **Offline Mode:** Basic offline capabilities (view cached restaurant data, saved orders)
- **Browser Support:** Support for latest two versions of major browsers (Chrome, Firefox, Safari, Edge)
- **User Guidance:** Contextual help and onboarding tutorials for new features
- **Feedback Mechanisms:** In-app feedback forms and user satisfaction surveys

### 12.5 Maintainability and Code Quality
- **Documentation:** Comprehensive API documentation using OpenAPI/Swagger
- **Code Standards:** Strict adherence to coding standards and style guides
- **Testing:** Minimum 85% code coverage with unit, integration, and end-to-end tests
- **CI/CD:** Automated build, test, and deployment pipelines
- **Monitoring:** Comprehensive logging and monitoring with ELK stack or similar
- **Versioning:** Semantic versioning for APIs; clear deprecation policy
- **Code Reviews:** Mandatory code reviews before merging to main branch

---

## 13. Future Enhancements and Roadmap

### 13.1 Phase 2 Features (Post-MVP)
- **AI-Powered Recommendations:** Machine learning models for personalized restaurant and dish recommendations
- **Social Features:** Friend lists, shareable order lists, group ordering capabilities
- **Loyalty Program:** Points-based loyalty system with tiered rewards
- **Restaurant Takeover:** Live cooking shows and restaurant takeover events
- **Real-Time Chat:** In-app chat support with restaurants for order inquiries
- **Subscription Service:** Premium subscription with benefits (free delivery, exclusive discounts)
- **Voice Ordering:** Voice-activated ordering via smart assistants (Alexa, Google Home)

### 13.2 Phase 3 Features (Long-term)
- **Global Expansion:** Multi-country support with localization for 15+ languages
- **Virtual Dining:** AR-based virtual dining experiences and restaurant previews
- **Health Integration:** Connect to health and fitness apps (Apple Health, Fitbit) for integrated tracking
- **Smart Kitchen Integration:** Direct integration with restaurant kitchen management systems
- **Blockchain Integration:** Blockchain-based review verification and loyalty points
- **Sustainable Choices:** Carbon footprint tracking and eco-friendly restaurant highlighting
- **Corporate Accounts:** Dedicated features for corporate lunch programs and expense management

### 13.3 Continuous Improvement
- **User Feedback Loop:** Regular user surveys and beta testing programs
- **A/B Testing:** Continuous A/B testing for feature optimization
- **Performance Optimization:** Ongoing performance monitoring and optimization
- **Security Updates:** Regular security audits and timely patch management
- **Technology Upgrades:** Regular technology stack upgrades for security and performance

---

*This requirements specification is a living document and will be updated as the project evolves through development phases. All team members are expected to refer to this document for clarity on system functionality and scope.*