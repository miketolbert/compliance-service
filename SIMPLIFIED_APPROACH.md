# Compliance Service Design (Simplified)

## Compliance Service

This is a new compliance service to modularize the existing code base. Each US state can have its own regulatory and compliance laws, which necessitate runtime injection of logic to map data schema to the expectations and schemas of each marketspace.

### High-Level Design for Simplified Approach

```mermaid
graph TD
    A[User] -->|API Request| B[API Gateway]
    B --> C[Compliance Service - Monolithic Application]

    subgraph Observability
        E[Basic Logging]
        F[Basic Monitoring]
    end

    C --> E
    C --> F
```

```mermaid
graph TD

    subgraph Compliance Service - Monolithic Application
        C1[Compliance Module]
        C2[Configuration Management Module]
        C3[Schema Transformation Module]
        C4[Rule Engine Module]
    end

    C1 --> D[PostgreSQL Database]
    C2 --> D
    C3 --> D
    C4 --> D
```

#### 1. Architecture Overview
- **Monolithic Core with Modular Components**:
  - Develop a monolithic application initially, with clearly defined modules for Compliance Service, Configuration Management, and Schema Transformation. This can be later refactored into microservices as the need arises.
- **Tech Stack**:
  - Use Node.js for the back-end with PostgreSQL for data storage.
  - Deploy on a cloud platform like AWS, using cost-effective services (e.g., AWS RDS for PostgreSQL).

#### 2. Component Breakdown
- **Compliance Module**:
  - Centralize compliance logic in a single module within the monolithic application. This module handles all compliance-related checks and operations, ensuring adherence to state-specific regulations.
- **Configuration Management**:
  - Store compliance rules and configurations in PostgreSQL.
- **Schema Transformation**:
  - Implement transformation logic within the same monolith, but structure it as a separate module.
- **Rules Engine Module**:
  - Embed a rule engine within the monolithic application to evaluate compliance rules.

#### 3. Project Management
- **Phase 1**: Requirement Gathering and Planning
  - **Stakeholder Interviews**: Conduct interviews with stakeholders to gather detailed requirements and understand the compliance needs across different states.
  - **Requirements Documentation**: Document the requirements, including state-specific compliance rules and data schemas.
  - **Architecture Design**: Design the monolithic architecture for the new compliance service, focusing on modularity and clear separation of concerns.

- **Phase 2**: Core Feature Development
  - **Compliance Module**: Implement the core compliance logic within the new monolithic application.
  - **Configuration Management**: Develop a centralized configuration management system within the monolith to store compliance rules and configurations in PostgreSQL.
  - **Schema Transformation**: Implement the schema transformation logic as a separate module within the monolith.
  - **Rules Engine Module**: Embed a rule engine within the monolithic application to evaluate compliance rules and support pluggable rules.

- **Phase 3**: Testing and Deployment
  - **Unit and Integration Testing**: Conduct thorough unit and integration testing for all modules.
  - **Deployment**: Deploy the monolithic application to a cloud environment.

- **Phase 4**: Incremental Improvements
  - **User Feedback**: Gather feedback from users to identify areas for improvement and new feature requests.
  - **Iteration**: Iterate on the product based on user feedback, making necessary adjustments and enhancements.
  - **Refactoring to Microservices**: Gradually refactor monolithic components into microservices as the application grows and the need for independent scaling and deployment arises.

#### 4. Cost-Effective Monitoring and Logging
- Ensure all services are properly monitored and logs are collected for auditing purposes.
- Start with basic logging using existing or built-in tools.
- Implement basic monitoring with tools like AWS CloudWatch.
- Integrate more advanced observability solutions like Datadog as the product and budget allow.

### Conclusion
By starting with a monolithic architecture that is modular, we can quickly develop and deploy the compliance service, and iteratively improve the product. This approach balances the need for speed and cost-efficiency with the ability to scale and adapt the architecture as we grow.