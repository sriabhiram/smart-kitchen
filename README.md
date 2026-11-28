# smart-kitchen
# SmartLunch AI

An open-source and hosted platform for school lunch providers and small cloud kitchens.

SmartLunch AI helps food providers manage meal plans, recurring subscriptions, menus, kitchen operations, and customer communication. It is designed to combine straightforward operational workflows with an AI assistant that helps parents and kitchen teams complete tasks more easily.

The project has two goals:

* Real business: Validate and develop a practical product for food providers, beginning with school lunch providers.
* Open-source community: Build a useful, extensible core that developers and operators can self-host, customise, and contribute to.

Project status: Early development. Product requirements, architecture, and initial implementation are being developed. This project is not yet production-ready.

Why SmartLunch AI?

Meal providers often coordinate subscriptions, menu changes, pauses, payments, delivery locations, and daily meal counts through spreadsheets, messaging apps, and manual processes.

SmartLunch AI aims to bring these workflows into one system, while keeping operational decisions and safety checks under the control of the backend.

The initial focus is on small providers where a simple, affordable system can reduce administrative effort without requiring a large technology team.

Initial target customers

First focus: School lunch providers

The first version will prioritise providers serving school students, including workflows such as:

* Parent and student/meal-recipient management
* School and delivery-location management
* Weekly menus and meal plans
* Recurring subscriptions and meal changes
* School-wise and day-wise kitchen counts
* Allergy declarations and acknowledgement records
* Parent communication and operational reports

Next segment: Small cloud kitchens

After validating the school lunch workflows, the platform can expand to small cloud kitchens offering recurring meal subscriptions.

The design will avoid making every customer or meal recipient dependent on a school-specific model. Generic customers, meal recipients, kitchens, and delivery destinations can support additional business types over time.

Product goals

* Make meal subscriptions and changes easier for parents and customers.
* Help providers plan menus and prepare accurate daily meal quantities.
* Reduce manual coordination and repetitive administrative work.
* Provide clear records for payments, subscription changes, and operational actions.
* Offer an AI assistant for supported questions and tasks.
* Support self-hosted deployments as well as a managed hosted service.

Planned features

Customer and recipient management

* Customer/parent profiles
* Multiple meal recipients per customer
* Schools and delivery locations
* Food preferences and structured allergy declarations
* Role-based access for business staff

Menus and meal plans

* Weekly menus
* Meal plans and pricing
* Menu items and food categories
* Availability and ordering cut-off times

Subscription management

* Weekly or monthly subscriptions
* Recurring meal schedules
* Pause, skip, and cancellation workflows
* Renewal and subscription history
* Confirmation before creating or changing a subscription

Kitchen operations

* Daily meal counts
* School-wise or delivery-location-wise packing lists
* Kitchen reports
* Allergy alerts and acknowledgement records
* Operational audit history

Payments and notifications

* Planned Razorpay integration
* Payment history and reconciliation
* Verified payment webhooks
* In-app notifications and Web Push
* Optional email notifications

AI assistant

The assistant is intended to help customers and operators interact with the platform using conversational language.

Possible use cases include:

* Answering questions about menus and meal plans
* Helping a parent navigate subscription options
* Preparing a subscription change for confirmation
* Answering supported operational questions
* Helping kitchen staff retrieve reports

The AI assistant will use controlled backend tools. It will not independently determine payment success, pricing, delivery eligibility, or allergy safety. The backend remains responsible for validating business rules, and actions that affect subscriptions require appropriate confirmation.

Product principles

1. Backend-enforced business rules: The backend validates prices, eligibility, subscription changes, and operational actions.
2. AI with controlled permissions: AI can assist through approved tools, but does not directly access the database or bypass validation.
3. Explicit confirmation: Parents or authorised users must confirm subscription creation or significant changes.
4. Safety and traceability: Allergy declarations, acknowledgements, payment events, and important actions should have appropriate records.
5. Privacy by design: Collect only necessary personal information and apply access controls, retention, and deletion policies.
6. Start small: Build a modular monolith and validate workflows before introducing complex infrastructure.

Architecture

The initial architecture is a modular monolith. This keeps development and deployment manageable while allowing the codebase to grow into separate services later if there is a demonstrated need.

Planned technology stack

Area	Planned technology
Parent and provider interface	React, TypeScript, Vite, Material UI
Backend API	Python, FastAPI, Pydantic
Database access	SQLAlchemy 2.x, Alembic
Database	PostgreSQL, initially through Supabase
AI integration	OpenAI API; LangGraph introduced when useful
Tool integration	Backend tools first; MCP considered later
Payments	Razorpay
Notifications	In-app notifications, Web Push, optional email
Initial scheduled tasks	APScheduler
Testing	Pytest, HTTPX, Playwright
Packaging and deployment	Docker, GitHub Actions; hosted frontend and backend

Technology choices may evolve as the project is implemented and validated.

Multi-tenant design

SmartLunch AI is intended to support multiple independent food businesses.

The planned data model includes:

* Organisations: Business or tenant accounts
* Kitchens: One or more kitchens belonging to an organisation
* Users and memberships: Login identities and their organisation roles
* Customers and meal recipients: Parents/customers and the people receiving meals
* Schools and delivery locations: Places where meals are delivered
* Menus and plans: Available meals and subscription offerings
* Subscriptions: Recurring meal arrangements and scheduled days
* Payments and payment events: Payment records and verified provider events
* Delivery records: Delivery eligibility and operational fulfilment
* Allergy declarations and acknowledgements: Structured declarations and audit history
* Notifications and audit logs: Communication records and important actions

Business-owned records will be scoped to an organisation. The backend must derive the organisation context from the authenticated user’s membership rather than trusting an organisation ID supplied by the frontend.

Tenant isolation will be covered by tests to ensure one organisation cannot access another organisation’s customers, recipients, subscriptions, or payment records.

Security and privacy

Security and privacy are core requirements, not optional later enhancements.

Planned safeguards include:

* Authentication and role-based access control
* Organisation-level data isolation
* Server-side validation of all business operations
* Verified and idempotently processed payment webhooks
* No storage of payment card details
* Audit records for important operational actions
* Secure configuration through environment variables
* No secrets committed to the repository
* Appropriate data minimisation, retention, and deletion practices

Before commercial deployment in India, the project must be reviewed for applicable requirements, including the Digital Personal Data Protection framework and its applicable commencement rules, and relevant FSSAI licensing obligations. This README is not legal or regulatory advice.

Open-source and business model

The intended model is open-source core plus commercial hosted services and support.

Community Edition

The planned self-hosted edition will provide the core application and basic workflows. Operators can deploy and customise it themselves and supply their own credentials for external services.

SmartLunch Cloud

A potential paid hosted offering may include:

* Managed hosting and database
* Backups, monitoring, and updates
* Managed notification infrastructure
* Managed AI usage
* Easier onboarding and operational support

Business and enterprise services

Potential paid services include custom integrations, multi-kitchen configuration, reporting, deployment assistance, training, and support.

The initial commercial model will favour a predictable subscription or service fee rather than a transaction percentage, subject to customer validation.

Licence

The planned licence is Apache License 2.0, subject to legal review and confirmation before public release.

Apache 2.0 supports broad use and commercial reuse. The hosted service’s value would come from reliability, managed operations, support, integrations, and ongoing product development—not from restricting use of the open-source code.

The SmartLunch AI name and branding will be handled separately from the software licence. Name and trademark availability must be checked before public launch.

Development roadmap

Milestone 0 — Market validation

* Interview approximately 10–15 school lunch providers and small cloud kitchens.
* Understand current ordering, subscription, payment, and kitchen workflows.
* Identify the most urgent problems and willingness to pay.
* Find 1–2 potential pilot customers.

Milestone 1 — SaaS-ready backend

* Establish the multi-tenant data model.
* Implement organisations, kitchens, users, memberships, and roles.
* Add authentication and organisation-level access controls.
* Add parent/customer, recipient, and school management.
* Test tenant isolation.

Milestone 2 — Core meal operations

* Add menus and meal plans.
* Implement subscriptions, scheduled days, pause, skip, and cancellation.
* Add delivery eligibility and daily kitchen counts.
* Generate school-wise or delivery-location-wise packing lists.

Milestone 3 — Parent and provider PWA

* Build the responsive React application.
* Add parent/customer and provider/admin workflows.
* Support conventional forms and buttons as well as conversational interaction.

Milestone 4 — Payments and notifications

* Integrate Razorpay in test mode.
* Implement verified, idempotent payment webhooks.
* Add payment history and reconciliation.
* Add in-app notifications and Web Push, with optional email.

Milestone 5 — AI assistant

* Add an LLM-based assistant with structured outputs.
* Expose approved backend tools for supported workflows.
* Add confirmation and escalation paths.
* Introduce LangGraph or MCP only when they solve a demonstrated need.

Milestone 6 — Open-source release

* Publish the licence and project documentation.
* Add Docker-based setup instructions.
* Add contribution guidelines, issue templates, and security reporting.
* Provide sample configuration without real credentials.

Milestone 7 — Commercial pilot

* Deploy a hosted version.
* Onboard 1–2 pilot providers.
* Start with a small customer group.
* Measure operational outcomes and improve the product before expanding.

Milestone 8 — Expansion

* Support additional kitchens and business types.
* Add integrations and reporting.
* Explore regional languages and additional payment providers.
* Expand hosted services based on validated customer needs.

Success measures

The pilot should measure practical outcomes, including:

* Time required to create or renew a subscription
* Reduction in manual administration
* Accuracy of daily kitchen counts
* Payment reconciliation effort
* Subscription renewal and retention
* Number and type of support issues
* Provider willingness to continue using and paying for the product

A second independent kitchen or organisation is an important validation of the multi-tenant design.

Repository structure

The repository is expected to evolve towards a structure similar to:

smartlunch-ai/
├── backend/
│   ├── app/
│   │   ├── api/
│   │   ├── core/
│   │   ├── db/
│   │   ├── models/
│   │   ├── schemas/
│   │   ├── repositories/
│   │   ├── services/
│   │   ├── agents/
│   │   └── integrations/
│   ├── migrations/
│   └── tests/
├── frontend/
├── docs/
│   ├── architecture.md
│   ├── database-design.md
│   ├── api-design.md
│   ├── deployment.md
│   ├── contributing.md
│   └── security.md
├── examples/
├── .github/
│   ├── workflows/
│   ├── ISSUE_TEMPLATE/
│   └── PULL_REQUEST_TEMPLATE.md
├── LICENSE
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── SECURITY.md
├── .gitignore
├── docker-compose.yml
└── README.md

Getting started

The development setup and commands will be documented as the first backend milestone is implemented.

The initial local development environment is expected to use:

* Python 3.12 or later
* Node.js and npm
* PostgreSQL
* Git

A .env.example file will document required configuration using placeholders. Actual secrets and .env files must not be committed.

Contributing

Contributions, issue reports, documentation improvements, and feedback are welcome once the contribution guidelines are published.

Please do not include real customer, student, payment, or other personal data in issues, examples, or test fixtures.

Disclaimer

SmartLunch AI is an early-stage project. Features, architecture, licensing, and commercial plans may change based on implementation and customer feedback. Do not use it to manage real customer or child data until appropriate security, privacy, operational, and legal reviews have been completed.

