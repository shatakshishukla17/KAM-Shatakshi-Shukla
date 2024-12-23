# Lead Management System for Udaan's B2B Platform (Shatakshi Shukla)

## Project Overview
This is a web-based lead management system designed for Udaan's B2B e-commerce platform to help Key Account Managers (KAMs) track their restaurant leads and interactions. The system provides a comprehensive solution for managing restaurant leads, contacts, and interactions through an intuitive interface.

## Features

### Lead Management
- Create and manage restaurant leads with detailed information
- Track essential details including restaurant name, address, contact information
- Monitor lead status (New, Active, Inactive)
- Assign leads to specific KAMs

### Contact Management
- Store multiple contacts per restaurant
- Maintain contact details including name, role, phone number, and email
- Support different role types (Owner, Manager, Staff)

### Interaction Tracking
- Log various types of interactions (Calls, Visits, Orders)
- Record interaction dates and detailed notes
- Flag interactions requiring follow-up
- Maintain a chronological history of all lead interactions

### Dashboard Features
- View comprehensive list of all leads
- Track pending calls for the day
- Monitor recent interactions
- Implement real-time search functionality
- Display key metrics and statistics

## Technical Architecture

### Backend
- **Framework**: Node.js with Express
- **Database**: MySQL with connection pooling
- **API Structure**: RESTful architecture
- **Main Routes**:
  - `/api/leads`: Lead management endpoints
  - `/api/contacts`: Contact management endpoints
  - `/api/interactions`: Interaction tracking endpoints

### Frontend
- **Framework**: Vanilla JavaScript with Bootstrap 
- **UI Components**: 
  - Responsive dashboard
  - Modal forms for data entry
  - Interactive data tables
  - Real-time search functionality
- **Styling**: Bootstrap for consistent and responsive design

## Database Schema

### Leads Table
```sql
CREATE TABLE leads (
  id INT PRIMARY KEY AUTO_INCREMENT,
  restaurant_name VARCHAR(255) NOT NULL,
  address TEXT,
  contact_number VARCHAR(20),
  status ENUM('New', 'Active', 'Inactive') DEFAULT 'New',
  assigned_kam VARCHAR(255),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
)
```

### Contacts Table
```sql
CREATE TABLE contacts (
  id INT PRIMARY KEY AUTO_INCREMENT,
  lead_id INT,
  name VARCHAR(255) NOT NULL,
  role VARCHAR(100),
  phone_number VARCHAR(20),
  email VARCHAR(255),
  FOREIGN KEY (lead_id) REFERENCES leads(id) ON DELETE CASCADE
)
```

### Interactions Table
```sql
CREATE TABLE interactions (
  id INT PRIMARY KEY AUTO_INCREMENT,
  lead_id INT,
  interaction_date DATE NOT NULL,
  interaction_type ENUM('Call', 'Visit', 'Order') NOT NULL,
  notes TEXT,
  follow_up_required BOOLEAN DEFAULT false,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (lead_id) REFERENCES leads(id) ON DELETE CASCADE
)
```

## Setup Instructions

1. **Clone the Repository**
   ```bash
   git clone https://github.com/shatakshishukla17/KAM-Shatakshi-Shukla-Udaan.git
   cd lead-management-system
   ```
   OR
   Download the zip file

3. **Install Dependencies**
   ```bash
   npm install
   ```

4. **Database Configuration**
   - Create a MySQL database
   - Update database configuration in `config/database.js`:
     ```javascript
     const connection = mysql.createConnection({
       host: 'localhost',
       user: 'your_username',
       password: 'your_password', //write your MySQL password here
       database: 'lead_management'
     });
     ```

5. **Start the Server**
   ```bash
   npm start
   ```
   The application will be available at `http://localhost:3000`


## API Endpoints

### Leads
- `GET /api/leads`: Retrieve all leads
- `GET /api/leads/search`: Search leads
- `GET /api/leads/:id`: Get specific lead details
- `POST /api/leads`: Create new lead
- `PUT /api/leads/:id`: Update lead
- `DELETE /api/leads/:id`: Delete lead

### Contacts
- `GET /api/contacts/lead/:leadId`: Get contacts for a lead
- `POST /api/contacts`: Add new contact

### Interactions
- `GET /api/interactions/lead/:leadId`: Get interactions for a lead
- `GET /api/interactions/pending`: Get pending calls
- `GET /api/interactions/recent`: Get recent interactions
- `POST /api/interactions`: Add new interaction

## Contact
For any inquiries, please contact [shatakshi1712@gmail.com](mailto:shatakshi1712@gmail.com).
