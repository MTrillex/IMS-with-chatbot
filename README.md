# Inventory Management System (IMS)

A comprehensive full-stack inventory management system with AI-powered chatbot integration. Built with React frontend, Spring Boot backend, and integrated with Helper-AI for intelligent document Q&A capabilities.

---

## Table of Contents

1. [Overview](#overview)
2. [System Architecture](#system-architecture)
3. [Technology Stack](#technology-stack)
4. [Project Structure](#project-structure)
5. [Backend (InventoryMS)](#backend-inventoryms)
   - [Models](#models)
   - [Controllers](#controllers)
   - [Services](#services)
   - [Security](#security)
   - [Chatbot Integration](#chatbot-integration)
   - [API Endpoints](#api-endpoints)
6. [Frontend (ims-react)](#frontend-ims-react)
   - [Pages](#pages)
   - [Components](#components)
   - [Services](#services-1)
   - [Routing](#routing)
7. [Helper-AI Integration](#helper-ai-integration)
8. [Installation & Setup](#installation--setup)
9. [Configuration](#configuration)
10. [Usage Guide](#usage-guide)

---

## Overview

The Inventory Management System (IMS) is a complete solution for managing products, suppliers, transactions, and users. It features:

- **Product Management**: CRUD operations for products with categories and images
- **Supplier Management**: Track and manage supplier information
- **Transaction Processing**: Handle purchases, sales, and returns
- **User Management**: Role-based access control (Admin, Manager, User)
- **Dashboard Analytics**: Visual charts showing transaction trends
- **AI Chatbot**: Intelligent Q&A powered by Helper-AI with document knowledge

---

## System Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        Inventory Management System                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                               │
│  ┌─────────────────────────────────────────────────────────────────────────┐ │
│  │                          Frontend (ims-react)                            │ │
│  │                              Port: 3000                                  │ │
│  ├─────────────────────────────────────────────────────────────────────────┤ │
│  │                                                                          │ │
│  │  ┌──────────────┐ ┌──────────────┐ ┌──────────────┐ ┌────────────────┐  │ │
│  │  │  Dashboard   │ │   Products   │ │ Transactions │ │    Chatbot     │  │ │
│  │  │    Page      │ │    Page      │ │    Page      │ │    Widget      │  │ │
│  │  └──────────────┘ └──────────────┘ └──────────────┘ └────────────────┘  │ │
│  │                                                                          │ │
│  │  ┌──────────────────────────────────────────────────────────────────┐   │ │
│  │  │                    Services Layer (Axios)                         │   │ │
│  │  │     ApiService.js    │    ChatbotService.js    │    Guard.js      │   │ │
│  │  └──────────────────────────────────────────────────────────────────┘   │ │
│  │                                                                          │ │
│  └─────────────────────────────────────────────────────────────────────────┘ │
│                                      │                                        │
│                                      ▼                                        │
│  ┌─────────────────────────────────────────────────────────────────────────┐ │
│  │                       Backend (InventoryMS)                              │ │
│  │                           Port: 5050                                     │ │
│  ├─────────────────────────────────────────────────────────────────────────┤ │
│  │                                                                          │ │
│  │  ┌─────────────────────────────────────────────────────────────────┐    │ │
│  │  │                      REST Controllers                           │    │ │
│  │  │  Auth │ Product │ Category │ Supplier │ Transaction │ Chatbot  │    │ │
│  │  └─────────────────────────────────────────────────────────────────┘    │ │
│  │                                │                                         │ │
│  │  ┌─────────────────────────────────────────────────────────────────┐    │ │
│  │  │                      Service Layer                               │    │ │
│  │  │  UserService │ ProductService │ TransactionService │ etc.       │    │ │
│  │  └─────────────────────────────────────────────────────────────────┘    │ │
│  │                                │                                         │ │
│  │  ┌─────────────────────────────────────────────────────────────────┐    │ │
│  │  │                    Spring Security + JWT                         │    │ │
│  │  └─────────────────────────────────────────────────────────────────┘    │ │
│  │                                │                                         │ │
│  │  ┌─────────────────────────────────────────────────────────────────┐    │ │
│  │  │                    JPA Repositories                              │    │ │
│  │  └─────────────────────────────────────────────────────────────────┘    │ │
│  │                                │                                         │ │
│  └────────────────────────────────┼─────────────────────────────────────────┘ │
│                                   │                                           │
│         ┌─────────────────────────┼──────────────────────────┐               │
│         │                         │                          │               │
│         ▼                         ▼                          ▼               │
│  ┌─────────────┐          ┌─────────────┐          ┌──────────────────┐     │
│  │   MySQL     │          │  File       │          │    Helper-AI     │     │
│  │  Database   │          │  Storage    │          │   Flask API      │     │
│  │  Port: 3306 │          │  (images)   │          │   Port: 5001     │     │
│  └─────────────┘          └─────────────┘          └──────────────────┘     │
│                                                                               │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Technology Stack

### Backend (InventoryMS)
| Component | Technology | Version |
|-----------|------------|---------|
| **Framework** | Spring Boot | 3.5.3 |
| **Language** | Java | 17 |
| **Database** | MySQL | 8.x |
| **ORM** | Spring Data JPA | - |
| **Security** | Spring Security + JWT | jjwt 0.12.6 |
| **Build Tool** | Maven | - |
| **Reactive** | Spring WebFlux | - |
| **Validation** | Jakarta Validation | - |

### Frontend (ims-react)
| Component | Technology | Version |
|-----------|------------|---------|
| **Framework** | React | 19.1.0 |
| **Router** | React Router DOM | 7.6.3 |
| **HTTP Client** | Axios | 1.9.0 |
| **Charts** | Recharts | 2.15.3 |
| **Encryption** | CryptoJS | 4.2.0 |
| **Build Tool** | React Scripts | 5.0.1 |

### AI Integration (Helper-AI)
| Component | Technology |
|-----------|------------|
| **Framework** | Flask + LangChain |
| **LLM** | OpenAI GPT-4o-mini |
| **Vector DB** | Pinecone |
| **Embeddings** | HuggingFace |

---

## Project Structure

### Root Structure
```
├── InventoryMS/                 # Spring Boot Backend
│   └── InventoryMS/
│       ├── pom.xml
│       ├── src/main/java/...
│       └── src/main/resources/
│
├── ims-react/                   # React Frontend
│   ├── package.json
│   ├── public/
│   └── src/
│       ├── component/
│       ├── pages/
│       └── service/
│
└── Helper-AI/                   # AI Chatbot Service
    ├── api.py
    ├── app.py
    └── core/
```

---

## Backend (InventoryMS)

### Models

The backend uses JPA entities for data persistence:

#### User
```java
@Entity
@Table(name = "users")
public class User {
    Long id;
    String name;
    String email;           // Unique
    String password;
    String phoneNumber;
    UserRole role;          // ADMIN, MANAGER, USER
    List<Transaction> transactions;
    LocalDateTime createdAt;
}
```

#### Product
```java
@Entity
@Table(name = "products")
public class Product {
    Long id;
    String name;
    String sku;             // Unique
    BigDecimal price;
    Integer stockQuantity;
    String description;
    LocalDate expiryDate;
    String imageUrl;
    Category category;      // ManyToOne
    LocalDateTime createdAt;
    LocalDateTime updatedAt;
}
```

#### Category
```java
@Entity
@Table(name = "categories")
public class Category {
    Long id;
    String name;
    List<Product> products; // OneToMany
}
```

#### Supplier
```java
@Entity
@Table(name = "suppliers")
public class Supplier {
    Long id;
    String name;
    String contactInfo;
    String address;
}
```

#### Transaction
```java
@Entity
@Table(name = "transactions")
public class Transaction {
    Long id;
    Integer totalProducts;
    BigDecimal totalPrice;
    TransactionType transactionType; // PURCHASE, SALE, RETURN
    TransactionStatus status;         // PENDING, PROCESSING, COMPLETED, CANCELLED
    Product product;        // ManyToOne
    User user;              // ManyToOne
    Supplier supplier;      // ManyToOne (for purchases/returns)
    String description;
    String note;
    LocalDateTime createdAt;
    LocalDateTime updatedAt;
}
```

### Enums

```java
public enum UserRole {
    ADMIN, MANAGER, USER
}

public enum TransactionType {
    PURCHASE, SALE, RETURN
}

public enum TransactionStatus {
    PENDING, PROCESSING, COMPLETED, CANCELLED
}
```

### Controllers

#### AuthController (`/api/auth`)
| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| POST | `/register` | Register new user | Public |
| POST | `/login` | User login, returns JWT | Public |

#### ProductController (`/api/products`)
| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| POST | `/add` | Add new product | ADMIN |
| PUT | `/update` | Update product | ADMIN |
| GET | `/all` | Get all products | ADMIN |
| GET | `/for-transaction` | Get products for transaction | ADMIN, MANAGER |
| GET | `/{id}` | Get product by ID | All |
| DELETE | `/delete/{id}` | Delete product | ADMIN |
| GET | `/search?input=` | Search products | All |

#### CategoryController (`/api/categories`)
| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| POST | `/add` | Create category | ADMIN |
| GET | `/all` | Get all categories | ADMIN |
| GET | `/{id}` | Get category by ID | All |
| PUT | `/update/{id}` | Update category | ADMIN |
| DELETE | `/delete/{id}` | Delete category | ADMIN |

#### SupplierController (`/api/suppliers`)
| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| POST | `/add` | Add supplier | ADMIN |
| GET | `/all` | Get all suppliers | ADMIN |
| GET | `/for-transaction` | Get suppliers for transaction | ADMIN, MANAGER |
| GET | `/{id}` | Get supplier by ID | All |
| PUT | `/update/{id}` | Update supplier | ADMIN |
| DELETE | `/delete/{id}` | Delete supplier | ADMIN |

#### TransactionController (`/api/transactions`)
| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| POST | `/purchase` | Create purchase transaction | Authenticated |
| POST | `/sell` | Create sale transaction | Authenticated |
| POST | `/return` | Create return transaction | Authenticated |
| GET | `/all` | Get all transactions (paginated) | Authenticated |
| GET | `/{id}` | Get transaction by ID | Authenticated |
| GET | `/by-month-year` | Get transactions by month/year | Authenticated |
| PUT | `/{transactionId}` | Update transaction status | Authenticated |

#### UserController (`/api/users`)
| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| GET | `/all` | Get all users | ADMIN |
| GET | `/{id}` | Get user by ID | Authenticated |
| PUT | `/update/{id}` | Update user | Authenticated |
| DELETE | `/delete/{id}` | Delete user | ADMIN |
| GET | `/transactions/{userId}` | Get user's transactions | Authenticated |
| GET | `/current` | Get current logged-in user | Authenticated |

#### ChatbotController (`/api/chatbot`)
| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| POST | `/ask` | Send message to chatbot | Authenticated |
| GET | `/status` | Get chatbot connection status | Authenticated |
| POST | `/connect` | Connect to Pinecone index | Authenticated |
| POST | `/clear` | Clear conversation history | Authenticated |
| GET | `/health` | Check Helper-AI health | Public |
| POST | `/toggle-internet-fallback` | Toggle internet search | Authenticated |

### Services

Each entity has a corresponding service interface and implementation:

| Service | Implementation | Description |
|---------|----------------|-------------|
| `UserService` | `UserServiceImpl` | User CRUD, authentication, JWT generation |
| `ProductService` | `ProductServiceImpl` | Product CRUD, image handling, search |
| `CategoryService` | `CategoryServiceImpl` | Category CRUD operations |
| `SupplierService` | `SupplierServiceImpl` | Supplier CRUD operations |
| `TransactionService` | `TransactionServiceImpl` | Transaction processing, stock updates |

### Security

#### JWT Authentication
The system uses JWT (JSON Web Token) for stateless authentication:

**JwtUtils.java:**
- Token generation with email as subject
- Token validation against UserDetails
- Expiration: 100 days
- Algorithm: HmacSHA256

**Security Flow:**
1. User logs in via `/api/auth/login`
2. Server validates credentials and returns JWT
3. Client stores JWT (encrypted with CryptoJS)
4. Client sends JWT in `Authorization: Bearer <token>` header
5. `AuthFilter` validates token on each request
6. Role-based access control via `@PreAuthorize` annotations

**Security Configuration:**
- CORS enabled for all origins
- CSRF disabled (stateless API)
- Public endpoints: `/api/auth/**`, `/api/chatbot/health`
- All other endpoints require authentication

### Chatbot Integration

The backend integrates with Helper-AI through reactive WebClient:

**ChatbotApiService.java:**
```java
@Service
public class ChatbotApiService {
    private final WebClient webClient;
    
    // Configured with 45-second timeout for chat requests
    // 10-second timeout for other operations
    
    public Mono<Map> askQuestion(String message, boolean useInternetFallback);
    public Mono<Map> getStatus();
    public Mono<Map> connectToIndex(String indexName, String namespace);
    public Mono<Map> clearConversation();
    public Mono<Map> checkHealth();
    public Mono<Map> toggleInternetFallback(boolean enabled);
}
```

**Configuration (application.properties):**
```properties
chatbot.api.base-url=http://localhost:5001/api
chatbot.api.timeout.chat=45000
chatbot.api.timeout.connect=10000
chatbot.api.timeout.status=5000
```

### API Endpoints

#### DTOs (Data Transfer Objects)

**LoginRequest:**
```json
{ "email": "string", "password": "string" }
```

**RegisterRequest:**
```json
{
  "name": "string",
  "email": "string",
  "password": "string",
  "phoneNumber": "string",
  "role": "ADMIN|MANAGER|USER"
}
```

**ProductDTO:**
```json
{
  "productId": "number",
  "name": "string",
  "sku": "string",
  "price": "decimal",
  "stockQuantity": "number",
  "categoryId": "number",
  "description": "string"
}
```

**TransactionRequest:**
```json
{
  "productId": "number",
  "quantity": "number",
  "supplierId": "number",
  "description": "string",
  "note": "string"
}
```

**Response (Standard):**
```json
{
  "status": 200,
  "message": "string",
  "token": "string (for auth)",
  "role": "string (for auth)",
  "expirationTime": "string (for auth)",
  "user": { },
  "users": [ ],
  "product": { },
  "products": [ ],
  "category": { },
  "categories": [ ],
  "supplier": { },
  "suppliers": [ ],
  "transaction": { },
  "transactions": [ ],
  "totalPages": "number"
}
```

---

## Frontend (ims-react)

### Pages

| Page | File | Description |
|------|------|-------------|
| **Dashboard** | `DashboardPage.jsx` | Transaction charts with Recharts (Line chart showing count/quantity/amount by day) |
| **Login** | `LoginPage.jsx` | User authentication form |
| **Register** | `RegisterPage.jsx` | New user registration form |
| **Products** | `ProductPage.jsx` | Product listing with search, delete |
| **Add/Edit Product** | `AddEditProductPage.jsx` | Product form with image upload |
| **Categories** | `CategoryPage.jsx` | Category management |
| **Suppliers** | `SupplierPage.jsx` | Supplier listing |
| **Add/Edit Supplier** | `AddEditSupplierPage.jsx` | Supplier form |
| **Transactions** | `TransactionsPage.jsx` | Transaction listing with pagination |
| **Transaction Details** | `TransactionDetailsPage.jsx` | Single transaction view |
| **Purchase** | `PurchasePage.jsx` | Create purchase transaction |
| **Sell** | `SellPage.jsx` | Create sale transaction |
| **Profile** | `ProfilePage.jsx` | User profile with transaction history |

### Components

#### Layout (`Layout.jsx`)
Wraps all pages with consistent structure:
- Sidebar navigation
- Chatbot widget
- Main content area

#### Sidebar (`Sidebar.jsx`)
Navigation menu with:
- Dashboard link
- Category (Admin only)
- Products (Admin only)
- Suppliers (Admin only)
- Transactions
- Purchase (Admin/Manager)
- Sell (Admin/Manager)
- Profile
- Logout

#### ChatbotWidget (`ChatbotWidget.jsx`)
AI-powered chat interface:
- Floating chat button
- Expandable chat window
- Message history display
- Loading indicators
- Internet search toggle
- Clear conversation button
- Auto-scroll to latest message

Features:
```jsx
const ChatbotWidget = () => {
  const [messages, setMessages] = useState([]);
  const [inputMessage, setInputMessage] = useState('');
  const [isOpen, setIsOpen] = useState(false);
  const [isLoading, setIsLoading] = useState(false);
  const [isConnected, setIsConnected] = useState(false);
  const [useInternetFallback, setUseInternetFallback] = useState(true);
  
  // Handles: sending messages, checking status, clearing history
  // Displays: bot/user messages, sources, internet search indicator
};
```

#### PaginationComponent (`PaginationComponent.jsx`)
Reusable pagination for tables.

### Services

#### ApiService (`ApiService.js`)
Central API communication service with 365+ lines of functionality:

**Authentication Methods:**
```javascript
static registerUser(registration)      // POST /auth/register
static loginUser(loginDetails)         // POST /auth/login
static isAuthenticated()               // Check if token exists
static isAdmin()                       // Check if user is ADMIN
static isAdminOrManager()              // Check if ADMIN or MANAGER
static logout()                        // Clear stored credentials
```

**Token Management:**
```javascript
static saveToken(token)                // Encrypt and store token
static getToken()                      // Decrypt and retrieve token
static saveRole(role)                  // Encrypt and store role
static getRole()                       // Decrypt and retrieve role
```

**Product Methods:**
```javascript
static saveProduct(formData)           // POST /products/add (multipart)
static updateProduct(formData)         // PUT /products/update (multipart)
static getAllProducts()                // GET /products/all
static getProductById(id)              // GET /products/{id}
static deleteProduct(id)               // DELETE /products/delete/{id}
static searchProduct(input)            // GET /products/search?input=
```

**Category Methods:**
```javascript
static createCategory(body)            // POST /categories/add
static getAllCategory()                // GET /categories/all
static getCategoryById(id)             // GET /categories/{id}
static updateCategory(id, body)        // PUT /categories/update/{id}
static deleteCategory(id)              // DELETE /categories/delete/{id}
```

**Supplier Methods:**
```javascript
static addSupplier(body)               // POST /suppliers/add
static getAllSuppliers()               // GET /suppliers/all
static getSupplierById(id)             // GET /suppliers/{id}
static updateSupplier(id, body)        // PUT /suppliers/update/{id}
static deleteSupplier(id)              // DELETE /suppliers/delete/{id}
```

**Transaction Methods:**
```javascript
static purchase(body)                  // POST /transactions/purchase
static sell(body)                      // POST /transactions/sell
static returnToSupplier(body)          // POST /transactions/return
static getAllTransactions(page, size, search)  // GET /transactions/all
static getTransactionById(id)          // GET /transactions/{id}
static getTransactionsByMonthYear(m, y) // GET /transactions/by-month-year
static updateTransactionStatus(id, status) // PUT /transactions/{id}
```

**User Methods:**
```javascript
static getAllUsers()                   // GET /users/all
static getUserById(id)                 // GET /users/{id}
static updateUser(id, body)            // PUT /users/update/{id}
static deleteUser(id)                  // DELETE /users/delete/{id}
static getUserTransactions(userId)     // GET /users/transactions/{userId}
static getCurrentUser()                // GET /users/current
```

#### ChatbotService (`ChatbotService.js`)
Dedicated service for chatbot API calls:

```javascript
static async sendMessage(message, useInternetFallback)  // POST /chatbot/ask
static async getStatus()                                 // GET /chatbot/status
static async connectToIndex(indexName, namespace)        // POST /chatbot/connect
static async clearConversation()                         // POST /chatbot/clear
static async checkHealth()                               // GET /chatbot/health
static async toggleInternetFallback(enabled)             // POST /chatbot/toggle-internet-fallback
```

#### Guard (`Guard.js`)
Route protection components:

```javascript
export const ProtectedRoute = ({ children }) => {
  // Redirects to /login if not authenticated
  return ApiService.isAuthenticated() ? children : <Navigate to="/login" />;
};

export const AdminRoute = ({ children }) => {
  // Redirects to /profile if not ADMIN
  return ApiService.isAdmin() ? children : <Navigate to="/profile" />;
};
```

### Routing

**App.js Route Configuration:**
```jsx
<Routes>
  {/* Public Routes */}
  <Route path="/login" element={<LoginPage />} />
  <Route path="/register" element={<RegisterPage />} />
  
  {/* Protected Routes (Authenticated Users) */}
  <Route path="/" element={<ProtectedRoute><DashboardPage /></ProtectedRoute>} />
  <Route path="/profile" element={<ProtectedRoute><ProfilePage /></ProtectedRoute>} />
  <Route path="/transactions" element={<ProtectedRoute><TransactionsPage /></ProtectedRoute>} />
  <Route path="/transaction/:transactionId" element={<ProtectedRoute><TransactionDetailsPage /></ProtectedRoute>} />
  
  {/* Admin-Only Routes */}
  <Route path="/category" element={<AdminRoute><CategoryPage /></AdminRoute>} />
  <Route path="/products" element={<AdminRoute><ProductPage /></AdminRoute>} />
  <Route path="/add-product" element={<AdminRoute><AddEditProductPage /></AdminRoute>} />
  <Route path="/edit-product/:productId" element={<AdminRoute><AddEditProductPage /></AdminRoute>} />
  <Route path="/suppliers" element={<AdminRoute><SupplierPage /></AdminRoute>} />
  <Route path="/add-supplier" element={<AdminRoute><AddEditSupplierPage /></AdminRoute>} />
  <Route path="/edit-supplier/:supplierId" element={<AdminRoute><AddEditSupplierPage /></AdminRoute>} />
  
  {/* Admin or Manager Routes */}
  <Route path="/purchase" element={<ProtectedRoute><PurchasePage /></ProtectedRoute>} />
  <Route path="/sell" element={<ProtectedRoute><SellPage /></ProtectedRoute>} />
</Routes>
```

---

## Helper-AI Integration

### How It Works

The IMS uses Helper-AI as an intelligent chatbot for document Q&A. The integration flow:

```
┌─────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  React UI   │───▶│  Spring Boot    │───▶│   Helper-AI     │
│  Chatbot    │    │  ChatbotController│    │   Flask API     │
│  Widget     │◀───│  ChatbotApiService│◀───│   Port 5001     │
└─────────────┘    └─────────────────┘    └─────────────────┘
```

### Integration Points

1. **ChatbotWidget.jsx** (Frontend)
   - Provides chat UI
   - Calls ChatbotService methods
   - Displays messages and sources

2. **ChatbotService.js** (Frontend)
   - HTTP client for chatbot endpoints
   - Handles authentication headers

3. **ChatbotController.java** (Backend)
   - REST endpoints for chatbot operations
   - Proxies requests to Helper-AI

4. **ChatbotApiService.java** (Backend)
   - WebClient for reactive HTTP calls
   - Configurable timeouts
   - Error handling

### Configuration

**Backend (application.properties):**
```properties
# Helper-AI Connection
chatbot.api.base-url=http://localhost:5001/api
chatbot.api.timeout.chat=45000
chatbot.api.timeout.connect=10000
chatbot.api.timeout.status=5000
```

**Frontend (ChatbotService.js):**
```javascript
const BASE_URL = "http://localhost:5050/api/chatbot";
```

### Features Available Through Integration

- **Document Q&A**: Ask questions about uploaded documents
- **Internet Fallback**: Search the web when document knowledge is insufficient
- **Conversation Memory**: Maintain context across messages
- **Source Citations**: See which documents provided the answer
- **Connection Status**: Check if Helper-AI is available
- **Clear History**: Reset conversation context

---

## Installation & Setup

### Prerequisites

- **Java 17** or higher
- **Node.js 18** or higher
- **MySQL 8.x**
- **Python 3.8+** (for Helper-AI)
- **Maven** (for backend build)

### Step 1: Database Setup

```sql
CREATE DATABASE inventory_db;
CREATE USER 'root'@'localhost' IDENTIFIED BY 'samos';
GRANT ALL PRIVILEGES ON inventory_db.* TO 'root'@'localhost';
FLUSH PRIVILEGES;
```

### Step 2: Backend Setup (InventoryMS)

```bash
cd InventoryMS/InventoryMS

# Build the project
./mvnw clean install

# Run the application
./mvnw spring-boot:run
```

The backend will start on `http://localhost:5050`

### Step 3: Frontend Setup (ims-react)

```bash
cd ims-react

# Install dependencies
npm install

# Start development server
npm start
```

The frontend will start on `http://localhost:3000`

### Step 4: Helper-AI Setup (Optional)

```bash
cd Helper-AI

# Create virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Set environment variables
export OPENAI_API_KEY=your_key
export PINECONE_API_KEY=your_key
export TAVILY_API_KEY=your_key  # Optional

# Run the API
python api.py
```

Helper-AI will start on `http://localhost:5001`

---

## Configuration

### Backend Configuration

**InventoryMS/InventoryMS/src/main/resources/application.properties:**
```properties
# Server
server.port=5050

# Database
spring.datasource.url=jdbc:mysql://localhost:3306/inventory_db
spring.datasource.username=root
spring.datasource.password=samos
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=false

# File Upload
spring.servlet.multipart.max-file-size=50MB
spring.servlet.multipart.max-request-size=50MB

# Image Storage
product.image.directory=product-images

# Chatbot
chatbot.api.base-url=http://localhost:5001/api
chatbot.api.timeout.chat=45000
chatbot.api.timeout.connect=10000
chatbot.api.timeout.status=5000
```

### Frontend Configuration

**ims-react/src/service/ApiService.js:**
```javascript
const BASE_URL = "http://localhost:5050";
const SECRET_KEY = "ims-secret-key-2024";
```

**ims-react/src/service/ChatbotService.js:**
```javascript
const BASE_URL = "http://localhost:5050/api/chatbot";
```

---

## Usage Guide

### Default User Roles

| Role | Capabilities |
|------|--------------|
| **ADMIN** | Full access to all features |
| **MANAGER** | Can process transactions, view products |
| **USER** | Can view transactions and profile |

### Common Workflows

#### 1. Add a New Product (Admin)
1. Login as Admin
2. Navigate to Products → Add Product
3. Fill in product details and upload image
4. Select category
5. Click Save

#### 2. Process a Sale (Admin/Manager)
1. Login as Admin or Manager
2. Navigate to Sell
3. Select product and quantity
4. Add description and notes
5. Submit transaction

#### 3. Use the Chatbot
1. Click the chat icon in the bottom-right corner
2. Type a question about your documents
3. View the response and sources
4. Toggle internet fallback for web search
5. Click "Clear" to start fresh

#### 4. View Analytics (Dashboard)
1. Login to the system
2. Go to Dashboard
3. Select month and year
4. Toggle between Count/Quantity/Amount views
5. View the line chart for transaction trends

---

## Dependencies

### Backend (pom.xml)
```xml
<dependencies>
    <dependency>spring-boot-starter-web</dependency>
    <dependency>spring-boot-starter-data-jpa</dependency>
    <dependency>spring-boot-starter-security</dependency>
    <dependency>spring-boot-starter-validation</dependency>
    <dependency>spring-boot-starter-webflux</dependency>
    <dependency>mysql-connector-java</dependency>
    <dependency>lombok</dependency>
    <dependency>jjwt-api (0.12.6)</dependency>
    <dependency>jjwt-impl</dependency>
    <dependency>jjwt-jackson</dependency>
</dependencies>
```

### Frontend (package.json)
```json
{
  "dependencies": {
    "react": "^19.1.0",
    "react-dom": "^19.1.0",
    "react-router-dom": "^7.6.3",
    "axios": "^1.9.0",
    "crypto-js": "^4.2.0",
    "recharts": "^2.15.3"
  }
}
```

---

## License

This project is proprietary software developed by Trillex.

---

## Support

For issues or questions, please refer to:
- Backend documentation: `InventoryMS/InventoryMS/HELP.md`
- Chatbot integration guide: `InventoryMS/InventoryMS/CHATBOT_INTEGRATION_GUIDE.md`
- Helper-AI documentation: `Helper-AI/README.md`
