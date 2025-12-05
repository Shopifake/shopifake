# 🛍️ Shopifake

**Shopifake** is a modern multi-tenant e-commerce platform that allows businesses to create and manage their own customized online storefronts. Built with a microservices architecture, it provides a complete solution for catalog management, order processing, customer relations, and sales analytics.

## 🎯 Purpose

Shopifake enables merchants to:
- Create and customize their own branded storefronts with unique subdomains
- Manage product catalogs with inventory tracking and pricing strategies
- Process orders and handle customer relationships
- Monitor sales performance with real-time dashboards
- Leverage AI-powered features (chatbot, product recommendations)

Each merchant gets their own storefront accessible via `<slug>.domain.com`, with centralized management through an admin interface.

## 🏗️ Architecture

The project is organized as a monorepo with two main submodules:

### 📦 Submodules

- **[shopifake-front](https://github.com/Shopifake/shopifake-front)** - React + TypeScript + Vite frontend application
  - Multi-tenant storefront interface (B2C)
  - Admin dashboard for merchants (B2E)
  - Subdomain-based routing for tenant isolation
  
- **[shopifake-back](https://github.com/Shopifake/shopifake-back)** - Microservices backend with Spring Boot & Python
  - 11 independent microservices
  - Event-driven architecture with RabbitMQ
  - API Gateway for unified access
  - Full observability stack (Prometheus, Grafana, OpenTelemetry)

### 🔧 Backend Microservices

| Service | Technology | Purpose |
|---------|-----------|---------|
| **shopifake-access** | Spring Boot | Authentication & authorization |
| **shopifake-audit** | Spring Boot | Audit logging & compliance |
| **shopifake-catalog** | Spring Boot | Product catalog management |
| **shopifake-chatbot** | Python FastAPI | AI-powered customer support |
| **shopifake-customers** | Spring Boot | Customer relationship management |
| **shopifake-inventory** | Spring Boot | Stock management |
| **shopifake-orders** | Spring Boot | Order processing & fulfillment |
| **shopifake-pricing** | Spring Boot | Dynamic pricing strategies |
| **shopifake-recommender** | Python FastAPI | AI product recommendations |
| **shopifake-sales-dashboard** | Spring Boot | Analytics & reporting |
| **shopifake-sites** | Spring Boot | Multi-tenant site management |

### 🛠️ Infrastructure Components

- **shopifake-gateway** - Spring Cloud Gateway (API routing & load balancing)
- **shopifake-bus** - RabbitMQ message broker (async communication)
- **shopifake-auth-b2c** - Customer authentication service
- **shopifake-auth-b2e** - Employee authentication service
- **shopifake-grafana** - Monitoring dashboards
- **shopifake-prometheus** - Metrics collection
- **shopifake-otel-collector** - OpenTelemetry telemetry
- **shopifake-test-runner** - Python-based test orchestration (system/load/chaos tests)

## 🚀 Getting Started

### Clone the Repository

```bash
# Clone with all submodules
git clone --recurse-submodules https://github.com/Shopifake/shopifake.git
cd shopifake
```

### Frontend Setup

```bash
cd shopifake-front
npm install
npm run dev
```

Access the application:
- Landing page: `http://127.0.0.1.nip.io:3000`
- Storefront: `http://<slug>.127.0.0.1.nip.io:3000`

### Backend Setup

```bash
cd shopifake-back
# Follow instructions in shopifake-back/README.md
```

## 🔄 Development Workflow

The project uses a comprehensive CI/CD pipeline:

1. **Development** (`dev` branch)
   - Feature development and unit testing
   
2. **Pull Request** (dev → staging)
   - Lock file generation (pins all submodule versions)
   - System tests with Docker Compose
   - Automated PR comments with deployment summary

3. **Staging** (Kubernetes)
   - Automated deployment via Helm charts
   - Full test suite (system + load + chaos)
   - Auto-promotion to production on success

4. **Production** (`main` branch)
   - Stable, production-ready code

## 🧪 Testing Strategy

- **System Tests**: Health checks & integration validation
- **Load Tests**: Performance & scalability verification
- **Chaos Tests**: Resilience & failure recovery

All tests are orchestrated by the `shopifake-test-runner` Python CLI.

## 📊 Observability

Full observability stack included:
- **Metrics**: Prometheus + Grafana dashboards
- **Traces**: OpenTelemetry distributed tracing
- **Logs**: Centralized logging with audit service

## 🛡️ Multi-Tenancy

Each merchant site has:
- Unique subdomain (`<slug>.domain.com`)
- Isolated data and configuration
- Three states: `DRAFT`, `ACTIVE`, `DISABLED`
- Custom branding and theme support

## 📚 Documentation

- Frontend docs: See [shopifake-front/README.md](shopifake-front/README.md)
- Backend docs: See [shopifake-back/README.md](shopifake-back/README.md)
- Service endpoints: See [shopifake-front/service-endpoints.md](shopifake-front/service-endpoints.md)

## 🤝 Contributing

This is a monorepo aggregating multiple Git submodules. Each service is developed independently in its own repository.

### Update Submodules

```bash
# Update all submodules to latest
git submodule update --remote --merge
```

## 📝 License

[Specify your license here]

## 🔗 Links

- Frontend Repository: https://github.com/Shopifake/shopifake-front
- Backend Repository: https://github.com/Shopifake/shopifake-back

---

Built with ❤️ using Spring Boot, React, FastAPI, and Kubernetes