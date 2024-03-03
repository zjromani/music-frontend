# Music Frontend

This repository contains the frontend code for a Music Frontend project, a web application that allows users to explore Music concerts, setlists, and song performances. The project is built using Svelte and integrates with backend services to fetch and display concert and song data.

## Service Interaction Diagram

Below is a sequence diagram showing how the frontend interacts with the [Concert](https://github.com/zjromani/concertservice) and [Song](https://github.com/zjromani/songservice) services, as well as external APIs to retrieve data:

```mermaid
sequenceDiagram
    participant User
    participant Frontend Service
    participant Concert Service
    participant MusicVendor API
    participant Song Service
    participant MusicVendor API

    User->>+Frontend Service: Search concerts by date/location or open text
    Frontend Service->>+Concert Service: Request concerts data
    Concert Service->>+MusicVendor API: Fetch concert data
    MusicVendor API->>-Concert Service: Return concert data
    Concert Service->>-Frontend Service: Return concerts data
    Frontend Service->>-User: Display concerts list

    User->>+Frontend Service: Select a concert
    Frontend Service->>+Concert Service: Request concert details
    Concert Service->>+MusicVendor API: Fetch concert details
    MusicVendor API->>-Concert Service: Return concert details
    Concert Service->>+Song Service: Request songs for concert via gRPC
    Song Service->>+MusicVendor API: Fetch songs data
    MusicVendor API->>-Song Service: Return songs data
    Song Service->>-Concert Service: Return enriched concert details
    Concert Service->>-Frontend Service: Return concert details with songs
    Frontend Service->>-User: Display concert details and songs

    User->>+Frontend Service: Search songs by open text
    Frontend Service->>+Song Service: Request songs data
    Song Service->>+MusicVendor API: Fetch songs data
    MusicVendor API->>-Song Service: Return songs data
    Song Service->>-Frontend Service: Return songs data
    Frontend Service->>-User: Display songs list
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

