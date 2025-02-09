# Vocera Run Test Manual

Run automated test scenarios against Vocera agents directly from your GitHub workflow.

This composite action allows you to configure and execute scenarios against specified Vocera agents. It requires specifying an agent ID, the scenario IDs to run, and optionally how many times to run them and a timeout.

## Usage

Add the following workflow to your repository (e.g., `.github/workflows/run-scenarios.yml`):

```yaml
name: Vocera Run Test Manual

on:
  workflow_dispatch:  # Allows manual triggering
    inputs:
      agent_id:
        description: "Agent ID"
        required: true
      scenarios:
        description: "Comma-separated list of scenario IDs"
        required: true
      frequency:
        description: "Number of times to run each scenario"
        required: false
        default: "1"
      timeout:
        description: "Timeout in seconds"
        required: false
        default: "3600"

jobs:
  run-scenarios:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - name: Run Vocera Scenarios
        uses: vocera-ai/vocera-run-test-manual@main
        with:
          agent_id: ${{ github.event.inputs.agent_id }}
          scenarios: ${{ github.event.inputs.scenarios }}
          frequency: ${{ github.event.inputs.frequency }}
          timeout: ${{ github.event.inputs.timeout }}
        secrets:
          API_BASE_URL: ${{ secrets.API_BASE_URL }}
          API_KEY: ${{ secrets.API_KEY }}
```

## Inputs

| Name       | Description                                   | Required | Default |
|------------|-----------------------------------------------|----------|---------|
| agent_id   | ID of the agent where scenarios are executed  | true     | N/A     |
| scenarios  | Comma-separated list of scenario IDs          | true     | N/A     |
| frequency  | Number of times to run each scenario          | false    | 1       |
| timeout    | Timeout in seconds                            | false    | 3600    |

## Secrets

| Name          | Description                           | Required |
|---------------|---------------------------------------|----------|
| API_BASE_URL  | Base URL for connecting to Vocera API | true     |
| API_KEY       | API Key for authentication            | true     |

Make sure to configure the secrets in your GitHub repository settings under "Settings" → "Secrets and variables" → "Actions".

## License

This project is licensed under the [MIT License](LICENSE).

## Support

For questions or assistance, please open an issue in this repository or contact Vocera AI support.

---

© 2024 Vocera AI. All rights reserved.
