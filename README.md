Event Board
A web application for managing events and participant registrations.

Built with Java 21, Servlets, JSP, JDBC, and PostgreSQL. No frameworks.

Features
Create upcoming events with a title, date, and seat limit
View all upcoming events with registration counts
Register students for events by name and email
Duplicate email and no-seats-available protection
Tech Stack
Java 21
Jakarta Servlet API 6.0 (Tomcat 10.1+)
JSP + JSTL 3.0
JDBC (plain, no ORM)
PostgreSQL
Maven
Prerequisites
Java 21+
Maven 3.6+
PostgreSQL (any recent version)
Apache Tomcat 10.1+
Setup
1. Create the database
   In pgAdmin or psql, create a database named event_board, then run the schema:

-- src/main/resources/schema.sql
Or run it directly:

psql -U postgres -d event_board -f src/main/resources/schema.sql
2. Configure the database connection
   Edit src/main/resources/database.properties:

db.url=jdbc:postgresql://localhost:5432/event_board
db.username=postgres
db.password=your_password
db.driver=org.postgresql.Driver
3. Build
   mvn package
   This produces target/event-board.war.

4. Deploy to Tomcat
   Copy the WAR to Tomcat's webapps folder:

# Linux / Mac
cp target/event-board.war /path/to/tomcat/webapps/

# Windows (PowerShell)
copy target\event-board.war "C:\Program Files\Apache Software Foundation\Tomcat 10.1\webapps\"
Then start (or restart) Tomcat.

5. Open the app
   http://localhost:8080/event-board/events
   Project Structure
   src/
   ├── main/
   │   ├── java/com/example/eventboard/
   │   │   ├── com.example.eventboard.config/        # DB connection (ConnectionFactory, DatabaseConfig)
   │   │   ├── com.example.eventboard.controller/    # Servlets (EventsServlet, EventServlet)
   │   │   ├── com.example.eventboard.exception/     # Business exceptions
   │   │   ├── com.example.eventboard.model/         # Event, Participant, EventDetails, EventSummary
   │   │   ├── com.example.eventboard.repository/    # JDBC repositories
   │   │   └── com.example.eventboard.service/       # EventService (business logic)
   │   ├── resources/
   │   │   ├── database.properties
   │   │   └── schema.sql
   │   └── webapp/
   │       ├── WEB-INF/
   │       │   ├── views/     # JSP pages (events.jsp, event.jsp)
   │       │   └── web.xml
   │       └── assets/css/
   └── test/
   └── java/              # EventServiceTest (JUnit 5 + Mockito)
   Running Tests
   mvn test