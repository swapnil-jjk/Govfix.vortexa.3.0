# JanSetu --- Civic Grievance Resolution & Demand Intelligence

**Turning citizen complaints into accountable civic action.**

JanSetu is an AI-assisted civic grievance management platform designed
to improve transparency, accountability, and municipal service delivery.
It connects citizens, ward officers, field execution teams, and
government administrators through a unified complaint-to-resolution
workflow.

The platform is modelled around municipal workflows such as those of
Pune Municipal Corporation (PMC), Maharashtra.

## Problem Statement

Municipal authorities face several challenges in managing public
grievances:

-   **Unstructured complaints:** Citizens report the same issue multiple
    times, often without accurate location information or supporting
    evidence.
-   **Inefficient routing:** Complaints can reach the wrong department
    or remain unassigned.
-   **Unverified resolutions:** Work may be marked complete without
    sufficient evidence of execution.
-   **Limited citizen feedback:** Citizens often lack a structured way
    to evaluate completed work.
-   **Lack of demand intelligence:** Recurring local problems are not
    always connected to long-term infrastructure planning.

JanSetu addresses these challenges by connecting complaint registration,
AI-assisted classification, departmental assignment, field execution,
photographic evidence, citizen feedback, and geographic analytics in one
platform.

## Our Solution

JanSetu provides four role-based portals:

1.  **Citizen Portal:** Register complaints or infrastructure demands,
    submit location and media, track progress, send reminders, and rate
    completed work.
2.  **Ward Officer Portal:** Review AI-generated classifications,
    approve or reject requests, assign field teams, and monitor
    ward-level issues using maps.
3.  **Field Team Portal:** Access assigned work orders, upload
    before-and-after photographs, and record completion notes.
4.  **Government Dashboard:** Monitor grievance statistics, ward
    hotspots, departmental performance, resolution rates, and
    AI-generated summaries.

## Key Features

### 1. AI-Powered Complaint Classification

Uses Google Gemini 3.7 Flash to suggest complaint categories,
priorities, severity scores, summaries, responsible departments, and
recommended actions.

### 2. Complaint and Demand Management

Distinguishes immediate civic problems, such as potholes and garbage
accumulation, from longer-term infrastructure demands.

### 3. Geographic Intelligence

Uses browser geolocation, OpenStreetMap-based mapping, and reverse
geocoding to associate complaints with locations and visualize
geographic patterns.

### 4. Evidence-Based Workflows

Requires a before photograph to start a task and an after photograph
with completion notes to mark it complete.

### 5. Citizen Feedback

Allows citizens to submit a five-star rating and written feedback after
a complaint is completed.

### 6. Spam Reduction and Reminders

Implements a 24-hour cooldown for repeated complaints in the same
category and a seven-day interval for citizen follow-up reminders.

### 7. Multi-Role Access

Provides role-specific access for citizens, ward officers, field teams,
and government administrators.

### 8. Multilingual and Voice Support

Includes browser-based audio recording and a Google Cloud
speech-processing service layer for transcription and translation,
subject to service configuration and availability.

## End-to-End Workflow

``` text
Citizen submits complaint or demand
                 |
                 v
   Location and media collection
                 |
                 v
    AI classification and triage
                 |
                 v
    Ward officer reviews request
                 |
        +--------+--------+
        |                 |
      Reject            Approve
                          |
                          v
                Assign field team
                          |
                          v
                 Upload before photo
                          |
                          v
                   Execute work
                          |
                          v
              Upload after photo
               and completion notes
                          |
                          v
               Citizen rates outcome
                          |
                          v
           Government analytics dashboard
```

## Technology Stack

  -----------------------------------------------------------------------
  Layer                               Technologies
  ----------------------------------- -----------------------------------
  Frontend                            React 19, Vite

  Styling                             Tailwind CSS

  Maps                                Leaflet, OpenStreetMap

  HTTP Client                         Axios

  Backend                             Node.js, Express.js

  Primary Database                    PostgreSQL

  Local Fallback                      SQLite

  Generative AI                       Google Gemini 3.7 Flash

  Geocoding                           OpenStreetMap Nominatim

  File Uploads                        Multer

  Authentication                      JWT-based authentication and
                                      role-based access control
  -----------------------------------------------------------------------

## System Architecture

``` text
React Frontend
      |
      v
Express REST API
      |
      +---- Authentication and Authorization
      |
      +---- Citizen Grievance Management
      |
      +---- Ward and Regional Intelligence
      |
      +---- Field Team Task Management
      |
      +---- Ratings and Dashboard Analytics
      |
      +---- AI and Speech Services
      |
      v
PostgreSQL / SQLite
      |
      +---- Google Gemini API
      |
      +---- Google Cloud Services
      |
      +---- OpenStreetMap Nominatim
```

## Core Business Rules

-   A citizen cannot submit another complaint in the same category
    during the configured 24-hour cooldown.
-   Citizens can request a follow-up reminder only after the configured
    seven-day interval.
-   Field tasks cannot move to `In Progress` without a before
    photograph.
-   Field tasks cannot move to `Completed` without an after photograph
    and completion notes.
-   Only the citizen who created a completed request can rate it.
-   Duplicate ratings for the same request and citizen are prevented.

## Project Structure

``` text
jan_setu/
├── client/
│   ├── src/
│   │   ├── components/
│   │   ├── context/
│   │   ├── hooks/
│   │   ├── utils/
│   │   ├── App.jsx
│   │   └── main.jsx
│   └── package.json
│
├── server/
│   ├── controllers/
│   ├── routes/
│   ├── services/
│   ├── database/
│   │   ├── schema.sql
│   │   └── migrations/
│   └── server.js
│
├── .env
└── package.json
```

*This is a representative structure based on the audited repository;
check the actual repository before publishing it as an exact directory
listing.*

## Getting Started

### Prerequisites

-   Node.js 20 or a compatible version
-   npm
-   PostgreSQL for the primary database configuration, or SQLite for
    local development
-   A Google Gemini API key for live AI classification
-   Google Cloud credentials if live speech services are required

### Installation

Clone the repository:

``` bash
git clone <YOUR_REPOSITORY_URL>
cd jan_setu
```

Install the root dependencies:

``` bash
npm install
```

Install the client and server dependencies if they are maintained
separately:

``` bash
cd client
npm install

cd ../server
npm install
```

Configure the environment variables using the names required by the
project's existing configuration. Typical settings may include database
connection details, JWT signing secrets, Gemini credentials, and Google
Cloud credentials. **Do not commit real credentials or API keys to
GitHub.**

Start the frontend and backend using the scripts defined in their
respective `package.json` files.

> Setup commands and environment variable names should be verified
> against the actual repository before deployment. This document does
> not assume that a particular production configuration is already
> complete.

## Security and Production Readiness

The audited prototype includes JWT-based authentication, role-based
access controls, masked citizen information in selected views, and
backend validation for key workflow transitions.

The audit also identifies important production dependencies:

-   Aadhaar and OTP verification currently use a mock or sandbox
    implementation.
-   Live OTP delivery requires an appropriate notification provider.
-   Official municipal ERP integration and verified ward-boundary data
    remain pending.
-   Automated background SLA escalation requires further implementation.
-   Speech transcription may use a fallback when external credentials
    are unavailable.

JanSetu should therefore be treated as a working prototype rather than
an officially deployed municipal service. Real citizen data and identity
verification should only be introduced after the necessary security,
privacy, authorization, and integration requirements have been met.

## Expected Impact

JanSetu aims to help municipal authorities:

-   Improve complaint routing and ownership.
-   Make field-work completion more transparent.
-   Identify recurring civic issues geographically.
-   Gather structured citizen feedback.
-   Monitor departmental workload and resolution performance.
-   Use complaint patterns to inform infrastructure planning.

These are intended outcomes that should be measured through a municipal
pilot using indicators such as resolution time, SLA compliance, citizen
satisfaction, and evidence completeness.

## Future Roadmap

-   Complete secure, authorized identity-verification integration.
-   Integrate live SMS or other notification services.
-   Add automated SLA monitoring and escalation.
-   Improve duplicate-complaint detection.
-   Validate official ward boundaries and municipal data integrations.
-   Strengthen multilingual and offline field-worker support.
-   Evaluate AI classification accuracy using validated complaint
    datasets.
-   Conduct a controlled pilot with municipal stakeholders.

## Conclusion

JanSetu aims to move civic service delivery beyond complaint
registration toward a transparent and accountable resolution process.

By combining AI-assisted triage, geographic intelligence, evidence-based
field execution, and citizen feedback, the platform provides a
foundation for more measurable and data-driven municipal governance.

**JanSetu --- From reporting problems to verifying resolutions.**
