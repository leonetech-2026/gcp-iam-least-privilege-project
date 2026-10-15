
# GCP IAM Least Privilege Security Project

**Google Cloud IAM and Service Accounts Security Project**

## Project Links

- **GitHub Repository:** [View Project Repository](https://github.com/leonetech-2026/gcp-iam-least-privilege-project)
- **GCP Working Environment:** [Google Cloud Project Dashboard](https://console.cloud.google.com/home/dashboard?project=gcp-iam-least-privilege)
- **Architecture Diagram:** [View Security Architecture](https://github.com/leonetech-2026/gcp-iam-least-privilege-project/blob/main/diagram.png)
- **Presentation Slides:** [View Project Presentation](https://docs.google.com/presentation/d/1xm9LhcoWYKnEH3b6ag9PGbShNFfTFLrX/edit?usp=sharing&ouid=102980885387166603628&rtpof=true&sd=true)

**Note:** The Google Cloud dashboard requires authorized access. It is not a publicly accessible application. Presentation access depends on Google Drive sharing permissions.

## Project Overview

This project demonstrates how Google Cloud Platform (GCP) Identity and Access Management (IAM) protects cloud resources through the **principle of least privilege**.

The project uses Google Cloud Storage, IAM policies, and two service accounts with different permissions to demonstrate secure access management.

The IAM Reader service account is assigned read-only access, while the IAM Writer service account is assigned permissions to read and upload storage objects.

Testing was performed using Google Cloud Shell and service account impersonation to verify successful operations and permission-denied behavior.

**Project Status:** IAM configuration and core storage permission tests completed. Evidence is documented through screenshots and Cloud Shell command outputs. Cloud Audit Logs verification is not yet documented.

## Project Objectives

- Understand IAM principals, roles, permissions, and policies.
- Configure access using predefined roles with limited permissions.
- Implement the principle of least privilege.
- Configure secure service accounts.
- Test authorized read and write operations.
- Verify unauthorized access restrictions.
- Document configurations and security testing evidence.

## Technologies and Services

| Technology | Purpose |
| --- | --- |
| Google Cloud Platform | Cloud computing environment |
| Cloud IAM | Access control and role assignments |
| Service Accounts | Separate Reader and Writer identities |
| Google Cloud Storage | Storage resource for testing |
| Google Cloud Shell | Command-line configuration and testing |
| Service Account Impersonation | Test permissions without downloading keys |
| Cloud Audit Logs | Review supported administrative and access events |
| GitHub | Version control and project documentation |

## Security Architecture

![GCP IAM Security Architecture](./diagram.png)

The architecture illustrates the interaction between the Google Cloud environment, the IAM Reader, the IAM Writer, and the secured Cloud Storage bucket.

The IAM Reader has read-only access, while the IAM Writer can perform authorized read and write operations.

**Security principle:** Users and service accounts receive only the permissions necessary to perform their assigned responsibilities.

## Implementation Plan and Completed Activities

### Step 1: Prepare the Google Cloud Project

1. Sign in to the Google Cloud Console.
2. Select the project `gcp-iam-least-privilege`.
3. Review billing and budget settings.
4. Configure Google Cloud Shell for the project.
5. Identify the Cloud Storage bucket used for testing.

**Project ID:** `gcp-iam-least-privilege`

**Storage Bucket:** `gcp-iam-least-privilege-2026-demo`

**Bucket Region:** `US-EAST1`

### Step 2: Review IAM Access

1. Open IAM & Admin > IAM.
2. Review principals and their assigned roles.
3. Identify the required storage permissions.
4. Verify the IAM Reader and IAM Writer role assignments.
5. Review the bucket IAM policy using Google Cloud Shell.

### Step 3: Configure Least Privilege

Two service accounts were configured with separate responsibilities.

| Service Account | IAM Role | Access |
| --- | --- | --- |
| IAM Reader | Storage Object Viewer | Read and list storage objects |
| IAM Writer | Storage Object User | Read, list, and upload storage objects |

The roles were assigned to the Cloud Storage bucket.

The bucket configuration includes:

- Uniform bucket-level access enabled.
- Public access prevention enforced.
- Standard storage class.
- Google-managed encryption keys.

### Step 4: Review Service Account Security

1. Open IAM & Admin > Service Accounts.
2. Verify that the Reader and Writer service accounts exist.
3. Review their assigned permissions.
4. Verify that the service accounts do not require downloaded private keys for testing.
5. Configure authorized service account impersonation.

An initial impersonation attempt was denied because the testing user lacked the required Service Account Token Creator permission.

After the appropriate impersonation permissions were configured, testing proceeded successfully.

### Step 5: Validate Access

Cloud Shell was used to test operations under the configured service account identities.

The tests verified that:

- Authorized storage operations succeeded.
- The IAM Reader could list storage objects.
- The IAM Reader could not upload a new object.
- The IAM Writer could upload objects.
- The IAM Writer could list storage objects.

## Testing Results

| Test Case | Expected Result | Actual Result |
| --- | --- | --- |
| Authorized storage upload | Upload succeeds | Passed |
| IAM Reader lists objects | Read permitted | Passed |
| IAM Reader uploads object | Permission denied | Passed |
| IAM Writer uploads object | Upload succeeds | Passed |
| IAM Writer lists objects | Read permitted | Passed |
| IAM role verification | Assigned roles visible | Passed |
| Cloud Audit Logs review | Relevant events visible if enabled | Not yet verified |

## Evidence and Screenshots

The following screenshots document the IAM configuration and testing activities.

### Evidence 1: IAM Role Assignments

This screenshot shows the IAM configuration used to manage access to the Google Cloud environment.

![IAM Role Assignments](./screenshots/iam-role-assignments.png)

### Evidence 2: Service Account Configuration

This screenshot shows the IAM Reader and IAM Writer service accounts configured for the project.

![Service Account Configuration](./screenshots/service-account-configuration.png)

### Evidence 3: Successful Storage Upload

A test file was successfully uploaded to the Cloud Storage bucket using an authorized identity.

![Storage Upload Success](./screenshots/storage-upload-success.png)

### Evidence 4: Permission Denied

The IAM Reader attempted to upload a file but was denied because it lacked the `storage.objects.create` permission.

This demonstrates the enforcement of least privilege.

![Permission Denied](./screenshots/permission-denied.png)

### Evidence 5: Authorized Writer Access

The IAM Writer successfully uploaded a test file to the Cloud Storage bucket using service account impersonation.

![Authorized Access](./screenshots/authorized-access.png)

### Evidence 6: Writer Read Access

The IAM Writer successfully listed objects stored in the Cloud Storage bucket.

![Writer Read Access](./screenshots/writer-read-access.png)

## Repository Structure

```text
gcp-iam-least-privilege-project/
├── README.md
├── diagram.png
└── screenshots/
    ├── README.md
    ├── iam-role-assignments.png
    ├── service-account-configuration.png
    ├── storage-upload-success.png
    ├── authorized-access.png
    ├── permission-denied.png
    └── writer-read-access.png
```

## Expected Outcomes and Achievements

- Documented IAM role assignments.
- Configured separate Reader and Writer service accounts.
- Verified authorized Cloud Storage operations.
- Demonstrated permission-denied behavior.
- Confirmed least privilege enforcement.
- Documented security architecture.
- Captured evidence of cloud security testing.

## Security Best Practices

- Grant only the permissions required for assigned tasks.
- Use separate identities for different responsibilities.
- Avoid unnecessary Owner and Editor permissions.
- Prefer service account impersonation over downloadable keys.
- Enable public access prevention where appropriate.
- Review IAM policies regularly.
- Use Cloud Audit Logs for supported security investigations.
- Never publish private keys, access tokens, or credentials.
- Remove temporary lab resources when the assignment is complete.

## Project Limitations

The Google Cloud Console dashboard requires authentication and appropriate IAM permissions.

Cloud Audit Logs availability depends on the service and audit-log configuration. Log verification has not yet been documented.

The project demonstrates IAM access restrictions for a selected Cloud Storage bucket. It does not represent a complete production security deployment.

## Conclusion

This project successfully demonstrates how Google Cloud IAM and service accounts support the principle of least privilege.

The IAM Reader was able to perform authorized read operations but was prevented from uploading objects. The IAM Writer successfully performed authorized storage operations.

These results demonstrate how carefully assigned IAM permissions help protect cloud resources from unauthorized access.

The project also provides practical experience with cloud security configuration, service account management, permission testing, and technical documentation.

## References

- [Google Cloud IAM Overview](https://cloud.google.com/iam/docs/overview)
- [IAM Roles and Permissions](https://cloud.google.com/iam/docs/understanding-roles)
- [Service Accounts Overview](https://cloud.google.com/iam/docs/service-account-overview)
- [Cloud Storage IAM Roles](https://cloud.google.com/storage/docs/access-control/iam-roles)
- [Service Account Impersonation](https://cloud.google.com/iam/docs/impersonating-service-accounts)
- [Cloud Audit Logs Overview](https://cloud.google.com/logging/docs/audit)
