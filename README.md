# SKILLAB Platform

This repository contains 4 deployable "flavors" of the SKILLAB Platform, each packaged as a separate Docker Compose stack:

- `citizen`
- `education`
- `industry`
- `policy`

Each flavor has its own `docker-compose.yml` under its folder and can be started independently.

## Prerequisites

- [Docker Engine](https://docs.docker.com/engine/install/)
- [Docker Compose plugin](https://docs.docker.com/compose/install/)

## Clone The Repository

```bash
git clone https://github.com/skillab/SKILLAB-platform.git
cd SKILLAB-platform
```

## 🍓 Flavor Overview

| Component | Citizen | Industry | Education | Policy | GitHub link |
| --- | --- | --- | --- | --- | --- |
| XAI Occupation Analyser | ✅ | ✅ | ✅ | ✅ | [View Repository](https://github.com/skillab-project/xai-occupation-analyser) |
| Diversity Analysis | ✅ | ✅ | ✅ | ✅ | [View Repository](https://github.com/skillab-project/Diversity-analysis) |
| HCV - Hierarchical Cumulative Voting | ✅ | ✅ | ✅ | ✅ | [View Repository](https://github.com/skillab-project/hierarchical-cumulative-voting) |
| Skill Ageing | ✅ | ✅ | ✅ | ✅ | [View Repository](https://github.com/skillab-project/skill-ageing) |
| Giant Component Networks | ✅ | ✅ | ✅ | ✅ | [View Repository](https://github.com/skillab-project/giant_component_networks) |
| Escoplus Skills Extender | ❌ | ❌ | ✅ | ✅ | [View Repository](https://github.com/skillab-project/escoplus-skills-extender) |
| Role Classification | ❌ | ❌ | ❌ | ✅ | [View Repository](https://github.com/skillab-project/role_classification) |
| Occupational Demand Forecaster | ✅ | ✅ | ✅ | ✅ | [View Repository](https://github.com/skillab-project/occupational-demand-forecaster) |
| KU-Detection | ✅ | ✅ | ✅ | ✅ | [View Repository](https://github.com/skillab-project/KU-Detection) |
| SKILLAB Tracker | ✅ | ✅ | ✅ | ✅ | [View Repository](https://github.com/skillab-project/Skillab-Tracker) |
| Hiring Management | ❌ | ✅ | ❌ | ❌ | [View Repository](https://github.com/skillab-project/hiring-management) |
| Employee Management | ❌ | ✅ | ❌ | ❌ | [View Repository](https://github.com/skillab-project/employee-management) |
| Digital Policy Management | ❌ | ❌ | ❌ | ✅ | [View Repository](https://github.com/skillab-project/digital-policy-management) |
| skillab-ui | ✅ | ✅ | ✅ | ✅ | [View Repository](https://github.com/skillab-project/skillab-ui) |
| Curriculum Skills | ✅ | ✅ | ✅ | ✅ | [View Repository](https://github.com/skillab-project/curriculum-skills) |
| Policy Success Evaluator | ❌ | ❌ | ❌ | ✅ | [View Repository](https://github.com/skillab-project/digital-transformation-policymaker/tree/main/policy-success-evaluator) |
| Future Technology Trends Identifier | ❌ | ❌ | ❌ | ✅ | [View Repository](https://github.com/skillab-project/digital-transformation-policymaker/tree/main/future-technology-trends-identifier) |
| Organizational Skills Recommender | ❌ | ✅ | ❌ | ❌ | [View Repository](https://github.com/skillab-project/organizational_skills_recommender) |
| jBPM | ❌ | ❌ | ❌ | ✅ | * |
| User Management | ✅ | ✅ | ✅ | ✅ | [View Repository](https://github.com/skillab-project/user-management) |

**jBPM is used “of the shelf” by pulling the Docker image maintained by the jBPM community.*

## 🚀 Choose And Run A Flavor

Pick exactly one flavor folder and start its Compose stack.

### Citizen

```bash
cd citizen
docker compose up -d
```

### Education

```bash
cd education
docker compose up -d
```

### Industry

```bash
cd industry
docker compose up -d
```

### Policy

```bash
cd policy
docker compose up -d
```

## 🩺 Verify Services

Check running containers:

```bash
docker compose ps
```

Open the UI:

- [http://localhost:3000](http://localhost:3000)

Follow logs:

```bash
docker compose logs -f
```

## 🗑️ Stop And Remove A Stack

From the same flavor folder you started:

```bash
docker compose down
```

To also remove volumes (this deletes local persisted data):

```bash
docker compose down -v
```

## ⚙️ Mandatory Configuration Variables

Before launching the containers, users must update specific environment variables in the compose files. These variables ensure secure access and enable critical functionalities like automated email notifications and administrative control.

### 1. Common variables (all flavors)

The following variables must be configured within the `user-management-backend` service for every installation:

| Variable | Description |
| --- | --- |
| `SPRING_MAIL_USERNAME` | The email address used by the platform to send automated notifications. |
| `SPRING_MAIL_PASSWORD` | The application-specific password for the notification email account. |
| `APP_ADMIN_EMAIL` | The primary email address for the initial platform administrator account. |
| `APP_ADMIN_PASSWORD` | The secure password for the initial administrator account. |
| `APP_JWT_SECRET` | A unique secret key used for signing JSON Web Tokens (JWT) for authentication. |

### 2. Industry-specific variables

In addition to the common variables, the `industry` flavor requires the definition of the organization's identity within the `user-management-backend` and `employee-management-backend` services:

| Variable | Description |
| --- | --- |
| `APP_ORGANIZATION_NAME` | Defines the default organization name. The platform supports multi-tenancy, and additional organizations can be created through the UI once the platform is running. |

### 3. Policy-specific variables

The `policy` flavor includes advanced AI-driven analytical tools. To enable these, the `policy-success-evaluator` and `future-technology-trends-identifier` services should be pointed to a private LLM instance (for example, Ollama):

| Variable | Description |
| --- | --- |
| `API_URL` | The URL of the private Ollama instance. |
| `API_TOKEN` | The authentication token required to connect to the Ollama instance. |

Note: The Policy platform remains functional without these LLM variables, but certain automated analysis features are disabled.

## 🐛 Troubleshooting

- Port already in use: stop conflicting local services or change host port mappings in the flavor's `docker-compose.yml`.
- Pull/auth issues with Docker images: run `docker login` and retry.
- Service startup ordering: use `docker compose logs -f <service-name>` to inspect readiness and errors.

## 📁 Repository Layout

```text
SKILLAB-platform/
├── citizen/
│   └── docker-compose.yml
├── education/
│   └── docker-compose.yml
├── industry/
│   └── docker-compose.yml
├── policy/
│   └── docker-compose.yml
└── README.md
```
