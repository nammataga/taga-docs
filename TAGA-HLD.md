# High Level Design (HLD)
**Project:** Tamil Nadu Agriculture Graduates Association (TAGA) Website  

---

## 1. Purpose
The purpose of this document is to provide a high-level architectural and functional overview of the TAGA website. This system aims to digitize association activities, provide information to members and the public, and enable authenticated member services such as reservations and access to resources.

---

## 2. Scope
The system includes:
- Public informational pages
- Member authentication and registration
- Role-based access for members and administrators
- Content management for office bearers and resources
- Guest house (TAGA Tower) reservation functionality

**Out of Scope**
- Online payment gateway
- Native mobile application

---

## 3. Stakeholders
- TAGA State Committee
- District Committees
- Registered Members
- General Public
- System Administrators / DevOps Team

---

## 4. Technology Stack

### Frontend
- React (SPA)
- React Router
- Axios
- Context API / Redux (optional)

### Backend
- GoLang
- Gin Web Framework
- Swagger
- Zap Logger

### Storage
- PostgreSQL
- JSON (static / seed data)

### DevOps
- Bash scripts
- Git
- Linux hosting

---

## 5. System Architecture (High Level)

[ Client Browser ]  
        |  
        v  
[ React Frontend ]  
        |  
 REST APIs (HTTPS)  
        |  
        v  
[ GoLang Gin Backend ]  
        |  
        |-- PostgreSQL  
        |-- JSON Storage  

---

## 6. Functional Overview

### 6.1 About Us
- Vision & Mission
- History
- Objectives

### 6.2 Office Bearers
- State level
- District level
- Term & role based

### 6.3 Resources
- Government Orders
- Articles
- Statistics
- Filters & search

### 6.4 Member Registration & Login
- JWT-based authentication
- Role-based access

### 6.5 TAGA Tower Reservation
- Availability check
- Booking request
- Admin approval
- Booking history

---

## 7. Non-Functional Requirements

### Security
- HTTPS
- bcrypt password hashing
- JWT auth
- RBAC

### Performance
- <300ms average API response

### Maintainability
- Modular React components
- Layered Go backend

---

## 8. Backend Modules
- Auth
- Members
- Office Bearers
- Resources
- Reservations

---

## 9. Database Design (High Level)
- members
- roles
- office_bearers
- districts
- resources
- reservations

---

## 10. API Documentation
Swagger UI:
/swagger/index.html

---

## 11. Deployment
1. Build frontend
2. Build backend
3. Run migrations
4. Deploy services

---

## 12. Future Enhancements
- Payments
- Notifications
- Mobile app
- Multi-language support

---

**End of Document**
