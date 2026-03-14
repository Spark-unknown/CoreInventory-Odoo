# Core Inventory Management System (IMS)

A modern, modular **Inventory Management System** designed to digitize and streamline stock-related operations. This system replaces manual Excel tracking with a centralized, real-time application built on Next.js and MySQL.

---

## 🚀 Key Features

- **Product Management**: Create and update products with SKU, Category, and Unit of Measure
- **Incoming Receipts**: Track goods from vendors; stock increases automatically upon validation
- **Delivery Orders**: Manage outgoing shipments; stock decreases upon validation  
- **Internal Transfers**: Move stock between warehouses or specific racks (e.g., Rack A to Rack B)
- **Stock Adjustments**: Reconcile physical counts with system stock to fix mismatches
- **Real-time Dashboard**: View KPIs like Low Stock items, Pending Receipts, and Total Products

---

## 👥 System Users

- **Inventory Managers**: Manage overall flow of incoming and outgoing stock
- **Warehouse Staff**: Handle physical tasks like picking, shelving, and stock counts

---

## 🛠 Tech Stack

- **Frontend**: Next.js 14+ (App Router)
- **Styling**: Tailwind CSS + Shadcn/UI
- **Backend**: Next.js Server Actions
- **Database**: MySQL with Prisma ORM
- **Authentication**: NextAuth.js
- **State Management**: TanStack Query (React Query)

---

## 📁 Project Structure

```
/src
 ├── /app              # Next.js App Router (Pages & Layouts)
 │    ├── /(auth)      # Login, Signup, OTP Reset
 │    ├── /(dashboard) # Dashboard, Products, Operations
 │    └── layout.tsx   # Sidebar & Navigation
 ├── /components       # Reusable UI (Buttons, Tables, Forms)
 │    ├── /ui          # Shadcn components
 │    └── /inventory   # Stock-specific components
 ├── /lib              # Database client (Prisma), Utilities
 ├── /services         # Business logic (Stock calculation, Validation)
 ├── /hooks            # Custom React hooks
 └── /types            # TypeScript interfaces
/prisma
 └── schema.prisma     # Database schema (MySQL)
```

---

## 🚀 Getting Started

### Prerequisites

- Node.js 18+ 
- MySQL database
- npm or yarn

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd CoreInventory-Odoo
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   ```bash
   cp .env.example .env.local
   ```
   Configure your database URL and authentication secrets.

4. **Set up the database**
   ```bash
   npx prisma migrate dev
   npx prisma generate
   npx prisma db seed
   ```

5. **Run the development server**
   ```bash
   npm run dev
   ```

Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## 📋 Implementation Roadmap

### Phase 1: Foundation (Week 1)
- [x] Database schema design
- [ ] Authentication system
- [ ] Product CRUD operations
- [ ] Basic dashboard

### Phase 2: Core Operations (Week 2)
- [ ] Receipt management
- [ ] Delivery workflows
- [ ] Stock ledger implementation
- [ ] Automatic stock updates

### Phase 3: Advanced Features (Week 3)
- [ ] Internal transfers
- [ ] Inventory adjustments
- [ ] Dynamic filters
- [ ] Low stock alerts

---

## 🗄️ Database Schema

### Core Tables

#### Products
```sql
- id (Primary Key)
- name (String)
- sku (String, Unique)
- category_id (Foreign Key)
- unit_of_measure (String)
- current_stock (Integer)
- reorder_point (Integer)
- created_at (DateTime)
- updated_at (DateTime)
```

#### Stock Ledger
```sql
- id (Primary Key)
- product_id (Foreign Key)
- location_id (Foreign Key)
- move_type (Enum: RECEIPT, DELIVERY, TRANSFER, ADJUSTMENT)
- quantity (Integer)
- reference (String)
- created_at (DateTime)
- created_by (Foreign Key)
```

#### Locations
```sql
- id (Primary Key)
- name (String)
- type (Enum: WAREHOUSE, RACK, BIN)
- parent_id (Foreign Key, nullable)
```

---

## 🔧 Development Commands

```bash
# Development
npm run dev

# Build for production
npm run build

# Start production server
npm run start

# Database operations
npx prisma studio
npx prisma migrate dev
npx prisma generate
```

---

## 📊 Key Workflows

### 1. Incoming Receipts
1. Select supplier and products
2. Enter quantities received
3. Validate → Stock increases automatically
4. Entry logged in Stock Ledger

### 2. Delivery Orders
1. Create delivery order for customer
2. Pick items from inventory
3. Pack and validate shipment
4. Stock decreases automatically
5. Entry logged in Stock Ledger

### 3. Internal Transfers
1. Select source and destination locations
2. Choose products and quantities
3. Validate → Stock moves between locations
4. Total company stock unchanged
5. Entry logged in Stock Ledger

---

## 🎯 KPI Dashboard Metrics

- **Total Products**: Count of active products in system
- **Low Stock Items**: Products below reorder point
- **Pending Receipts**: Receipts awaiting validation
- **Pending Deliveries**: Delivery orders to be processed
- **Recent Stock Moves**: Latest inventory movements

---

## 🔐 Security Features

- JWT-based authentication
- Role-based access control
- OTP-based password reset
- Activity logging and audit trails

---

## 📱 Mobile Considerations

- Responsive design for tablets and phones
- Touch-friendly interfaces for warehouse staff
- Offline capability for stock counting

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

---

## 📄 License

This project is licensed under the MIT License.

---

## 📞 Support

For support and questions, please open an issue in the repository.
