# 1. Research on how they use Microservices at Netflix and how it works for them
## Microservices at Netflix
### Introduction

Microservices are a software architecture style in which a large application is divided into many small, independent services. Each service performs a specific function and communicates with other services through Application Programming Interfaces (APIs). This approach closely relates to the SOLID principles of object-oriented design, which are guidelines used to create software that is easier to maintain, extend, and manage. In a microservices architecture, each service is independent and focused on a single responsibility, which aligns with the Single Responsibility Principle (SRP) of SOLID. Communication between services occurs through well-defined interfaces such as APIs, allowing systems to be modified, updated, or extended without significantly affecting other parts of the application.

Netflix originally used a monolithic architecture, where the entire system was built as a single large application. However, as the platform grew to support millions of users streaming content simultaneously, the monolithic system became difficult to scale and maintain. To address this challenge, Netflix migrated to a microservices architecture, where the platform is composed of hundreds of small services working together. This design enables Netflix to scale individual components independently, deploy updates more efficiently, and maintain high system reliability.

How Netflix Microservices Work

Netflix’s platform is built as a collection of independent microservices that communicate with each other through APIs. Each microservice is responsible for handling a specific function within the system. Some of these services include authentication services, recommendation services, search services, and streaming services.

When a user interacts with Netflix, such as opening the app or selecting a movie to watch, the request is sent to Netflix’s servers. The request is first handled by an API gateway, which routes the request to the appropriate microservice. For example, if a user searches for a movie, the request is directed to the search service. If the user presses play, the request is directed to the streaming service.

These services may also communicate with other services to complete the request. For example, when a user plays a movie, the authentication service verifies the user’s identity, the data service retrieves movie information, and the streaming service delivers the video content. Each service performs its specific task and contributes to the final response sent back to the user.

### How Netflix Microservices Work

Netflix’s platform is built as a collection of independent microservices that communicate with each other through Application Programming Interfaces (APIs). Each microservice is responsible for handling a specific function within the system. This separation of responsibilities allows each service to operate independently and be developed, deployed, and scaled without affecting other services. Some of these services include authentication services, recommendation services, search services, payment services, and streaming services.

When a user interacts with Netflix, such as opening the application, browsing movies, or selecting a movie to watch, the request is sent from the user’s device to Netflix’s servers through the internet. The request is first handled by an API gateway, which acts as the entry point for all client requests. The API gateway is responsible for routing requests to the appropriate microservice, as well as handling tasks such as load balancing, security, and request filtering.

Once the request reaches the API gateway, it is forwarded to the correct microservice depending on the type of action the user is performing. For example, if a user searches for a movie or TV show, the request is directed to the search service, which processes the search query and retrieves relevant results from the database. If the user logs into the platform, the request is handled by the authentication service, which verifies the user’s identity and grants access to the platform.

If a user presses the play button to watch a movie, multiple microservices work together to complete the request. First, the authentication service confirms that the user is logged in and has permission to access the content. The system then retrieves information about the movie from the content or metadata service, such as the movie title, description, and available video files. At the same time, the recommendation service may record the viewing activity to improve future recommendations for that user.

After the necessary information has been retrieved, the streaming service is responsible for delivering the video content to the user’s device. This service ensures that the video is streamed smoothly by adjusting the video quality based on the user’s internet connection. The video is typically delivered through a content delivery network (CDN), which helps distribute the content efficiently across different geographic regions.

Throughout this process, microservices communicate with each other using APIs, allowing them to exchange information and coordinate tasks. Because each microservice performs a specific function, failures in one service are less likely to affect the entire system. This modular structure allows Netflix to maintain high reliability while supporting millions of users streaming content simultaneously around the world.

### How Netflix Manages Its Microservices
To effectively manage this architecture, Netflix developed and uses several specialized tools and technologies that help coordinate communication between services, route requests, and ensure that the system operates reliably.

One of the key tools used by Netflix is Zuul, which acts as an API Gateway. The API gateway serves as the main entry point for all client requests coming from user devices such as smartphones, smart TVs, or web browsers. Instead of allowing users to communicate directly with individual microservices, all requests pass through Zuul first. Zuul is responsible for routing incoming requests to the correct microservice based on the type of request being made. In addition to request routing, Zuul also performs important tasks such as load balancing, security filtering, authentication checks, and monitoring traffic. This helps ensure that the system remains secure and that no single service becomes overloaded with requests.

Another important tool used in Netflix’s microservices architecture is Eureka, which functions as a service discovery system. In a microservices environment, services may frequently start, stop, or change locations as the system scales or updates are deployed. Because of this, it would be difficult for services to keep track of where other services are located. Eureka solves this problem by acting as a central registry where all microservices register themselves when they start running. Other services can then query Eureka to find the location of the service they need to communicate with. This allows services to dynamically discover and communicate with each other without needing hard-coded addresses, making the system more flexible and scalable.

Netflix also uses Conductor, which is a workflow orchestration tool designed to manage complex operations that require multiple microservices to work together. In many situations, completing a single task may involve several services working in sequence or in parallel. Conductor coordinates these processes by defining workflows that specify how different services should interact and in what order tasks should be executed. For example, when a user interacts with Netflix, multiple services such as authentication, user profile management, recommendation engines, and streaming services may need to work together to deliver the final result. Conductor helps manage these interactions, ensuring that tasks are executed correctly and efficiently.

Together, tools such as Zuul, Eureka, and Conductor allow Netflix to effectively manage its large microservices ecosystem. These technologies help maintain system reliability, support scalability, and enable seamless communication between hundreds of independent services operating within the Netflix platform.

### Benefits of Microservices for Netflix

One major advantage of microservices is scalability. Since each service operates independently, Netflix can scale only the services that experience high demand. For example, the streaming service can be scaled during peak viewing hours without affecting other services.

Another advantage is fault isolation. If one service fails, the rest of the system can continue functioning. For instance, if the recommendation service encounters an issue, users can still watch movies.

Microservices also support faster development and deployment. Different teams can work on different services simultaneously, allowing Netflix to release updates more frequently without affecting the entire system.

### Challenges of Microservices

Despite their benefits, microservices also introduce challenges. Managing a large number of independent services can increase system complexity. Communication between services may also introduce latency, and maintaining data consistency across multiple services can be difficult.

Netflix addresses these challenges by using monitoring systems, automation tools, and orchestration technologies to manage and coordinate its services effectively.

# 2. Find out other 2 companies that use Microservices and how it is working for them.

## 1. M-Pesa (Safaricom – Kenya)

M-Pesa is one of the most widely used mobile money platforms in Africa. It allows users to send and receive money, pay bills, and perform financial transactions using their mobile phones. The platform has become a core part of the digital economy in Kenya and other African countries.

Modern digital platforms built around M-Pesa rely heavily on APIs and modular system architectures to process payments and communicate with other services. APIs act as the connection layer between mobile applications, payment providers, and enterprise systems such as banking platforms and accounting software.

Safaricom introduced the Daraja API platform, which allows developers and businesses to integrate their systems directly with M-Pesa. Through this system, businesses can automate transactions such as customer-to-business payments, automated payouts, and transaction status checks.

Modern payment systems that integrate with M-Pesa often use microservice-based architectures where the payment logic is separated into independent services. For example, systems may include a dedicated payment service that communicates with M-Pesa while other services handle user accounts, order processing, and notifications.

#### How microservices help M-Pesa-based systems

Scalability: Systems can process millions of transactions without overloading one component.

Flexibility: Businesses can integrate additional payment providers or financial services easily.

Reliability: Payment services can operate independently from other parts of the system.

## 2. SafeBoda (Uganda)

SafeBoda is a Ugandan technology company that provides ride-hailing and delivery services through a mobile application. The platform connects passengers with motorcycle taxi drivers and offers additional services such as digital payments and deliveries.

Behind the SafeBoda platform is a modern backend architecture composed of multiple services and APIs that support different parts of the application, including ride matching, payments, driver management, and user accounts. Some backend systems are implemented as microservices built using technologies such as Node.js and Elixir.

These microservices handle different responsibilities within the platform. For example:

1. Ride booking service

2. Driver management service

3. Payment service

4. Location and tracking service

5. User account service

Because each service operates independently, the platform can handle large numbers of users requesting rides at the same time while maintaining system reliability.

**How microservices help SafeBoda**
1. Independent scaling: Services such as ride matching or payment processing can scale depending on demand.

2. Faster development: Engineers can update or improve individual services without affecting the entire platform.

3. Reliability: If one service experiences problems, the rest of the application can continue operating.

This microservices approach enables SafeBoda to manage a complex platform that connects thousands of drivers and passengers across cities in East Africa.

These examples show that microservices and API-based architectures are widely used not only by global companies like Netflix but also by African technology platforms

# 3.Find out other 2 companies that were using Microservices but later turned back to monolith and why they went back to it.

## 1. Amazon Prime Video

Amazon Prime Video originally used a large number of microservices to manage different parts of its video streaming platform. These microservices handled tasks such as video analysis, encoding, quality checks, and content monitoring.

However, engineers later realized that this architecture introduced high operational costs and unnecessary complexity. Each microservice required its own infrastructure, communication mechanisms, and monitoring systems. Because the services had to communicate with each other through network calls and cloud services, the system became expensive to run and difficult to manage.

To address these issues, Amazon engineers redesigned part of the system by moving from many microservices to a more centralized monolithic architecture. Instead of separate services communicating through remote calls, several components were combined into a single application.

Reasons they moved back toward a monolith

Reduced infrastructure costs (fewer cloud services and network calls)

Lower system complexity

Improved performance because internal function calls replaced network communication

Simpler system maintenance

This change reportedly reduced operating costs significantly while still maintaining the functionality required by the platform.

## Segment

Segment, now part of Twilio, is a customer data platform that helps organizations collect, process, and route customer data to analytics and marketing tools. As the platform expanded, the engineering team adopted a microservices architecture in which many independent services handled tasks such as event collection, data processing, integrations, and storage.

Over time, however, the system grew to more than 140 microservices, which created significant operational challenges. Managing such a large number of distributed services introduced complexity in deployment, monitoring, and debugging. According to the Segment engineering team, the architecture that was supposed to help the company move faster instead created serious difficulties. Engineers reported that much of their time was spent troubleshooting issues between services rather than building new features. As they explained, the team became “mired in exploding complexity,” where development velocity decreased while the number of defects increased.

To address these challenges, Segment made the decision to collapse the 140+ microservices into a single monolithic architecture. By consolidating the services into one monolith, the system became significantly simpler to manage. The impact of this change was immediate. Test suites that previously took about an hour to complete were reduced to milliseconds, and developer productivity improved significantly. The engineering team reported shipping 46 improvements to shared libraries within a year, compared to 32 improvements during the microservices period.

### Reasons Segment moved back to a monolith

1. Operational complexity from managing over 140 microservices

2. Reduced development velocity due to constant troubleshooting between services

3. High defect rates caused by complex service interactions

4. Improved performance and productivity after consolidating into a monolithic system

This case demonstrates that while microservices can provide scalability and flexibility, they can also introduce significant complexity. In some cases, moving back to a well-designed monolithic architecture can improve system performance, developer productivity, and maintainability.
