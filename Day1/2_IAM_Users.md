# Practical 2: IAM – Identity and Access Management (AWS)

## Objective
Use AWS Identity and Access Management (IAM) or Azure Active Directory (AD) to manage user identities and access to cloud resources.

Learn to securely manage user identities and control access to AWS resources by:
- Creating IAM users and groups
- Attaching permission policies
- Using the principle of least privilege
- Testing access control via IAM console login

---

## teps to Perform

### Step 1: Open IAM Service
- Go to **AWS Console**
- Search for and open **IAM**
![IAM Dashboard](</Day1/Images/Screenshot 2025-04-21 at 5.34.51 PM.png>)

---

### Step 2: Create a User Group
1. Navigate to **User groups** > **Create group**
2. Group name: `ReadOnlyGroup`
3. Attach AWS Managed Policy: **`ReadOnlyAccess`**
4. Click **Create group**

![Creating Group & Policy](</Day1/Images/Screenshot 2025-04-21 at 5.38.16 PM.png>)
This group will only allow view access across all AWS services.

---

### Step 3: Create an IAM User
1. Navigate to **Users** > **Add users**
2. Set username: `testuser`
3. Select: **AWS Management Console access**
4. Set a custom password

![Created User](</Day1/Images/Screenshot 2025-04-21 at 5.40.21 PM.png>)

5. Assign the user to `ReadOnlyGroup`

![Assigned Policy](</Day1/Images/Screenshot 2025-04-21 at 5.41.04 PM.png>)

6. Click **Create user**

![User Created](</Day1/Images/Screenshot 2025-04-21 at 5.41.28 PM.png>)
---

### Step 4: Test Access
1. Use the provided **IAM login URL** (e.g. `https://<account-id>.signin.aws.amazon.com/console`)
2. Log in as `testuser`

![Log in Stage](</Day1/Images/Screenshot 2025-04-21 at 5.42.14 PM.png>)

3. Try accessing services like **S3**, **EC2**, etc.
   - ✅ View access should work
   - ❌ Create/Delete access will be blocked

![Access failed for upload](</Day1/Images/Screenshot 2025-04-21 at 5.46.57 PM.png>)
---

### Step 5 (Optional): Create a Custom Policy
1. Go to **Policies** > **Create policy**
2. Choose **JSON** tab and paste:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:Get*", "s3:List*"],
      "Resource": "*"
    }
  ]
}
```
![Custom Policy for S3](</Day1/Images/Screenshot 2025-04-21 at 5.50.38 PM.png>)

# Practical 2 Recap: IAM – Identity and Access Management (AWS)

##  What You Learned

- Accessed AWS IAM service
- Created a **user group** named `ReadOnlyGroup`
- Attached AWS-managed policy **ReadOnlyAccess** to the group
- Created a **new IAM user** named `testuser`
- Assigned the user to the `ReadOnlyGroup`
- Logged in with the new IAM user to test permissions
- (Optional) Created a **custom policy** for S3 read-only access

---


### IAM (Identity and Access Management)
A secure way to manage access to AWS services and resources.

### Key Concepts

| Component          | Description |
|--------------------|-------------|
| **IAM User**        | Represents a person/application with access credentials |
| **IAM Group**       | A way to manage permissions for multiple users at once |
| **IAM Policy**      | A JSON-based rule set defining allowed actions and resources |
| **Managed Policy**  | Predefined by AWS (e.g., `ReadOnlyAccess`) |
| **Custom Policy**   | Created manually for fine-grained control |
| **Least Privilege** | Security principle: give only the minimum necessary access |

---

## Why It Matters

- Helps maintain **security** and **auditability**
- Ensures proper **access control**
- Reduces the risk of **accidental changes** or **malicious activity**
- Forms the foundation for **secure AWS usage**

---

## Cleanup Checklist (Optional)

- ❌ Delete `testuser` if not needed
- ❌ Remove unused policies or groups
- 🔄 Rotate IAM credentials regularly
- ✅ Enable MFA (Multi-Factor Authentication) – coming up next when required!

---

## 📎 References

- [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [IAM Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html)

