# TicketRush

High-concurrency ticket booking platform: Spring Boot, Angular, PostgreSQL, Redis, Kafka.

**Status:** Session S1 in progress (repository, skeleton and containers).

## Planned features
- Browse and search events, view a seat map
- Hold seats with expiry, pay, receive an e-mail ticket
- Roles: customer, organizer, admin
- Building the backend image by docker build -t ticketrush-backend ./backend


## How to run backend 
1]Either run using the intellij run button or using spring boot:run
2]then open http://localhost:8080/actuator/health for verifying
-We can run the backed image -> docker run --rm -p 8080:8080 ticketrush-backend
-docker run --rm --entrypoint id ticketrush-backend then to check open [2] step.
