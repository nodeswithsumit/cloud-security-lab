# Practical 5: Enforcing Compliance with AWS Config

## Objective

Use **AWS Config** to:
- Continuously monitor AWS resource configurations
- Evaluate compliance with security best practices
- Set up rules that alert or report when resources drift from desired states

---

## What is AWS Config?

**AWS Config** is a service that:
- Tracks configuration changes to AWS resources over time
- Compares these configurations to desired policies using **rules**
- Helps in **audit**, **security**, and **compliance**

![AWS Config](</Day1/Images/Screenshot 2025-04-21 at 9.19.20 PM.png>)

---

## Prerequisites

- AWS Admin privileges
- An S3 bucket to store AWS Config snapshots (auto-created or existing)

---

## Steps to Set Up AWS Config

### Step 1: Open AWS Config

- Go to **AWS Console**
- Search for **Config** and open it

---

### Step 2: Set Up AWS Config

1. Click **Get Started**
2. Choose **Record all resources supported in this region**
3. Select an existing S3 bucket or create a new one (e.g., `aws-config-buckets`)

![Step1-1](</Day1/Images/Screenshot 2025-04-21 at 9.38.08 PM.png>)

4. Choose to stream configuration changes to **CloudWatch Logs** (optional)

![Step1-2](</Day1/Images/Screenshot 2025-04-21 at 9.38.12 PM.png>)

5. Click **Next**

---

### Step 3: Add Compliance Rules

1. Choose **Add Rule**
2. Pick **Managed Rules** (prebuilt by AWS)
3. Useful rules to select:
   - `ec2-instance-no-public-ip`: Prevents EC2s from having public IPs

![Select Rules](</Day1/Images/Screenshot 2025-04-21 at 9.34.58 PM.png>)

   - `iam-user-no-policies-check`: Ensures IAM users don’t have inline policies
   - `root-account-mfa-enabled`: Checks if MFA is enabled for the root user
   - `s3-bucket-public-read-prohibited`: Flags public-read S3 buckets

![Selected Rules](</Day1/Images/Screenshot 2025-04-21 at 9.39.13 PM.png>)

4. Configure rule scope:
   - Leave defaults unless you want to restrict to specific resources
5. Click **Add Rule**

![Dashboard](</Day1/Images/Screenshot 2025-04-21 at 9.39.32 PM.png>)

---

### Step 4: Review Compliance Results

- Go to **Rules** tab

![Rules Tab](</Day1/Images/Screenshot 2025-04-21 at 9.40.43 PM.png>)

- See compliance results as **Compliant / Noncompliant**
- Click a rule to view affected resources

![Selected Rule](</Day1/Images/Screenshot 2025-04-21 at 9.40.52 PM.png>)

---

## Key Concepts

| Concept                   | Description |
|---------------------------|-------------|
| **AWS Config**             | Tracks resource changes & compliance |
| **Rules**                  | Define desired configuration states |
| **Compliance Status**      | Shows whether resources meet rules |
| **S3 Bucket**              | Stores configuration snapshots |
| **Managed Rules**          | Predefined by AWS for common best practices |

---

## Use Cases

| Use Case                       | Benefit |
|--------------------------------|---------|
| Compliance Auditing           | Show proof of secure configurations |
| Automated Alerts              | Get notified when resources become non-compliant |
| Change Management            | Track how and when settings were altered |
| Prevent Security Misconfigurations | Flag risky setups like public S3 buckets |

---

## Cleanup (Optional)

- Go to **Settings > Delete AWS Config setup**
- Delete associated S3 bucket and logs

---

# Recap: Enforcing Compliance Using AWS Config

## What We Did

- Enabled **AWS Config** to continuously monitor resource configurations.
- Set up an S3 bucket to store configuration snapshots.
- Added **managed rules** to enforce compliance:
  - No public S3 buckets
  - No inline IAM policies for users
  - MFA for root user
  - EC2 instances without public IPs

---

## What We Learned

### What is AWS Config?

**AWS Config** is a monitoring and compliance tool that:
- Tracks changes to resource configurations
- Ensures your AWS environment follows best practices
- Helps with audits and troubleshooting

---

## Key Terms & Components

| Component                   | Description |
|-----------------------------|-------------|
| **AWS Config**              | Monitors AWS resource configurations |
| **Config Rules**            | Set of compliance checks (managed or custom) |
| **Managed Rules**           | Prebuilt compliance rules by AWS |
| **S3 Bucket**               | Stores resource snapshots and history |
| **Compliance Status**       | Shows which resources are compliant or not |
| **CloudWatch Logs (optional)** | Receives real-time change streams |

---

## Real-World Benefits

| Benefit                        | Why It Matters |
|-------------------------------|----------------|
| Compliance Audits           | Easy reporting for audits (e.g., ISO, HIPAA) |
| Security Best Practices     | Prevent misconfigurations and data leaks |
| Change Visibility           | Track "who changed what, and when" |
| Alerts & Automation         | Detect and respond to security risks quickly |

---

## Example Rules to Explore Further

- `s3-bucket-public-write-prohibited`
- `ec2-instance-managed-by-systems-manager`
- `iam-password-policy`
- `rds-storage-encrypted`

---

## Cleanup Tips

- Disable AWS Config when not in use to save costs
- Delete created S3 buckets if no longer needed

---

## Reference Links

- [AWS Config Home](https://console.aws.amazon.com/config/)
- [AWS Config Rule Reference](https://docs.aws.amazon.com/config/latest/developerguide/managed-rules-by-aws-config.html)