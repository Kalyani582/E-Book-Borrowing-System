
#  **Actors for E-Book Borrowing System**

### **Primary Actors**

* **User (Student/Reader)** → Borrows, returns, and searches for e-books.
* **Librarian/Admin** → Manages e-book inventory, approves borrow requests, and maintains the system.
* **E-Book Server** → Hosts the e-books and provides access to users.
* **Authentication Service** → Verifies user identity for secure borrowing and returning.

### **Secondary Actors**

* **Database** → Stores user data, borrow history, and e-book details.
* **Notification Service** → Sends alerts for due dates, new arrivals, etc.
* **Payment Gateway (Optional)** → Handles payments for late fees or subscriptions.
* **User’s Device (Browser/Mobile App)** → Interface through which users interact with the system.

---

#  **UML Use Case Diagram**

```mermaid
graph TD
    %% Actors
    U([User])
    L([Librarian/Admin])
    S([E-Book Server])
    A([Authentication Service])
    D([Database])
    N([Notification Service])
    P([Payment Gateway])

    %% User Actions
    U -->|"Search & Borrow e-Book"| S
    U -->|"Return e-Book"| S
    U -->|"View Borrow History"| D

    %% Librarian Actions
    L -->|"Manage Inventory"| D
    L -->|"Approve Requests"| S
    L -->|"Send Notifications"| N

    %% Authentication & Others
    A -->|"Verify Identity"| U
    S -->|"Serve e-Book"| U
    S -->|"Log Borrow Details"| D
    D -->|"Store Records"| L
    N -->|"Send Alerts"| U
    P -->|"Process Payments"| U
```

---

#  **UML Activity Diagram (User Flow + Borrowing Process)**

```mermaid
flowchart TD
    Start([Start])
    Login["User logs in via Authentication Service"]
    Search["Search for e-books"]
    Select["Select e-book to borrow"]
    CheckAvail["Check availability"]
    Approve["Librarian approves request"]
    Borrow["Borrow e-book"]
    Notify["Send notification"]
    Return["Return e-book"]
    UpdateDB["Update borrow history"]
    End([End])

    Start --> Login
    Login --> Search
    Search --> Select
    Select --> CheckAvail
    CheckAvail -->|Available| Approve
    Approve --> Borrow
    Borrow --> Notify
    Notify --> Return
    Return --> UpdateDB
    UpdateDB --> End
```

---

#  **UML Sequence Diagram (Borrowing Process)**

```mermaid
sequenceDiagram
    participant User
    participant Device as "User’s Device"
    participant Auth as "Authentication Service"
    participant Server as "E-Book Server"
    participant DB as "Database"
    participant Librarian
    participant Notify as "Notification Service"

    User->>Device: Login request
    Device->>Auth: Authenticate user
    Auth-->>Device: Authentication success
    Device->>Server: Search for e-books
    Server->>DB: Query e-book data
    DB-->>Server: Return list of books
    Server-->>Device: Display books
    User->>Device: Request to borrow book
    Device->>Server: Send borrow request
    Server->>Librarian: Forward request for approval
    Librarian-->>Server: Approves request
    Server->>DB: Update borrow record
    Server->>Notify: Send borrow notification
    Notify-->>User: Notify successful borrow
```

---


