# Google Cloud CLI Installation and Setup

## Installation Commands

### 1. Download Google Cloud CLI
```bash
curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-cli-linux-x86_64.tar.gz
```

### 2. Extract the Archive
```bash
tar -xf google-cloud-cli-linux-x86_64.tar.gz
```

### 3. Install Google Cloud CLI
```bash
./google-cloud-sdk/install.sh --quiet
```

### 4. Add to PATH (for current session)
```bash
export PATH=$PATH:/root/google-cloud-sdk/bin
```

### 5. Verify Installation
```bash
/root/google-cloud-sdk/bin/gcloud version
```

## Make PATH Permanent
Add to your shell profile for permanent access:
```bash
echo 'export PATH=$PATH:/root/google-cloud-sdk/bin' >> ~/.bashrc
```

## Authentication Options

### 1. Interactive Authentication (requires browser)
```bash
gcloud auth login
```

### 2. Service Account Authentication (recommended for headless environments)
```bash
gcloud auth activate-service-account --key-file=/path/to/service-account-key.json
```

### 3. Application Default Credentials
```bash
gcloud auth application-default login
```

## Common Commands

After authentication, you can use:
- `gcloud projects list` - List all projects
- `gcloud compute instances list` - List compute instances
- `gcloud storage ls` - List storage buckets
- `gcloud config set project PROJECT_ID` - Set default project

## Installation Status

✅ **COMPLETED** - Google Cloud CLI is installed and configured

- **Version**: 529.0.0
- **Installation Path**: `/root/google-cloud-sdk/`
- **Binary Path**: `/root/google-cloud-sdk/bin/gcloud`
- **PATH Configuration**: Added to ~/.bashrc for permanent access
- **Included Components**: 
  - BigQuery Command Line Tool (bq)
  - Cloud Storage Command Line Tool (gsutil)
  - Google Cloud CLI Core Libraries
  - Bundled Python 3.12

## Authentication Status

✅ **COMPLETED** - Successfully authenticated with Google Cloud

- **Active Account**: orders@nilgiristores.in
- **Available Projects**: 228 projects found
- **Current Project**: None (use `gcloud config set project PROJECT_ID` to set default)

### Common Next Steps
```bash
# Set a default project
gcloud config set project PROJECT_ID

# List all projects (includes system-generated projects)
gcloud projects list

# List only user-created projects (exclude system projects)
gcloud projects list --filter="NOT projectId:sys-*"

# List compute instances
gcloud compute instances list

# List storage buckets
gcloud storage ls

# View current configuration
gcloud config list
```

### Service Account Authentication (Alternative for automation)
1. Download a service account key file from Google Cloud Console
2. Use: `gcloud auth activate-service-account --key-file=/path/to/service-account-key.json`

## Additional Components

Install additional components as needed:
```bash
gcloud components install COMPONENT_ID
```

Popular components:
- `kubectl` - Kubernetes command-line tool
- `docker-credential-gcr` - Docker credential helper
- `alpha` - Alpha commands
- `beta` - Beta commands
