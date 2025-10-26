flowchart LR
    %% Actors
    User((User))
    Admin((Admin))

    %% System boundary (Book Platform)
    subgraph BOOK_PLATFORM["Book Platform"]
      direction TB
      signUp("Register / Sign Up")
      login("Login")
      dashboard("User Dashboard")
      browse("Browse/Discover Books")
      read("Continue Reading Book")
      viewDetails("View Book Details")
      audio("Listen to Audio Book")
      search("Search Books")
      requestBook("Request Book")
      aiChat("Use AI Chatbot")
      adminSignUp("Admin Registration")
      adminDashboard("Admin Dashboard")
      addBook("Add New Book")
      manageRequests("Manage Book Requests")
    end

    %% User associations (left)
    User -- " " --> signUp
    User -- " " --> login
    User -- " " --> dashboard
    User -- " " --> browse
    User -- " " --> read
    User -- " " --> viewDetails
    User -- " " --> audio
    User -- " " --> search
    User -- " " --> requestBook
    User -- " " --> aiChat

    %% Admin associations (right)
    Admin -- " " --> adminSignUp
    Admin -- " " --> adminDashboard
    Admin -- " " --> addBook
    Admin -- " " --> manageRequests

    %% Internal flows (examples)
    dashboard -- "can" --> browse
    dashboard -- "can" --> read
    dashboard -- "can" --> search
    dashboard -- "can" --> requestBook
    dashboard -- "can" --> aiChat

    browse -- "can" --> viewDetails
    browse -- "can" --> audio

    search -- "can" --> viewDetails
    search -- "can" --> audio

    adminDashboard -- "can" --> addBook
    adminDashboard -- "can" --> manageRequests

    requestBook -- "forwards" --> manageRequests

    %% Ovals for use cases
    classDef usecase stroke:#333,stroke-width:2px,fill:#eef,rx:30,ry:30;
    class signUp,login,dashboard,browse,read,viewDetails,audio,search,requestBook,aiChat,adminSignUp,adminDashboard,addBook,manageRequests usecase
