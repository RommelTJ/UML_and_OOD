# Case Study: Designing a Note-Taking App from Scratch

* Practice by designing a Note-taking app.
* Understand the requirements
* Write User Stories
* Map User Stories to Use Case Diagrams
* Identify the main entities and relationships
* Model Behavior
* Represent object states

## Collecting Requirements

Features:  
* Create and edit text-based notes
* Attach photos/videos
* Capture hand-drawn sketches
* Password-protect individual notes
* Sync app data to Dropbox, iCloud or Google Drive

Functional Requirements:  
* We need to build a note-taking app
* Users can create and edit text-based notes
* A note may include images or hand-drawn sketches
* Sensitive notes can be protected with a password
* App can automatically upload notes to cloud storage services

Non-Functional Requirements:  
* Should be easy to use and intuitive
* Must run in the latest version of iOS
* Should handle a large number of notes
* Must be secure
* Must include support email and link to website

## Creating User Stories

From the functional requirements, we've identified 3 major topics:   
* Note creation/editing
* Privacy
* Syncing to cloud servers

Thus, we create 3 epics:  
* Note Creation and Editing
  * As a user, I want to create and edit notes so that I can quickly jot down my thoughts.
  * As a user, I want to attach photos to a note so that I can keep my memories in one place.
  * As a user, I want to add handwritten sketches so that I can insert funny toons into my notes.
* Privacy
  * As a user, I want to create private notes so that only I can access them.
  * As a user, I want to protect my sensitive notes with a password.
* Syncing to cloud servers
  * As a user, I want to sync my notes across my iOS devices so that my data is up-to-date on all of them.
  * As a user, I want my notes automatically uploaded to cloud servers (Dropbox, Google Drive, or iCloud) so that 
    I have a backup of all my data. 

## Diagramming the main use cases

Note Creation and Editing Use Case Diagram
```mermaid
flowchart LR
  TRIGGER([User])-->S1
  TRIGGER([User])-->S2
  
  %% Main success scenario %%
  subgraph Note App
    S1[Create Note]-->S3
    S1[Create Note]-->S4
    S2[Edit Note]-->S3
    S2[Edit Note]-->S4
    
    S3[Attach Photo]
    S4[Add Handwritten Sketch]
  end
```

Privacy Use Case Diagram
```mermaid
flowchart LR
  TRIGGER([User])-->S1
  
  %% Main success scenario %%
  subgraph Note App
    S1[Create Note]-->S2
    S2[Create Private Note]-->S3
    S3[Protect with Password]
  end
```

Syncing to Cloud Servers Use Case Diagram
```mermaid
flowchart LR
  TRIGGER([User])-->S1
  TRIGGER([User])-->S2
  S1-- upload -->S3
  S2-- upload -->S3
  
  %% Main success scenario %%
  subgraph Note App
    S1[Create Note]
    S2[Edit Note]
  end
  
  subgraph Cloud Server
    S3[Dropbox]
  end
```

## Modeling the classes and relationships

```mermaid
classDiagram
  class Note {
    -note: String
    -photos: List[Image]
    -sketches: List[Sketch]
    +setText(text: String)
    +getText(): String
    +addImage(image: Image)
    +getImages(): List[Image]
    +addSketch(sketch: Sketch)
    +retrieveAllSketches(): List[Sketch]
  }
  
  class Image
  
  class Sketch
  
  class SecureNote {
   -passwordHash: String
  }
  
  class Crypto {
   + hash(input: String): String
  }
  
  class LocalPersistence {
    <<interface>>
    + getNotes(): List[Note]
    + save(note: Note)
    + update(note: Note)
    + delete(note: Note)
  }
  
  class FileManager
  
  class NetworkController {
    + create(note: Note)
    + getNotes(): List[Note]
    + delete(note: Note)
    + update(note: Note)
  }
  
  Note *--> Image
  Note *--> Sketch
  Note <|-- SecureNote
  Note <.. LocalPersistence
  Note <.. NetworkController
  
  SecureNote ..> Crypto
  
  FileManager ..|> LocalPersistence
```

## Describing the flow of note creation using sequence diagrams

* Adding a note flow
```mermaid
sequenceDiagram
    aView->>aController: onCreateNote
    aController-->>aNote: <<create>> new Note
    aView->>aController: onSaveNote
    par aController to aFileManager
      aController-->>aFileManager: <<async>> save(note: Note)
      aFileManager-->>aController: success
    and aController to anOnlineManager
      aController-->>anOnlineManager: <<async>> upload(note: Note)
      anOnlineManager-->>aController: success
    end
```

## Modeling the states of a note object

```mermaid
stateDiagram-v2
  [*] --> New: Note Created
  New --> Unsaved: Details Added
  Unsaved --> [*]: Cancel
  
  Unsaved --> Archived: app terminated
  Archived --> Unsaved: app started
    
  Unsaved --> Saved: Saved and Pending Upload
  Saved --> Unsaved: Save or Upload Failed
  Saved --> PersistedAndUploaded: Save and Upload Successful
  Saved --> Persisted: Save Ok, Upload Failed
  
  Persisted --> PendingUpload: Retry Upload
  PendingUpload --> Persisted: Retry Failed
  PendingUpload --> PersistedAndUploaded: Upload Successful
  
  PersistedAndUploaded --> [*]
```
