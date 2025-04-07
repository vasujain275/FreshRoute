# 🥬 FreshRoute: Perishable Goods Marketplace Platform

![GitHub workflow status](https://img.shields.io/github/workflow/status/yourusername/freshroute/CI)
![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Go Version](https://img.shields.io/badge/go-1.19+-00ADD8.svg)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.0+-6DB33F.svg)
![React](https://img.shields.io/badge/react-%2320232a.svg?style=flat&logo=react&logoColor=%2361DAFB)

FreshRoute is a high-performance microservices-based marketplace platform connecting local producers of perishable goods directly with consumers and businesses. The platform optimizes for the unique challenges of fresh food distribution, ensuring timely delivery while minimizing waste and maximizing quality.

## 🌟 Key Features

### For Producers 👨‍🌾

- **Dynamic Inventory Management**: Update product availability, freshness status, and harvest dates in real-time
- **Flexible Pricing Models**: Set pricing tiers based on freshness, quantity, and delivery timeframes
- **Batch Management**: Track different harvests/batches with specific quality attributes
- **Production Forecasting**: Indicate upcoming harvests and expected yields
- **Quality Certification**: Upload and manage certifications and quality verification
- **Real-time Analytics**: Track sales patterns, waste metrics, and demand forecasting

### For Consumers 🛒

- **Freshness Guarantee**: Clear indicators of harvest dates and remaining optimal consumption window
- **Locality Filtering**: Find producers within specific distance ranges
- **Subscription Options**: Regular recurring orders with seasonal adjustments
- **Delivery Slot Booking**: Select precise delivery windows that fit their schedule
- **Quality Feedback**: Rate freshness and quality of received items
- **Product Traceability**: View complete supply chain and provenance information

### For Logistics 🚚

- **Route Optimization**: Calculate optimal delivery routes considering product shelf-life
- **Temperature-Controlled Tracking**: Monitor cold chain compliance during transport
- **Delivery Capacity Management**: Dynamic scheduling based on vehicle availability
- **Last-Mile Coordination**: Real-time communication between producers, drivers, and customers
- **Contingency Handling**: Protocols for delayed deliveries or quality issues

## 🏗️ Architecture Overview

FreshRoute implements a modern microservices architecture with a mixed technology stack, strategically leveraging the strengths of different technologies for specific components.

![Architecture Diagram](./docs/architecture-diagram.png)

### Technology Stack

#### Backend Services

- **Go (Gin)**: High-performance, real-time critical services
- **Spring Boot**: Complex business logic and integration services
- **gRPC**: Service-to-service communication
- **GraphQL**: Flexible API queries for clients
- **Kafka**: Event streaming and asynchronous communication
- **Keycloak**: Authentication and authorization

#### Frontend Applications

- **React**: Web applications built with Vite
- **React Native**: Mobile application
- **Apollo Client**: GraphQL integration
- **TailwindCSS**: Styling

#### Data Storage

- **PostgreSQL**: Primary relational database
- **SQLC**: Type-safe SQL for Go services
- **Redis**: Caching and real-time features
- **Elasticsearch**: Search capabilities
- **InfluxDB**: Time-series data for monitoring
- **MongoDB**: Flexible document storage

#### DevOps & Infrastructure

- **Docker**: Containerization
- **Kubernetes**: Orchestration
- **Prometheus & Grafana**: Monitoring
- **GitHub Actions**: CI/CD
- **Helm**: Deployment management

## 🔍 Microservices Architecture

### Core Services

#### 1. API Gateway (Go/Gin)

- Serves as the entry point for all client requests
- Implements GraphQL API with gqlgen
- Handles authentication and authorization via Keycloak
- Provides request routing and aggregation
- Manages rate limiting and API security

#### 2. User Service (Spring Boot)

- Manages user registration and authentication via Keycloak
- Handles profile management for producers, consumers, and delivery partners
- Implements authorization and permissions
- Stores user preferences and settings

#### 3. Catalog Service (Go/Gin)

- Manages product listings and metadata
- Implements category and attribute management
- Provides search and discovery capabilities via Elasticsearch
- Handles product images and assets

#### 4. Inventory Service (Go/Gin)

- Implements real-time inventory tracking with temporal constraints
- Manages batch and freshness tracking
- Provides availability forecasting
- Handles high-frequency updates during harvest periods

#### 5. Order Service (Spring Boot)

- Processes order placement and management
- Implements complex order state management
- Handles order aggregation from multiple producers
- Manages transaction processing

#### 6. Pricing Service (Go/Gin)

- Implements dynamic pricing based on freshness, demand, and time-to-expiration
- Manages discount and promotion configurations
- Handles bulk pricing and wholesale rates
- Processes real-time price adjustments

#### 7. Logistics Service (Go/Gin)

- Manages delivery capacity planning
- Implements route planning and optimization
- Handles temperature and condition monitoring
- Coordinates last-mile delivery

#### 8. Notification Service (Go/Gin)

- Sends multi-channel alerts for critical events
- Manages delivery status updates
- Implements freshness reminders
- Handles marketing communications

#### 9. Rating & Review Service (Spring Boot)

- Collects quality and freshness feedback
- Manages producer and deliverer ratings
- Implements dispute handling and resolution
- Provides review moderation

#### 10. Analytics Service (Spring Boot)

- Generates sales and inventory analytics
- Tracks waste reduction metrics
- Implements demand forecasting
- Analyzes market trends

#### 11. Subscription Service (Spring Boot)

- Manages recurring order workflows
- Handles subscription plan configurations
- Processes seasonal adjustments
- Implements payment scheduling

## 📱 Frontend Applications

### Web Applications (React/Vite)

#### Producer Dashboard

- Inventory management interface
- Order fulfillment tracking
- Analytics and sales reporting
- Harvest forecasting tools

#### Consumer Marketplace

- Product discovery and search
- Shopping cart and checkout
- Account management and order history
- Subscription management

#### Admin Control Panel

- User management
- System monitoring
- Content moderation
- Platform analytics

### Mobile Application (React Native)

- Location-based product discovery
- Push notifications for order status and freshness alerts
- QR/barcode scanning for product traceability
- Simplified reordering of favorites
- Delivery tracking with real-time maps

## 🌐 API Design

### GraphQL API

- Unified API endpoint for frontend clients
- Flexible queries for specific data needs
- Subscriptions for real-time updates
- Detailed schema documentation

### gRPC Services

- High-performance inter-service communication
- Strongly typed service definitions with Protocol Buffers
- Bidirectional streaming for real-time features
- Service discovery and health checking

## 📊 Data Flow Architecture

### Event Streaming

- `inventory-updates`: Real-time stock changes
- `order-events`: Order status changes
- `delivery-tracking`: Location and condition updates
- `user-activity`: For analytics and personalization

### Data Consistency Patterns

- Event sourcing for critical workflows
- Saga patterns for distributed transactions
- Optimistic concurrency for high-throughput operations

## 🔒 Security Implementation

- OAuth2/OpenID Connect authentication with Keycloak
- Role-based access control
- API rate limiting and throttling
- Data encryption in transit and at rest
- Regular security scanning and monitoring

## 📈 Scalability Considerations

- Horizontal scaling for all services via Kubernetes
- Caching strategies for high-demand components
- Database sharding for large datasets
- Auto-scaling based on load metrics
- Regional deployment for locality optimization

## 🚀 Getting Started

### Prerequisites

- Docker and Docker Compose
- Go 1.19+
- Java 17+
- Node.js 16+
- Kubernetes cluster (for production deployment)

### Development Environment Setup

```bash
# Clone the repository
git clone https://github.com/yourusername/freshroute.git
cd freshroute

# Start infrastructure services
docker-compose up -d kafka postgres redis elasticsearch keycloak

# Start the development environment
make dev
```

### Building and Running Services

```bash
# Build all services
make build

# Run service locally
make run-service SERVICE=inventory

# Run tests
make test
```

### Local Deployment

```bash
# Deploy to local Kubernetes cluster (minikube/kind)
make deploy-local
```

## 📚 Documentation

- [Architecture Decision Records](./docs/adr/)
- [API Documentation](./docs/api/)
- [Development Guide](./docs/development.md)
- [Deployment Guide](./docs/deployment.md)
- [Contributing Guidelines](./CONTRIBUTING.md)

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

Contributions are welcome! Please see our [Contributing Guidelines](CONTRIBUTING.md) for more details.

## 💡 Acknowledgements

- [Go Gin Framework](https://github.com/gin-gonic/gin)
- [Spring Boot](https://spring.io/projects/spring-boot)
- [gRPC](https://grpc.io/)
- [GraphQL](https://graphql.org/)
- [React](https://reactjs.org/)
- [Kafka](https://kafka.apache.org/)
- [Kubernetes](https://kubernetes.io/)

