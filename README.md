# software-construction-mobile-app

## Name of App:

We chose the application Uber.

## Part A: Understanding the App

### App Overview
Uber solves the problem of finding convenient, on-demand transportation without needing to hail a taxi on the street or wait at a taxi rank. It connects riders with drivers through the app in real time, reducing uncertainty about wait times and route costs (Singh, 2025). The integration of GPS, booking, and cashless payment makes getting a ride easier and more efficient than the traditional taxi system.

### Primary Users
Uber has two main user groups:

- **Riders** — people who need transportation from one location to another. These include everyday commuters, travelers, students, shoppers, seniors, and parents booking rides for teens.
- **Drivers** — independent partners providing transportation services through the Uber platform. They use the app to accept ride requests and earn income.

### Core Features
- **Ride Booking:** Users request a ride by entering pickup and drop-off locations in the app.
- **Real-Time GPS Tracking:** Riders can see the driver’s location and estimated arrival time on a live map.
- **Multiple Ride Options:** Users can choose from different vehicle types (e.g., UberX, Uber Black, Uber Pool).
- **Secure Cashless Payments:** The app supports in-app payments via card, mobile wallet, or other digital payment methods.
- **Driver & Rider Ratings:** After each trip, both parties can rate each other, encouraging quality service.
- **Push Notifications:** Users receive updates such as driver arrival alerts, trip start, and trip end notifications.
- **Safety Features:** The app includes SOS/emergency buttons and the ability to share trip status with contacts.
- **Delivery Feature:** Users can place delivery orders through the app, and a courier delivers items to the specified fare splitting, which lets you easily divide the cost of a ride evenly with friends or group members directly in the app, avoiding awkward math or payments later.


## Part B: Thinking Behind the Scenes

### Feature 1: Ride Booking

#### User Interface (UI)
The ride booking interface allows users to input pickup and drop-off locations, select a ride type, and request a ride. The screens are designed to be intuitive and provide feedback when locations are invalid or when the request is being processed.

#### Business Logic
The business logic validates locations, calculates estimated fares, determines the nearest available drivers, and matches them to riders. It enforces rules such as valid addresses and supported ride types.

#### Network / APIs
APIs send ride requests to Uber’s backend servers, which process the request and return matched driver details. Real-time updates are exchanged between the client and server.

#### Data Storage
Ride requests are temporarily stored during the trip and permanently recorded for billing, analytics, and future reference.

> **Connectivity Note:** Ride booking requires internet connectivity. Slow or unavailable networks may delay or prevent requests.

---

### Feature 2: Real-Time GPS Tracking

#### User Interface (UI)
A live map displays the driver’s current location and route, updating continuously to show trip progress and estimated arrival times.

#### Business Logic
The system processes location updates, recalculates ETAs, updates trip status, and triggers alerts at milestones such as pickup and drop-off.

#### Network / APIs
GPS coordinates are transmitted from the driver’s device to Uber’s backend and forwarded to riders using APIs or socket connections.

#### Data Storage
Current locations are stored temporarily, while historical trip data is stored permanently for analytics and dispute resolution.

> **Connectivity Note:** Slow networks may cause lag, and network loss can freeze tracking until reconnection.

---

### Feature 3: Multiple Ride Options

#### User Interface (UI)
Available ride types are displayed with pricing and ETAs, allowing users to choose an option that suits their needs.

#### Business Logic
The system filters drivers by ride type, calculates pricing and ETAs, and applies surge pricing or promotions.

#### Network / APIs
The client communicates with backend services to retrieve updated ride options and driver availability.

#### Data Storage
Ride selections and driver data are stored temporarily for processing and permanently for reporting.

> **Connectivity Note:** Without internet access, ride options cannot be retrieved.

---

### Feature 4: Secure Cashless Payments

#### User Interface (UI)
The payment interface allows users to manage payment methods, view fare breakdowns, and receive digital receipts.

#### Business Logic
Fare calculation is based on distance, time, and promotions. Payment credentials are handled securely, with retry mechanisms for failures.

#### Network / APIs
Payment data is sent to external payment gateways or banking APIs for transaction processing.

#### Data Storage
Payment records are stored securely using encryption or tokenization for auditing and reconciliation.

> **Connectivity Note:** Network issues may delay or prevent payment confirmation.

---

### Feature 5: Driver & Rider Ratings

#### User Interface (UI)
After each trip, users rate each other using a star system and optional comments.

#### Business Logic
Ratings are validated, averaged, and used to update user profiles and enforce quality standards.

#### Network / APIs
Ratings are transmitted to backend servers and linked to trip records.

#### Data Storage
Ratings are permanently stored for analytics and quality assurance.

> **Connectivity Note:** Ratings may be queued locally if the network is unavailable.

---

### Feature 6: Push Notifications

#### User Interface (UI)
Notifications alert users about key trip events and are displayed on the device or within the app.

#### Business Logic
The system determines notification timing, recipients, and message content, including retries on failure.

#### Network / APIs
Push services such as Firebase Cloud Messaging or Apple Push Notification Service deliver notifications.

#### Data Storage
Notification logs may be stored for troubleshooting and analytics.

> **Connectivity Note:** Delays or failures may occur during poor network conditions.

---

### Feature 7: Safety Features

#### User Interface (UI)
SOS buttons and trip-sharing options are clearly accessible within the app interface.

#### Business Logic
The system handles emergency alerts, communicates with contacts or authorities, and logs incidents.

#### Network / APIs
Safety alerts and trip data are transmitted in real time to servers or designated contacts.

#### Data Storage
Safety logs and emergency records are stored for monitoring and investigations.

> **Connectivity Note:** These features rely heavily on internet availability.

---

### Feature 8: Delivery Feature

#### User Interface (UI)
Users place delivery orders through a dedicated interface that supports item selection, address input, and tracking.

#### Business Logic
Orders are validated, fees calculated, couriers assigned, and delivery progress monitored.

#### Network / APIs
Order and tracking data are exchanged between users, couriers, and backend servers via APIs.

#### Data Storage
Order details and delivery logs are stored for transaction records and analytics.

> **Connectivity Note:** Network issues can delay order placement and tracking updates.


## Part C: Change and Maintainability


### Which parts of the app would need changes?

Introducing mobile payments in Uganda would require changes across multiple layers of the Uber system rather than in a single isolated component. At the user interface level, the payment screens would need to be updated to allow users to select local mobile money options such as MTN Mobile Money or Airtel Money. This includes modifying payment setup screens, checkout flows, and receipts to clearly show mobile money as a supported method.

At the business logic level, significant changes would be required to handle new payment rules. The system would need logic to initiate mobile money payment requests, handle asynchronous payment confirmations, manage retries for failed transactions, and support partial or delayed payments. Unlike card payments, mobile money transactions often depend on user approval via USSD or SMS, which adds complexity to transaction state management.

At the network and API layer, Uber would need to integrate with local mobile money provider APIs or third-party payment aggregators operating in Uganda. This would involve building new secure API connections, handling different response formats, and managing callbacks from payment providers to confirm transaction success or failure.

At the data storage level, the database schema would need updates to store mobile money transaction references, provider identifiers, payment statuses, and reconciliation data. Existing payment tables designed primarily for card-based systems would likely need extensions or redesigns to support the different lifecycle of mobile money transactions.


### What existing features could break?

Several existing features could be affected or temporarily broken by the introduction of mobile payments. The payments and billing feature is the most directly impacted, as assumptions made for instant card authorization may no longer hold true for mobile money, which can be delayed or fail due to network or user interaction issues. This could lead to incorrect fare settlements if not handled carefully.

Ride completion workflows could also be affected, since Uber currently assumes that payment confirmation happens quickly after a trip ends. With mobile money, there may be delays in confirmation, which could cause issues such as rides being marked as unpaid or drivers not receiving timely earnings updates.

Promotions and discounts could break if they are tightly coupled to specific payment methods. For example, promo codes designed for card payments may not apply correctly to mobile money unless explicitly adapted.
Driver payouts may also be impacted, as Uber would need to ensure that funds collected via mobile money are correctly reconciled and transferred to drivers, possibly through different payout mechanisms than those used for card-based transactions.


### Why would this change be difficult to implement?

This change would be difficult to implement because it cuts across many core assumptions in Uber’s existing architecture. From a technical perspective, mobile money systems are fundamentally different from traditional card payment systems. They are often asynchronous, depend on external telecom infrastructure, and can be less reliable in terms of network availability, which requires robust error handling and state management.

From a maintainability standpoint, adding Uganda-specific payment logic risks introducing country-specific code paths that increase system complexity. If not carefully abstracted, this can lead to tightly coupled code that is harder to maintain and extend to other regions with similar payment needs.

Scalability is another challenge, as mobile money providers may have rate limits or performance constraints that differ from global card processors. Uber would need to design the system to handle spikes in payment requests without overwhelming local providers or degrading user experience.

Finally, regulatory and compliance requirements add further complexity. Financial regulations, data protection laws, and telecom policies in Uganda may require additional validation, auditing, and reporting mechanisms, increasing development time and ongoing maintenance costs.

---

## Part D: Software Construction Challenges

Building and maintaining a large-scale ride-hailing application such as Uber involves several complex software engineering challenges. These challenges arise from the need to support millions of users, operate in real time and continuously evolve the system without disrupting existing services;

1. Scalability and Performance

Uber must handle a very high volume of concurrent users including riders and drivers across multiple regions. The system needs to efficiently process ride requests, driver matching and pricing calculations in real time while maintaining low response times even during peak usage periods.

2. Real-Time Data Handling

The application depends heavily on continuous GPS location updates to track drivers and riders. Managing and synchronizing this real-time data accurately and efficiently is challenging especially when many users are in motion simultaneously.

3. Reliability Under Poor Network Conditions

Users often access the app in areas with unstable or slow internet connections. Ensuring that critical features such as ride requests, navigation and payments function reliably or fail gracefully under such conditions is a significant engineering challenge.

4. Security and Data Privacy

Uber handles sensitive information including user locations, personal details and payment data. Protecting this information from unauthorized access, fraud and data breaches requires strong security mechanisms and continuous monitoring.

5. Payment System Complexity

The app supports multiple payment methods across different countries. Integrating various payment gateways while complying with local financial regulations and ensuring secure and reliable transactions increases system complexity.

6. Maintainability and Continuous Evolution

Uber is constantly updated with new features and improvements. Engineers must design the system in a modular and maintainable way so that new changes do not break existing functionality which requires clean architecture and extensive testing.

7. Cross-Platform Compatibility

The application must provide a consistent user experience across different devices, screen sizes and operating systems such as Android and iOS. Supporting this wide range of platforms increases development and testing effort.

---

## Part E: Group Reflection

One of the most surprising aspects of analyzing this app was the level of complexity that exists behind features that appear simple to users. Actions such as requesting a ride or making a payment seem straightforward on the surface, but they rely on many interconnected systems working together in real time, including location tracking, pricing algorithms, payment processing, and network communication. The group was particularly surprised by how much coordination is required between frontend interfaces, backend services, and external systems to ensure that the app functions reliably and efficiently.

This exercise also helped us understand why writing “working code” is not sufficient for software systems at this scale. In large applications like Uber, code must not only work but also be maintainable, scalable, secure, and resilient to failures. A solution that works for a small number of users may fail when millions of users interact with the system simultaneously. Engineers must therefore consider performance, error handling, future changes, and integration with other components, not just whether the code produces the correct output.

From a teamwork perspective, we learned that effective collaboration is essential when dealing with complex software systems. Different members of the group focused on different aspects of the app, such as features, architecture, and potential challenges, which made it clear that no single person can fully understand or build such a system alone. Clear communication, division of responsibilities, and alignment on shared understanding were key to completing the task successfully. This reflects real-world software development, where teamwork and coordination are just as important as technical skills.

## Contribution Declaration
## Group Member Contributions

| Name               | Responsibility |
|--------------------|----------------|
| Alvin Rubagumya    | Identified and explained key software engineering challenges involved in building and maintaining the Uber application. |
| Agaba Itungo       | Analyzed the Uber app by explaining the problem it solves, identifying its primary users, and outlining its main features. |
| Mark Calvin Obba   | Focused on software change and maintainability by analyzing a change scenario and its impact on the application. |
| Nathaniel Mugenyi | Analyzed what happens behind the scenes for Uber’s features, including the user interface, backend systems, APIs, and data handling. |
| Isooba M Rachel   | Organized, structured, and finalized the `README.md` file on GitHub to ensure clarity, consistency, and completeness. |

