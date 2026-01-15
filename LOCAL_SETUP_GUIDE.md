# 🚀 TrackFlow Local Setup Guide

You're currently on the **main branch** and ready to set up TrackFlow locally!

## Current Status
✅ Code pulled from main branch
✅ All dependencies listed
⏳ Ready for local installation

---

## 🎯 Quick Start (Recommended - Docker Method)

This is the **easiest and fastest** way to get TrackFlow running on your local machine.

### Prerequisites
- Docker Desktop installed ([Download here](https://www.docker.com/products/docker-desktop))
- Git (already have this!)
- 4GB RAM minimum

### Installation Steps

1. **Navigate to TrackFlow directory** (you're already here!)
   ```bash
   cd /home/user/trackflow
   ```

2. **Start the development environment**
   ```bash
   ./dev.sh start
   ```

   This single command will:
   - Start MariaDB database
   - Start Redis cache
   - Initialize Frappe Framework v15
   - Install Frappe CRM
   - Install TrackFlow app
   - Set up a development site
   - Start the web server

3. **Access TrackFlow**
   - Open browser: http://localhost:8000
   - Username: `Administrator`
   - Password: `admin`

4. **Other useful commands**
   ```bash
   ./dev.sh stop      # Stop the environment
   ./dev.sh restart   # Restart everything
   ./dev.sh logs      # View application logs
   ./dev.sh shell     # Open shell in container
   ./dev.sh migrate   # Run database migrations
   ```

---

## 🛠️ Alternative: Manual Bench Setup (Advanced)

If you prefer not to use Docker or want more control:

### Prerequisites
- Python 3.10+
- Node.js 18+
- MariaDB 10.6+
- Redis 6.2+
- Frappe Bench CLI

### Installation Steps

1. **Install Frappe Bench**
   ```bash
   pip3 install frappe-bench
   ```

2. **Initialize a new bench**
   ```bash
   bench init frappe-bench --frappe-branch version-15
   cd frappe-bench
   ```

3. **Create a new site**
   ```bash
   bench new-site trackflow.localhost \
       --db-name trackflow_db \
       --admin-password admin
   ```

4. **Get Frappe CRM**
   ```bash
   bench get-app crm --branch develop
   bench --site trackflow.localhost install-app crm
   ```

5. **Get TrackFlow** (from your current directory)
   ```bash
   # If you cloned trackflow elsewhere
   bench get-app /home/user/trackflow

   # Or clone fresh
   bench get-app https://github.com/chinmaybhatk/trackflow.git
   ```

6. **Install TrackFlow**
   ```bash
   bench --site trackflow.localhost install-app trackflow
   ```

7. **Enable developer mode**
   ```bash
   bench --site trackflow.localhost set-config developer_mode 1
   bench use trackflow.localhost
   ```

8. **Start the development server**
   ```bash
   bench start
   ```

9. **Access TrackFlow**
   - Open browser: http://trackflow.localhost:8000
   - Username: `Administrator`
   - Password: `admin`

---

## 📋 What's Included

Once running, you'll have access to:

### Core Features
- ✅ **Link Tracking** - Create trackable short URLs with QR codes
- ✅ **Visitor Tracking** - Complete visitor journey tracking
- ✅ **Campaign Management** - Multi-channel campaign analytics
- ✅ **Attribution Models** - 5 different attribution models (First Touch, Last Touch, Linear, Time Decay, Position Based)
- ✅ **CRM Integration** - Deep integration with Frappe CRM
- ✅ **Email Tracking** - Email campaign tracking with open/click rates
- ✅ **Conversion Funnels** - Multi-stage funnel analysis
- ✅ **Real-time Dashboard** - Live analytics and reporting
- ✅ **REST API** - 10+ API endpoints for integrations

### Where to Start

1. **Go to TrackFlow Workspace**
   Navigate to: CRM → TrackFlow Analytics

2. **Configure Settings**
   Go to: TrackFlow → Settings
   - Enable Tracking: ON
   - Set Attribution Model
   - Configure GDPR settings

3. **Create Your First Campaign**
   CRM → TrackFlow Analytics → Campaigns → New

4. **Generate a Tracked Link**
   CRM → TrackFlow Analytics → Tracked Links → New

5. **View Analytics**
   Dashboard at: TrackFlow → Dashboard

---

## 🔍 Verify Installation

Once the server is running, check:

```bash
# In bench console
bench --site trackflow.localhost console

>>> import trackflow
>>> frappe.get_installed_apps()
# Should show: ['frappe', 'crm', 'trackflow']

>>> frappe.get_single("TrackFlow Settings")
# Should return settings object
```

---

## 🐛 Troubleshooting

### Docker Issues

**Port already in use**
```bash
# Check what's using port 8000
sudo lsof -i :8000
# Kill the process or change port in docker-compose.yml
```

**Containers won't start**
```bash
./dev.sh clean  # Clean everything
./dev.sh start  # Start fresh
```

**Database connection errors**
```bash
# Check logs
./dev.sh logs
# Wait for database to fully initialize (can take 30-60 seconds)
```

### Bench Issues

**Module import errors**
```bash
bench --site trackflow.localhost migrate
bench clear-cache
bench restart
```

**Permission issues**
```bash
# Fix permissions
chmod -R o+rx /home/user/trackflow
```

**Site not accessible**
```bash
# Check if server is running
bench start
# Or run in production mode
bench setup production $USER
sudo service nginx restart
sudo service supervisor restart
```

---

## 📚 Next Steps

After installation:

1. **Read the documentation**
   - Check `/home/user/trackflow/GETTING_STARTED.md`
   - Review `/home/user/trackflow/README.md`

2. **Explore the codebase**
   - Main app: `/home/user/trackflow/trackflow/`
   - API endpoints: `/home/user/trackflow/trackflow/api/`
   - DocTypes: `/home/user/trackflow/trackflow/trackflow/doctype/`

3. **Run the fix scripts** (if needed)
   ```bash
   python3 fix_doctypes.py
   python3 fix_internal_ip_range.py
   ```

4. **Start building!**
   - Create campaigns
   - Generate tracked links
   - Test attribution
   - Build custom integrations

---

## 💡 Development Tips

- **Auto-reload**: Developer mode is enabled - changes auto-reload
- **Debugging**: Use `frappe.log()` for logging
- **Database**: Access at http://localhost:3306 (user: frappe, pass: frappe)
- **Redis**: Access at localhost:6379
- **API Testing**: Use Postman or curl with API endpoints

---

## 🤝 Need Help?

- **Documentation**: Check `/home/user/trackflow/docs/`
- **Issues**: https://github.com/chinmaybhatk/trackflow/issues
- **Contributing**: See `/home/user/trackflow/CONTRIBUTING.md`

---

**🎉 You're all set! Happy tracking with TrackFlow!**
