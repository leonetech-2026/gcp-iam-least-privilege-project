# GCP IAM Least Privilege Security Project
**Security Project on Google Cloud IAM and Service Accounts**

## Links to Project
- **GitHub Repository:** [View Project Repo](https://github.com/leonetech-2026/gcp-iam-least-privilege-project)
- **GCP Working Environment:** Google Cloud Project Dashboard [https://console.cloud.google.com/home/dashboard?project=gcp-iam-least-privilege]- **Architecture Diagram:** [Security Architecture](https://github.com/leonetech-2026/gcp-iam-least-privilege-project/blob/main/diagram.png)
- **Presentation Slides** [Project Presentation](https://docs.google.com/presentation/d/1xm9LhcoWYKnEH3b6ag9PGbShNFfTFLrX/edit?usp=sharing&ouid=102980885387166603628&rtpof=true&sd=true)

**Note:** The Google Cloud dashboard is for authorized access only. It’s not something the public can use. Access to presentations is governed by sharing permissions set in Google Drive.

# Project Summary

This project illustrates how Google Cloud Platform (GCP) Identity and Access Management (IAM) secures cloud resources according to the **principle of least privilege**.

The project demonstrates how to handle secure access using Google Cloud Storage, IAM policies, and two service accounts with different access rights.

IAM Reader service account is granted read-only access IAM Writer service account is granted permissions to read and upload storage objects

We ran tests on Google Cloud Shell using service account impersonation to verify correct operation and permission-denied behavior.

**Project Status:** IAM configuration, permissions for the service account, tested Cloud Storage access, verified Cloud Audit Logs Evidence is provided in the form of screenshots and command outputs from Google Cloud Shell. All 7 recorded test cases passed successfully.

### Project Objectives

- Understand IAM principals, roles, permissions and policies.
- Set up access with pre-defined roles with restricted permissions.
- enforce the principle of least privilege.
- Properly configure service accounts.
- Test allowed reads and writes.
- Verify limitations on unauthorized access.
- Document configurations and security testing evidence

## Technologies and Services | Technology | Purpose | |---|---|---| | Google Cloud Platform | Cloud computing environment | | Cloud IAM | Access control and role assignments | | Service Accounts | Separate Reader and Writer identities | | Google Cloud Storage | Storage resource for testing | | Google Cloud Shell | Command-line configuration and testing | | Service Account Impersonation | Test permissions without downloading keys | | Cloud Audit Logs | Review supported administrative and access events | | GitHub | Version control and project documentation |

## Security architecture!![GCP IAM Security Architecture](./diagram.png)

The architecture depicts the interaction between the Google Cloud environment, the IAM Reader, the IAM Writer, and the secured Cloud Storage bucket.

The IAM Reader has read-only access. The IAM Writer can do authorized reads and writes.
**Security principle:** Users and service accounts are granted only the permissions they need to perform their job functions.

##Plan of implementation and activities undertaken

### Step 1: Create the Google Cloud Project

1. Log into the Google Cloud Console.
2. Choose the project `gcp-iam-least-privilege`.
3. Check billing and budget settings.
4. Set up Google Cloud Shell for the project.
5. Identify the bucket for testing in Cloud Storage.

**Project ID:** `gcp-iam-minimum-privilege`
** Storage Bucket: gcp-iam-least-privilege-2026-demo

**S3 Bucket Region:** `US-EAST-1`

### Step 2: Review IAM Access

1. Open IAM & Admin > IAM.
2. Review the principals and their assigned roles.
3. Determine the storage permissions needed.
4. Confirm IAM Reader and IAM Writer role assignments.
5. Review the bucket IAM policy in Google Cloud Shell. ### Step 3: Configure least privilege

We created two service accounts with different responsibilities. | Service account | IAM role | Access | |---|---|---| | IAM Reader | Storage Object Viewer | Read and list storage objects | | IAM Writer | Storage Object User | Read, list and upload storage objects |

The roles were added to the Cloud Storage bucket.

This project shows least privilege, with two service accounts that have different permissions on Cloud Storage. The IAM Reader uses the Storage Object Viewer role and the IAM Writer uses the Storage Object User role.

The IAM policy evidence also has broader administrative permissions for other project principals. These administrative permissions are different from the service account permissions tested in this project. The demonstrated least privilege enforcement is for Reader and Writer service accounts to access the selected Cloud Storage bucket .


The bucket set-up includes:
- Uniform bucket-level access turned on
- Enforced public access prevention.
- Default Storage Class.
- Keys that are managed by Google

#### Step 4: Review Service Account Security

1. Go to IAM & Admin > Service Accounts.
2. Check that the Reader and Writer service accounts exist.
3. Verify permissions.
4. Make sure that no service accounts require downloaded private keys to test.
5. Set up authorized service account impersonation.

The first attempt to impersonate failed because the user being tested did not have the necessary Service Account Token Creator permission.

Testing was successful once the correct permissions for impersonation were set up.

### Step 5: Check Access

Operations with the configured service account identities were tested with Cloud Shell.

The tests indicated that:

- Storage operation authorized, successful.- IAM Reader can list storage objects.
- The IAM Reader was unable to upload a new object.
- IAM Writer could upload objects.- IAM Writer could list storage objects.

## Test Results | Test Case | Expected Outcome | Actual Outcome | |---|---|---| | Authorized storage upload | Upload should succeed | Pass | | IAM Reader can list objects | Read should be permitted | Pass | | IAM Reader uploads object | Permission should be denied | Pass | | IAM Writer uploads object | Upload should succeed | Pass | | IAM Writer can list objects | Read should be permitted | Pass | | IAM role check | Assigned roles should be visible | Pass | | Cloud Audit Logs review | Relevant events should be visible if enabled | Pass |

## Screenshots and Proof

The following screenshots are for IAM configuration and test activities.

### Evidence 1: IAM Role Assignments

This screenshot shows the IAM configuration that controls who can access the Google Cloud environment.[IAM Role Assignments](screenshots/iam-role-assignments.png)

#### Evidence 2: Service Account Configuration

This screenshot shows the IAM Reader and IAM Writer service accounts that are set up for the project. ![Service Account Configuration](./screenshots/service-account-configuration.png)

### Proof 3: Successfully uploaded to storage

The test file was uploaded to the Cloud Storage bucket successfully, with an authorized identity.[Storage Upload Success](./screenshots/storage-upload-success.png)

### Evidence 4: Access denied

The IAM Reader tried to upload a file, but was denied because it didn't have the `storage.objects.create` permission.

This demonstrates least privilege enforcement.[Permission Denied](./screenshots/permission-denied.png)

### Proof 5: Access to Writer Granted

The IAM Writer successfully uploaded a test file to the Cloud Storage bucket using service account impersonation.[Authorized Access](./screenshots/authorized_access.png)

### Evidence 6: Access to Writer Read

The IAM Writer could list the objects in the bucket in Cloud Storage.[Writer Read Access](./screenshots/writer-read-access.png)

### Evidence 7: Verification of Cloud Audit Logs

We examined security-related activities using Google Cloud Logs Explorer. The review found 26 audit log records of IAM policy changes, Cloud Storage permission changes, and service account access-token generation events.

SetIAMPolicy The SetIAMPolicy audit record indicates that Google Cloud logged an IAM policy operation.

**Result**: Passed Relevant admin audit logs were successfully retrieved.[Cloud Audit Logs Validation](./screenshots/cloud-audit-logs-validation.png)

## Repository layout ```text gcp-iam-least-privilege-project/ ├── README.md ├── diagram.png
└── screenshots/ README.md iam-role-assignments.png service-account-configuration.png storage-upload-success.png
    ├── authorized-access.png
    ├── permission-denied.png ├── writer-read-access.png
    └── cloud-audit-logs.png


## Expected Results and Outcomes

- IAM role assignments recorded.- Create separate service accounts for the Reader and the Writer.
- Validated authorized Cloud Storage operations.- Showed permisssion denied behavior.
- Enforcement of least privilege confirmed.
- Documented security architecture.
- Evidence of cloud security testing documented.

### Security considerations

- Grant only the permissions needed to perform assigned tasks.
- Different roles should have different identities.
- Do not give Owner and Editor permissions unnecessarily.
- Prefer service account impersonation to downloadable keys.
- Allow for the avoidance of public access where appropriate.
Regularly review IAM policies.
- Use Cloud Audit Logs for security investigations where applicable.- Never post any private keys, access tokens or credentials
- Clean up temporary lab resources once the assignment is finished.

## Project Constrains
This project shows how to restrict IAM access to a chosen Cloud Storage bucket. It’s not a full production security deployment.

You need to be authenticated and have the correct IAM permissions to access the Google Cloud Console dashboard.

Verifying Cloud Audit Logs Using Google Cloud Logs Explorer. We retrieved a total of 26 relevant audit log entries including IAM policy operations, Cloud Storage permission updates, and service account access token creations. Availability of audit logs depends on the Google Cloud service and logging configuration.

## Final thoughts

This project successfully demonstrates how Google Cloud IAM and service accounts support the principle of least privilege.

The IAM Reader could perform authorized read operations, but it could not upload objects. The IAM Writer was able to perform authorized storage operations

The results illustrate the importance of assigning IAM permissions correctly to safeguard cloud resources against unauthorized access.

The project also offers practical experience with cloud security setups, service account management, permission testing, and technical documentation.

## Literaturverzeichnis
- [Google Cloud IAM introduction](https://cloud.google.com/iam/docs/overview)
- [IAM Roles and Permissions](https://cloud.google.com/iam/docs/understanding-roles)
- [Service account overview](https://cloud.google.com/iam/docs/service-account-overview)
- Cloud Storage IAM Roles https://cloud.google.com/storage/docs/access-control/iam-roles
- [Impersonating Service Accounts](https://cloud.google.com/iam/docs/impersonating-service-accounts)
- [Audit log overview](https://cloud.google.com/logging/docs/audit)
