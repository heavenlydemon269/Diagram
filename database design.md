
%% Relational Database Schema for E-lib Voice

erDiagram
    User {
        INT user_id PK
        VARCHAR username "unique, indexed"
        VARCHAR password_hash "nullable, for backup"
        BLOB voiceprint_embedding "Encrypted user voiceprint [cite: 36, 66]"
        TIMESTAMP created_at
    }

    Book {
        INT book_id PK
        VARCHAR title "indexed"
        VARCHAR author "indexed"
        VARCHAR genre "indexed"
        VARCHAR full_text_path "Path to e-book file for TTS "
    }

    Reading_History {
        INT history_id PK
        INT user_id FK
        INT book_id FK
        TIMESTAMP last_read_timestamp
        VARCHAR progress "e.g., last page/chapter"
    }

    Search_History {
        INT search_id PK
        INT user_id FK
        VARCHAR search_query
        TIMESTAMP timestamp
    }

    Chat_History {
        INT chat_id PK
        INT user_id FK
        TEXT user_query
        TEXT ai_response
        TIMESTAMP timestamp
    }

    User ||--o{ Reading_History : "tracks"
    Book ||--o{ Reading_History : "is read in"
    User ||--o{ Search_History : "performs"
    User ||--o{ Chat_History : "has"

