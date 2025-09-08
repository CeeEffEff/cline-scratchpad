# PR #271 Documentation: Introduce Dead Letter Service

## PR Overview

- **Title**: feat(dead-letter): PT-1021 Introduce Dead Letter Service for handling failed Pub/Sub messages
- **Author**: marian-stykhun
- **Created**: August 6, 2025
- **Type**: Feature
- **Intent**: Implement a system to handle messages that are in permanent retry state

This PR introduces a new service and its infrastructure for processing dead letters (failed Pub/Sub messages). It updates Terraform configurations to enable dead-letter topics and policies across services and implements FastAPI handlers, resources, and dependencies to manage dead-letter flows with Firestore and Pub/Sub.

## Files Modified

### New Service Implementation
- **src/dead_letter_service/main.py** (+58 lines): FastAPI service implementation for handling dead letter messages
- **src/dead_letter_service/models.py** (+11 lines): Data models for the dead letter service
- **src/dead_letter_service/Pipfile** (+29 lines): Dependencies for the dead letter service
- **src/dead_letter_service/Pipfile.lock** (+1104 lines): Locked dependencies
- **src/dead_letter_service/config.smx** (+1 line): Configuration file

### Core Dead Letter Implementation
- **src/seomax/services/dead_letter/base.py** (+209 lines): Base class for dead letter processing
- **src/seomax/services/dead_letter/factory.py** (+26 lines): Factory for creating dead letter processors
- **src/seomax/services/dead_letter/implementations.py** (+16 lines): Specific implementations of dead letter processors
- **src/seomax/services/dead_letter/models.py** (+11 lines): Data models for dead letter processing
- **src/seomax/services/dead_letter/__init__.py** (0 lines): Package initialization

### Modified Services
- **src/scraper_service/main.py** (+47, -16 lines): Updated to support dead letter handling

### Supporting Components
- **src/seomax/cloud_logging/enums.py** (+9 lines): Added logging enums for dead letter service
- **src/seomax/constants/config.py** (+4 lines): Added configuration constants
- **src/seomax/constants/constants.py** (+17, -1 lines): Added constants for dead letter handling
- **src/seomax/implementations/firestore_database.py** (+36, -9 lines): Updated database implementation
- **src/seomax/implementations/lazy_config.py** (+8, -1 lines): Updated configuration handling
- **src/seomax/interfaces/database_interface.py** (+10, -3 lines): Updated database interface
- **src/seomax/interfaces/notification_interface.py** (+35 lines): Added notification interface for dead letters
- **src/seomax/middleware/heartbeat_middleware.py** (+22 lines): Added middleware for heartbeat monitoring
- **src/seomax/models/config.py** (+13, -2 lines): Updated configuration models
- **src/seomax/models/database.py** (+96, -3 lines): Updated database models

### Tests
- **src/tests/test_dead_letter_service.py** (+257 lines): Unit tests for dead letter service
- **src/tests/test_e2e_dead_letter_service.py** (+160 lines): End-to-end tests for dead letter service
- **src/tests/test_e2e_scraper.py** (+183, -10 lines): Updated scraper tests

### Infrastructure (Terraform)
- **terraform/resources--services/dead_letter_service.tf** (+202 lines): New Terraform configuration for dead letter service
- **terraform/resources--services/subscriptions.tf** (+104, -78 lines): Updated subscription configurations
- **terraform/resources--services/pubsub.tf** (+25 lines): Updated Pub/Sub configurations
- **terraform/resources--services/variables.tf** (+21 lines): Added variables for dead letter service
- **terraform/resources--services/accounts.tf** (+17 lines): Added service account configurations
- **terraform/resources--services/outputs.tf** (+20 lines): Added outputs for dead letter service
- **terraform/resources--services/locals.tf** (+5 lines): Added local variables
- **terraform/resources--services/data.tf** (+4 lines): Updated data sources
- **terraform/modules/service_subscriptions/main.tf** (+12 lines): Updated subscription module
- **terraform/modules/service_subscriptions/variables.tf** (+18 lines): Added variables for dead letter topics
- **terraform/resources--services/aggregator_service.tf** (+5 lines): Updated aggregator service
- **terraform/resources--services/scraping_service.tf** (+5 lines): Updated scraping service

### CI/CD
- **.github/workflows/build-and-deploy.yml** (+7 lines): Updated CI/CD workflow to include dead letter service

### Documentation
- **terraform/modules/service_subscriptions/DOCS.md** (+3 lines): Updated documentation
- **terraform/resources--services/DOCS.md** (+14 lines): Updated documentation

## Business Logic Changes

The PR introduces a new business logic component for handling dead letter messages:

- **BaseDLTProcessor**: An abstract base class that defines the interface for processing dead letter messages
- The processor checks if a job has made progress and determines if a message should be resubmitted or dropped
- Implements transaction support for job mutations
- Provides statistics tracking for dead letter processing

Key functionality:
- Tracking of failed messages
- Ability to reprocess messages that failed due to transient issues
- Permanent failure handling for messages that cannot be processed

## Configuration Changes

The PR adds several configuration parameters for the dead letter service:

- **Dead Letter Topic Configuration**: Parameters for configuring dead letter topics in Pub/Sub
- **Service Configuration**: Parameters for the dead letter service itself
- **Retry Configuration**: Parameters for controlling retry behavior
- **Expiry Configuration**: Added `dead_letter_returned_partition_expiry_sec` parameter to control when partitions in RETURNED state are considered expired

## Service Changes

A new service has been added:

- **Dead Letter Service**: A FastAPI service that processes messages from the dead letter topic
  - Handles messages that have failed processing in other services
  - Implements retry logic with configurable parameters
  - Provides endpoints for managing dead letter flows

The existing Scraper Service has been modified to support dead letter handling.

## Dependency Changes

New dependencies added for the dead letter service:
- FastAPI and related web framework components
- Google Cloud libraries (Pub/Sub, Firestore, etc.)
- Data processing libraries

## Schema Changes

Several data models have been added or modified:

- **Dead Letter Models**: New models for representing dead letter messages and their state
- **Database Models**: Updated to support tracking of dead letter messages
- **Configuration Models**: Updated to include dead letter configuration

## Infrastructure Changes

Significant infrastructure changes have been made:

- **New Cloud Run Service**: Added configuration for the dead letter service
- **Dead Letter Topic**: Added a new Pub/Sub topic for dead letter messages
- **Subscription Configuration**: Updated to support dead letter topics
- **Service Accounts**: Added service account for the dead letter service
- **IAM Permissions**: Updated to grant necessary permissions

Key changes to the subscription configuration:
- Added `use_dead_letter_topic` parameter to control whether a subscription uses a dead letter topic
- Added `max_delivery_attempts` parameter to control how many times a message is attempted before being sent to the dead letter topic
- The scraper service now uses a dead letter topic with 5 max delivery attempts

## CI/CD Pipeline Changes

The CI/CD pipeline has been updated to:
- Build and deploy the new dead letter service
- Pass the necessary environment variables and configuration
- Include the dead letter service in the deployment process

## Impact Analysis

This PR has a moderate impact on the system:

- **Direct Impacts**:
  - Adds a new service for handling failed messages
  - Modifies how the scraper service handles message failures
  - Changes the Pub/Sub subscription configuration

- **Potential Wider Impacts**:
  - Improved reliability by properly handling failed messages
  - Better visibility into message processing failures
  - Potential for reprocessing messages that would otherwise be lost

- **Required Follow-up Changes**:
  - Monitoring and alerting for the dead letter service
  - Potential extension to other services beyond the scraper

## Conceptual Changes

This PR implements the dead letter pattern, a common messaging pattern where messages that cannot be processed are sent to a separate queue (dead letter queue) for later analysis or reprocessing. This improves system reliability by ensuring that problematic messages don't block the processing of other messages and provides a mechanism for handling transient failures.
