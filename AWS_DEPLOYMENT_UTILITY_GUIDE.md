# 🛠️ AWS Deployment Utility - Complete Guide

## Overview

This Python-based deployment utility **replaces bash scripts** with a full Streamlit UI. Deploy and manage AWS infrastructure entirely from Streamlit Cloud using boto3.

**No AWS CLI or bash scripts required!**

---

## ✅ What This Utility Does

### Instead of Bash Scripts
```bash
# OLD: Cannot run in Streamlit Cloud
./scripts/deploy.sh
aws cloudformation create-stack ...
aws lambda update-function-code ...
```

### Use Python + Streamlit UI
```python
# NEW: Works perfectly in Streamlit Cloud
from aws_deployment_utility import render_deployment_utility

# Full UI with buttons, forms, real-time monitoring
render_deployment_utility()
```

---

## 🎯 Features

### 🚀 Deploy Infrastructure Tab
- Create CloudFormation stack
- Real-time deployment monitoring
- Progress bar with status updates
- Event streaming
- Output display

### 📦 Deploy Lambda Tab
- Upload Lambda ZIP files
- Deploy from template
- View current code
- Version tracking

### 🧪 Test System Tab
- Create test threats
- Verify detection working
- Multiple test scenarios
- Automatic cleanup

### 📊 Monitor Status Tab
- System health dashboard
- Recent threats display
- Lambda logs viewer
- Component status checks

### 🔄 Update/Rollback Tab
- Update configuration
- Complete rollback
- Resource cleanup

---

## 🚀 Quick Integration

### Option 1: Separate Admin Page (Recommended)

**Create `pages/Admin_Deployment.py`:**

```python
import streamlit as st
from aws_deployment_utility import render_deployment_utility

st.set_page_config(
    page_title="AWS Deployment", 
    page_icon="🚀",
    layout="wide"
)

# Restrict access (optional)
if st.session_state.get('user_role') != 'admin':
    st.error("🔒 Admin access required")
    st.stop()

# Render the utility
render_deployment_utility()
```

**Access:** Your app → Pages → Admin Deployment

---

### Option 2: Add to Existing App

**In your main `streamlit_app.py`:**

```python
import streamlit as st
from aws_deployment_utility import render_deployment_utility

# Add to your sidebar
with st.sidebar:
    if st.checkbox("🔧 Show Deployment Utility"):
        render_deployment_utility()
```

---

### Option 3: Standalone Deployment App

**Create `deployment_app.py`:**

```python
import streamlit as st
from aws_deployment_utility import render_deployment_utility

st.set_page_config(page_title="AWS Deployment Utility", layout="wide")

render_deployment_utility()
```

**Run:** `streamlit run deployment_app.py`

---

## 📋 Prerequisites

### 1. Install Dependencies

**Update `requirements.txt`:**

```txt
streamlit==1.29.0
boto3==1.34.59
pandas==2.1.4
```

### 2. Configure Streamlit Secrets

**In Streamlit Cloud → Settings → Secrets:**

```toml
[aws]
region = "us-east-1"
threats_table = "security-threats"
sns_topic_arn = "arn:aws:sns:us-east-1:YOUR_ACCOUNT:security-threat-alerts"

# AWS Credentials (ADMIN for deployment)
[default]
aws_access_key_id = "AKIA..."
aws_secret_access_key = "..."
```

⚠️ **Important:** These need **admin permissions** for deployment. Use a dedicated deployment user.

### 3. Upload Files to GitHub

```bash
# Add the utility to your repo
cp aws_deployment_utility.py /your-repo/

# If using separate page
mkdir -p /your-repo/pages
cp Admin_Deployment.py /your-repo/pages/

# Push to GitHub
git add .
git commit -m "Add AWS deployment utility"
git push
```

---

## 🔐 Security Best Practices

### Create Dedicated Deployment User

```bash
# 1. Create IAM user for deployments
aws iam create-user --user-name streamlit-deployer

# 2. Attach necessary policies
aws iam attach-user-policy \
    --user-name streamlit-deployer \
    --policy-arn arn:aws:iam::aws:policy/PowerUserAccess

# 3. Create access keys
aws iam create-access-key --user-name streamlit-deployer

# Use these keys in Streamlit secrets
```

### Restrict Access in App

**Add authentication:**

```python
import streamlit as st

# Simple password protection
ADMIN_PASSWORD = st.secrets.get('admin_password', 'change-me')

if 'authenticated' not in st.session_state:
    st.session_state.authenticated = False

if not st.session_state.authenticated:
    password = st.text_input("Admin Password", type="password")
    if st.button("Login"):
        if password == ADMIN_PASSWORD:
            st.session_state.authenticated = True
            st.rerun()
        else:
            st.error("Invalid password")
    st.stop()

# Show utility only after authentication
render_deployment_utility()
```

---

## 🎯 Usage Workflow

### First-Time Deployment

1. **Go to deployment page**
2. **Click "Deploy Infrastructure" tab**
3. **Enter notification email**
4. **Click "🚀 Deploy Infrastructure"**
5. **Watch real-time progress** (3-5 minutes)
6. **Done!** System is detecting threats

### Update Lambda Code

1. **Go to "Deploy Lambda" tab**
2. **Upload new ZIP file** OR **click "Deploy Template Code"**
3. **Click "🚀 Deploy"**
4. **Lambda updated!**

### Test System

1. **Go to "Test System" tab**
2. **Select test type** (e.g., "IAM Policy Change")
3. **Click "🧪 Run Test"**
4. **Watch automatic test execution**
5. **Verify threat detected**

### Monitor Status

1. **Go to "Monitor Status" tab**
2. **View system health dashboard**
3. **See recent threats**
4. **Check Lambda logs**

### Rollback

1. **Go to "Update/Rollback" tab**
2. **Check "I understand" checkbox**
3. **Click "🗑️ Delete All Resources"**
4. **Wait for completion**

---

## 🧪 Testing the Utility

### Test 1: Verify Connection

```python
import boto3
import streamlit as st

# Test AWS connection
try:
    sts = boto3.client('sts',
        aws_access_key_id=st.secrets['default']['aws_access_key_id'],
        aws_secret_access_key=st.secrets['default']['aws_secret_access_key'],
        region_name=st.secrets['aws']['region']
    )
    
    account = sts.get_caller_identity()
    st.success(f"✅ Connected to AWS Account: {account['Account']}")
except Exception as e:
    st.error(f"❌ Connection failed: {e}")
```

### Test 2: Deploy Infrastructure

1. Open deployment utility
2. Go to "Deploy Infrastructure"
3. Enter your email
4. Click deploy
5. Watch progress bar

**Expected:** 
- ✅ Stack creation starts
- ✅ Progress bar moves
- ✅ Events display in real-time
- ✅ After 3-5 min: "Deployment Complete!"

### Test 3: Create Test Threat

1. Go to "Test System"
2. Select "IAM Policy Change (Critical)"
3. Click "🧪 Run Test"

**Expected:**
- ✅ Creates test role
- ✅ Adds wildcard policy
- ✅ Detects threat (10 sec)
- ✅ Shows "TEST PASSED!"
- ✅ Cleans up automatically

---

## 📊 Real-World Usage Examples

### Example 1: Daily Operations Team

```python
# Create separate deployment app for ops team
# deployment_app.py

import streamlit as st
from aws_deployment_utility import render_deployment_utility

st.set_page_config(page_title="Security Operations", layout="wide")

# Authentication
if 'user' not in st.session_state:
    st.session_state.user = st.text_input("Username")
    st.session_state.password = st.text_input("Password", type="password")
    if not st.session_state.user:
        st.stop()

# Render utility
st.title("🛡️ Security Operations Dashboard")
render_deployment_utility()
```

### Example 2: Emergency Response

```python
# Quick access for security incidents
import streamlit as st
from aws_deployment_utility import render_deployment_utility

st.sidebar.markdown("## 🚨 Emergency Actions")

if st.sidebar.button("🚀 Deploy Emergency Updates"):
    # Jump straight to Lambda deployment
    st.session_state.emergency_mode = True
    render_deployment_utility()
```

### Example 3: Automated Testing

```python
# Run tests on schedule
import streamlit as st
from aws_deployment_utility import render_deployment_utility

# Add to your monitoring dashboard
with st.expander("🧪 Run System Tests"):
    render_deployment_utility()
```

---

## 🐛 Troubleshooting

### Issue: "Failed to initialize AWS clients"

**Cause:** Incorrect credentials in Streamlit secrets

**Fix:**
1. Check secrets are named correctly: `[default]` and `[aws]`
2. Verify keys have no extra spaces
3. Test with: `aws sts get-caller-identity` (locally)

### Issue: "CloudFormation already exists"

**Cause:** Stack already deployed

**Options:**
1. Use different stack name
2. Delete existing stack first
3. Update stack instead (feature coming)

### Issue: "Permission denied"

**Cause:** IAM user lacks permissions

**Fix:**
```bash
# Attach PowerUser or Admin policy
aws iam attach-user-policy \
    --user-name streamlit-deployer \
    --policy-arn arn:aws:iam::aws:policy/PowerUserAccess
```

### Issue: Lambda deployment fails

**Cause:** ZIP file format issue

**Fix:**
- Ensure `threat_detection_lambda.py` is at ZIP root
- Don't put code in subdirectories
- Check file name is correct

### Issue: Test doesn't detect threat

**Cause:** Delay in detection pipeline

**Wait:** 30-60 seconds, then check again
- CloudTrail has ~5 second delay
- Lambda cold start can add 5-10 seconds

---

## 💡 Advanced Features

### Custom CloudFormation Parameters

**Modify the utility to accept custom parameters:**

```python
# In deployment form, add:
enable_encryption = st.checkbox("Enable enhanced encryption", value=True)
retention_days = st.slider("DynamoDB retention (days)", 7, 90, 30)

# Pass to deployment:
deploy_cloudformation_stack(
    clients, 
    stack_name,
    notification_email,
    account_id,
    enable_bedrock=True,
    custom_params={
        'encryption': enable_encryption,
        'retention': retention_days
    }
)
```

### Multi-Account Deployment

**Deploy to multiple AWS accounts:**

```python
accounts = st.multiselect(
    "Select accounts",
    ["prod-123456", "dev-789012", "staging-345678"]
)

for account in accounts:
    st.info(f"Deploying to {account}...")
    # Assume role in each account
    # Deploy infrastructure
```

### Scheduled Deployments

**Combine with cron or GitHub Actions:**

```yaml
# .github/workflows/deploy.yml
name: Scheduled Deployment
on:
  schedule:
    - cron: '0 2 * * 0'  # Weekly
  workflow_dispatch:

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Deploy
        run: python aws_deployment_utility.py --auto-deploy
```

---

## 📈 Performance Optimization

### Reduce Deployment Time

**Enable parallel resource creation:**
- Use CloudFormation nested stacks
- Deploy Lambda concurrently
- Batch DynamoDB operations

### Minimize Cold Starts

**Lambda optimization:**
```python
# In Lambda deployment
lambda_client.update_function_configuration(
    FunctionName='threat-detection-handler',
    MemorySize=1024,  # More memory = faster
    Timeout=60,
    Environment={
        'Variables': {
            'POWERTOOLS_SERVICE_NAME': 'threat-detection'
        }
    }
)
```

---

## 🎯 Best Practices

### 1. Version Control

```python
# Tag deployments
deployment_tags = [
    {'Key': 'Version', 'Value': '1.0.0'},
    {'Key': 'DeployedBy', 'Value': st.session_state.user},
    {'Key': 'DeployedAt', 'Value': datetime.now().isoformat()}
]
```

### 2. Notifications

```python
# Send Slack notification after deployment
import requests

def notify_slack(message):
    webhook = st.secrets.get('slack_webhook')
    if webhook:
        requests.post(webhook, json={'text': message})

# After deployment
notify_slack(f"✅ Threat detection deployed by {user}")
```

### 3. Audit Logging

```python
# Log all deployments
def log_deployment(action, status, details):
    log_entry = {
        'timestamp': datetime.now().isoformat(),
        'action': action,
        'status': status,
        'user': st.session_state.get('user', 'unknown'),
        'details': details
    }
    
    # Write to DynamoDB or S3
    dynamodb.put_item(
        TableName='deployment-audit-log',
        Item=log_entry
    )
```

---

## 🎉 Summary

### What You Get

✅ **Full deployment UI** in Streamlit  
✅ **No bash scripts** or AWS CLI needed  
✅ **Real-time monitoring** with progress bars  
✅ **Built-in testing** with automated cleanup  
✅ **Status dashboard** for all services  
✅ **One-click rollback** for emergencies  

### Time Investment

- **Setup:** 10 minutes (add file, configure secrets)
- **First deployment:** 5 minutes (automated)
- **Subsequent updates:** 30 seconds (click button)

### Security

- ✅ Credentials in Streamlit secrets (encrypted)
- ✅ Access control via authentication
- ✅ Audit trail for all actions
- ✅ Least-privilege IAM recommended

---

## 📞 Support

**Common Issues:**
1. Check Streamlit secrets format
2. Verify IAM permissions
3. Test AWS connection first
4. Review CloudWatch logs

**Advanced Help:**
- AWS CloudFormation documentation
- boto3 SDK reference
- Streamlit community forum

---

**🚀 Ready to deploy? Add the utility to your app and start managing AWS infrastructure from Streamlit Cloud!**
