graph TB
    subgraph "Browser Client"
        A[HTML Frontend] --> B[File Upload]
        A --> C[Video Player]
        A --> D[Audio Player]
    end

    subgraph "FastAPI Server"
        E[Session Manager] --> F[Streaming Routes]
        F --> G["/start-streaming-session"]
        F --> H["/stream-mjpeg"]
        F --> I["/get-audio"]
        F --> J["/stop-streaming-session"]
        E --> K[Model Cache]
    end

    subgraph "Core Processing"
        L[yield_frames Generator] --> M[OpenCV Frame Processing]
        M --> N[JPEG Encoding]
        N --> O[MJPEG Stream]
        L --> P[Wav2Lip Model]
        L --> Q[Face Detector]
    end

    subgraph "AI/ML Stack"
        R[PyTorch + MPS] --> S[Wav2Lip Neural Network]
        S --> T[Face Alignment]
        T --> U[Audio Mel Spectrogram]
    end

    B --> G
    G --> E
    H --> L
    I --> D
    L --> P
    L --> Q
    P --> R
    Q --> R
    O --> C

    style A fill:#e1f5fe
    style E fill:#f3e5f5
    style L fill:#e8f5e8
    style R fill:#fff3e0
