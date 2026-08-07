# CortexNexus AI Automation System - Complete Setup Guide

## 🚀 Overview

This automation system handles ALL your social media activities across:
- Facebook (Company Page)
- Instagram (Business Account)
- TikTok
- YouTube
- LinkedIn (Company Page)
- Twitter/X

**What It Does Automatically:**
✅ Generates AI content for all platforms  
✅ Schedules and posts content at optimal times  
✅ Responds to comments and messages  
✅ Tracks analytics and engagement  
✅ Creates stories, reels, shorts  
✅ Manages customer interactions  
✅ Monitors brand mentions  
✅ Generates daily reports

---

## 📋 Prerequisites

### 1. **Required Accounts**
- [ ] Facebook Business Page
- [ ] Instagram Business Account
- [ ] TikTok Creator/Business Account
- [ ] YouTube Channel
- [ ] LinkedIn Company Page
- [ ] Twitter/X Account
- [ ] Anthropic API Account (for Claude AI)

### 2. **System Requirements**
- Python 3.9 or higher
- 4GB RAM minimum
- Internet connection
- Linux/Mac/Windows with WSL

---

## 🛠️ Installation Steps

### Step 1: Clone/Download Files

```bash
# Create project directory
mkdir cortexnexus-automation
cd cortexnexus-automation

# Place all files here:
# - cortexnexus_automation_main.py
# - cortexnexus_automation_system.json
# - platform_integrations.py
# - requirements.txt
```

### Step 2: Install Dependencies

```bash
# Create virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install requirements
pip install -r requirements.txt
```

### Step 3: Configure API Keys

Create a `.env` file in the project directory:

```bash
# Copy this template and fill in your actual keys
cat > .env << 'EOF'
# ===== ANTHROPIC (CLAUDE AI) =====
ANTHROPIC_API_KEY=your_anthropic_api_key_here

# ===== FACEBOOK =====
FACEBOOK_PAGE_TOKEN=your_facebook_page_access_token
FACEBOOK_PAGE_ID=your_facebook_page_id

# ===== INSTAGRAM =====
INSTAGRAM_USERNAME=your_instagram_username
INSTAGRAM_PASSWORD=your_instagram_password

# ===== TIKTOK =====
TIKTOK_ACCESS_TOKEN=your_tiktok_access_token

# ===== YOUTUBE =====
YOUTUBE_API_KEY=your_youtube_api_key
YOUTUBE_CHANNEL_ID=your_youtube_channel_id

# ===== TWITTER/X =====
TWITTER_API_KEY=your_twitter_api_key
TWITTER_API_SECRET=your_twitter_api_secret
TWITTER_ACCESS_TOKEN=your_twitter_access_token
TWITTER_ACCESS_SECRET=your_twitter_access_secret

# ===== LINKEDIN =====
LINKEDIN_ACCESS_TOKEN=your_linkedin_access_token
LINKEDIN_COMPANY_ID=your_linkedin_company_id

# ===== EMAIL (for notifications) =====
SENDGRID_API_KEY=your_sendgrid_api_key
NOTIFICATION_EMAIL=your.email@cortexnexus.com

EOF
```

---

## 🔑 Getting API Keys

### **Anthropic (Claude AI)** - REQUIRED
1. Go to https://console.anthropic.com
2. Sign up / Log in
3. Go to API Keys section
4. Create new key
5. Copy and save to `.env`

### **Facebook Page**
1. Go to https://developers.facebook.com
2. Create an App (Business type)
3. Add Facebook Login product
4. Generate Page Access Token
5. Get your Page ID from Page Settings

### **Instagram Business**
1. Convert your Instagram to Business Account
2. Link to Facebook Page
3. Use Facebook Graph API tokens
4. OR use username/password for instagrapi

### **TikTok**
1. Go to https://developers.tiktok.com
2. Create an app
3. Apply for Content Posting API access
4. Get access token

### **YouTube**
1. Go to https://console.cloud.google.com
2. Create project
3. Enable YouTube Data API v3
4. Create credentials (API Key and OAuth)
5. Get your Channel ID from YouTube Studio

### **Twitter/X**
1. Go to https://developer.twitter.com
2. Apply for Developer Account
3. Create an App
4. Generate API keys and tokens

### **LinkedIn**
1. Go to https://www.linkedin.com/developers
2. Create an App
3. Request access to Marketing Developer Platform
4. Generate access token

---

## ⚙️ Configuration

### Edit `cortexnexus_automation_system.json`

Update these key sections:

```json
{
  "automation_config": {
    "company_name": "CortexNexus AI Industry",
    "brand_handle": "@Nexusindustry",
    "active": true
  },
  
  "platforms": {
    "facebook": {
      "enabled": true,  // ← Set to true for active platforms
      "page_name": "Your Page Name",
      "post_frequency": "3_per_day"
    }
    // ... repeat for each platform
  }
}
```

### Customize Content Types

For each platform, specify what types of content to create:

```json
"content_types": [
  "ai_insights",
  "product_updates",
  "customer_stories",
  "tech_news",
  "tutorials"
]
```

### Set Posting Times

Adjust optimal posting times for your audience:

```json
"best_times": ["09:00", "14:00", "19:00"]
```

---

## 🚀 Running the System

### Quick Start (Test Mode)

```bash
# Activate environment
source venv/bin/activate

# Run automation
python cortexnexus_automation_main.py
```

### Production Deployment

#### Option 1: Run as Background Service (Linux)

Create systemd service:

```bash
sudo nano /etc/systemd/system/cortexnexus-automation.service
```

Add this content:

```ini
[Unit]
Description=CortexNexus Social Media Automation
After=network.target

[Service]
Type=simple
User=your_username
WorkingDirectory=/path/to/cortexnexus-automation
Environment="PATH=/path/to/cortexnexus-automation/venv/bin"
ExecStart=/path/to/cortexnexus-automation/venv/bin/python cortexnexus_automation_main.py
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```

Enable and start:

```bash
sudo systemctl enable cortexnexus-automation
sudo systemctl start cortexnexus-automation
sudo systemctl status cortexnexus-automation
```

#### Option 2: Docker Deployment

Create `Dockerfile`:

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["python", "cortexnexus_automation_main.py"]
```

Build and run:

```bash
docker build -t cortexnexus-automation .
docker run -d --name cortexnexus --env-file .env cortexnexus-automation
```

#### Option 3: Cloud Deployment (AWS/GCP/Azure)

Deploy to cloud server:

```bash
# SSH to your cloud instance
ssh user@your-server

# Clone repo and setup
git clone your-repo
cd cortexnexus-automation
./setup.sh

# Use screen or tmux for persistent session
screen -S automation
python cortexnexus_automation_main.py
# Ctrl+A, D to detach
```

---

## 📊 Monitoring & Analytics

### View Real-time Logs

```bash
# Follow logs
tail -f automation.log

# Or if using systemd
journalctl -u cortexnexus-automation -f
```

### Access Dashboard

The system generates daily reports automatically. View them:

```bash
# Check reports directory
ls -la reports/

# View latest report
cat reports/analytics_$(date +%Y%m%d).json
```

### Email Reports

Configure email in `.env`:

```bash
SENDGRID_API_KEY=your_key
NOTIFICATION_EMAIL=your.email@cortexnexus.com
REPORT_FREQUENCY=daily
```

---

## 🎯 Usage Examples

### Generate Content for Specific Platform

```python
from cortexnexus_automation_main import CortexNexusAutomation

automation = CortexNexusAutomation()

# Generate Instagram post
content = automation.generate_content('instagram', 'post')
print(content['text'])
```

### Schedule Custom Post

```python
automation.schedule_content(
    platform='facebook',
    content={'text': 'Your custom post here #AI #Tech'},
    post_time='14:00'
)
```

### Get Analytics

```python
metrics = automation.monitor_engagement('instagram')
print(f"Followers: {metrics['followers']}")
print(f"Engagement: {metrics['engagement_rate']}%")
```

---

## 🔧 Troubleshooting

### Common Issues

**Issue: "API Key not found"**
```bash
# Solution: Check .env file exists and is loaded
cat .env | grep ANTHROPIC_API_KEY
```

**Issue: "Platform posting failed"**
```bash
# Solution: Verify API credentials
python -c "import os; from dotenv import load_dotenv; load_dotenv(); print(os.getenv('FACEBOOK_PAGE_TOKEN'))"
```

**Issue: "No content generated"**
```bash
# Solution: Check Claude API quota
# Go to https://console.anthropic.com/settings/usage
```

### Debug Mode

Run with verbose logging:

```bash
python cortexnexus_automation_main.py --debug
```

---

## 📱 Integration with Your App

### Link to CortexNexus Mobile App

The automation system can push notifications to your app:

```python
# In cortexnexus_automation_main.py
def notify_app(self, message):
    """Send notification to mobile app"""
    import requests
    requests.post('https://cortexnexus.netlify.app/api/notifications', {
        'message': message,
        'platform': 'automation_system'
    })
```

### Sync with Website

Update website with latest posts:

```python
def sync_to_website(self, posts):
    """Sync latest posts to cortexnexus.com"""
    # Upload to your website's content management
    pass
```

---

## 🔒 Security Best Practices

1. **Never commit `.env` file**
   ```bash
   echo ".env" >> .gitignore
   ```

2. **Use environment-specific configs**
   ```bash
   .env.development
   .env.production
   ```

3. **Rotate API keys regularly**
   - Set reminders every 90 days
   - Update in `.env` and restart service

4. **Monitor API usage**
   - Check platform dashboards weekly
   - Set up usage alerts

5. **Backup configuration**
   ```bash
   cp cortexnexus_automation_system.json backup/config_$(date +%Y%m%d).json
   ```

---

## 📈 Scaling & Optimization

### Handle More Platforms

Add new platforms in `cortexnexus_automation_system.json`:

```json
"platforms": {
  "new_platform": {
    "enabled": true,
    "post_frequency": "2_per_day",
    "best_times": ["10:00", "16:00"],
    "content_types": ["posts"]
  }
}
```

### Increase Posting Frequency

```json
"post_frequency": "6_per_day",  // Was 3_per_day
"best_times": ["08:00", "10:00", "12:00", "14:00", "17:00", "20:00"]
```

### Add More Content Types

```python
def generate_content(self, platform, content_type):
    content_prompts = {
        'tutorial': 'Create a tutorial post about...',
        'case_study': 'Write a case study about...',
        'infographic': 'Design an infographic about...',
        # Add more...
    }
```

---

## 💰 Cost Optimization

### API Usage Estimates

**Claude API:**
- ~$0.003 per content generation
- 50 posts/day = $0.15/day = $4.50/month

**Platform APIs:**
- Mostly free (within limits)
- Monitor usage dashboards

### Reduce Costs

1. **Cache generated content**
   ```python
   cache_content = True
   ```

2. **Batch requests**
   ```python
   generate_multiple_contents(count=10)
   ```

3. **Use cheaper models for simple tasks**
   ```python
   model="claude-haiku-3-20240307"  # For simple responses
   ```

---

## 🎓 Best Practices

### Content Strategy

1. **Mix content types** - Don't post the same thing repeatedly
2. **Engage authentically** - Respond to comments personally
3. **Track what works** - Analyze top-performing posts
4. **Stay consistent** - Post regularly, don't go silent
5. **Be human** - AI assists, but your voice matters

### Posting Schedule

- **Mornings**: Motivational, news
- **Afternoons**: Educational, tutorials
- **Evenings**: Entertainment, community

### Hashtag Strategy

- Use 5-10 relevant hashtags
- Mix popular and niche tags
- Create branded hashtag (#CortexNexusAI)

---

## 📞 Support & Maintenance

### Regular Maintenance

**Weekly:**
- [ ] Check automation logs
- [ ] Review analytics
- [ ] Update content calendar

**Monthly:**
- [ ] Rotate API keys
- [ ] Backup configuration
- [ ] Update dependencies
- [ ] Review and optimize posting times

**Quarterly:**
- [ ] Full system audit
- [ ] Update AI prompts
- [ ] Refresh content strategy

### Getting Help

**System Issues:**
- Check logs: `journalctl -u cortexnexus-automation`
- Debug mode: `python cortexnexus_automation_main.py --debug`

**API Issues:**
- Facebook: https://developers.facebook.com/support
- Instagram: Help Center in app
- YouTube: https://support.google.com/youtube
- Twitter: https://developer.twitter.com/en/support

---

## 🎉 You're Ready!

Your CortexNexus automation system is now set up and ready to run 24/7, handling all your social media activities automatically.

**What happens next:**
1. System generates content for all platforms
2. Posts automatically at optimal times
3. Responds to comments and messages
4. Tracks analytics and performance
5. Sends you daily reports
6. Learns and optimizes over time

**You just focus on:**
- Strategic decisions
- High-level content direction
- Building your business

The AI handles the rest! 🚀

---

**Last Updated:** May 19, 2026  
**System Version:** A18Plus Sovereign Core  
**Status:** Production Ready ✅
