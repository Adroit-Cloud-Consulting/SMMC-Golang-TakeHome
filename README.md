# **Middle-earth Meal Tracker**

## Overview

## Welcome to the Shire

The **Shire Meal Monitoring Council (SMMC)** needs a backend service to track and publish Hobbit meal events. Hobbits eat **seven** times a day, the SMMC wants each meal logged, stored, and broadcast via a message broker (Kafka, simulated here). This service will run inside a Kubernetes cluster and must expose relevant K8s metadata for observability.

This is a take-home assessment followed by a short debrief with our engineering team.

---

## Hobbit Meal Schedule


| Meal             | Time     |
| ---------------- | -------- |
| Breakfast        | 07:00 AM |
| Second Breakfast | 09:00 AM |
| Elevenses        | 11:00 AM |
| Luncheon         | 01:00 PM |
| Afternoon Tea    | 03:00 PM |
| Dinner           | 06:00 PM |
| Supper           | 09:00 PM |

---

## Requirements

### 1. HTTP API in Go

Build a RESTful HTTP API that exposes the following endpoints:

#### `POST /meals`

- Accepts a Hobbit meal event in JSON
- Validates and stores the meal in memory
- Publishes the event to a mocked Kafka topic

#### `GET /meals`

- Returns all meals submitted today in JSON

#### `GET /healthz`

- Returns a basic health check (`200 OK`)

#### `GET /shire`

- Returns Kubernetes pod metadata:
  - Pod name
  - Namespace
  - Node name
- This may be mocked locally, but you must show how it would work with the K8s API (`client-go` or REST)

### 2. Example Request Payload

```json
{
  "meal": "Second Breakfast",
  "hobbit": "Peregrin Took",
  "time": "2025-05-15T09:00:00Z",
  "calories": 700
}
```

### 3. Kafka Simulation

* Define a `MealPublisher` interface.
* Implement a mock version that logs the meal to stdout.
* In the README, explain how this would integrate with a real Kafka producer in production.


### 4. Kubernetes API Integration

* Use either the `client-go` library or direct REST calls to fetch pod metadata.
* When running locally, simulate/mock the output.
* Describe how this would behave when running inside a cluster (e.g., in-cluster config).


### 5. Observability

* Log all HTTP requests: method, path, response time.
* Expose `/metrics` in Prometheus format with:

  * Count of meals submitted
  * Count per meal type
  * Request durations

### 6. Testing

* Add unit tests for:
  * Meal validation
  * Kafka interface
  * K8s client (if applicable)
* Use mocks/stubs as needed




## README Checklist

Please include a short README in your submission covering:

* How to run the service locally
* How to test it
* Any assumptions or known limitations
* How you would improve it with more time
* How it would be deployed to Kubernetes (mention Helm, Kustomize, etc.)


## Panel Debrief

Be prepared to walk the panel through:

* Your architecture
* Interfaces and design patterns used
* How it integrates with Kubernetes and Kafka
* How it could scale
* Any compromises made under time pressure


## What We’re Looking For

* Idiomatic Go
* Clear, testable code
* Use of interfaces and abstractions
* Comfort working with Kubernetes APIs
* Good architectural thinking
* Strong communication in the debrief
