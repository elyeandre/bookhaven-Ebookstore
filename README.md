# 📚 BookHaven Online Bookstore

[![Made With Java][made-with-java]][forthebadge-url]
[![Built With Love][built-with-love]][forthebadge-url]

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-issues-url]

A comprehensive **desktop application** built with Java Swing that provides a complete online bookstore experience. This academic project demonstrates enterprise-level software development practices for book inventory management, user authentication, shopping cart functionality, and order processing with integrated voucher system.

## 📋 Table of Contents
- [🎯 Project Overview](#-project-overview)
- [✨ Key Features](#-key-features)
- [🛠️ Tech Stack](#️-tech-stack)
- [🏗️ Architecture](#️-architecture)
- [📁 Project Structure](#-project-structure)
- [🚀 Quick Start](#-quick-start)
- [⚙️ Configuration](#️-configuration)
- [📱 Usage Guide](#-usage-guide)
- [:lock: Security Notes](#security-notes)
- [🧪 Testing](#-testing)
- [🚀 Deployment](#-deployment)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)
- [:camera_flash: Screenshots](#screenshots)

## 🎯 Project Overview

**BookHaven** is a sophisticated desktop application that recreates the online bookstore experience in a rich graphical user interface. Built as an academic project using Java Swing and MySQL, it demonstrates modern software development principles while providing a fully functional e-commerce platform for book sales.

### 🎯 Target Users
- **📖 Book Readers / Customers**: Browse catalog, search, manage cart, apply vouchers, print a receipt

> Note: No dedicated admin UI or post‑checkout order history functionality is implemented.

### 🌟 Problem Statement
Deliver an academic demonstration of a basic bookstore purchasing flow (browse → cart → checkout → printable receipt) with simple voucher discount logic using Java Swing + MySQL.

## ✨ Key Features

### 📚 **Book Catalog Management**
- **Catalog Display**: Grid-style list with cover thumbnails
- **Search Filter**: Simple text filter (title/author/genre substring match)
- **Book Details**: Author, publisher, genre, pages, price (shown in UI panels)
- **Stock Field**: `stock_count` read only (no decrement logic on checkout)
- **Cover Art**: Scaled images for presentation

### 🛒 **Shopping Cart System**
- **Add / Remove**: Manage selected books and quantity spinner
- **Book Types**: Paperback vs Hardcover (Hardcover +15% price)
- **Totals**: Recompute subtotal & discount when quantities or voucher change
- **Cart Indicator**: Count & empty view state
- **Checkout Trigger**: Opens inline panel for customer & voucher info

### 🔐 **User Authentication & Profiles**
- **Registration**: Username, email (basic format/Gmail check), birthday, password
- **Login**: Plaintext credential check against DB record
- **Profile Edit**: Update basic fields & password; avatar BLOB storage
- **Validation**: Duplicate username/email detection; password strength helper
- **Limitation**: No hashed passwords or persistent session management

### 🎫 **Voucher & Discount System**
- **In-Memory Codes**: Added at runtime (resets each launch)
- **Validation**: Lookup + date check
- **Discount Application**: Adjusts total at checkout view
- **Scope**: Not persisted in DB

### 📄 **Order Processing & Receipts**
- **Order Summary**: Detailed breakdown of purchases and totals
- **Payment Methods**: Multiple payment options (COD, Banking partners)
- **Receipt Generation**: Professional receipt printing functionality
- **Customer Information**: Delivery address and contact management
- **Order Confirmation**: Complete transaction workflow

### 🔍 **Advanced UI/UX Features**
- **Custom Components**: Specialized UI elements (CustomComboBox, CustomSpinner)
- **Responsive Design**: Adaptive layout for different screen sizes
- **Visual Feedback**: Hover effects, button states, and animations
- **Accessibility**: Keyboard navigation and focus management
- **Error Handling**: User-friendly error messages and validation feedback

## 🛠️ Tech Stack

### **Core Technologies**
- **Language**: Java 11+
- **GUI Framework**: Java Swing with NetBeans GUI Builder
- **Database**: MySQL 8.0.33 with JDBC connectivity
- **Build Tool**: Apache Maven 3.x
- **IDE**: NetBeans IDE (recommended)

### **Java Libraries & Dependencies**
- **MySQL Connector**: `mysql-connector-java:8.0.33`
- **AbsoluteLayout**: NetBeans layout manager for precise component positioning
- **Java AWT/Swing**: Core GUI components and event handling
- **JDBC**: Database connectivity and SQL operations

### **Development Tools**
- **NetBeans GUI Builder**: Visual form designer for Swing interfaces
- **Maven**: Dependency management and project building
- **MySQL Workbench**: Database design and management
- **Git**: Version control and collaboration

### **Architecture Patterns**
- **MVC Pattern**: Separation of Model (data), View (UI), Controller (logic)
- **DAO Pattern**: Data Access Objects for database operations
- **Observer Pattern**: Event-driven UI updates and notifications
- **Singleton Pattern**: Database connection management

## 🏗️ Architecture

### **System Architecture**
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  Presentation   │    │   Business      │    │   Data Layer    │
│     Layer       │    │     Logic       │    │                 │
│                 │    │                 │    │                 │
│ ┌─────────────┐ │    │ ┌─────────────┐ │    │ ┌─────────────┐ │
│ │    Swing    │ │    │ │   Models    │ │    │ │   MySQL     │ │
│ │     UI      │◄├────┤►│   Classes   │◄├────┤►│  Database   │ │
│ └─────────────┘ │    │ └─────────────┘ │    │ └─────────────┘ │
│ ┌─────────────┐ │    │ ┌─────────────┐ │    │ ┌─────────────┐ │
│ │   Event     │ │    │ │   Service   │ │    │ │    JDBC     │ │
│ │  Handlers   │ │    │ │   Classes   │ │    │ │ Connection  │ │
│ └─────────────┘ │    │ └─────────────┘ │    │ └─────────────┘ │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

### **Database Schema**
```sql
-- Core Tables
users (user_id, username, password, email, profile_picture, birthday)
books (book_id, title, author, publisher, description, size, genre, pages, languages, price, cover_image, stock_count)

-- Relationships
- Users can place multiple orders
- Books have stock management
- Orders contain multiple book items
- Vouchers have expiration dates
```

### **Class Hierarchy**
```
BookHaven Application
├── Init.java (Entry Point)
├── Index.java (Authentication UI)
├── MainMenu.java (Main Application Window)
├── Models/
│   ├── User.java (User data model)
│   ├── Book.java (Book data model)
│   └── BookItem.java (Cart item model)
├── Services/
│   ├── DatabaseConnection.java (DB connectivity)
│   └── VoucherSystem.java (Discount management)
├── UI Components/
│   ├── CustomComboBox.java (Styled dropdown)
│   ├── CustomSpinner.java (Number input)
│   └── RoundedPanel.java (Custom panel)
└── Utilities/
    ├── Receipt.java (Print dialog)
    ├── Invoice.java (Receipt generation)
    └── Various Helper Classes
```

## 📁 Project Structure

```
bookhaven-ebookstore/
├── 📄 pom.xml                        # Maven project configuration
├── 📄 README.md                      # Project documentation
├── 📄 nbactions.xml                  # NetBeans IDE actions
├── 📁 lib/                           # External libraries
│   └── unknown/binary/AbsoluteLayout/ # NetBeans layout library
├── 📁 src/main/java/com/bookstore/casestudy/
│   ├── 📄 Init.java                  # Application entry point
│   ├── 📄 Index.java                 # Login/Registration window
│   ├── 📄 MainMenu.java             # Main application interface
│   ├── 📄 Splash.java               # Loading screen
│   ├── 📄 DatabaseConnection.java    # Database connectivity
│   ├── 📄 User.java                 # User data model
│   ├── 📄 Book.java                 # Book data model
│   ├── 📄 BookItem.java             # Shopping cart item
│   ├── 📄 VoucherSystem.java        # Discount system
│   ├── 📄 Receipt.java              # Receipt dialog
│   ├── 📄 Invoice.java              # Receipt printing
│   ├── 📄 InvoicePanel.java         # Receipt UI panel
│   ├── 📄 CustomComboBox.java       # Styled dropdown component
│   ├── 📄 CustomSpinner.java        # Custom number input
│   ├── 📄 CustomRadioButton.java    # Styled radio button
│   ├── 📄 RoundedPanel.java         # Custom panel with rounded corners
│   ├── 📄 TextPrompt.java           # Input field placeholder
│   ├── 📄 PasswordStrength.java     # Password validation
│   ├── 📄 FocusTraversalUtils.java  # Keyboard navigation
│   ├── 📄 ExitConfirmation.java     # Exit dialog
│   └── 📄 NoResult.java             # Search empty state
├── 📁 target/                        # Maven build output
│   ├── 📁 classes/                   # Compiled Java classes
│   └── 📁 maven-status/              # Build metadata
└── 📁 resources/                     # Application resources
    └── 📁 images/                    # UI icons and book covers
```

### **Key Components Explained**

- **`Init.java`**: Application bootstrap with splash screen and Windows Look & Feel
- **`Index.java`**: Authentication interface handling login and registration
- **`MainMenu.java`**: Primary application window with book browsing, cart, and user management
- **`DatabaseConnection.java`**: Simple helper for obtaining a JDBC connection (no pooling)
- **Model Classes**: Data structures for User, Book, and BookItem entities
- **Custom UI Components**: Enhanced Swing components with custom styling and behavior

## 🚀 Quick Start

### **Prerequisites**
- Java Development Kit (JDK) 11 or higher
- MySQL Server 8.0 or higher
- Apache Maven 3.6+
- NetBeans IDE (recommended) or any Java IDE

### **Installation**

1. **Clone the Repository**
   ```bash
   git clone https://github.com/elyeandre/bookhaven-Ebookstore.git
   cd bookhaven-ebookstore
   ```

2. **Database Setup**
   ```sql
   -- Create database
   CREATE DATABASE onlinebookstore;
   
   -- Create users table
   CREATE TABLE users (
       user_id INT AUTO_INCREMENT PRIMARY KEY,
       username VARCHAR(50) UNIQUE NOT NULL,
       password VARCHAR(255) NOT NULL,
       email VARCHAR(100) UNIQUE NOT NULL,
       profile_picture LONGBLOB,
       birthday DATE
   );
   
   -- Create books table
   CREATE TABLE books (
       book_id INT AUTO_INCREMENT PRIMARY KEY,
       title VARCHAR(255) NOT NULL,
       author VARCHAR(255) NOT NULL,
       publisher VARCHAR(255),
       description TEXT,
       size VARCHAR(50),
       genre VARCHAR(100),
       pages INT,
       languages VARCHAR(100),
       price DECIMAL(10,2) NOT NULL,
       cover_image LONGBLOB,
       stock_count INT DEFAULT 0
   );
   
   -- Insert sample book data
   INSERT INTO books (title, author, publisher, description, size, genre, pages, languages, price, stock_count) VALUES
   ('The Great Gatsby', 'F. Scott Fitzgerald', 'Scribner', 'A classic American novel', '5x8 inches', 'Fiction', 180, 'English', 15.99, 25),
   ('To Kill a Mockingbird', 'Harper Lee', 'J.B. Lippincott & Co.', 'A gripping tale of racial injustice', '5x8 inches', 'Fiction', 281, 'English', 18.99, 30),
   ('1984', 'George Orwell', 'Secker & Warburg', 'Dystopian social science fiction', '5x8 inches', 'Science Fiction', 328, 'English', 16.99, 20);
   ```

3. **Configure Database Connection**
   ```java
   // Update DatabaseConnection.java with your database credentials
   private static final String DB_URL = "jdbc:mysql://localhost:3306/onlinebookstore";
   private static final String USER = "your_username";
   private static final String PASS = "your_password";
   ```

4. **Build the Project**
   ```bash
   mvn clean compile
   ```

5. **Run the Application**
   ```bash
   mvn exec:java -Dexec.mainClass="com.bookstore.casestudy.Init"
   ```

### **Using NetBeans IDE**

1. **Open Project**
   - File → Open Project
   - Navigate to the bookhaven-ebookstore directory
   - Select the project folder

2. **Run Application**
   - Right-click on the project
   - Select "Run" or press F6
   - The application will start with the splash screen

## ⚙️ Configuration

### **Database Configuration**
The application uses MySQL for data persistence. Update the database connection settings in `DatabaseConnection.java`:

```java
public class DatabaseConnection {
    private static final String DB_URL = "jdbc:mysql://localhost:3306/onlinebookstore";
    private static final String DATABASE_DRIVER = "com.mysql.cj.jdbc.Driver";
    private static final String USER = "root";
    private static final String PASS = "";
    
    // Configure connection pooling and timeouts as needed
}
```

### **Voucher System Configuration**
Pre-configured vouchers can be set up in `MainMenu.java`:

```java
// Add vouchers during initialization
voucherSystem.addVoucher("WELCOME20", 20.0, LocalDate.of(2024, 12, 31));
voucherSystem.addVoucher("STUDENT10", 10.0, LocalDate.of(2024, 6, 30));
voucherSystem.addVoucher("NEWUSER50", 50.0, LocalDate.of(2024, 12, 31));
```

### **UI Theme Configuration**
The application uses Windows Look and Feel for native appearance:

```java
// In Init.java
UIManager.setLookAndFeel("com.sun.java.swing.plaf.windows.WindowsLookAndFeel");
```

## 📱 Usage Guide

### **User Registration & Authentication**

1. **Creating an Account**
   - Launch the application
   - Click "Sign Up" on the login screen
   - Fill in required information:
     - Username (must be unique)
     - Email address (Gmail validation)
     - Birthday (MM/dd/yyyy format)
     - Password and confirmation
   - Click "Sign Up" to create account

2. **Logging In**
   - Enter username and password
   - Click "Login" button
   - System validates credentials and opens main interface

3. **Profile Management**
   - Click user icon in main menu
   - Update personal information
   - Change password (requires current password)
   - Upload profile picture

### **Browsing and Shopping**

1. **Book Catalog**
   - Browse books in grid layout
   - View book covers, titles, authors, and prices
   - Use search functionality to find specific books
   - Click on books to view detailed information

2. **Adding to Cart**
   - Click "Add to Cart" on any book
   - Select book type (Paperback/Hardcover)
   - Adjust quantity using spinner controls
   - Monitor cart count in navigation

3. **Shopping Cart Management**
   - Navigate to Cart section
   - Review selected books and quantities
   - Modify quantities or remove items
   - Select books for checkout using radio buttons

4. **Checkout Process**
   - Click checkout button with selected items
   - Fill in delivery information:
     - Full name (First, Middle, Last)
     - Complete address details
     - Mobile number
   - Select payment method
   - Apply voucher codes for discounts
   - Review order summary and totals

5. **Order Completion**
   - Confirm order details
   - Generate and print receipt
   - Receipt includes:
     - Order items and quantities
     - Pricing breakdown
     - Voucher discounts
     - Payment method
     - Customer information

### **Voucher System**

1. **Available Vouchers**
   - "ELYEANDRE": ₱100 discount
   - "Hello": ₱150 discount  
   - "ELYEANDRE123": ₱5000 discount

2. **Applying Vouchers**
   - Enter voucher code in checkout
   - System validates code and expiration
   - Discount automatically applied to total
   - Voucher details shown in receipt

### **Search and Navigation**

1. **Book Search**
   - Use search bar in main interface
   - Search by title, author, or genre
   - Results update in real-time
   - No results message when applicable

2. **Menu Navigation**
   - Browse: Book catalog (default view)
   - Cart: Shopping cart management
   - User: Profile and account settings
   - Message: FAQ and support information
   - Logout: End session and return to login

## :lock: Security Notes

This is an academic prototype; security hardening is minimal.

### Current State
- Plaintext password storage (no hashing or salting)
- Basic duplicate + format validation only
- Mixed use of prepared statements (needs full audit for injection safety)
- No role-based access or authorization layers
- Single-user in-memory "session"; no token or timeout mechanism

### Recommended Improvements (Not Implemented Yet)
- Hash passwords with bcrypt/Argon2
- Centralize input validation & sanitize all user-provided strings
- Introduce DAO/data layer with consistent prepared statements
- Add transaction handling for multi-step operations
- Implement proper session management and logout invalidation
- Add logging & audit trails for auth events


## 🚀 Deployment

### **Desktop Application Deployment**

#### **JAR Package Creation**
```bash
# Create executable JAR with dependencies
mvn clean compile assembly:single

# The JAR file will be created in target/ directory
# Run with: java -jar target/bookhaven-ebookstore-jar-with-dependencies.jar
```

#### **Windows Executable (Optional)**
```bash
# Using jpackage (Java 14+)
jpackage --input target/ \
         --name "BookHaven" \
         --main-jar bookhaven-ebookstore.jar \
         --main-class com.bookstore.casestudy.Init \
         --type exe \
         --icon src/main/resources/icon.ico
```

### **Database Deployment**

#### **Production Database Setup**

Preferred (phpMyAdmin on XAMPP):
1. Start MySQL in XAMPP.
2. Open phpMyAdmin → Create database `onlinebookstore` (utf8mb4_unicode_ci).
3. Select the database → Import → Choose file: `database/onlinebookstore.sql` → Go.

CLI alternative:
```bash
# Create DB and user (optional but recommended for production)
mysql -u root -p -e "CREATE DATABASE IF NOT EXISTS onlinebookstore CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;"
mysql -u root -p -e "CREATE USER IF NOT EXISTS 'bookstore_app'@'localhost' IDENTIFIED BY 'secure_password';"
mysql -u root -p -e "GRANT SELECT, INSERT, UPDATE, DELETE ON onlinebookstore.* TO 'bookstore_app'@'localhost'; FLUSH PRIVILEGES;"

# Import the provided dump that includes schema + data
mysql -u bookstore_app -p onlinebookstore < database/onlinebookstore.sql
```

#### **Configuration for Production**
```java
// Update DatabaseConnection.java for production
private static final String DB_URL = "jdbc:mysql://production-server:3306/onlinebookstore";
private static final String USER = "bookstore_app";
private static final String PASS = System.getenv("DB_PASSWORD"); // Use environment variable
```

### **Installation Package**

#### **Create Installation Directory Structure**
```
BookHaven-Installer/
├── bookhaven.jar
├── lib/
│   └── mysql-connector-java-8.0.33.jar
├── config/
│   └── database.properties
├── resources/
│   └── images/
├── README.txt
└── install.bat (Windows) / install.sh (Linux)
```

#### **Installation Script (Windows)**
```batch
@echo off
echo Installing BookHaven Bookstore...

REM Create application directory
mkdir "C:\Program Files\BookHaven"

REM Copy application files
copy bookhaven.jar "C:\Program Files\BookHaven\"
xcopy lib "C:\Program Files\BookHaven\lib\" /E /I
xcopy resources "C:\Program Files\BookHaven\resources\" /E /I

REM Create desktop shortcut
echo Creating desktop shortcut...
REM Add shortcut creation commands here

echo Installation complete!
pause
```

### **System Requirements**

#### **Minimum Requirements**
- **Operating System**: Windows 7+ / macOS 10.12+ / Linux
- **Java Runtime**: JRE 11 or higher
- **Memory**: 512 MB RAM minimum, 1 GB recommended
- **Storage**: 50 MB free disk space
- **Database**: MySQL 5.7+ or MariaDB 10.2+

#### **Recommended Requirements**
- **Java Runtime**: JRE 17 (LTS version)
- **Memory**: 2 GB RAM or higher
- **Storage**: 200 MB free disk space
- **Database**: MySQL 8.0+ with InnoDB engine
- **Display**: 1024x768 minimum resolution

## 🤝 Contributing

We welcome contributions to improve BookHaven! Here's how you can help:

### **Getting Started**

1. **Fork the Repository**
   ```bash
   # Click the "Fork" button on GitHub
   git clone https://github.com/elyeandre/bookhaven-Ebookstore.git
   cd bookhaven-ebookstore
   ```

2. **Set Up Development Environment**
   ```bash
   # Install dependencies
   mvn clean install
   
   # Set up database (see Quick Start section)
   # Configure your IDE (NetBeans recommended)
   ```

3. **Create Feature Branch**
   ```bash
   git checkout -b feature/your-feature-name
   # or
   git checkout -b bugfix/issue-description
   ```

### **Development Guidelines**

#### **Code Style**
- Follow Java naming conventions (PascalCase for classes, camelCase for methods)
- Use meaningful variable and method names
- Add JavaDoc comments for public methods and classes
- Maintain consistent indentation and formatting
- Keep methods focused and reasonably sized

#### **Database Changes**
- Create migration scripts for schema changes
- Test with sample data
- Document any new table structures
- Ensure backward compatibility when possible

#### **UI Development**
- Use NetBeans GUI Builder for consistency
- Follow existing color scheme and styling
- Ensure responsive behavior
- Test across different screen resolutions
- Maintain accessibility standards

### **Contribution Types**

#### **🐛 Bug Fixes**
- Fix authentication issues
- Resolve cart calculation problems
- Address UI/UX inconsistencies
- Database connection improvements

#### **✨ New Features**
- Enhanced search functionality
- Additional payment methods
- User rating and review system
- Book recommendation engine
- Advanced inventory management

#### **📚 Documentation**
- Improve code documentation
- Create user guides and tutorials
- API documentation
- Setup and deployment guides

#### **🧪 Testing**
- Unit tests for business logic
- Integration tests for database operations
- UI automation tests
- Performance testing scenarios

### **Pull Request Process**

1. **Before Submitting**
   - [ ] Test your changes thoroughly
   - [ ] Update documentation if needed
   - [ ] Ensure code follows style guidelines
   - [ ] Add appropriate comments

2. **PR Description Template**
   ```markdown
   ## Description
   Brief description of changes made

   ## Type of Change
   - [ ] Bug fix (non-breaking change)
   - [ ] New feature (non-breaking change)
   - [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
   - [ ] Documentation update

   ## Testing
   - [ ] Tested locally
   - [ ] Database changes tested
   - [ ] UI changes verified

   ## Screenshots (if applicable)
   Add screenshots for UI changes
   ```

### **Code Review Guidelines**
- Reviews required for all pull requests
- Focus on code quality, security, and maintainability
- Provide constructive feedback
- Test changes locally when possible

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

### **MIT License Summary**
- ✅ Commercial use allowed
- ✅ Modification allowed
- ✅ Distribution allowed
- ✅ Private use allowed
- ❌ No liability
- ❌ No warranty
- ❗ License and copyright notice required

```
Copyright (c) 2024 BookHaven Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## :camera_flash: Screenshots

> Disclaimer: Screens reflect an academic prototype; features like order history, payment gateway integration, and secure password handling are not implemented.

### Main Application Interface
![Main Menu](https://github.com/user-attachments/assets/caef18c2-0500-4815-b995-88810cebd237)
*Main application window showing book catalog with search functionality*

### User Authentication
![Login Screen](https://github.com/user-attachments/assets/7d5fd3da-d616-43bf-ac0f-b456d068a465)
*Secure login interface with user registration option*

### Shopping Cart Management
![Shopping Cart](https://github.com/user-attachments/assets/b000c863-7a3b-462f-8bc7-42474829d749)
*Interactive shopping cart with quantity controls and selection*

### Checkout Process
![Checkout](https://github.com/user-attachments/assets/09093a4b-23e8-4360-aaaa-47ced5eb5fbb)
*Comprehensive checkout with customer information and payment options*

### User Profile Management
![User Profile](https://github.com/user-attachments/assets/b573702c-c844-44be-bd83-b6ade7d853a0)
*User account management with profile picture and password update*

### Book Details View
![Book Details](https://github.com/user-attachments/assets/fca2b4ce-97da-4cda-a9d4-1df6a8c47546)
*Detailed book information display with purchase options*

### Search Results
![Search Feature](https://github.com/user-attachments/assets/8b1b094c-aef0-4cdb-9197-95273de60f71)
*Advanced search functionality with real-time filtering*

---

**📚 Built with ❤️ for Book Lovers Everywhere**

*"Connecting readers with their next great adventure through technology"*

---

[made-with-java]: https://img.shields.io/badge/Made%20with-Java-orange.svg?style=for-the-badge
[built-with-love]: https://img.shields.io/badge/Built%20with-❤️-red.svg?style=for-the-badge
[forthebadge-url]: http://forthebadge.com
[contributors-shield]: https://img.shields.io/github/contributors/elyeandre/bookhaven-Ebookstore.svg?style=for-the-badge
[contributors-url]: https://github.com/elyeandre/bookhaven-Ebookstore/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/elyeandre/bookhaven-Ebookstore.svg?style=for-the-badge
[forks-url]: https://github.com/elyeandre/bookhaven-Ebookstore/network/members
[stars-shield]: https://img.shields.io/github/stars/elyeandre/bookhaven-Ebookstore.svg?style=for-the-badge
[stars-url]: https://github.com/elyeandre/bookhaven-Ebookstore/stargazers
[issues-shield]: https://img.shields.io/github/issues/elyeandre/bookhaven-Ebookstore.svg?style=for-the-badge
[issues-issues-url]: https://github.com/elyeandre/bookhaven-Ebookstore/issues

*Last updated: September 23, 2025*

