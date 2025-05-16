# Agentic AI Project for Dark Data Discovery and Deep Research

## Project Overview

This document outlines the comprehensive planning for an Agentic AI project focused on dark data discovery and deep research. The system is designed to enable users to upload, analyze, and visualize data from various sources, with a particular emphasis on identifying patterns and relationships that might otherwise remain hidden or underutilized (dark data). The project draws inspiration from the RYLTI Knowledge Engineering Platform (RKE) described in the requirements, which has successfully been applied to genomic research in areas such as endometriosis, rheumatoid arthritis, breast cancer, Alzheimer's, and colon cancer.

The system will leverage modern technologies including Pydantic AI, MCP Servers, Neo4j graph database, PostgreSQL, Docker, and a Next.js/TypeScript frontend to create a powerful, flexible, and user-friendly platform for knowledge discovery and data analysis. Additionally, the system will feature a conversational chat interface that enables users to interact with an AI agent capable of executing complex tasks and assisting with data analysis, similar to how Manus operates.

## System Architecture

The architecture of the Agentic AI project is designed to be modular, scalable, and robust, with clear separation of concerns between different components. The high-level architecture consists of the following layers:

### 1. Data Layer

The data layer is responsible for storing, retrieving, and managing all data within the system. It consists of two primary components:

- **Neo4j Graph Database**: Serves as the foundation for the knowledge graph, storing nodes, relationships, and properties that represent the interconnected data. This database will be particularly important for visualizing data in a node and relationship fashion, allowing users to explore connections and patterns.

- **PostgreSQL Database**: Functions as the document store and RAG (Retrieval-Augmented Generation) database. It will store PDF and text files after they have been processed and chunked, making them available for queries and reviews. The PostgreSQL database will also store metadata about the documents and their relationships to entities in the knowledge graph. Additionally, it will store conversation history and task execution logs for the chat agent functionality.

### 2. Processing Layer

The processing layer handles the transformation, analysis, and enrichment of data before it is stored in the data layer. Key components include:

- **Data Ingestion Service**: Responsible for accepting and processing uploaded files (.csv, PDF, text). This service will handle the initial validation, transformation, and routing of data to the appropriate storage and processing components.

- **PDF to Text Conversion Service**: Converts PDF files to text format before storing them in the PostgreSQL database. This service will ensure that all document content is searchable and can be analyzed by the system.

- **Data Chunking Service**: Breaks down large documents into smaller, manageable chunks for efficient storage and retrieval in the PostgreSQL database. This service will implement appropriate chunking strategies based on the content type and structure.

- **Embedding Service**: Generates vector embeddings for text content using either OpenAI or Ollama models, as specified in the configuration. These embeddings will be used for semantic search and similarity analysis.

- **Biomimetic Engine**: Implements the patent-pending technology described in the requirements for analyzing data and discovering patterns. This engine will be particularly important for identifying correlations and relationships that might not be immediately apparent through traditional analysis methods.

### 3. Application Layer

The application layer provides the business logic and services that enable users to interact with the system. Key components include:

- **Pydantic AI Core**: Serves as the foundation for the agentic AI capabilities, providing type validation, data modeling, and integration with AI services. This component will ensure that all data flowing through the system is properly validated and structured.

- **MCP (Model-Controller-Presenter) Servers**: Implement the server-side logic for handling user requests, managing data flow, and coordinating between different components of the system. These servers will provide the APIs needed for the frontend to interact with the backend services.

- **Knowledge Graph Service**: Manages the creation, modification, and analysis of the knowledge graph stored in Neo4j. This service will provide the CRUD operations needed for users to interact with the graph data.

- **Document Service**: Handles the storage, retrieval, and querying of documents in the PostgreSQL database. This service will provide the functionality needed for users to search and analyze the content of uploaded documents.

- **Analysis Service**: Implements the algorithms and methods for analyzing data and generating insights. This service will leverage the biomimetic engine and other analytical tools to help users discover patterns and relationships in their data.

- **Chat Agent Service**: Manages the conversational interface and task execution capabilities of the system. This service will process natural language inputs, maintain conversation context, and coordinate the execution of user-requested tasks across the system.

- **Task Orchestration Service**: Coordinates the execution of complex tasks requested through the chat interface. This service will break down high-level tasks into smaller steps, manage their execution, and report progress and results back to the user.

### 4. Presentation Layer

The presentation layer provides the user interface for interacting with the system. Key components include:

- **Next.js Frontend**: Implements the web-based user interface using Next.js and TypeScript. This frontend will provide a responsive, intuitive interface for users to upload data, create and modify knowledge graphs, run analyses, and visualize results.

- **Knowledge Graph Visualization**: Provides interactive visualization of the knowledge graph, allowing users to explore nodes and relationships, zoom in and out, and interact with specific elements to view detailed information.

- **Document Viewer**: Allows users to view and search the content of uploaded documents, with highlighting and navigation features to help users find relevant information.

- **Process Flow Designer**: Provides a drag-and-drop interface for creating and modifying process flows, similar to the one described in the requirements. This component will allow users to define the steps for preparing data, creating knowledge graphs, and running analyses.

- **Chat Interface**: Provides a conversational interface for interacting with the AI agent. This component will allow users to submit natural language requests, receive responses, and track the progress of ongoing tasks.

### 5. Infrastructure Layer

The infrastructure layer provides the foundation for deploying, scaling, and managing the system. Key components include:

- **Docker Containers**: Package the different components of the system into containers for easy deployment and scaling. Each major component (Neo4j, PostgreSQL, application servers, etc.) will be containerized to ensure consistency across different environments.

- **Docker Compose**: Orchestrates the deployment of the containerized components, defining the relationships and dependencies between them. This will make it easy to deploy the entire system with a single command.

- **Configuration Management**: Manages the configuration of the different components, allowing users to customize the behavior of the system according to their needs. This includes the ability to choose between OpenAI and Ollama for embeddings and LLM functionality.

## Data Flow and Processing

The data flow within the system follows a logical progression from ingestion to analysis and visualization. The key steps in this flow are:

### 1. Data Ingestion

1. User uploads .csv, PDF, or text files through the web interface or via chat commands.
2. The Data Ingestion Service validates the files and routes them to the appropriate processing components.
3. CSV files are processed and prepared for storage in the Neo4j graph database.
4. PDF files are converted to text by the PDF to Text Conversion Service.
5. Text files (including converted PDFs) are chunked by the Data Chunking Service.
6. Chunked text is stored in the PostgreSQL database, along with metadata about the original documents.

### 2. Knowledge Graph Creation

1. User creates a process flow using the Process Flow Designer or via chat commands, defining the steps for preparing data and creating the knowledge graph.
2. The process flow is executed by the MCP Servers, which coordinate the different steps.
3. Data is retrieved from the PostgreSQL database and/or Neo4j graph database as needed.
4. Transformations and analyses are applied according to the process flow.
5. The resulting knowledge graph is stored in the Neo4j database.

### 3. Analysis and Discovery

1. User defines the parameters for analysis, such as the variables to correlate and the methods to use, either through the UI or via chat commands.
2. The Analysis Service, including the biomimetic engine, processes the data according to the specified parameters.
3. Results are generated and stored in the Neo4j database and/or PostgreSQL database as appropriate.

### 4. Visualization and Exploration

1. User accesses the Knowledge Graph Visualization to explore the results or requests visualizations via chat.
2. The visualization retrieves data from the Neo4j database and renders it in an interactive format.
3. User can zoom in and out, click on nodes to view details, and explore relationships between different elements.
4. Additional analyses can be performed based on the user's exploration and discoveries.

### 5. Chat-Based Interaction and Task Execution

1. User submits a natural language request through the chat interface.
2. The Chat Agent Service processes the request, identifies the user's intent, and determines the appropriate action.
3. For simple queries, the agent retrieves information from the system and responds directly.
4. For complex tasks, the Task Orchestration Service breaks down the task into smaller steps and coordinates their execution.
5. The agent provides progress updates and results to the user through the chat interface.
6. The conversation history and task execution logs are stored in the PostgreSQL database for future reference and context.

## Technology Stack Components

### 1. Database Technologies

- **Neo4j**: A graph database that will store the knowledge graph, representing entities as nodes and their relationships as edges. Neo4j provides powerful query capabilities through the Cypher query language, as well as visualization tools that can be integrated with the frontend.

- **PostgreSQL**: A relational database that will serve as the document store and RAG database. PostgreSQL provides robust support for storing and querying large volumes of text data, as well as advanced features like full-text search and JSON support. It will also store conversation history, task execution logs, and user preferences.

### 2. Backend Technologies

- **Pydantic AI**: A data validation and settings management library that extends Pydantic with AI capabilities. It will be used to define the data models and ensure type safety throughout the application.

- **MCP Servers**: Implement the server-side logic using the Model-Controller-Presenter pattern. These servers will be built using Python, leveraging frameworks like FastAPI or Flask for creating RESTful APIs.

- **OpenAI / Ollama**: Provide the embedding and LLM capabilities for the system. The architecture will support both options, allowing users to choose based on their requirements for performance, cost, and privacy. These will be used for both data analysis and powering the chat agent.

- **Python Libraries**: Various Python libraries will be used for data processing, analysis, and integration with the different components of the system. These include libraries for working with Neo4j (neo4j-python-driver), PostgreSQL (psycopg2, SQLAlchemy), PDF processing (PyPDF2, pdf2image), and machine learning (scikit-learn, TensorFlow).

- **LangChain / LlamaIndex**: Frameworks for building applications with LLMs. These will be used to implement the chat agent's reasoning, context management, and task execution capabilities.

### 3. Frontend Technologies

- **Next.js**: A React framework that provides server-side rendering, static site generation, and other advanced features for building web applications. Next.js will be used to create a fast, responsive, and user-friendly interface.

- **TypeScript**: A typed superset of JavaScript that adds static types to the language. TypeScript will be used to ensure type safety and improve the maintainability of the frontend code.

- **React**: A JavaScript library for building user interfaces. React will be the foundation for the frontend components, providing a component-based architecture that promotes reusability and maintainability.

- **D3.js / Vis.js**: JavaScript libraries for creating interactive data visualizations. These libraries will be used to implement the knowledge graph visualization, allowing users to explore and interact with the graph data.

- **Socket.io / WebSockets**: Technologies for real-time, bidirectional communication between the client and server. These will be used to implement the chat interface and provide real-time updates on task progress.

### 4. Infrastructure Technologies

- **Docker**: A platform for developing, shipping, and running applications in containers. Docker will be used to package the different components of the system into containers for easy deployment and scaling.

- **Docker Compose**: A tool for defining and running multi-container Docker applications. Docker Compose will be used to orchestrate the deployment of the containerized components, defining the relationships and dependencies between them.

## Knowledge Graph Implementation

The knowledge graph is a central component of the system, representing entities and their relationships in a way that facilitates discovery and analysis. The implementation of the knowledge graph will follow these principles:

### 1. Graph Structure

- **Nodes**: Represent entities in the domain, such as genes, samples, groups, or concepts. Each node has a type and a set of properties that describe its attributes.

- **Relationships**: Represent connections between entities, such as "belongs to," "is related to," or "influences." Each relationship has a type and can also have properties that describe the nature of the connection.

- **Properties**: Describe the attributes of nodes and relationships. Properties can be simple values (strings, numbers, dates) or complex structures (arrays, objects).

### 2. Graph Creation

The creation of the knowledge graph will be driven by the process flows defined by users. These process flows will specify:

- **Input Data**: The source data for the graph, such as CSV files uploaded by the user.

- **Transformations**: Operations to clean, filter, and enrich the data before adding it to the graph.

- **Node and Relationship Definitions**: Specifications for how to create nodes and relationships from the transformed data.

- **Analysis Parameters**: Settings for the biomimetic engine and other analytical tools that will process the graph data.

### 3. Graph Querying and Modification

The system will provide a set of tools for querying and modifying the knowledge graph:

- **Cypher Queries**: Allow users to write custom queries using Neo4j's Cypher query language to retrieve and analyze graph data.

- **CRUD Operations**: Provide a user-friendly interface for creating, reading, updating, and deleting nodes and relationships in the graph.

- **Visual Editor**: Allow users to modify the graph through a visual interface, adding or removing nodes and relationships by interacting with the visualization.

- **Natural Language Interface**: Allow users to query and modify the graph using natural language commands through the chat interface.

### 4. Graph Visualization

The visualization of the knowledge graph will be a key feature of the system, allowing users to explore and understand the data in an intuitive way:

- **Interactive Display**: Show nodes and relationships in a visually appealing and interactive format, allowing users to zoom in and out, pan, and focus on specific areas of interest.

- **Node and Relationship Styling**: Apply different styles (colors, sizes, shapes) to nodes and relationships based on their types and properties, making it easier to identify patterns and relationships.

- **Detail Views**: Provide detailed information about nodes and relationships when users click on them, showing all properties and related entities.

- **Filtering and Highlighting**: Allow users to filter the visualization based on node and relationship types, properties, or other criteria, and highlight specific elements of interest.

## Chat Agent and Task Execution

The chat agent and task execution capabilities are new additions to the system, providing a conversational interface for interacting with the platform and executing complex tasks. The implementation of these features will follow these principles:

### 1. Chat Interface

- **Conversational UI**: Provide a user-friendly chat interface for interacting with the AI agent, with support for text input, file uploads, and rich media responses.

- **Message History**: Maintain a history of conversations, allowing users to reference previous interactions and the agent to maintain context.

- **Real-Time Updates**: Provide real-time updates on task progress and system events, keeping users informed about the status of their requests.

- **Multi-Modal Interaction**: Support various forms of input and output, including text, images, files, and interactive elements.

### 2. Natural Language Understanding

- **Intent Recognition**: Identify the user's intent from natural language input, determining whether they are asking a question, requesting information, or instructing the system to perform a task.

- **Entity Extraction**: Identify and extract relevant entities from user input, such as file names, data types, analysis parameters, or specific nodes in the knowledge graph.

- **Context Management**: Maintain context across multiple turns of conversation, allowing for more natural and efficient interactions.

- **Disambiguation**: Handle ambiguous requests by asking clarifying questions or providing options for the user to choose from.

### 3. Task Orchestration

- **Task Decomposition**: Break down complex tasks into smaller, manageable steps that can be executed by the system's components.

- **Workflow Management**: Coordinate the execution of task steps, ensuring they are performed in the correct order and with the appropriate dependencies.

- **Progress Tracking**: Monitor the progress of ongoing tasks, providing updates to the user and handling any errors or exceptions that occur.

- **Result Presentation**: Format and present the results of completed tasks in a way that is easy for the user to understand and act upon.

### 4. Knowledge and Reasoning

- **Domain Knowledge**: Incorporate knowledge about the system's capabilities, data structures, and domain-specific concepts to provide informed responses and recommendations.

- **Reasoning**: Apply logical reasoning to solve problems, answer questions, and make recommendations based on available information.

- **Learning**: Improve over time by learning from user interactions, feedback, and the results of executed tasks.

- **Explanation**: Provide explanations for recommendations, decisions, and analysis results, helping users understand the reasoning behind the system's actions.

## User Interface Design

The user interface will be designed to be intuitive, responsive, and powerful, providing access to all the features of the system while maintaining a clean and organized layout. The main components of the interface will be:

### 1. Data Lake Section

- **File Upload**: Allow users to upload CSV, PDF, and text files to the system.
- **File Browser**: Show a list of all uploaded and generated files, with options to view, download, or delete them.
- **File Details**: Provide detailed information about each file, including metadata, processing status, and relationships to other data in the system.

### 2. Modeling Section

- **Process Flow Designer**: Provide a drag-and-drop interface for creating and modifying process flows, with a toolbox of available components and a canvas for arranging them.
- **Process Flow List**: Show a list of all created process flows, with options to run, edit, or delete them.
- **Process Flow Details**: Provide detailed information about each process flow, including its components, parameters, and execution history.

### 3. Knowledge Graph Section

- **Graph Visualization**: Show an interactive visualization of the knowledge graph, allowing users to explore nodes and relationships.
- **Graph Explorer**: Provide tools for querying and analyzing the graph, including a Cypher query editor and predefined queries for common tasks.
- **Graph Editor**: Allow users to modify the graph by adding, updating, or deleting nodes and relationships.

### 4. Analysis Section

- **Analysis Configuration**: Allow users to configure the parameters for the biomimetic engine and other analytical tools.
- **Analysis Results**: Show the results of analyses in various formats, including visualizations, tables, and reports.
- **Analysis History**: Keep track of all analyses performed, with options to view, rerun, or modify them.

### 5. Chat Section

- **Chat Interface**: Provide a conversational interface for interacting with the AI agent, with support for text input, file uploads, and rich media responses.
- **Task Status**: Show the status of ongoing tasks, including progress indicators and estimated completion times.
- **Conversation History**: Allow users to view and search their conversation history, with options to continue previous conversations or start new ones.
- **Suggested Actions**: Provide contextual suggestions for actions the user might want to take, based on the current conversation and system state.

### 6. Administration Section

- **User Management**: Allow administrators to manage users and their permissions.
- **System Configuration**: Provide options for configuring the system, including the choice between OpenAI and Ollama for embeddings and LLM.
- **Monitoring and Logging**: Show system status, performance metrics, and logs for troubleshooting and optimization.

## Deployment Strategy

The deployment of the system will be facilitated by Docker, which will package all components into containers for easy installation and scaling. The deployment strategy will include:

### 1. Development Environment

- **Local Development**: Provide a Docker Compose configuration for setting up a local development environment with all necessary components.
- **Development Tools**: Include tools for debugging, testing, and profiling the application during development.
- **Hot Reloading**: Configure the development environment to support hot reloading of code changes for faster iteration.

### 2. Testing Environment

- **Automated Testing**: Set up continuous integration pipelines to run automated tests on code changes.
- **Integration Testing**: Provide a testing environment that mimics the production environment for thorough integration testing.
- **Performance Testing**: Include tools and configurations for testing the performance and scalability of the system.

### 3. Production Environment

- **Scalability**: Design the deployment to be scalable, allowing additional instances of components to be added as needed to handle increased load.
- **High Availability**: Configure the deployment for high availability, with redundancy and failover mechanisms to minimize downtime.
- **Security**: Implement security best practices, including encryption, authentication, and authorization, to protect sensitive data.
- **Monitoring**: Set up monitoring and alerting to track the health and performance of the system in production.

### 4. Deployment Process

- **Continuous Deployment**: Implement a continuous deployment pipeline to automate the process of deploying new versions of the application.
- **Version Management**: Use semantic versioning to track changes to the application and ensure compatibility between components.
- **Rollback Procedures**: Define procedures for rolling back to previous versions in case of issues with new deployments.
- **Documentation**: Provide comprehensive documentation for the deployment process, including requirements, steps, and troubleshooting guides.

## Conclusion

This planning document outlines the architecture, components, and implementation strategy for the Agentic AI project for dark data discovery and deep research. The system will leverage modern technologies and innovative approaches to provide a powerful platform for knowledge discovery and data analysis, with a particular focus on identifying patterns and relationships in complex data sets.

The addition of a chat-based interface and agentic task execution capabilities enhances the system's usability and power, allowing users to interact with the platform in a more natural and intuitive way. By combining the strengths of knowledge graphs, document analysis, and conversational AI, the system provides a comprehensive solution for exploring and understanding complex data.

The modular design of the system, with clear separation of concerns between different components, will ensure flexibility, scalability, and maintainability. The use of Docker for deployment will simplify the installation and operation of the system in various environments.

The next steps will be to implement the system according to this plan, starting with the core components and gradually adding more advanced features. The implementation will be guided by the task list provided in the accompanying TASK.md document.
