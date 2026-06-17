# Jarvis - Developer Setup

Follow these steps to set up your local development environment for running the Jarvis ingestion and synthesis pipeline.

## Prerequisites

1. **Python 3:** Ensure Python 3.8+ is installed:
   ```bash
   python3 --version
   ```

2. **Pip & MarkItDown:** Install the markdown converter library:
   ```bash
   pip install markitdown==0.1.1
   ```

3. **Git:** Initialize Git if not already configured:
   ```bash
   git init
   ```

## Folder Setup
Create the required workspace folder structure:
```bash
mkdir -p source-raw source-md wiki public temp
```

## Dependency Verification
Run the bootstrap check script to ensure all tools and files are in place:
```bash
python3 -c "import os,sys; d=['source-raw','source-md','wiki','public','temp']; f=['agents.md','map.md']; sys.exit(0 if all(os.path.isdir(x) for x in d) and all(os.path.isfile(x) for x in f) else 1)" && echo "Bootstrap: OK" || echo "Bootstrap FAILED — re-check files and folders"
```
