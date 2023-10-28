# Kubernetes Logger Pod Backup to AWS S3

This script facilitates the backup of log files from a specific Kubernetes pod to an AWS S3 bucket.

## Description

When you run this script:

1. It sets the Kubernetes context to the desired cluster.
2. Searches for the logger pod in a specified namespace.
3. If the logger pod is found, it copies all the log files from the pod to a temporary directory on your local system.
4. Each log file from the temporary directory is then uploaded to a designated S3 bucket under a directory named after the logger pod.
5. After successful uploads, the temporary directory and its contents are deleted.

## Prerequisites

- AWS CLI configured with the necessary permissions to write to the specified S3 bucket.
- `kubectl` installed and configured with access to the desired Kubernetes cluster.
- Proper permissions to copy files from the specified Kubernetes pod.

## Configuration

Before using the script, update the placeholder values in the following variables:

- `k8s_context`: The context of your Kubernetes cluster.
- `S3_BUCKET_NAME`: The name of your AWS S3 bucket.
- In the `kubectl get pods` command, replace `<namespace>` with the namespace where your logger pod resides and `<pod_name>` with a pattern that matches your logger pod's name.

## Usage

To run the script:

```bash
./<script_name>.sh
```

Replace `<script_name>` with the name you've given to the script.

## Notes

- The script currently searches for pods based on a name pattern. Ensure the pattern uniquely identifies your logger pod to prevent unexpected behaviors.
- Ensure proper cleanup if you make any modifications to the script. Leaving files or sensitive data behind can be a security risk.
- Handle any errors or exceptions that might occur during the script's execution, especially when working in production environments.

## Author

- **Pubudu Dias** - *Initial work* - [Date: 2023/04/13]

## Acknowledgments

- OpenAI's ChatGPT for README preparation.

## Recommendations

For added functionality, consider:

- Enhancing error handling to include more descriptive messages.
- Sending email notifications upon success or failure, similar to the previous scripts.
- Adding functionality to rotate or delete old log files in the S3 bucket.