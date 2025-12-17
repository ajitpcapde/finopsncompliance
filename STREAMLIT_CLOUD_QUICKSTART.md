# ⚡ Streamlit Cloud - Quick Start Guide

## 🎯 TL;DR

**You cannot run bash scripts directly in Streamlit Cloud**, but you can:

1. ✅ Deploy AWS infrastructure **once** from your local machine (5 minutes)
2. ✅ Streamlit Cloud app **reads** the threats (read-only access)
3. ✅ Everything works perfectly together!

---

## 🚀 3-Step Setup for Streamlit Cloud

### Step 1: Deploy AWS (Local Machine - 5 Minutes)

```bash
# On YOUR computer (not Streamlit Cloud)
cd production-deployment
./scripts/deploy.sh --email your-email@company.com

# This creates:
# ✅ DynamoDB table for threats
# ✅ Lambda function for detection
# ✅ EventBridge rules
# ✅ SNS alerts

# DONE! AWS is now running and detecting threats
```

---

### Step 2: Prepare GitHub Repository

**Your repository structure:**

```
your-repo/
├── streamlit_app.py                    # Your main app
├── ai_threat_scene_6_PRODUCTION.py    # Copy from our package
├── requirements.txt                    # Add boto3
└── .streamlit/
    └── secrets.toml.example           # Example for others
```

**In `streamlit_app.py`:**

```python
# Change this import:
# OLD: from ai_threat_scene_6_complete import render_ai_threat_analysis_scene
# NEW:
from ai_threat_scene_6_PRODUCTION import render_ai_threat_analysis_scene

# In your AI Remediation tab:
with ai_tabs[0]:
    render_ai_threat_analysis_scene()  # Now shows REAL threats!
```

**In `requirements.txt`:**

```txt
streamlit==1.29.0
boto3==1.34.59      # Add this for AWS
pandas==2.1.4
plotly==5.18.0
```

**Push to GitHub:**

```bash
git add .
git commit -m "Add production threat detection"
git push origin main
```

---

### Step 3: Configure Streamlit Cloud

**In Streamlit Cloud Dashboard:**

1. Go to your app → **Settings** → **Secrets**
2. Add this:

```toml
[aws]
region = "us-east-1"
threats_table = "security-threats"

# Use READ-ONLY credentials (see below)
[default]
aws_access_key_id = "AKIA..."
aws_secret_access_key = "..."
```

**That's it!** Your Streamlit Cloud app now shows real threats.

---

## 🔐 Create Read-Only AWS Credentials

**IMPORTANT:** Don't use admin credentials in Streamlit Cloud!

Create a dedicated read-only user:

```bash
# 1. Create IAM policy
cat > streamlit-policy.json <<EOF
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "dynamodb:GetItem",
        "dynamodb:Query",
        "dynamodb:Scan"
      ],
      "Resource": "arn:aws:dynamodb:*:*:table/security-threats*"
    }
  ]
}
EOF

# 2. Create policy and user
aws iam create-policy \
    --policy-name StreamlitReadOnly \
    --policy-document file://streamlit-policy.json

aws iam create-user --user-name streamlit-reader

aws iam attach-user-policy \
    --user-name streamlit-reader \
    --policy-arn arn:aws:iam::YOUR_ACCOUNT_ID:policy/StreamlitReadOnly

# 3. Create access keys
aws iam create-access-key --user-name streamlit-reader

# Use these keys in Streamlit Cloud secrets!
```

---

## ✅ Verification

### Test It Works

1. **Create a test threat:**

```bash
aws iam put-role-policy \
    --role-name TestRole \
    --policy-name Test \
    --policy-document '{
        "Version": "2012-10-17",
        "Statement": [{
            "Effect": "Allow",
            "Action": "s3:*",
            "Resource": "*"
        }]
    }'
```

2. **Wait 5 seconds**

3. **Refresh your Streamlit Cloud app**

4. **Navigate to:** AI-Powered Remediation → Threat Analysis

5. **You should see:** Red CRITICAL alert box with your test threat!

---

## 📊 Architecture

```
┌─────────────────────────────────────────────┐
│ YOUR AWS ACCOUNT                             │
│                                              │
│  CloudTrail → EventBridge → Lambda          │
│                                ↓             │
│                          DynamoDB            │
│                          (threats)           │
└──────────────────────┬──────────────────────┘
                       │
                       │ boto3 reads data
                       │ (read-only)
                       ↓
┌─────────────────────────────────────────────┐
│ STREAMLIT CLOUD                              │
│                                              │
│  Your App → ai_threat_scene_6_PRODUCTION.py │
│             ↓                                │
│       Displays threats                       │
│       (real-time)                            │
└─────────────────────────────────────────────┘
```

**AWS detects threats → DynamoDB stores them → Streamlit reads them**

---

## 💡 Key Points

### ✅ What Works in Streamlit Cloud

- Reading from DynamoDB ✅
- Displaying threats ✅
- AI analysis ✅
- Boto3 Python library ✅

### ❌ What Doesn't Work in Streamlit Cloud

- Running bash scripts ❌
- AWS CLI commands ❌
- CloudFormation deployment ❌
- Installing system packages ❌

### 💡 The Solution

- Deploy AWS infrastructure **once** from your machine
- Streamlit Cloud app **only reads** the data
- Best of both worlds!

---

## 🎯 Summary

| Task | Where | How |
|------|-------|-----|
| **Deploy AWS** | Local machine | `./scripts/deploy.sh` |
| **Update Lambda** | Local machine | `aws lambda update-function-code` |
| **View threats** | Streamlit Cloud | Automatic (reads DynamoDB) |
| **Execute remediation** | Streamlit Cloud | Via boto3 API calls |

**Time investment:**
- AWS deployment: 5 minutes (one-time)
- Streamlit setup: 2 minutes
- Total: 7 minutes

**Monthly cost:**
- AWS: ~$10.50
- Streamlit Cloud: Free (Community) or $20 (Pro)

---

## 🐛 Troubleshooting

### "ModuleNotFoundError: No module named 'boto3'"

**Fix:** Add to `requirements.txt`:
```txt
boto3==1.34.59
```

### "AccessDenied" when reading DynamoDB

**Fix:** Check Streamlit Cloud secrets have correct AWS credentials

### "Table does not exist"

**Fix:** Verify AWS infrastructure deployed:
```bash
aws dynamodb describe-table --table-name security-threats
```

### No threats showing

**Fix:** Create a test threat:
```bash
aws iam put-role-policy --role-name TestRole --policy-name Test --policy-document '{"Version":"2012-10-17","Statement":[{"Effect":"Allow","Action":"s3:*","Resource":"*"}]}'
```

---

## 🎉 You're Done!

Your Streamlit Cloud app now:
- ✅ Shows **real** AWS threats (not demo data)
- ✅ Updates in **real-time** (<5 seconds)
- ✅ Uses **AI analysis** from Claude
- ✅ Executes **automated remediation**
- ✅ Works from **anywhere** (cloud-hosted)

**All threats detected in AWS appear instantly in your Streamlit dashboard!** 🚀

---

## 📞 Need Help?

1. **Full guide:** See `STREAMLIT_CLOUD_DEPLOYMENT.md`
2. **AWS deployment:** See `QUICKSTART.md`
3. **Architecture:** See `docs/ARCHITECTURE_DIAGRAM.md`

---

**Ready?** Deploy AWS now, then push to Streamlit Cloud! 🎊
