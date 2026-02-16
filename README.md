# Test runners and CI

# Author Arsenio Tiu

#

#Test Plan
1 Objective

To validate the functionality, reliability, and database integrity of the mock Payment Gateway API, specifically the POST /checkout endpoint, under different payment scenarios.

The goal is to ensure:

Correct API response behavior

Accurate database updates

Proper error handling

Reliable execution within CI pipeline

2 Scope
In Scope

API Functional Testing

Integration Testing (API + PostgreSQL)

Database validation (sales_hdr, sales_lin)

CI/CD pipeline automation

Code coverage validation (minimum 70%)

3 Automation scripts

This folder contains C# test checkers (TC01–TC04). Use these commands to run tests locally or in CI.

Windows (PowerShell):

```powershell
# Run a single checker (example: TC01)
docker compose -f \docker-compose.test.yml run --rm checker-tc01

# Run the full sequence (checker-all)
docker compose -f \docker-compose.test.yml run --rm checker-all
```

Linux / macOS:

```bash
# Run a single checker (example: TC01)
docker compose -f ../../../docker-compose.test.yml run --rm checker-tc01

# Run the full sequence (checker-all)
docker compose -f ../../../docker-compose.test.yml run --rm checker-all
```

CI notes:

- GitHub Actions workflow: `.github/workflows/ci.yml` — sets up PostgreSQL service, runs `dotnet test` with coverage, publishes TRX and coverage report, and fails if coverage < 70%.
- Azure Pipelines job: `azure-pipelines.ci.yml` — similar steps using the Azure tasks to publish test and coverage results.

Coverage enforcement:

- Both workflows generate a Cobertura coverage file and run a small script to enforce a minimum 70% line coverage. Adjust the threshold in the workflow files if needed.

# Test Runner instructions

Requires Docker Engine and Docker Compose.

1. Build and start the test stack:

```bash
docker compose -f docker-compose.test.yml up --build -d
```
