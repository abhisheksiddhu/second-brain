## Data Sources

- **Outlook**: Email integration service providing communication data and message processing capabilities for the business workflows.
- **N Drive**: Network file storage system serving as a centralized repository for documents, files, and shared resources across the organization.
- **Amicus**: Specialized business application providing domain-specific data and business logic integration.
- **SharePoint**: Microsoft collaboration platform offering document management, content sharing, and team collaboration features for the enterprise.
- **ERP System**: Enterprise Resource Planning system managing core business processes, financial data, and operational workflows.

## Processing Layer

- **Azure Data Factory**: Cloud-based data orchestration service that extracts, transforms, and loads data from various sources into the system. Handles data pipeline automation and scheduling for batch processing workflows.
- **Azure Functions**: Serverless compute service (.NET-based) that processes business logic, handles API calls, and manages data transformations. Acts as the middleware between data sources and applications.

## Storage Layer

- **Azure SQL**: Relational database storing structured application data, user information, and transactional records. Provides ACID compliance and supports complex queries for the backend API.
- **Azure Blob**: Object storage service hosting unstructured data like documents, images, and large files. Serves as the primary storage for file uploads and media content.

## Application Layer

- **Azure Web App (Backend)**: .NET API application hosted on Azure App Services providing RESTful endpoints and business logic. Handles authentication, data processing, and serves the React frontend with structured data.
- **Azure Web App (Frontend)**: React-based user interface hosted on Azure App Services delivering the user experience. Consumes backend APIs and provides responsive web interface for end users.

## Search & Intelligence

- **Cognitive Search**: AI-powered search service providing full-text search, semantic search, and document indexing capabilities. Enables intelligent content discovery across all data sources.
- **Log Analytics/App Insights**: Monitoring and telemetry service collecting application logs, performance metrics, and user analytics. Enables proactive monitoring, debugging, and business intelligence reporting.

## Security & Access

- **Azure AD**: Identity and access management service providing single sign-on, multi-factor authentication, and user directory services. Manages user permissions and integrates with enterprise identity systems.
- **Front Door**: Global load balancer and CDN service providing SSL termination, traffic routing, and DDoS protection. Ensures high availability and performance optimization for global users.
- **Key Vault**: Secure secrets management service storing API keys, connection strings, and certificates. Provides encrypted storage and access control for sensitive configuration data.
- **Azure Firewall**: Network security service to control and monitor traffic between different network segments
- **Azure Security Center**: Unified security management providing threat protection and security recommendations
