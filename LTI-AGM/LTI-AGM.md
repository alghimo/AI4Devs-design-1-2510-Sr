# LTI - Applicant Tracking System (ATS)

## 1. Description & Value Proposition

### Brief Description
LTI is a next-generation Applicant Tracking System (ATS) designed to revolutionize the recruitment process. It leverages advanced AI and automation to streamline workflows, enhance collaboration between recruiters and hiring managers, and significantly reduce time-to-hire while improving the quality of hires.

### Value Added & Competitive Advantages
-   **AI-Driven Efficiency**: Automates repetitive tasks like resume screening, scheduling, and candidate communication, allowing HR teams to focus on strategic decision-making.
-   **Real-Time Collaboration**: A unified platform where recruiters and managers can collaborate seamlessly, share feedback instantly, and make data-driven hiring decisions together.
-   **Smart Matching Engine**: Utilizes AI to match candidates to job descriptions with high accuracy, reducing the time spent on manual screening.
-   **User-Centric Design**: A modern, intuitive interface that requires minimal training and provides a superior user experience for both recruiters and candidates.

### Main Features
1.  **Smart Job Posting**: Create and distribute job openings across multiple channels with AI-assisted description writing.
2.  **Candidate Matching Engine**: Automatically ranks candidates based on skills, experience, and cultural fit using AI algorithms.
3.  **Collaborative Hiring Portal**: A shared workspace for recruiters and managers to review profiles, leave comments, and rate candidates in real-time.
4.  **Automated Workflows**: Custom triggers for email notifications, interview scheduling, and status updates.
5.  **Analytics Dashboard**: Real-time insights into the hiring pipeline, time-to-hire, and source effectiveness.

## 2. Lean Canvas

### Mermaid Diagram
```mermaid
block-beta
  columns 5
  block:Problem
    P1["Inefficient HR workflows"]
    P2["Poor collaboration"]
    P3["Manual screening"]
  end
  block:Solution
    S1["AI Automation"]
    S2["Real-time Portal"]
    S3["Smart Matching"]
  end
  block:Value
    V1["Reduce time-to-hire"]
    V2["Improve hire quality"]
    V3["Seamless collaboration"]
  end
  block:Advantage
    A1["AI-first approach"]
    A2["Superior UX"]
  end
  block:Customer
    C1["HR Departments"]
    C2["Recruitment Agencies"]
    C3["Hiring Managers"]
  end

  P1 --> S1
  P2 --> S2
  P3 --> S3

  S1 --> V1
  S2 --> V3
  S3 --> V2
```

### Lean Canvas Table

| Section | Description |
| :--- | :--- |
| **Problem** | 1. Inefficient manual workflows in HR departments.<br>2. Lack of real-time collaboration between recruiters and hiring managers.<br>3. Time-consuming manual candidate screening. |
| **Solution** | 1. AI-driven automation for repetitive tasks.<br>2. A unified collaborative portal for real-time feedback.<br>3. Smart Candidate Matching Engine. |
| **Unique Value Proposition** | The ATS that empowers HR teams to hire faster and better through AI automation and seamless collaboration, turning recruitment into a strategic advantage. |
| **Unfair Advantage** | Proprietary AI matching algorithms and a "collaboration-first" design philosophy that competitors lack. |
| **Customer Segments** | 1. Mid-to-large sized companies with internal HR departments.<br>2. Recruitment agencies looking for efficiency.<br>3. Fast-growing startups needing scalable hiring solutions. |
| **Key Metrics** | 1. Time-to-Hire.<br>2. Cost-per-Hire.<br>3. Candidate Satisfaction Score (NPS).<br>4. Recruiter/Manager Collaboration Index. |
| **Channels** | 1. Direct Sales (B2B).<br>2. Digital Marketing (LinkedIn, SEO).<br>3. Partnerships with HR consultancies. |
| **Cost Structure** | 1. Software Development & Maintenance.<br>2. AI Model Training & Hosting.<br>3. Sales & Marketing expenses.<br>4. Customer Support. |
| **Revenue Streams** | 1. SaaS Subscription (Monthly/Yearly per user).<br>2. Enterprise Licensing.<br>3. Premium AI Features Add-on. |

## 3. Functional Design (Use Cases)

### Use Case 1: Job Posting Creation
**Actor**: Recruiter / Hiring Manager
**Description**: The user creates a new job posting, utilizing AI to generate the job description, and publishes it to multiple job boards.

```mermaid
sequenceDiagram
    actor User as Recruiter
    participant FE as Frontend
    participant BE as Backend Service
    participant AI as AI Service
    participant DB as Database
    participant Ext as Job Boards

    User->>FE: Click "Create Job"
    FE->>User: Show Job Form
    User->>FE: Enter Job Title & Keywords
    User->>FE: Click "Generate Description"
    FE->>BE: Request AI Description
    BE->>AI: Generate Description Prompt
    AI-->>BE: Generated Text
    BE-->>FE: Return Description
    FE->>User: Show Generated Description
    User->>FE: Edit & Confirm
    User->>FE: Click "Publish"
    FE->>BE: Submit Job Posting
    BE->>DB: Save Job Data
    BE->>Ext: Publish to Job Boards
    Ext-->>BE: Confirmation
    BE-->>FE: Success Message
    FE-->>User: Show "Job Published"
```

### Use Case 2: Candidate Application & Parsing
**Actor**: Candidate
**Description**: A candidate applies for a job, and the system automatically parses their resume to extract structured data.

```mermaid
flowchart TD
    A[Candidate] -->|Uploads Resume| B(Application Portal)
    B -->|Submit Application| C{Resume Parser Service}
    C -->|Extract Info| D[Structured Data]
    D -->|Save Profile| E[(Database)]
    C -->|Error| F[Manual Entry Request]
    E --> G[Application Received Email]
    G --> A
```

### Use Case 3: AI Candidate Matching
**Actor**: Recruiter
**Description**: The system automatically ranks candidates for a specific job based on the match between their profile and the job requirements.

```mermaid
sequenceDiagram
    actor Recruiter
    participant FE as Dashboard
    participant BE as Matching Engine
    participant DB as Database
    participant AI as AI Model

    Recruiter->>FE: View Job Details
    FE->>BE: Request Candidate Matches
    BE->>DB: Fetch Job Requirements
    BE->>DB: Fetch Candidates
    loop For each Candidate
        BE->>AI: Compare Profile vs Job
        AI-->>BE: Match Score & Rationale
    end
    BE->>BE: Sort by Score
    BE-->>FE: Return Ranked List
    FE-->>Recruiter: Display Ranked Candidates
```

## 4. Technical Design

### 4.1 Data Model

The data model is designed to support the core tracking and matching capabilities of the ATS.

```mermaid
erDiagram
    COMPANY ||--|{ JOB : posts
    JOB ||--|{ APPLICATION : receives
    CANDIDATE ||--|{ APPLICATION : submits
    CANDIDATE ||--o{ SKILL : has
    JOB ||--o{ SKILL : requires
    USER ||--|{ COMMENT : writes
    APPLICATION ||--|{ COMMENT : has
    APPLICATION ||--|{ INTERVIEW : schedules

    COMPANY {
        uuid id PK
        string name
        string industry
        string size
    }

    JOB {
        uuid id PK
        uuid company_id FK
        string title
        text description
        string status
        datetime created_at
    }

    CANDIDATE {
        uuid id PK
        string first_name
        string last_name
        string email
        string phone
        string resume_url
        string linkedin_url
    }

    APPLICATION {
        uuid id PK
        uuid job_id FK
        uuid candidate_id FK
        string status
        float match_score
        datetime applied_at
    }

    SKILL {
        uuid id PK
        string name
        string category
    }

    USER {
        uuid id PK
        string email
        string role
    }
```

### 4.2 High-Level System Design

The system follows a **Modular Monolith** architecture with a clear separation between the Frontend (Web App) and the Backend (API). The Backend is structured using **Hexagonal Architecture** and **Vertical Slicing** to ensure maintainability and scalability.

**Components:**
1.  **Web App (SPA)**: React/Next.js application serving as the single frontend for all user roles (Recruiters, Managers, Candidates).
2.  **API Gateway / Load Balancer**: Entry point for SSL termination and routing.
3.  **LTI API (Modular Monolith)**: The core application containing all business logic, organized by features (Vertical Slices).
4.  **Database**: PostgreSQL for relational data.
5.  **Object Storage**: S3 for resumes and documents.
6.  **External Services**: Integrations with Job Boards, Email Providers, etc.

```mermaid
architecture-beta
    group client(cloud)[Client]
    service web(internet)[WebApp] in client

    group backend(cloud)[Backend]
    service api(server)[LTI_API] in backend

    group data(database)[Data]
    service db(database)[PostgreSQL] in data
    service s3(disk)[Object_Storage] in data

    web:R -- L:api
    api:B -- T:db
    api:B -- T:s3
```

### 4.3 C4 Component Diagram: LTI API (Hexagonal Architecture)

This diagram illustrates the internal structure of the **LTI API**, following **Hexagonal Architecture (Ports & Adapters)** and **Vertical Slicing**. The application is divided into feature modules (Slices), each containing its own domain logic, ports, and adapters.

**Key Concepts:**
-   **Vertical Slicing**: Code is organized by feature (e.g., `JobPosting`, `CandidateMatching`) rather than technical layer.
-   **Screaming Architecture**: Folder/Component names clearly indicate what the system *does*.
-   **Hexagonal**: Domain logic is isolated from external concerns (Database, API, AI Services) via Ports and Adapters.

```mermaid
C4Component
    title Component Diagram - LTI API (Hexagonal Structure)

    Container(web_app, "Web App", "React/Next.js", "Frontend Client")

    Container_Boundary(api_boundary, "LTI API (Modular Monolith)") {

        Component(api_driver, "API Driver (Primary Adapter)", "REST/GraphQL Controllers", "Handles HTTP requests")

        Boundary(slice_job, "Feature: Job Posting") {
            Component(job_service, "Job Service (Domain)", "Business Logic", "Manages job creation & publishing")
            Component(job_port, "Job Repository Port", "Interface", "Defines data access contract")
        }

        Boundary(slice_match, "Feature: Candidate Matching") {
            Component(match_service, "Matching Service (Domain)", "Business Logic", "Orchestrates AI matching")
            Component(match_port, "Matching Port", "Interface", "Defines AI service contract")
        }

        Component(db_adapter, "Persistence Adapter (Secondary)", "ORM/SQL", "Implements Repository Ports")
        Component(ai_adapter, "AI Adapter (Secondary)", "Python Client", "Connects to AI Models")
    }

    ContainerDb(db, "PostgreSQL", "Relational DB", "Stores all application data")
    System_Ext(ai_model, "AI Model", "External/Internal AI Service")

    Rel(web_app, api_driver, "Uses", "JSON/HTTPS")

    Rel(api_driver, job_service, "Invokes")
    Rel(api_driver, match_service, "Invokes")

    Rel(job_service, job_port, "Uses")
    Rel(match_service, match_port, "Uses")

    Rel(db_adapter, job_port, "Implements")
    Rel(ai_adapter, match_port, "Implements")

    Rel(db_adapter, db, "Reads/Writes")
    Rel(ai_adapter, ai_model, "Inferences")
```
