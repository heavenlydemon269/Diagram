```mermaid
%% Use Case Diagram for E-lib Voice
usecaseDiagram
    actor User
    actor Admin
    
    rectangle "E-lib Voice System" {
        User -- (Register)
        (Register) ..> (Enroll Voiceprint) : <<Include>>
        note right of (Register) : "Hello My name is [name]..."
        
        User -- (Login)
        (Login) ..> (Authenticate Voiceprint) : <<Include>>
        note right of (Login) : "Hello, I'm [name]..."
        
        User -- (Search for Books)
        User -- (Browse Recommendations)
        User -- (View Book Details)
        User -- (Listen to Audio Book)
        (Listen to Audio Book) ..> (Control Playback) : <<Include>>
        
        User -- (Request New Book)
        (Search for Books) ..> (Request New Book) : <<Extend>>
        note right of (Request New Book)
          BRP: Book Request Page
        end note

        User -- (Get AI Assistance)
        (Get AI Assistance) ..> (AI Chatbot)
        note left of (Get AI Assistance)
          ACA: AI Chatbot Assistant
        end note

        User -- (Manage Data)
        note left of (Manage Data)
          Allows deleting voiceprint 
        end note

        Admin -- (Admin Login)
        Admin -- (Manage Book Requests)
        note right of (Manage Book Requests)
          ADP: Admin Dashboard
        end note
        
        Admin -- (Add New Book)
        note right of (Add New Book)
          ABAP: Book Adding Page
        end note
    }

    actor "AI Chatbot" as AIChatbot
    (Get AI Assistance) -- AIChatbot
```
