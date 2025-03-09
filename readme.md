# **Employee Rotation Schedule - Backend Development Guide**

## **Overview**

This is the backend for the **Employee Rotation Schedule** web application. It handles all the logic, data storage, and API endpoints for managing employee schedules, requests, and user data. The backend is responsible for authenticating users, handling schedule management, storing employee data, and notifying employees/managers of schedule changes.

---

## **Key Features**

- **Authentication**
  - User login (employees and managers).
  - Session persistence with JWT authentication.
  - Role-based access control to ensure employees and managers have the correct permissions.
  
- **Schedule Management**
  - Managers can create and modify employee schedules.
  - Employees can view schedules and request schedule changes.
  - Holiday requests can be submitted and managed by managers.
  
- **Unavailable Times**
  - Employees can define unavailable times (e.g., night shifts only).
  - Managers can still assign shifts during unavailable times but are alerted with a conflict warning.

- **Notifications**
  - Integration with WhatsApp/Email to send notifications to employees and managers for schedule updates and requests.

---

## **API Endpoints**

### **Authentication**

- **POST /login**  
  - **Description**: Logs in a user (employee or manager) and returns a session token.
  - **Request**: `{ "email": "user@example.com", "password": "yourpassword" }`
  - **Response**: `{ "token": "your-jwt-token" }`

- **POST /register**  
  - **Description**: Registers a new employee, including unavailable time slots.
  - **Request**: `{ "name": "John Doe", "email": "johndoe@example.com", "password": "password123", "unavailable_times": ["night shift"] }`
  - **Response**: `{ "message": "User registered successfully" }`

- **POST /forgot-password**  
  - **Description**: Allows users to reset their password.
  - **Request**: `{ "email": "user@example.com" }`
  - **Response**: `{ "message": "Password reset email sent" }`

---

### **Schedule Management**

- **GET /schedule**  
  - **Description**: Retrieves the current schedule for an employee or all employees (depending on user role).
  - **Request**: `Authorization: Bearer <jwt-token>`
  - **Response**: `{ "schedule": [ { "day": "Monday", "shift": "Morning" }, ... ] }`

- **POST /schedule/manage**  
  - **Description**: Allows managers to modify schedules and assign shifts.
  - **Request**: `{ "employee_id": "123", "day": "Monday", "shift": "Night" }`
  - **Response**: `{ "message": "Schedule updated successfully" }`

- **POST /schedule/notifications**  
  - **Description**: Sends notifications to employees regarding schedule changes.
  - **Request**: `{ "employee_id": "123", "notification_type": "schedule_change", "message": "Your schedule has been updated." }`
  - **Response**: `{ "message": "Notification sent successfully" }`

---

### **Requests Management**

- **POST /requests/holidays**  
  - **Description**: Allows employees to request holidays.
  - **Request**: `{ "employee_id": "123", "start_date": "2025-03-20", "end_date": "2025-03-25" }`
  - **Response**: `{ "message": "Holiday request submitted" }`

- **POST /requests/schedule-change**  
  - **Description**: Allows employees to request a schedule change.
  - **Request**: `{ "employee_id": "123", "day": "Monday", "requested_shift": "Night" }`
  - **Response**: `{ "message": "Schedule change request submitted" }`

- **GET /requests/pending**  
  - **Description**: Allows managers to view all pending holiday and schedule change requests.
  - **Request**: `Authorization: Bearer <jwt-token>`
  - **Response**: `{ "requests": [ { "type": "holiday", "employee_id": "123", "status": "pending" }, ... ] }`

---

## **Database Structure**

### **Tables**

- **Users**: Stores user information (name, email, password, role, etc.).
- **Schedules**: Stores employee schedules (employee_id, day, shift).
- **Requests**: Stores requests (employee_id, type [holiday, schedule-change], status [pending, approved, rejected]).

---

## **Development Setup**

### 1. **Environment Setup**
   - Install dependencies:  
     ```bash
     npm install
     ```
   - Set up environment variables:
     - **DB_HOST**: Database host.
     - **DB_USER**: Database user.
     - **DB_PASS**: Database password.
     - **JWT_SECRET**: Secret key for JWT.
   
### 2. **Run the Development Server**
   - Start the backend server:  
     ```bash
     npm run dev
     ```

### 3. **Testing**
   - You can test the API with Postman or any other API testing tool.

---

## **Security Considerations**
- Ensure proper **JWT authentication** for secure access to sensitive endpoints.
- Sanitize user input to prevent SQL injection and other vulnerabilities.
- Implement **role-based access control** (RBAC) for managers and employees.

---

## **Future Enhancements**

1. **Mobile App Backend Integration**
   - Set up a mobile-friendly backend API to accommodate mobile apps in the future.
   
2. **Analytics and Reporting**
   - Implement analytics features to track employee work hours, performance, and schedule patterns.

3. **AI-Based Schedule Optimization**
   - Introduce AI/ML techniques to optimize employee schedules based on availability, workload, and preferences.

---

This guide outlines the backend structure and the API endpoints needed for the Employee Rotation Schedule application. The backend ensures that employees and managers can efficiently manage schedules and requests, with proper security measures in place.
