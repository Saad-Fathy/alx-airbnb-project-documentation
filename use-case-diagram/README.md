Airbnb Clone Backend Use Case Diagram
Overview
This directory (use-case-diagram) contains the use case diagram for the Airbnb Clone backend, as part of the ALX Airbnb Project Documentation. The diagram, created with Draw.io, visualizes the interactions between actors (Guest, Host, Admin, External Payment Gateway) and the system for key functionalities, including user registration, property booking, payments, and more. This supports the RESTful API design and aligns with the features from Task 0.
Files

README.md: This file, describing the use case diagram, actors, and interactions.
use-case-diagram.png: A Draw.io diagram visualizing the actors and their interactions with the system.

Use Case Diagram Details
The use case diagram represents the Airbnb Clone backend system, capturing how actors interact with key functionalities. The diagram uses UML notation, with actors as stick figures, use cases as ovals, and associations as lines. Include and extend relationships clarify dependencies between use cases.
Actors

Guest: A user who searches and books properties, submits reviews, makes payments, and sends messages.
Host: A user who manages property listings, responds to bookings, and communicates with guests.
Admin: A user with elevated privileges to manage users, properties, bookings, and analytics.
External Payment Gateway: An external system (e.g., Stripe, PayPal) that processes payments.

Use Cases
Grouped by functional area, aligned with Task 0 features:

User Management:
Register User: Create an account (Guest, Host, Admin).
Login: Authenticate with email/password, receive JWT (Guest, Host, Admin).
Update Profile: Modify user details (Guest, Host, Admin).
Delete Account: Remove account and related data (Guest, Host, Admin).


Property Management:
Create Property: Add a new listing (Host).
Update Property: Modify listing details (Host).
Delete Property: Remove a listing, if no active bookings (Host).
View Properties: List all properties (Guest, Host, Admin).
Search Properties: Filter by location, price, etc. (Guest, Host, Admin).


Booking System:
Create Booking: Book a property for specific dates (Guest).
View Bookings: View own bookings (Guest, Host) or all bookings (Admin).
Update Booking Status: Change status to pending/confirmed/canceled (Host, Admin).
Cancel Booking: Cancel a booking (Guest, Admin).


Payment Processing:
Process Payment: Pay for a booking via payment gateway (Guest, External Payment Gateway).
Confirm Payment: Record payment success (External Payment Gateway).
Process Refund: Issue refunds for cancellations (Admin, External Payment Gateway).


Review System:
Submit Review: Add a rating and comment post-stay (Guest).
View Reviews: View reviews for a property or user (Guest, Host, Admin).
Edit/Delete Review: Modify or remove a review (Guest).


Messaging System:
Send Message: Send a message to another user (Guest, Host).
View Messages: View sent/received messages (Guest, Host).


Admin Features:
Manage Users: View, update, or delete users (Admin).
Moderate Properties: Review and remove listings (Admin).
Manage Bookings: Resolve booking disputes (Admin).
View Analytics: Access system metrics (Admin).



Relationships

Include: Create Booking includes Search Properties (to find a property). Process Payment includes Confirm Payment (to record success).
Extend: Process Refund extends Cancel Booking (optional for cancellations).
Associations: Connect actors to their use cases (e.g., Guest to Create Booking, Host to Create Property).

Diagram
The use-case-diagram.png file, created with Draw.io, visualizes these actors and use cases within a system boundary (“Airbnb Clone Backend”). Actors are on the left/right, use cases are grouped by category within the system, and associations are shown as lines. Include/extend relationships are marked with dashed arrows and labels (<<include>>, <<extend>>). Colors differentiate functional areas, and text is legible (font size ≥12).
Creation Instructions

Open diagrams.net and select the “UML” template.
Add actors (stick figures): Guest, Host, Admin, External Payment Gateway.
Add use cases (ovals) within a system boundary box labeled “Airbnb Clone Backend”.
Group use cases by category (e.g., User Management, Booking System).
Draw solid lines for associations (e.g., Guest to Create Booking).
Add dashed arrows for include/extend relationships (e.g., Create Booking → Search Properties with <<include>>).
Use colors for categories and ensure legible text.
Export as use-case-diagram.png (File > Export As > PNG, 300 DPI).
Save in the use-case-diagram directory.

Submission

Directory: use-case-diagram
Files: README.md, use-case-diagram.png
Repository: alx-airbnb-project-documentation
