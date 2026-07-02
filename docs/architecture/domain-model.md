# Domain Model

| Document Information | Value |
|----------------------|-------|
| Module | Phase 0.5 - Module A |
| Document ID | DSP-DOM-001 |
| Document Name | Domain Model |
| Project | DevStorm Portfolio Platform |
| Version | 0.1 (Draft) |
| Status | In Progress |
| Author | Kaushik Musale |
| Last Updated | July 2026 |

---

# Revision History

| Version | Date | Description | Author |
|----------|------|-------------|--------|
| 0.1 | July 2026 | Initial domain model | Kaushik Musale |

---

# Table of Contents

1. Purpose
2. Scope
3. Domain Overview
4. Ubiquitous Language
5. Domain Classification
6. Domain Boundaries

---

# 1. Purpose

The Domain Model defines the business concepts, entities, relationships, terminology, and business rules of the DevStorm Portfolio Platform.

Unlike the database design or API specification, this document focuses on the business itself rather than its technical implementation.

It establishes a shared vocabulary that will be used consistently across planning, implementation, testing, and documentation.

---

# 2. Scope

This document covers:

- Business entities
- Domain terminology
- Relationships
- Business rules
- Aggregate boundaries
- Entity lifecycles
- Domain services
- Domain events

This document intentionally excludes implementation details such as database schemas, API endpoints, and frontend components.

---

# 3. Domain Overview

The DevStorm Portfolio Platform is a personal portfolio management system that enables an administrator to manage professional information while allowing visitors to explore projects, technical skills, certifications, reports, and contact details.

The platform is composed of three logical domains.

---

## Portfolio Domain

Responsible for presenting professional achievements and technical work.

Includes:

- Projects
- Skills
- Certifications
- Reports
- Resume
- Technologies
- Categories

---

## Communication Domain

Responsible for interactions between visitors and the portfolio owner.

Includes:

- Contact Messages
- Social Links

---

## Administration Domain

Responsible for authenticated management of platform content.

Includes:

- User
- Authentication
- Content Management
- Dashboard

---

# 4. Ubiquitous Language

The following terminology shall be used consistently throughout the project.

| Term | Meaning |
|------|---------|
| User | Authenticated administrator of the platform |
| Visitor | Unauthenticated person browsing the portfolio |
| Project | A portfolio project showcasing technical work |
| Skill | A technical competency possessed by the administrator |
| Technology | A programming language, framework, tool, or platform associated with a project |
| Category | A logical grouping for projects or reports |
| Certification | A professional or academic certification |
| Report | A cybersecurity write-up or technical article |
| Resume | The administrator's downloadable résumé |
| Contact Message | A message submitted through the contact form |
| Social Link | A link to an external professional profile (LinkedIn, GitHub, etc.) |
| Dashboard | Administrative interface for managing content |

---

# 5. Domain Classification

To simplify architectural reasoning, the domain is divided into three categories.

---

## Core Domain

These entities represent the primary business value of the platform.

- Project
- Skill
- Certification
- Report

---

## Supporting Domain

These entities enrich or organize the core domain.

- Technology
- Category
- Resume
- Social Link
- Contact Message

---

## Generic Domain

These services support the application but do not represent business concepts.

- Authentication
- Authorization
- File Storage
- Logging
- Email Notification
- Configuration

---

# 6. Domain Boundaries

The application is divided into bounded contexts to separate responsibilities.

| Bounded Context | Responsibility |
|-----------------|----------------|
| Portfolio | Manage projects, skills, certifications, reports, and resume |
| Communication | Manage contact messages and social links |
| Administration | Authenticate users and manage protected resources |
| Infrastructure | File storage, logging, email, configuration, and external integrations |

Each bounded context owns its business rules and interacts with other contexts only through well-defined interfaces.

---

# Part Status

| Section | Status |
|----------|--------|
| Document Information | Complete |
| Purpose | Complete |
| Scope | Complete |
| Domain Overview | Complete |
| Ubiquitous Language | Complete |
| Domain Classification | Complete |
| Domain Boundaries | Complete |

---

# 7. Core Domain Entities

Core domain entities represent the primary business value of the DevStorm Portfolio Platform.

---

## 7.1 Project

### Purpose

A Project represents a technical solution, application, research initiative, or cybersecurity activity developed by the portfolio owner.

Projects form the primary showcase of professional experience.

---

### Identity

A Project is uniquely identified by its slug.

Example:

```text
password-strength-checker
```

---

### Responsibilities

- Present technical work
- Showcase technologies used
- Demonstrate practical experience
- Support categorization
- Maintain publication status

---

### Business Attributes

- Title
- Slug
- Description
- Category
- Technologies
- Repository Link
- Live Demo Link
- Featured Status
- Publication Status

---

### Business Invariants

The following rules must always hold:

- A Project shall have exactly one title.
- A Project shall belong to one category.
- A Project may use multiple technologies.
- Slug values must remain unique.
- A published Project must include a description.

---

### Relationships

Project

- belongs to one Category
- references many Technologies
- is managed by one User

---

## 7.2 Skill

### Purpose

A Skill represents a professional competency possessed by the administrator.

---

### Identity

A Skill is uniquely identified by its name.

---

### Responsibilities

- Represent technical expertise
- Support skill categorization
- Display proficiency level

---

### Business Attributes

- Name
- Category
- Proficiency
- Display Order
- Visibility

---

### Business Invariants

- Skill names must be unique.
- Proficiency shall remain within the defined scale.
- Hidden skills shall not appear publicly.

---

### Relationships

Skill

- belongs to one Skill Category
- is managed by one User

---

## 7.3 Certification

### Purpose

A Certification represents formal recognition earned by the administrator.

---

### Identity

Certification Number or Title.

---

### Responsibilities

- Showcase achievements
- Demonstrate professional learning
- Provide verification information

---

### Business Attributes

- Title
- Issuing Organization
- Issue Date
- Expiry Date
- Credential ID
- Verification URL

---

### Business Invariants

- Title is mandatory.
- Issuing organization is mandatory.
- Expiry date, when present, must be later than the issue date.

---

### Relationships

Certification

- belongs to one Organization
- is managed by one User

---

## 7.4 Report

### Purpose

A Report represents technical research, cybersecurity documentation, or professional write-ups authored by the administrator.

---

### Identity

Slug.

---

### Responsibilities

- Publish research
- Demonstrate technical understanding
- Provide downloadable resources

---

### Business Attributes

- Title
- Slug
- Summary
- Category
- Publication Date
- Download URL

---

### Business Invariants

- Every Report shall have a unique slug.
- Every published Report shall include a summary.
- Publication date cannot be in the future.

---

### Relationships

Report

- belongs to one Category
- is authored by one User

---

# 8. Supporting Domain Entities

Supporting entities organize and enrich the Core Domain.

---

## Technology

Represents a programming language, framework, platform, tool, or service used within Projects.

Examples:

- React
- Express.js
- MongoDB
- Docker
- AWS

A Technology may be associated with multiple Projects.

---

## Category

Represents a logical classification for Projects and Reports.

Examples:

- Web Development
- Cybersecurity
- Machine Learning
- Research

A Category may contain many Projects and Reports.

---

## Resume

Represents the administrator's current downloadable résumé.

Business Rules

- Only one active Resume may exist at any time.
- Uploading a new Resume replaces the previous active version.

---

## Social Link

Represents an external professional profile.

Examples:

- GitHub
- LinkedIn
- TryHackMe
- HackerRank
- Medium

Business Rules

- Platform names shall be unique.
- Only active links are displayed publicly.

---

## Contact Message

Represents communication initiated by a Visitor.

Business Attributes

- Name
- Email
- Subject
- Message
- Status
- Created Date

Business Rules

- Email must be valid.
- Empty messages are not permitted.
- Every message begins with the status **New**.

---

# 9. Value Objects

Unlike entities, Value Objects do not possess independent identity.

---

## URL

Used by:

- Repository Link
- Live Demo
- Verification URL
- Social Links

Rules

- Must be a valid HTTPS URL.

---

## Email Address

Used by:

- User
- Contact Message

Rules

- Must follow RFC-compliant email formatting.
- Stored in normalized lowercase format.

---

## Slug

Used by:

- Projects
- Reports

Rules

- Lowercase
- Hyphen-separated
- Unique within its entity type

---

## Proficiency Level

Represents the administrator's competency.

Allowed Values

- Beginner
- Intermediate
- Advanced
- Expert

---

# Part Status

| Section | Status |
|----------|--------|
| Core Domain Entities | Complete |
| Supporting Domain Entities | Complete |
| Value Objects | Complete |

---
# 10. Entity Relationship Matrix

The following matrix describes the business relationships between domain entities.

| Entity | Relationship | Target Entity | Cardinality |
|----------|-------------|---------------|-------------|
| User | manages | Project | One-to-Many |
| User | manages | Skill | One-to-Many |
| User | manages | Certification | One-to-Many |
| User | manages | Report | One-to-Many |
| User | manages | Resume | One-to-One |
| User | manages | Social Link | One-to-Many |
| User | receives | Contact Message | One-to-Many |
| Project | belongs to | Category | Many-to-One |
| Project | references | Technology | Many-to-Many |
| Report | belongs to | Category | Many-to-One |
| Certification | issued by | Organization | Many-to-One |

---

# 11. Aggregate Boundaries

To maintain consistency and transactional integrity, related entities are grouped into aggregates.

Each aggregate has one Aggregate Root responsible for maintaining business rules.

---

## Project Aggregate

### Aggregate Root

Project

### Child Objects

- Technology References

### Responsibilities

- Maintain project information.
- Control publication state.
- Validate associated technologies.

### Transaction Boundary

Creating or updating a Project is performed as a single business transaction.

---

## Skill Aggregate

### Aggregate Root

Skill

### Responsibilities

- Maintain skill information.
- Control visibility.
- Maintain proficiency level.

---

## Certification Aggregate

### Aggregate Root

Certification

### Responsibilities

- Maintain credential information.
- Validate issuing organization.
- Manage verification details.

---

## Report Aggregate

### Aggregate Root

Report

### Responsibilities

- Publish technical content.
- Manage downloadable resources.
- Maintain publication metadata.

---

## Contact Message Aggregate

### Aggregate Root

Contact Message

### Responsibilities

- Receive visitor communication.
- Track processing status.
- Preserve message history.

---

# 12. Ownership Rules

Ownership determines which entity is responsible for lifecycle management.

| Parent | Owns |
|---------|------|
| User | Projects |
| User | Skills |
| User | Certifications |
| User | Reports |
| User | Resume |
| User | Social Links |
| Project | Technology References |
| Category | None |
| Technology | None |

---

## Ownership Principles

- Aggregate Roots control their child objects.
- Child objects shall not modify parent entities directly.
- Business rules are enforced by the Aggregate Root.
- External entities interact only with Aggregate Roots.

---

# 13. Transaction Boundaries

Business operations should execute atomically wherever practical.

---

## Project Creation

Transaction includes:

- Create Project
- Associate Technologies
- Validate Category
- Generate Slug

---

## Certification Creation

Transaction includes:

- Validate issuing organization
- Store certification
- Generate verification metadata

---

## Contact Submission

Transaction includes:

- Validate visitor input
- Store message
- Assign initial status
- Record submission timestamp

---

## Resume Upload

Transaction includes:

- Upload new resume
- Archive previous active resume
- Update active reference

---

# 14. Cross-Aggregate References

Aggregates should reference one another by identity rather than embedding business logic.

---

## Project

References:

- Category
- Technology

Does Not Own:

- Category
- Technology

---

## Report

References:

- Category

Does Not Own:

- Category

---

## Certification

References:

- Organization

Does Not Own:

- Organization

---

## Contact Message

Independent aggregate.

No ownership dependencies.

---

# 15. Business Rules

The following rules apply across multiple entities.

---

## Publication Rules

Only published Projects and Reports are visible to Visitors.

Draft content is accessible only to authenticated administrators.

---

## Resume Rules

Exactly one Resume may be active.

Uploading a new Resume automatically replaces the previously active version.

---

## Technology Rules

A Technology may be referenced by multiple Projects.

Deleting a Technology shall not automatically delete associated Projects.

---

## Category Rules

A Category may organize both Projects and Reports.

Deleting a Category requires reassignment or removal of dependent entities.

---

## Contact Rules

Every Contact Message begins with the status:

```text
New
```

Permitted lifecycle:

```text
New

↓

Read

↓

Replied

↓

Archived
```

Status transitions shall occur only through authenticated administrative actions.

---

## Authentication Rules

Only authenticated administrators may:

- Create content
- Update content
- Delete content
- Upload files
- Manage messages

Visitors have read-only access except for contact form submission.

---

# 16. Domain Invariants

The following conditions must always remain true.

---

## Project

- Slug is unique.
- Title is mandatory.
- Category must exist.
- Publication requires a description.

---

## Skill

- Name is unique.
- Proficiency must be valid.

---

## Certification

- Issue date precedes expiry date.
- Title is mandatory.

---

## Report

- Slug is unique.
- Published reports include summaries.

---

## Resume

- Exactly one active resume exists.

---

## Contact Message

- Email is valid.
- Message content is not empty.
- Initial status is "New".

---

# Part Status

| Section | Status |
|----------|--------|
| Entity Relationship Matrix | Complete |
| Aggregate Boundaries | Complete |
| Ownership Rules | Complete |
| Transaction Boundaries | Complete |
| Cross-Aggregate References | Complete |
| Business Rules | Complete |
| Domain Invariants | Complete |

---

