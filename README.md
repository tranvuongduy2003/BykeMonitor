# 1. Core Services
Each service will be responsible for a specific domain, making the system modular, scalable, and easy to manage.
## A. User Service
### Responsibilities:
- Handle user authentication, registration, user profiles, and session management.
### Key Functions:
- User registration and login
- Retrieve user profile and session details
- Handle user roles (e.g., admin, operator, user)
## B. Motorbike Service
### Responsibilities: 
- Manage motorbike information, including registration, status updates (checked in or out), and tracking.
### Key Functions:
- Register motorbikes in the system
- Update motorbike status (available, in-use, parked)
- Retrieve motorbike data
## C. Parking Service
### Responsibilities: 
- Manage parking spots, their availability, and location data.
### Key Functions:
- Allocate or release parking spots during check-in/check-out
- Track parking spot availability in real time
- Associate parking spots with locations (geographical coordinates)
## D. Check-In/Check-Out Service
### Responsibilities: 
- Handle the core business logic of motorbike check-ins and check-outs, including validation, time logging, and charging (if applicable).
### Key Functions:
- Motorbike check-in process (parking spot assignment, status update)
- Motorbike check-out process (spot release, timing, and logging)
- Validate user and motorbike information before check-in/out
- Time tracking for each motorbike in/out event
## E. Notification Service
### Responsibilities: 
- Send real-time notifications to users or administrators about status updates (e.g., motorbike checked in/out, available spots, alerts).
### Key Functions:
- Notify users of successful check-in/check-out
- Send alerts for anomalies (e.g., system overload, motorbike not found)
- Handle async notifications via email, SMS, or push notifications
## F. Payment Service (optional, if billing is required)
### Responsibilities: 
- Manage payments for parking services, including billing and invoicing.
### Key Functions:
- Calculate parking charges based on duration
- Process payments via different methods (credit card, mobile payment, etc.)
- Issue invoices to users
## G. Reporting & Analytics Service
### Responsibilities: 
- Provide insights and reports based on system usage (e.g., daily check-ins, occupancy rate).
### Key Functions:
- Generate real-time reports for admins (e.g., peak check-in times, popular locations)
- Provide audit logs of check-ins/check-outs
# 2. Core Entities
Each service will manage a set of entities (data models) that represent the core data objects in your system.
## A. User Entity
### Attributes:
- UserId: Unique identifier for the user
- Username: User's login name
- Password: (hashed) user password
- Role: Role of the user (admin, operator, customer)
- FullName: User's full name
- Email: Contact email
- Phone: Contact phone number
- SessionToken: Token for user sessions (for authentication)
## B. Motorbike Entity
### Attributes:
- BikeId: Unique identifier for the motorbike
- LicensePlate: License plate number
- OwnerId: Reference to the UserId of the motorbike owner
- Model: Motorbike model
- Status: Current status (checked-in, checked-out, parked)
- CheckInTime: Timestamp of last check-in
- CheckOutTime: Timestamp of last check-out
- LocationId: Reference to the location/parking spot where it's checked in
## C. ParkingSpot Entity
### Attributes:
- SpotId: Unique identifier for the parking spot
- LocationId: Geographical identifier (or lot identifier) for where the parking spot is
- IsAvailable: Boolean indicating if the spot is available
- BikeId: Reference to the motorbike currently occupying the spot (null if empty)
- SpotType: Type of parking spot (e.g., regular, premium)
## D. CheckInOutLog Entity
### Attributes:
- LogId: Unique identifier for the log entry
- UserId: Reference to the UserId who performed the check-in/out
- BikeId: Reference to the motorbike being checked in/out
- CheckInTime: Timestamp of check-in
- CheckOutTime: Timestamp of check-out
- SpotId: Reference to the parking spot used
- Duration: Duration of stay (calculated at check-out)
- Charge: Cost associated with the duration of stay (optional)
## E. Location Entity
### Attributes:
- LocationId: Unique identifier for the parking location
- Address: Full address or coordinates of the location
- Capacity: Total number of parking spots at the location
- AvailableSpots: Current number of available spots
## F. Payment Entity (optional)
### Attributes:
- PaymentId: Unique identifier for the payment
- UserId: Reference to the user making the payment
- Amount: Payment amount
- PaymentMethod: Payment method used
- Timestamp: Time of payment transaction
## G. NotificationLog Entity
### Attributes:
- NotificationId: Unique identifier for the notification
- UserId: Reference to the recipient user
- Message: Content of the notification
- Type: Notification type (email, SMS, push)
- Timestamp: Time the notification was sent
