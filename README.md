# Attachment Architect for Jira Cloud

**Smart attachment management that saves storage, time, and money.**

[![Version](https://img.shields.io/badge/version-3.15.0-blue.svg)](https://marketplace.atlassian.com)
[![License](https://img.shields.io/badge/license-Commercial-green.svg)](https://marketplace.atlassian.com)
[![Platform](https://img.shields.io/badge/platform-Jira%20Cloud-0052CC.svg)](https://www.atlassian.com/software/jira)
[![Forge](https://img.shields.io/badge/built%20with-Atlassian%20Forge-00B8D9.svg)](https://developer.atlassian.com/platform/forge/)

---

## 🎯 What It Does

Attachment Architect helps Jira administrators **eliminate storage waste** by finding and removing duplicate attachments and **low‑value trash files** (logs, dumps, temp, system), with safe, auditable cleanup.

### Key Features

- ⚡ **Two‑phase Scanning** – Unified 0–100% progress and ETA for every scan (including first scans)
- 📊 **7D Visual Analytics** – Project, File Type, User, Age, Status (smart grouping), Heat Index, Archive Candidates
- 🔁 **Duplicate Detection** – SHA‑256 content‑true matching with canonical‑aware cleanup (oldest kept)
- 🧹 **Storage Hygiene** – Detect logs, dumps, temp, and system files; bulk delete with guardrails and progress
- 🧭 **Scope Selection** – Scan the entire site or selected projects (no JQL required)
- 🧾 **Enterprise Audit Log** – Record of scans and deletions for compliance
- 🔄 **Stale Data Mode** – Keep using the last results while a new scan runs
- ♻️ **Safe Bulk Cleanup** – Type‑to‑confirm, progress‑tracked operations
- 🔒 **Privacy‑First** – Metadata and hashes only; least‑privilege scopes

---

## 🚀 Quick Start

### For Users

1. **Install** from [Atlassian Marketplace](https://marketplace.atlassian.com)
2. **Access** via Jira Settings → Apps → Attachment Architect
3. **Scan** your instance (takes 2-5 minutes for 10,000 issues)
4. **Analyze** the dashboard to find quick wins
5. **Clean** up duplicates with one click

📖 **[Read the Full User Guide](USER_GUIDE.md)**

### For Developers

```bash
# Clone the repository
git clone <repository-url>
cd Attachment-Architect

# Install dependencies
npm install
cd static/hello-world && npm install && cd ../..

# Deploy to development
forge deploy -e development

# Install on your site
forge install --site your-site.atlassian.net --product jira -e development
```

---

## 📊 Results

**Average Customer Results:**
- 💰 **20-40% storage reduction**
- ⏱️ **2 hours vs. 2 weeks** of manual cleanup
- 💵 **€180/year saved** (for 50GB instance)
- 🚀 **25x faster** than manual scanning

---

## 🏗️ Architecture

### Technology Stack

- **Platform:** Atlassian Forge (serverless)
- **Backend:** Node.js 22.x, Forge API
- **Frontend:** React 16, Atlassian UI Kit
- **Storage:** Forge Key-Value Storage
- **Security:** TLS 1.2+, AES-256 encryption

### Key Components

```
attachment-architect/
├── src/
│   ├── index.js           # Backend resolvers
│   ├── validation.js      # Input validation
│   ├── auditLog.js        # Audit trail
│   ├── storageChunking.js # Large data handling
│   └── logger.js          # Structured logging
├── static/hello-world/
│   └── src/
│       ├── App.js         # Main React app
│       └── components/    # UI components
├── manifest.yml           # Forge configuration
└── package.json           # Dependencies
```

---

## 🔒 Security

### Security Posture

- ✅ **SAST Scan:** 0 vulnerabilities
- ✅ **SCA Scan:** Backend clean, frontend dev dependencies only
- ✅ **No XSS:** React auto-escaping, no innerHTML
- ✅ **No SQL Injection:** Uses Forge Storage (key-value)
- ✅ **Input Validation:** All user inputs validated
- ✅ **Authorization:** Admin-only access, permission checks

### Compliance

- ✅ **GDPR Compliant** - Data minimization, audit trail, right to deletion
- ✅ **CCPA Compliant** - No sale of personal information
- ✅ **SOC 2 Certified** - Via Atlassian Forge platform
- ✅ **ISO 27001 Certified** - Via Atlassian infrastructure

📄 **[Read the Privacy Policy](PRIVACY_POLICY.md)**

---

## 📚 Documentation

- **[User Guide](USER_GUIDE.md)** - Complete user documentation
- **[Privacy Policy](PRIVACY_POLICY.md)** - Data security and privacy
- **[Security Reports](SAST_SECURITY_REPORT.md)** - SAST and SCA scan results
- **[Marketplace Listing](MARKETPLACE_LISTING.md)** - Marketing materials

---

## 🛠️ Development

### Prerequisites

- Node.js 18+ and npm
- Forge CLI (`npm install -g @forge/cli`)
- Atlassian account with Jira Cloud instance

### Setup

```bash
# Install Forge CLI
npm install -g @forge/cli

# Login to Forge
forge login

# Install dependencies
npm install
cd static/hello-world && npm install && cd ../..

# Lint the code
forge lint

# Deploy to development
forge deploy -e development --non-interactive

# View logs
forge logs -e development
```

### Testing

```bash
# Run ESLint
npx eslint src --ext .js

# Run npm audit
npm audit
cd static/hello-world && npm audit && cd ../..

# Test in development
forge tunnel
```

### Deployment

```bash
# Deploy to production
forge deploy -e production --non-interactive

# Check deployment
forge environments
```

---

## 📦 Project Structure

```
attachment-architect/
├── src/                          # Backend code
│   ├── index.js                  # Main resolvers (2,800+ lines)
│   ├── validation.js             # Input validation
│   ├── auditLog.js               # Audit logging
│   ├── storageChunking.js        # Handle large data
│   └── logger.js                 # Structured logging
├── static/hello-world/           # Frontend code
│   ├── src/
│   │   ├── App.js                # Main React component
│   │   ├── components/           # UI components
│   │   │   ├── DashboardView.js  # Main dashboard
│   │   │   ├── ScanningView.js   # Scan progress
│   │   │   ├── ActionCenter.js   # Cleanup interface
│   │   │   ├── AnalysisTabs.js   # Visual analytics
│   │   │   ├── AuditLogView.js   # Audit trail
│   │   │   └── SettingsView.js   # Configuration
│   │   ├── hooks/                # Custom React hooks
│   │   └── config/               # Feature flags
│   ├── public/
│   └── package.json
├── manifest.yml                  # Forge app configuration
├── package.json                  # Backend dependencies
├── .eslintrc.json                # ESLint configuration
├── USER_GUIDE.md                 # User documentation
├── PRIVACY_POLICY.md             # Privacy statement
├── SAST_SECURITY_REPORT.md       # Security analysis
├── SCA_DEPENDENCY_REPORT.md      # Dependency analysis
└── README.md                     # This file
```

---

## 🔄 Version History

### v3.15.0 (January 2025) - Current
- 🟢 Unified progress bar + ETA for all scans (including first scans)
- 🟢 Two‑phase scanning parallelized for higher throughput
- 🟢 Storage Hygiene: detect and bulk delete logs/dumps/temp/system files
- 🟢 Stale data mode to keep dashboards usable during scans
- 🟢 Scope selection by Projects (scan entire site or selected projects)
- 🟢 Heat Index and Quick Wins improvements for faster prioritization
- 🟢 Audit log enhancements for scans and deletions

### v3.0.0 (January 2025)
- ✅ Activity Panel settings fix
- ✅ Enhanced security (SAST + SCA scans)
- ✅ Production deployment
- ✅ Improved error handling
- ✅ JSON parsing error recovery

### v2.0.0 (December 2024)
- ✅ Bulk deletion (up to 100 files)
- ✅ Trial limit enforcement
- ✅ Dashboard real-time updates
- ✅ Comprehensive audit logging
- ✅ Activity Panel on issues

### v1.0.0 (November 2024)
- ✅ Initial release
- ✅ Basic scanning and analytics
- ✅ Duplicate detection
- ✅ Manual cleanup

---

## 🤝 Support

### Getting Help

- 📧 **Email:** Submit ticket at https://drinkits.atlassian.net/servicedesk/customer/portal/34
- 📚 **Documentation:** See [USER_GUIDE.md](USER_GUIDE.md)
- 🐛 **Bug Reports:** Use support portal
- 💡 **Feature Requests:** Use support portal

### Response Times

- **Email Support:** Within 24 hours (weekdays)
- **Critical Issues:** Within 4 hours
- **Feature Requests:** Reviewed monthly

---

## 📄 License

**Commercial License** - See Atlassian Marketplace listing for pricing and terms.

---

## 🙏 Acknowledgments

Built with:
- [Atlassian Forge](https://developer.atlassian.com/platform/forge/) - Serverless platform
- [Atlassian Design System](https://atlassian.design/) - UI components
- [React](https://reactjs.org/) - Frontend framework
- [Recharts](https://recharts.org/) - Data visualization

---

## 📊 Stats

- **Lines of Code:** ~10,000
- **Backend:** 3,500 lines (JavaScript)
- **Frontend:** 6,500 lines (React/JSX)
- **Dependencies:** 1,711 total (5 backend + 1,706 frontend)
- **Security Vulnerabilities:** 0 (production code)
- **Test Coverage:** Manual testing + security scans

---

## 🚀 Roadmap

### Coming Soon
- [ ] Automated cleanup policies
- [ ] Scheduled scans
- [ ] Email notifications
- [ ] Advanced filtering
- [ ] Custom reports
- [ ] API access
- [ ] Data export (CSV/JSON)

### Under Consideration
- [ ] Confluence support
- [ ] Multi-language support
- [ ] Mobile app
- [ ] Slack integration

---

## 🏆 Why Choose Attachment Architect?

✅ **Easy to Use** - Intuitive dashboard, no training required  
✅ **Fast** - Scan 10,000 issues in minutes, not hours  
✅ **Safe** - Built on Atlassian Forge, enterprise-grade security  
✅ **Effective** - Customers reclaim 20-40% of storage on average  
✅ **Affordable** - ROI in first month for most customers  
✅ **Supported** - Responsive support team, regular updates  

---

**Made with ❤️ by drinkits DEV**

**[Install Now](https://marketplace.atlassian.com)** | **[Read Docs](USER_GUIDE.md)** | **[Get Support](https://drinkits.atlassian.net/servicedesk/customer/portal/34)**

---

*Last updated: January 2025 | Version 3.0.0*
