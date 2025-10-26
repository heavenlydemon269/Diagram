
%% User Journey (rebuilt as a Flowchart 'graph TD')
%% Refactored: Removed ALL special characters from labels.
graph TD
    
    %% 1. Define All Nodes
    A(Start)
    B[User visits Main Landing Page]
    C{New User?}
    D[Go to Sign Up Page]
    E[Enroll Voiceprint<br>Hello My name is...]
    F[Create Account]
    G[Go to Login Page]
    H[Authenticate Voiceprint<br>Hello I am name...]
    I[Access User Dashboard]
    J[Use Search]
    K[Browse Recommendations]
    L[Continue Reading]
    M[Search for book]
    N{Book Found?}
    O[Go to Book Request Page]
    O1[Submit Book Request]
    P[View Book Details]
    Q{Listen to Audio?}
    R[Go to Audio Book Page]
    S[Control Playback Play Pause]
    Z(Stop)

    %% 2. Define All Links
    A --> B
    B --> C
    C -- Yes --> D
    D --> E
    E --> F
    C -- No --> G
    G --> H
    F --> I
    H --> I
    I --> J
    I --> K
    I --> L
    J --> M
    K --> P
    L --> P
    M --> N
    N -- Yes --> P
    N -- No --> O
    O --> O1
    O1 --> Z
    P --> Q
    Q -- Yes --> R
    R --> S
    S --> Z
    Q -- No --> Z
