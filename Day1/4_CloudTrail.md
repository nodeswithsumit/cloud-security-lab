# Practical 4: Using AWS CloudTrail for Security Monitoring

## Objective

Enable **AWS CloudTrail** to track all user and service activity within your AWS account for auditing, compliance, and security monitoring purposes.

---

## What is CloudTrail?

**AWS CloudTrail** is a service that enables governance, compliance, operational auditing, and risk auditing by recording account activity.

It records actions taken via:
- AWS Management Console
- AWS CLI
- AWS SDKs and APIs

---

## Prerequisites

- Admin-level AWS account
- S3 bucket (can create during setup or reuse an existing one)

---

## Steps to Enable CloudTrail

### Step 1: Open CloudTrail

- Go to **AWS Console**
- Search for **CloudTrail**

![CloudTrail Dashboard](</Day1/Images/Screenshot 2025-04-21 at 8.45.00 PM.png>)

---

### Step 2: Create a New Trail

1. Click **Create trail**
2. Name your trail (e.g., `SecurityTrail`)
3. Choose **Create a new S3 bucket** or use an existing one -- I Created new bucket
4. (Optional) Enable log file encryption with AWS KMS - I kept if disabled for now

![Step1-1](</Day1/Images/Screenshot 2025-04-21 at 8.59.48 PM.png>)

5. Select **Apply trail to all regions** (recommended)
6. Choose **Management events**:
   - Read/Write events: **All**

![Step1-2](</Day1/Images/Screenshot 2025-04-21 at 8.59.54 PM.png>)

7. Leave **Insight events** off for now (or enable if needed)

![Step1-3](</Day1/Images/Screenshot 2025-04-21 at 9.00.14 PM.png>)

8. Click **Create trail**


![Step1-4](</Day1/Images/Screenshot 2025-04-21 at 9.00.22 PM.png>)


CloudTrail is now logging activity to your S3 bucket.

![Trail Created](</Day1/Images/Screenshot 2025-04-21 at 9.00.33 PM.png>)

---

### Step 3: Test It

1. Perform an action (e.g., log in, create or delete a resource)
2. Go to your **S3 bucket**

![My Bucket](</Day1/Images/Screenshot 2025-04-21 at 9.02.07 PM.png>)

I created a folder called Sample for logging check. 

![sample folder ](</Day1/Images/Screenshot 2025-04-21 at 9.02.07 PM-1.png>)

3. Open folders: `AWSLogs/ACCOUNT_ID/CloudTrail/REGION/YYYY/MM/DD/`

![Log Created](</Day1/Images/Screenshot 2025-04-21 at 9.02.24 PM.png>)

4. Download and open the `.json.gz` log file
5. Use a JSON viewer or text editor to read actions
![json file](</Day1/Images/Screenshot 2025-04-21 at 9.03.38 PM.png>)

---

## Key Concepts

| Component          | Description |
|--------------------|-------------|
| **CloudTrail**      | Logs all account activity |
| **Event**           | A record of an action performed by a user/service |
| **S3 Bucket**       | Stores log files |
| **Read/Write Events** | Distinguishes between actions like "viewing" vs "modifying" |
| **Multi-region Trail** | Captures events from all regions, not just the one you're in |

---

## Use Cases

| Use Case                            | Benefit |
|-------------------------------------|---------|
| Incident Investigation            | Know who did what and when |
| Compliance Audits                 | Provide logs for auditors |
| Detecting Misuse or Misconfigurations | See unauthorized or risky actions |
| Change Tracking                   | Track changes across services like EC2, IAM, S3 |

---

## Cleanup (Optional)

- Go to **CloudTrail > Trails**
- Delete the trail if not needed
- Delete the related S3 bucket if no longer used

---


# Recap: AWS CloudTrail – Monitoring Cloud Activity

## What We Did

- Enabled **AWS CloudTrail** to record API activity and user actions.
- Configured a trail that:
  - Applies to all regions
  - Logs both read and write management events
  - Stores logs in an S3 bucket
- Performed test actions and verified activity logs in the S3 bucket.

---

## What We Learned

### What is AWS CloudTrail?

CloudTrail is a governance and security service that records AWS account activity, giving visibility into actions taken by users, roles, and AWS services.

---

## Key Components Used

| Component           | Description |
|---------------------|-------------|
| **CloudTrail**       | Records API activity across AWS |
| **Trail**            | Configuration for what and where to log |
| **S3 Bucket**        | Stores logs securely |
| **Events**           | Represent actions performed (e.g., `CreateUser`, `RunInstances`) |
| **Multi-Region Trail** | Ensures all AWS regions are monitored |

---

## Why It’s Important

| Benefit                        | Impact |
|--------------------------------|--------|
| Incident Analysis            | Know who did what and when |
| Audit & Compliance           | Meet legal/regulatory requirements |
| Security Threat Detection    | Spot unusual or unauthorized activity |
| Operational Insight         | Understand API usage patterns |

---

## Real-World Example

If a malicious actor creates a new IAM user or deletes an S3 bucket, CloudTrail captures that activity, which can be:
- Reviewed for investigation
- Triggered for alerts using AWS Config, CloudWatch, or GuardDuty

---

## Cleanup Tips

- Delete trail and S3 logs if no longer needed (to avoid storage costs)
- Retain if you want continuous monitoring

---


## References

- [CloudTrail Official Documentation](https://docs.aws.amazon.com/cloudtrail/index.html)
- [Analyzing CloudTrail Logs](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-log-file-examples.html)

---