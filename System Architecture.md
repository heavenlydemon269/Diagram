
%% E-lib Voice System Architecture
graph TD

    %% 1. Define All Nodes
    
    %% Actors
    User([User])
    Admin([Admin])

    %% Client Layer
    subgraph "Client Layer (User Device)"
        UserWebApp["User Web App<br>(HTML/JS/Tailwind)"]
        AdminWebApp["Admin Web App<br>(HTML/JS/Tailwind)"]
        Mic[("Microphone<br>(Voice Input)")]
        Speaker[("Speaker<br>(Voice Output)")]
    end

    %% Backend Services Layer
    subgraph "Backend Services Layer (Microservices)"
        APIGateway["API Gateway<br>(Django REST API)"]
        AuthService["Auth Service<br>(Handles Login/Register)"]
        LibraryService["Library Service<br>(Search, Details, Playback)"]
        AdminService["Admin Service<br>(Upload Books, Manage Requests)"]
        VoiceService["Voice Interface Service<br>(Handles STT/TTS)"]
        ChatbotService["AI Chatbot Service<br>(RAG Pipeline w/ LangChain)"]
    end

    %% Data & AI Model Layer
    subgraph "Data & AI Model Layer"
        MySQL[("MySQL DB<br>User Profiles, Voiceprints, Book Metadata")]
        Pinecone[("Pinecone DB<br>Book Vector Embeddings")]
        
        ResemblyzerModel["Resemblyzer Model<br>(Speaker Recognition)"]
        WhisperModel["OpenAI Whisper Model<br>(Speech-to-Text)"]
        gTTSModel["gTTS Model<br>(Text-to-Speech)"]
        MistralModel["Mistral LLM<br>(Conversational AI)"]
        RecEngine["Recommendation Engine<br>(TF-IDF/Cosine Sim)"]
    end

    %% 2. Define All Links

    %% User -> Client
    User --> Mic
    User <-- Speaker
    Mic --> UserWebApp
    UserWebApp --> Speaker
    
    %% Admin -> Client
    Admin --> AdminWebApp

    %% Client -> Backend
    UserWebApp <--> APIGateway
    AdminWebApp <--> APIGateway

    %% API Gateway -> Services
    APIGateway <--> AuthService
    APIGateway <--> LibraryService
    APIGateway <--> AdminService
    APIGateway <--> VoiceService
    APIGateway <--> ChatbotService

    %% Service -> AI Models & DBs
    AuthService --> ResemblyzerModel
    AuthService <--> MySQL
    
    LibraryService <--> MySQL
    LibraryService --> RecEngine
    
    AdminService <--> MySQL
    
    VoiceService --> WhisperModel
    VoiceService --> gTTSModel
    
    ChatbotService --> MistralModel
    ChatbotService --> Pinecone
    ChatbotService --> MySQL

    %% Style Definitions
    classDef actor fill:#E8F5E9,stroke:#1E8E3E,stroke-width:2px
    classDef webapp fill:#E1F5FE,stroke:#0277BD,stroke-width:2px
    classDef service fill:#FFF3E0,stroke:#E65100,stroke-width:2px
    classDef db fill:#FCE4EC,stroke:#C2185B,stroke-width:2px
    classDef model fill:#F3E5F5,stroke:#6A1B9A,stroke-width:2px
    
    class User,Admin actor
    class UserWebApp,AdminWebApp webapp
    class APIGateway,AuthService,LibraryService,AdminService,VoiceService,ChatbotService service
    class MySQL,Pinecone db
    class ResemblyzerModel,WhisperModel,gTTSModel,MistralModel,RecEngine model
