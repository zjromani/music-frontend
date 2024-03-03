# Music Frontend

This repository contains the frontend code for a Music Frontend project, a web application that allows users to explore Music concerts, setlists, and song performances. The project is built using Svelte and integrates with backend services to fetch and display concert and song data.

## Service Interaction Diagram

Below is a sequence diagram showing how the frontend interacts with the [Concert](https://github.com/zjromani/concertservice) and [Song](https://github.com/zjromani/songservice) services, as well as external APIs to retrieve data:


```mermaid
sequenceDiagram
    participant User
    participant Frontend as Svelte Frontend
    participant GraphQL as GraphQL Server
    participant MusicSvc as Music Service
    participant PredictionSvc as Music Prediction Service
    participant DB as Database
    participant Kafka as Kafka Event Bus
    participant ExternalAPI as External MusicVendor API

    User->>Frontend: Requests data (concerts, songs, artists)
    Frontend->>GraphQL: GraphQL query
    GraphQL->>MusicSvc: Fetch requested data
    MusicSvc->>DB: Check for cached data
    DB->>MusicSvc: Return cached data (if fresh)
    alt Data not fresh or not found
        MusicSvc->>ExternalAPI: Fetch latest data
        ExternalAPI->>MusicSvc: Return new data
        MusicSvc->>DB: Update cache with new data
    end
    MusicSvc->>GraphQL: Return data to GraphQL
    GraphQL->>Frontend: Display data to user

    alt Polling for Updates
        loop Every X minutes
            MusicSvc->>ExternalAPI: Poll for updates
            ExternalAPI->>MusicSvc: Send updates
            MusicSvc->>DB: Update cached data
            MusicSvc->>Kafka: Publish update events
        end
    end

    Kafka->>PredictionSvc: Consume update events
    PredictionSvc->>PredictionSvc: Generate predictive insights
    PredictionSvc->>GraphQL: Provide insights to GraphQL
    GraphQL->>Frontend: Update user with predictive insights

```

## Learning Goals

This project and related backend services aim to provide hands on learning with:

- Svelte for Dynamic UIs
- gRPC & Kotlin
- Micronaut
- GraphQL Integration
- Event-Driven Architecture with Kafka
- Domain-Driven Design (DDD)
- API Design
- GitOps for Continuous Deployment
  - Terraform
  - Docker & Kubernetes

