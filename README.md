# Food Delivery System

## Overview

The Food Delivery System is a web-based platform that allows customers to browse restaurants, order food, make payments, and track deliveries. It also provides functionalities for restaurant owners to manage their menus and orders, while delivery agents can track and complete deliveries.

## Table of Contents

- [Food Delivery System](#food-delivery-system)
  - [Overview](#overview)
  - [Table of Contents](#table-of-contents)
  - [Key Features](#key-features)
    - [1. User Management](#1-user-management)
      - [Pseudocode for User Registration \& Authentication](#pseudocode-for-user-registration--authentication)
        - [1. Sign Up](#1-sign-up)
        - [2. Login](#2-login)
        - [3. Forget Password](#3-forget-password)
        - [4. Email/OTP Verification](#4-emailotp-verification)
        - [5. User/Customer Profile](#5-usercustomer-profile)
        - [6. Logout](#6-logout)
        - [7. Social Media Authentication](#7-social-media-authentication)
        - [8. Enable/Disable Account](#8-enabledisable-account)
        - [9. Role-based \& Permissions](#9-role-based--permissions)
      - [Sequence Diagram for User Registration \& Authentication](#sequence-diagram-for-user-registration--authentication)
      - [Flowchart for User Registration \& Authentication](#flowchart-for-user-registration--authentication)
    - [2. Restaurant Management](#2-restaurant-management)
    - [3. Menu \& Food Management](#3-menu--food-management)
    - [4. Cart Management](#4-cart-management)
    - [5. Order Processing](#5-order-processing)
    - [6. Payment \& Transaction Management](#6-payment--transaction-management)
    - [7. Delivery Management](#7-delivery-management)
    - [8. Reviews \& Ratings](#8-reviews--ratings)
    - [9. Coupons \& Discounts](#9-coupons--discounts)
    - [10. Admin Panel](#10-admin-panel)
  - [Database Structure](#database-structure)
    - [Key Tables](#key-tables)
  - [Future Enhancements](#future-enhancements)
  - [Conclusion](#conclusion)

## Key Features

### 1. User Management

**Description:** Handles user registration, authentication, and role-based access control.

```plaintext
- Database Design: Structured schema for storing user information.
- API Endpoints:
  - Sign up
  - Login
  - Forgot Password
  - Email verification or OTP verification
  - User/Customer Profile Management
  - Logout
  - Social Media Authentication (Google, Facebook, etc.)
  - Enable or Disable Account
- Role-based & Permissions: Admin, Restaurant Owner, Customer, Delivery Agent.
```

#### Pseudocode for User Registration & Authentication

##### 1. Sign Up

```plaintext
FUNCTION SignUp(username, email, password)
    IF Database.CheckUserExists(email) THEN
        RETURN "Error: User already exists"
    ELSE
        Database.StoreUser(username, email, password)
        verificationCode = GenerateVerificationCode()
        EmailService.SendVerificationEmail(email, verificationCode)
        RETURN "Verification email sent"
    END IF
END FUNCTION
```

##### 2. Login

```plaintext
FUNCTION Login(email, password)
    IF Database.ValidateCredentials(email, password) THEN
        token = GenerateAuthToken()
        RETURN "Login Successful. Token: " + token
    ELSE
        RETURN "Error: Invalid credentials"
    END IF
END FUNCTION
```

##### 3. Forget Password

```plaintext
FUNCTION ForgetPassword(email)
    IF Database.CheckUserExists(email) THEN
        resetToken = GenerateResetToken()
        EmailService.SendPasswordResetEmail(email, resetToken)
        RETURN "Password reset email sent"
    ELSE
        RETURN "Error: User not found"
    END IF
END FUNCTION
```

##### 4. Email/OTP Verification

```plaintext
FUNCTION VerifyEmail(email, verificationCode)
    IF Database.VerifyCode(email, verificationCode) THEN
        Database.MarkEmailAsVerified(email)
        RETURN "Email verified successfully"
    ELSE
        RETURN "Error: Invalid verification code"
    END IF
END FUNCTION
```

##### 5. User/Customer Profile

```plaintext
FUNCTION GetProfile(userId)
    profileData = Database.FetchProfile(userId)
    RETURN profileData
END FUNCTION
```

##### 6. Logout

```plaintext
FUNCTION Logout(token)
    Database.InvalidateToken(token)
    RETURN "Logout successful"
END FUNCTION
```

##### 7. Social Media Authentication

```plaintext
FUNCTION SocialMediaLogin(socialMediaToken)
    userData = SocialMediaAPI.Authenticate(socialMediaToken)
    IF userData THEN
        Database.StoreOrUpdateUser(userData)
        RETURN "Social media login successful"
    ELSE
        RETURN "Error: Social media authentication failed"
    END IF
END FUNCTION
```

##### 8. Enable/Disable Account

```plaintext
FUNCTION ToggleAccountStatus(userId, status)
    Database.UpdateAccountStatus(userId, status)
    RETURN "Account status updated"
END FUNCTION
```

##### 9. Role-based & Permissions

```plaintext
FUNCTION CheckAccess(userId, resource)
    userRole = Database.GetUserRole(userId)
    IF userRole.HasPermission(resource) THEN
        RETURN "Access granted"
    ELSE
        RETURN "Error: Access denied"
    END IF
END FUNCTION
```

#### Sequence Diagram for User Registration & Authentication

![Sequence Diagram for User Registration & Authentication](./images/SD-User%20Management.png)

---

#### Flowchart for User Registration & Authentication

![Flowchart for User Registration & Authentication](./images/Flowchart-User%20Management.png)

---

### 2. Restaurant Management

**Description:** Enables restaurant owners to manage their business operations.

```plaintext
- Restaurant Registration: Owners can register their restaurants.
- Menu Management: Add, update, or remove food items.
- Restaurant Profile Update: Change contact details, address, and business hours.
- Order Management: Accept or reject orders and update order statuses.
```

### 3. Menu & Food Management

**Description:** Manages restaurant menus and food items.

```plaintext
- Add/Edit/Delete Menu Items: Restaurant owners can update their menus.
- Category Management: Organize food items into categories (e.g., Pizza, Sushi, Desserts).
- Item Availability: Mark items as available or unavailable.
```

### 4. Cart Management

**Description:** Allows customers to manage their food selection before ordering.

```plaintext
- Add to Cart: Customers can add multiple items to the cart.
- Modify Cart: Increase or decrease item quantity or remove items.
- Apply Coupons: Apply discount codes before checkout.
- Calculate Total Price: Displays total price including taxes and discounts.
```

### 5. Order Processing

**Description:** Handles food orders from creation to completion.

```plaintext
- Place Order: Customers can place an order after finalizing their cart.
- Order Tracking: Track order status (pending, preparing, out for delivery, delivered).
- Cancel Order: Customers can cancel orders before they are prepared.
- Order Notifications: Sends updates via email/SMS or push notifications.
```

### 6. Payment & Transaction Management

**Description:** Processes payments securely.

```plaintext
- Payment Methods: Supports credit/debit cards, PayPal, and cash on delivery.
- Payment Gateway Integration: Secure transactions via third-party providers.
- Refund Processing: Handles refunds for canceled orders.
- Payment Status Updates: Updates payment status (pending, completed, failed).
```

### 7. Delivery Management

**Description:** Manages food delivery operations.

```plaintext
- Delivery Assignment: Assign orders to delivery agents.
- Real-time Tracking: Allows customers to track their delivery in real time.
- Delivery Status Updates: Updates status (out for delivery, delivered).
- Estimated Delivery Time: Provides estimated arrival time for food.
```

### 8. Reviews & Ratings

**Description:** Allows customers to rate and review restaurants.

```plaintext
- Rate Restaurants: Give ratings from 1 to 5 stars.
- Leave Reviews: Customers can write reviews on completed orders.
- View Reviews: Publicly visible reviews for restaurants.
```

### 9. Coupons & Discounts

**Description:** Provides promotions and discounts.

```plaintext
- Create Coupons: Admins can generate discount codes.
- Apply Discounts: Customers can enter valid codes during checkout.
- Coupon Validity: Set expiration dates for discounts.
```

### 10. Admin Panel

**Description:** Centralized control for system administrators.

```plaintext
- User Management: View and manage all registered users.
- Order Oversight: Monitor all orders and their statuses.
- Restaurant Approval: Approve or reject restaurant registrations.
- System Logs & Analytics: View statistics and logs.
```

## Database Structure

### Key Tables

```plaintext
- users: Stores customer, restaurant owner, and delivery agent details.
- restaurants: Stores restaurant information.
- menu_items: Stores menu items for each restaurant.
- orders: Stores order details including customer and restaurant data.
- order_items: Stores individual items in each order.
- payments: Stores payment transactions.
- deliveries: Tracks food delivery assignments and statuses.
- reviews: Stores customer reviews and ratings.
- coupons: Stores discount codes and validity details.
```

## Future Enhancements

```plaintext
- AI-Based Recommendations: Suggests popular dishes based on customer preferences.
- Loyalty Program: Rewards returning customers with discounts.
- Multiple Payment Options: Expanding support for more payment gateways.
- Multi-Language Support: Adding localization for different regions.
```

## Conclusion

This **Food Delivery System** ensures a seamless experience for customers, restaurant owners, and delivery agents. The platform is designed with a scalable architecture, making it easy to add new features and expand in the future.
