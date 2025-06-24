## Description

Scout Suite is an open source multi-cloud security-auditing tool, which enables security posture assessment of cloud environments. Using the APIs exposed by cloud providers, Scout Suite gathers configuration data for manual inspection and highlights risk areas. Rather than going through dozens of pages on the web consoles, Scout Suite presents a clear view of the attack surface automatically.

Scout Suite was designed by security consultants/auditors. It is meant to provide a point-in-time security-oriented view of the cloud account it was run in. Once the data has been gathered, all usage may be performed offline.

The project team can be contacted at <scoutsuite@nccgroup.com>.

### Cloud Provider Support

The following cloud providers are currently supported:

- Amazon Web Services
- Microsoft Azure
- Google Cloud Platform
- Alibaba Cloud (alpha)
- Oracle Cloud Infrastructure (alpha)
- Kubernetes clusters on a cloud provider (alpha)
- DigitalOcean Cloud (alpha)

## Installation

### Prerequisites

- [VS Code](https://code.visualstudio.com/) or [Cursor](https://cursor.sh/) (VS Code derivative)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- Dev Containers:
   - [for Cursor](https://marketplace.cursorapi.com/items?itemName=anysphere.remote-containers)
   - [for VS Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### Setup with DevPod and VS Code/Cursor

1. **Clone the Scout Suite repository:**
   ```bash
   git clone https://github.com/aft-analytics/ScoutSuite.git
   cd ScoutSuite
   ```

3. **Connect via VS Code or Cursor:**
   - Open VS Code or Cursor
   - Use `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac) to open the command palette
   - enter "Reopen in container"

   This will automatically open VS Code with the remote connection established.

5. **Verify the environment:**
   ```bash
   # Check if Scout Suite is available
   scout --help
   ```

For additional setup options and troubleshooting, refer to the [wiki](https://github.com/nccgroup/ScoutSuite/wiki/Setup).

## Usage

configure credentials for AWS accounts

```bash
aws configure --profile [ds|prod|dev]

# to select a profile use below
export AWS_PROFILE=ds
```

Scout Suite is run through the CLI:

![Running Scout Suite](https://user-images.githubusercontent.com/13310971/78389085-22659d00-75b0-11ea-9f22-ea6fcaa6a1cd.gif)

Once this has completed, it will generate an HTML report including findings and Cloud account configuration:

![Scout Suite Report](https://user-images.githubusercontent.com/13310971/77861662-342bf680-71e4-11ea-8eed-ccaeb78c5f45.gif)

### Region-Specific Scanning

You can restrict the scan to specific regions or exclude certain regions from the scan:

#### AWS
```bash
# Scan specific regions
scout aws -r us-east-1 us-west-2

# Exclude specific regions
scout aws -xr ap-southeast-1 ap-southeast-2
```

#### Azure
```bash
# Scan specific regions
scout azure -r eastus westus2

# Exclude specific regions
scout azure -xr southeastasia eastasia
```

#### GCP
```bash
# Scan specific regions
scout gcp -r us-central1 europe-west1

# Exclude specific regions
scout gcp -xr asia-east1 asia-southeast1
```

Additional information can be found in the [wiki](https://github.com/nccgroup/ScoutSuite/wiki). 
There are also a number of handy [tools](https://github.com/nccgroup/ScoutSuite/tree/master/tools) for automation of common tasks.

## Synchronizing with upstream

checkout upstream

```bash
cd ScoutSuite
git remote add upstream https://github.com/nccgroup/ScoutSuite
```

pull updates

```bash
git checkout -b upstream-master upstream/master
# pull all updates from upstream
git pull

# go back to origin/master branch to rebase upstream changes onto our own
git checkout master
git rebase upstream-master
# resolve conflicts if any

# push all updated changes to origin/master branch
git push
```