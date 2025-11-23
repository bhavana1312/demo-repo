# Flight Booking App – WebFlux + MongoDB  

## Overview  
This project is a fully reactive **Flight Ticket Booking System** built using **Spring WebFlux** and **Reactive MongoDB**.  
It supports end‑to‑end user flow including:

- Flight Search  
- Ticket Booking  
- Seat Map Handling  
- PNR Lookup  
- Booking History  
- Ticket Cancellation  
- Airline & Flight Inventory Management  
- Validation + Error Handling  
- Concurrent seat booking protection  
- JUnit + WebFluxTest + Mockito test coverage  
- Load testing using JMeter

---

## 🧰 Tech Stack  
**Backend Framework:** Spring Boot (WebFlux)  
**Database:** MongoDB (Reactive)  
**Language:** Java 17  
**Build Tool:** Maven  
**Testing:**  
- JUnit 5  
- Mockito  
- WebTestClient  
- Reactor StepVerifier  
- Jacoco (Coverage Report > 85%)  

**Load Testing:**  
- Apache JMeter (Sequential seat booking test)

---

## 📦 Modules Implemented

### ✔ Airline Management  
- Create airline (auto‑created if not existing during inventory add)

### ✔ Flight Inventory  
- Add flight schedule  
- Maintain available seats  
- Maintain seat map (`S001 … S150`)  
- Prevent duplicate airline + flight number combinations  

### ✔ Booking System  
- Book ticket  
- Validate seats  
- Prevent double booking  
- Generate unique PNR  
- Save passenger details  
- Update seat map  
- Reduce available seats  

### ✔ Ticket Retrieval  
- Fetch booking details by PNR  

### ✔ Booking History  
- Fetch bookings by email  

### ✔ Ticket Cancellation  
- Allowed only >= 24 hours before flight  
- Marks booking as cancelled  
- Frees seat numbers  
- Increases available seats  

---

# 📡 REST API Endpoints

---

## 1️⃣ Add Inventory (Admin)
### **POST**  
`http://localhost:8080/api/flight/airline/inventory/add`

### Request Body
{
  "airlineName": "Air India",
  "airlineCode": "AI",
  "airlineLogo": "logo.png",
  "flightNumber": "AI123",
  "from": "HYD",
  "to": "DEL",
  "departure": "2025-12-01T10:00:00",
  "arrival": "2025-12-01T12:00:00",
  "totalSeats": 150,
  "price": 4200
}

---

## 2️⃣ Search Flights  
### **POST**  
`http://localhost:8080/api/flight/search`

### Request Body  
{
  "from": "HYD",
  "to": "DEL",
  "date": "2025-12-01"
}

---

## 3️⃣ Book Flight  
### **POST**  
`http://localhost:8080/api/flight/booking/{flightId}`  
Example:  
`http://localhost:8080/api/flight/booking/6921efee743d6f6a27890955`

### Request Body  
{
  "name": "bhavana",
  "email": "bhavana@gmail.com",
  "seats": 2,
  "meal": "Veg",
  "seatNumbers": ["S12","S13"],
  "passengers": [
    { "name": "bhavana", "gender": "Female", "age": 21, "seatNo": "S12" },
    { "name": "siddharth", "gender": "Male", "age": 22, "seatNo": "S13" }
  ]
}

---

## 4️⃣ Get Ticket by PNR  
### **GET**  
`http://localhost:8080/api/flight/ticket/587AD95532`

---

## 5️⃣ Booking History  
### **GET**  
`http://localhost:8080/api/flight/booking/history/bhavana@gmail.com`

---

## 6️⃣ Cancel Ticket  
### **DELETE**  
`http://localhost:8080/api/flight/booking/cancel/587AD95532`

---

# 🧪 Testing Setup

### Unit Tests
- BookingService  
- InventoryService  
- FlightController  
- Seat map logic  
- Cancellation rules  

### Jacoco  
Coverage achieved: **85%+**

---

# ⚡ Load Testing (JMeter)

Sequential seat booking (S001 to S100)
Counter config:
- Start: 1  
- Increment: 1  
- Format: `S%03d`

Works with:
"seatNumbers": ["${seatNo}"]

---

# 🎯 Final Outcome

A full‑featured **Reactive Flight Booking System** with:
- High performance non‑blocking APIs  
- Validation & business logic  
- Airline + inventory module  
- Booking + cancellation  
- JUnit + Jacoco + WebFlux tests  
- JMeter tested  
- Production‑ready backend  

