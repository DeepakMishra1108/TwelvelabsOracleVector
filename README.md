# TwelvelabsOracleVector

A solution for generating, storing, and querying video embeddings using the [Twelve Labs Marengo model](https://www.twelvelabs.io/) and Oracle Database with vector search capabilities.

## Overview

This repository enables you to:
- **Generate embeddings** for video files using the Twelve Labs Marengo model.
- **Store video segment embeddings** in an Oracle Database (with vector datatype and vector index).
- **Perform semantic and similarity search** on video embeddings stored in Oracle DB.

It is ideal for building video search, recommendation, or content understanding applications leveraging Oracle's vector search features.

## Features

- **Video Embedding Pipeline**: Extract and store segment-wise embeddings (visual-text & audio) from videos.
- **Oracle Vector Database Integration**: Store embeddings in Oracle DB with efficient vector search.
- **Batch Processing**: Supports single video or batch processing of directories.
- **Similarity Search**: Query the database using natural language and find similar video segments.
- **Schema Automation**: Scripts for creating and dropping vector-enabled schema/index.

## Directory Structure

- `store_video_embeddings.py`: Main script to process video files, generate embeddings, and store in Oracle DB.
- `query_video_embeddings.py`: Script to run similarity search queries on stored embeddings.
- `create_schema_video_embeddings.py`: Script to create/drop the vector-enabled schema and index in Oracle DB.

## Requirements

- Python 3.8+
- Oracle Database 23.7+ (for vector datatype and index)
- [twelvelabs](https://pypi.org/project/twelvelabs/) Python SDK
- [oracledb](https://pypi.org/project/oracledb/) Python driver
- [python-dotenv](https://pypi.org/project/python-dotenv/)
- Oracle Cloud wallet files (for secure DB connection)
- Twelve Labs API key

## Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/DeepakMishra1108/TwelvelabsOracleVector.git
   cd TwelvelabsOracleVector
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set environment variables:**
   Create a `.env` file with the following (replace with your credentials):
   ```
   ORACLE_DB_USERNAME=your_db_username
   ORACLE_DB_PASSWORD=your_db_password
   ORACLE_DB_CONNECT_STRING=your_db_connect_string
   ORACLE_DB_WALLET_PATH=path_to_wallet_dir
   ORACLE_DB_WALLET_PASSWORD=your_wallet_password
   TWELVE_LABS_API_KEY=your_twelvelabs_api_key
   ```

## Usage

### 1. Create Schema

Run the schema creation script to set up the table and vector index:
```bash
python create_schema_video_embeddings.py
```

### 2. Store Video Embeddings

Process a video file (or all videos in a folder) and store segment embeddings:
```bash
python store_video_embeddings.py <path_to_video_or_folder>
```

### 3. Query Video Embeddings

Perform semantic similarity search using a text query:
```bash
python query_video_embeddings.py "Describe the scene where..."
```

You can pass multiple queries as arguments for batch search:
```bash
python query_video_embeddings.py "query1" "query2"
```

## How It Works

- **Embedding Extraction:** Uses Twelve Labs API to generate segment-wise video embeddings (visual-text, audio).
- **Database Storage:** Stores each segment's embedding vector, start/end time, and video file info in Oracle DB.
- **Vector Search:** Uses Oracle's vector index for fast similarity search based on cosine distance.

## Customization

- **Segment Duration:** Set the segment duration in seconds via `SEGMENT_DURATION` in the code.
- **Model Selection:** Change embedding models via `EMBEDDING_MODEL`.
- **Batch Size:** Adjust batch insert/search sizes as needed.

## Notes

- Ensure your Oracle Database version supports vector datatypes and indexing.
- The solution handles both individual video files and batch video directories.
- Task IDs and processing state are tracked in `video_task_ids.json` to avoid reprocessing.

## License

[MIT](LICENSE)

## Author

Deepak Mishra

---

For issues or feature requests, open an [issue](https://github.com/DeepakMishra1108/TwelvelabsOracleVector/issues).
