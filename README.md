# Bridgecrew Orb for CircleCI

## The Bridgecrew Orb

Use the Bridgecrew orb to scan for infrastructure-as-code errors in your CircleCI Workflows.
By utilizing this orb in your project workflow, you can automatically start to find,
fix and monitor your project for configuration errors in Terraform and CloudFormation. 
By signing up for a free Bridgecrew Community plan you can also view dashboards and reports. 
The community plan does not limit the number of scans or users you can invite to view the results.
​
## How to use the Bridgecrew Orb

In fact, it is very easy to start using the Orb.
All you need to do is:

1. Follow the instructions at the [Orb Quick Start Guide](https://circleci.com/orbs/registry/orb/bridgecrew/bridgecrew#quick-start) to enable usage of Orbs in your project workflow.
2. Set up an environment variable with your Bridgecrew API key, which you can get from your [Bridgecrew account](https://www.bridgecrew.cloud/integrations).
3. In the app build job, call the `bridgecrew/scan`
4. Optionally, supply parameters to customize orb behaviour
5. Prisma members - set your prisma cloud API URL which you can get from [Prisma cloud API URLs](https://prisma.pan.dev/api/cloud/api-urls). Your environment variable (api-key-variable) requires to be a prisma cloud access key in the following format: <access_key_id>::<secret_key>

## Usage Examples

### Scan IaC Directory

```yaml
version: 2.1

  orbs:
    bridgecrew: bridgecrew/bridgecrew@x.y.z

  jobs:
    build:
      executor: bridgecrew/default
      steps:
        - checkout
        - bridgecrew/scan:
            directory: '.'
            soft-fail: true
            api-key-variable: BC_API_KEY
            prisma-api-url: PRISMA_API_URL
```

### Scan IaC Files

```yaml
version: 2.1

orbs:
  bridgecrew: bridgecrew/bridgecrew@x.y.z

jobs:
  build:
    executor: bridgecrew/default
    steps:
      - checkout
      - bridgecrew/scan:
          file: "./terraform/db-app.tf"
          api-key-variable: BC_API_KEY
          prisma-api-url: PRISMA_API_URL
```

### Advanced Example

```yaml
version: 2.1

orbs:
bridgecrew: bridgecrew/bridgecrew@x.y.z

jobs:
build:
    executor: bridgecrew/default
    steps:
    - checkout
    - bridgecrew/scan:
        directory: "./terragoat"                # tell bridgecrew where is the directory you want to scan
        soft-fail: true                         # do not fail the workflow in case vulnerabilities have found 
        api-key-variable: BC_API_KEY            # bridgecrew API key or prisma cloud access key (see PRISMA_API_URL)
        prisma-api-url: PRISMA_API_URL # prisma cloud API URL (see: https://prisma.pan.dev/api/cloud/api-urls). Requires api-key-variable to be a prisma cloud access key in the following format: <access_key_id>::<secret_key>
```

## Orb Parameters

Full reference docs https://circleci.com/orbs/registry/orb/bridgecrew/bridgecrew

| Parameter  | Description                                                          | Required | Default | Type                  |
| -----------|----------------------------------------------------------------------| ------------- | ------------- |-----------------------|
| api-key-variable | Environment variable name for the Bridgecrew API key from Bridgecrew app | no | BC_API_KEY | env_var_name          |
| prisma-api-url | Prisma Cloud API URL                  | no | "none" | string                |
| directory | IaC root directory to scan                                           | no | "none" | string                |
| file | IaC file to scan                                                     | no | "none" | string                |
| soft-fail | Runs checks without failing build                                    | no | false | boolean               |
| output | Report output format                                                 | no | "cli" | cli \ json \ junitxml |

## Screenshots
Run bridgecrew orb in your CircleCI workflow
![scan-screenshot](https://raw.githubusercontent.com/bridgecrewio/bridgecrew-orb/master/screenshot.gif)
