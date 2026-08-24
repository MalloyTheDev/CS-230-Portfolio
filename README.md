# CS 230 Portfolio

## Draw It or Lose It

This repository contains my completed software design document for The Gaming Room project in CS 230.

### Project File

* [CS 230 Software Design Document](CS-230-Software-Design-Document.docx)

## Reflection

### Briefly summarize The Gaming Room client and their software requirements. Who was the client? What type of software did they want you to design?

The Gaming Room was the client for this project. The company already had an Android game called Draw It or Lose It and wanted to expand it into a distributed web application that could run through browsers on Windows, macOS, Linux, iOS, and Android. The game needed to support multiple teams and players, keep every game, team, and player name unique, control the rounds and drawing timers from the server, and eventually support thousands of users at the same time. The design also needed to account for security, reliable communication, storage for the drawing library, accessibility, and different screen sizes.

### What did you do particularly well in developing this documentation?

I think I did particularly well at connecting the client's requirements to specific design decisions instead of only comparing operating systems in general terms. For example, I explained why Linux was the strongest server platform for the Java application, why the browser client should stay lightweight, and why the server has to be the authority for timing, scoring, and unique identifiers. I also explained the relationships between `GameService`, `Game`, `Team`, `Player`, and `Entity` in the UML diagram and connected those relationships to inheritance, encapsulation, composition, and the singleton pattern used in the code.

### What about the process of working through a design document did you find helpful when developing the code?

The design document made me slow down and decide what each part of the application was responsible for before treating the program as one large block of code. Mapping the domain model showed where shared behavior belonged in `Entity` and where collection management belonged in `GameService`, `Game`, and `Team`. It also exposed a limitation that is easy to miss while only looking at a small local program: a singleton controls one Java process, but it does not create one shared state across several application servers. Finding that during the design stage makes it possible to plan the database and distributed state correctly before the code becomes harder to change.

### If you could choose one part of your work on these documents to revise, what would you pick? How would you improve it?

I would revise the platform evaluation section. The information is useful, but the table became dense because each cell covers hosting, development tools, testing, staffing, and cost. I would split it into a shorter decision matrix with the same criteria for every platform, then move the detailed reasoning into smaller sections below it. I would also attach direct citations to current vendor documentation for licensing and support details because those facts can change over time.

### How did you interpret the user's needs and implement them into your software design? Why is it so important to consider the user's needs when designing?

I treated cross-platform support as a user experience requirement, not just a list of operating systems. Players should be able to open the game in a browser without installing a different native application for every device. That led to a responsive HTML, CSS, and JavaScript client backed by a centralized Java service. I kept game state and timing on the server so a slow connection, browser refresh, or modified client could not control the result of a round. I also planned for HTTPS, secure WebSockets, shared storage, automatic reconnection, and accessible layouts because those details directly affect whether the game is fair and usable. Considering the user's needs is important because technically correct software can still fail if it is confusing, unreliable, inaccessible, or inconsistent across the devices people actually use.

### How did you approach designing software? What techniques or strategies would you use in the future to analyze and design a similar software application?

I started with the client's rules and converted them into functional requirements, constraints, and responsibilities. From there, I modeled the main objects and their relationships, compared the available platforms, selected a layered architecture, and then worked through storage, memory, networking, scaling, and security. For a similar project in the future, I would keep that requirements-first approach while adding a traceability matrix that connects every requirement to a design decision and a planned test. I would also use sequence diagrams for the timed round and reconnect flows, build a basic threat model, record capacity assumptions, and create a small prototype for the highest-risk parts before committing to the full implementation.
