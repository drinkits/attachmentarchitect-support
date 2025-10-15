# Privacy Policy & Data Security Statement
## Attachment Architect for Jira Cloud

**Last Updated:** January 2025  
**Version:** 2.0.0  
**App Owner:** drinkits DEV  
**Contact:** https://drinkits.atlassian.net/servicedesk/customer/portal/34

---

## 1. Introduction

Attachment Architect is a Jira Cloud app built on the Atlassian Forge platform. This Privacy Policy explains how we handle data when you use our app. We are committed to protecting your privacy and ensuring the security of your data.

**Key Principle:** We do not store, transmit, or access any personal data outside of your Jira instance. All data processing occurs within Atlassian's secure Forge infrastructure.

---

## 2. Data We Access

### 2.1 Attachment Metadata
To provide attachment analysis and management features, our app accesses:

- **Attachment filenames** - To identify and display files
- **File sizes** - To calculate storage usage
- **File hashes (SHA-256)** - To detect duplicate files
- **Upload dates** - To analyze file age
- **MIME types** - To categorize files by type
- **Author information** - To show who uploaded files (display name and account ID)

**Important:** We **never** access or read the actual content of your attachment files. We only analyze metadata.

### 2.2 Issue Metadata
To provide context for attachments, we access:

- **Issue keys** (e.g., PROJ-123)
- **Project keys and names**
- **Issue status and status categories**
- **Issue creation and update dates**

### 2.3 User Information
For audit logging and permission checks, we access:

- **User account IDs** - Atlassian's unique user identifier
- **Display names** - To show who performed actions
- **Email addresses** - For audit trail purposes only
- **Admin permissions** - To verify authorization for sensitive operations

---

## 3. How We Use Your Data

### 3.1 Storage Analysis
We analyze attachment metadata to provide:

- Total storage usage statistics
- Duplicate file detection
- Storage breakdown by project, file type, user, age, and status
- Recommendations for storage optimization

### 3.2 Audit Logging
We maintain audit logs of:

- Scan operations (who started them and when)
- File deletion operations (who deleted what, when, and why)
- Settings changes (who modified app configuration)

**Purpose:** Enterprise compliance, accountability, and troubleshooting.

### 3.3 License Management
We track:

- Trial deletion counts (for trial users only)
- License status (trial, active, or inactive)

**Purpose:** Enforce trial limits and provide appropriate features based on subscription level.

---

## 4. Where Your Data Is Stored

### 4.1 Forge Storage (Atlassian Infrastructure)
All app data is stored using **Atlassian Forge Storage**, which is:

- **Hosted by Atlassian** - Not on our own servers
- **Encrypted at rest** - Using Atlassian's encryption standards
- **Isolated per instance** - Your data is never shared with other customers
- **Region-specific** - Stored in the same region as your Jira instance

### 4.2 Data Stored in Forge Storage

| Data Type | Purpose | Retention |
|-----------|---------|-----------|
| Scan statistics | Dashboard display | Until next scan or manual deletion |
| Duplicate file groups | Quick Wins and analysis | Until next scan or manual deletion |
| Deletion logs | Audit trail | Permanent (last 100 records per issue) |
| App settings | Configuration | Until changed by admin |
| Trial deletion counter | License enforcement | Permanent (trial users only) |

### 4.3 Entity Properties (Jira Storage)
We store minimal markers on Jira issues:

- **Property:** `attachmentArchitect-hasActivity`
- **Value:** `true` (boolean flag)
- **Purpose:** Enable Activity Panel to load on issues with deletion history
- **Storage:** Jira's native entity property storage (not Forge storage)

---

## 5. Data We Do NOT Collect

We explicitly **DO NOT**:

- ❌ Access or read attachment file contents
- ❌ Store attachments outside your Jira instance
- ❌ Transmit data to external servers or third parties
- ❌ Use your data for marketing or analytics
- ❌ Share data with other customers or organizations
- ❌ Track user behavior for advertising purposes
- ❌ Store personal data beyond what's necessary for app functionality

---

## 6. Data Security Measures

### 6.1 Platform Security (Atlassian Forge)
Our app runs on Atlassian Forge, which provides:

- **Sandboxed execution** - Isolated from other apps
- **Automatic security updates** - Managed by Atlassian
- **DDoS protection** - Built into Atlassian's infrastructure
- **Compliance certifications** - SOC 2, ISO 27001, GDPR, etc.

### 6.2 Application Security
We implement security best practices:

- **Permission checks** - Only Jira Admins can access the app
- **Authorization enforcement** - `.asUser()` API calls respect user permissions
- **Input validation** - All user inputs are validated and sanitized
- **Rate limiting** - Protection against API abuse
- **Secure API usage** - HTTPS-only communication with Jira APIs
- **No external egress** - App does not communicate with external services

### 6.3 Deletion Security
File deletion operations:

- **Require admin permissions** - Only users with DELETE_ATTACHMENTS permission
- **Are logged** - Full audit trail of who deleted what and when
- **Are irreversible** - Deleted files cannot be recovered by the app
- **Respect Jira permissions** - Users can only delete files they have access to

---

## 7. Data Retention and Deletion

### 7.1 Automatic Data Cleanup
- **Scan data** - Overwritten with each new scan
- **Deletion logs** - Limited to last 100 records per issue (automatic trimming)

### 7.2 Manual Data Deletion
Administrators can delete app data by:

1. **Running a new scan** - Overwrites previous scan data
2. **Uninstalling the app** - Removes all Forge storage data
3. **Contacting support** - For manual data deletion requests

### 7.3 App Uninstallation
When you uninstall Attachment Architect:

- ✅ All Forge storage data is deleted automatically
- ✅ Entity properties on issues are removed
- ✅ No data remains in our systems
- ⚠️ Jira's native audit logs may retain records of API calls (managed by Atlassian)

---

## 8. Data Sharing and Third Parties

### 8.1 No Third-Party Sharing
We **DO NOT**:

- Share your data with third-party services
- Use third-party analytics or tracking tools
- Integrate with external APIs or services
- Sell or rent your data to anyone

### 8.2 Atlassian Platform
Your data is processed within:

- **Atlassian Forge** - Serverless platform managed by Atlassian
- **Jira Cloud APIs** - To access attachment and issue metadata
- **Atlassian's infrastructure** - Subject to Atlassian's Privacy Policy

**Reference:** [Atlassian Privacy Policy](https://www.atlassian.com/legal/privacy-policy)

---

## 9. Compliance and Regulations

### 9.1 GDPR Compliance (EU)
For European users:

- **Data minimization** - We only collect necessary data
- **Purpose limitation** - Data used only for stated purposes
- **Right to access** - Contact us to request your data
- **Right to deletion** - Uninstall the app or contact us
- **Data portability** - Export scan results from the dashboard
- **Lawful basis** - Legitimate interest (storage optimization)

### 9.2 CCPA Compliance (California)
For California residents:

- **Right to know** - This policy discloses what data we collect
- **Right to delete** - Uninstall the app or contact us
- **Right to opt-out** - Do not install the app
- **No sale of data** - We never sell personal information

### 9.3 Other Regulations
We comply with:

- **SOC 2** - Via Atlassian Forge platform
- **ISO 27001** - Via Atlassian infrastructure
- **HIPAA** - Not applicable (we don't process health data)
- **PCI DSS** - Not applicable (we don't process payment data)

---

## 10. User Rights and Control

### 10.1 Access Your Data
You can view all data the app has collected:

- **Dashboard** - View scan statistics and analysis
- **Audit Log** - View all actions performed by the app
- **Settings** - View app configuration

### 10.2 Delete Your Data
You can delete data by:

- **Running a new scan** - Overwrites old data
- **Uninstalling the app** - Removes all data
- **Contacting support** - Request manual deletion

### 10.3 Control App Behavior
Administrators can:

- **Enable/disable Activity Panel** - Control issue panel visibility
- **Control who can delete files** - Via Jira permissions
- **View audit logs** - Track all app actions

---

## 11. Children's Privacy

Attachment Architect is a business application intended for use by organizations. We do not knowingly collect data from children under 13 (or 16 in the EU). If you believe a child has provided data to our app, please contact us immediately.

---

## 12. Changes to This Policy

We may update this Privacy Policy to reflect:

- Changes in app functionality
- Changes in legal requirements
- Changes in Atlassian Forge platform

**Notification:** We will notify users of material changes via:

- App changelog in Atlassian Marketplace
- In-app notifications (if applicable)
- Email to app administrators (if contact provided)

**Version History:**
- **v2.0.0** (January 2025) - Initial comprehensive privacy policy
- **v1.0.0** (2024) - Beta release (no formal policy)

---

## 13. Contact Information

### 13.1 Data Controller
**Company:** drinkits DEV  
**App Owner:** Kārlis Rozenbergs  
**Support Portal:** https://drinkits.atlassian.net/servicedesk/customer/portal/34

### 13.2 Privacy Inquiries
For privacy-related questions or requests:

1. **Submit a support ticket** - Via our support portal (preferred)
2. **Email** - Contact via Atlassian Marketplace listing
3. **Response time** - Within 5 business days

### 13.3 Data Subject Requests
To exercise your rights (access, deletion, portability):

1. Submit a request via our support portal
2. Include your Jira instance URL and account email
3. We will verify your identity and respond within 30 days

---

## 14. Technical Details

### 14.1 Forge Platform Security
Atlassian Forge provides:

- **Runtime isolation** - Each app runs in a separate container
- **Storage isolation** - Data is scoped to your Jira instance
- **API rate limiting** - Automatic protection against abuse
- **Automatic scaling** - Handles traffic spikes securely
- **Security monitoring** - Managed by Atlassian

### 14.2 Data Encryption
- **In transit** - TLS 1.2+ for all API communications
- **At rest** - AES-256 encryption (managed by Atlassian)
- **Key management** - Handled by Atlassian (not accessible to us)

### 14.3 Authentication and Authorization
- **User authentication** - Handled by Atlassian (OAuth 2.0)
- **Permission checks** - Via Jira REST API
- **Admin verification** - ADMINISTER permission required
- **Session management** - Handled by Atlassian

---

## 15. Transparency Commitments

We commit to:

- ✅ **Open communication** - Clear documentation of data practices
- ✅ **Minimal data collection** - Only what's necessary
- ✅ **No hidden tracking** - No analytics or telemetry
- ✅ **Prompt support** - Respond to privacy inquiries quickly
- ✅ **Regular updates** - Keep this policy current
- ✅ **User control** - Provide tools to manage your data

---

## 16. Frequently Asked Questions

### Q: Can you see the contents of my attachments?
**A:** No. We only access metadata (filename, size, hash). We never read file contents.

### Q: Is my data shared with other customers?
**A:** No. Your data is completely isolated to your Jira instance.

### Q: What happens to my data if I uninstall the app?
**A:** All app data is automatically deleted from Forge storage.

### Q: Do you use my data for AI training?
**A:** No. We do not use your data for machine learning or AI training.

### Q: Can you recover deleted attachments?
**A:** No. When you delete files via our app, they are permanently deleted from Jira. We cannot recover them.

### Q: Do you track how I use the app?
**A:** No. We do not use analytics or telemetry tools.

### Q: Is my data stored outside my region?
**A:** No. Data is stored in the same AWS region as your Jira instance.

### Q: Can I export my data?
**A:** Currently, the app does not have a built-in export feature. However, you can:
- Take screenshots of the dashboard for reporting purposes
- Copy data from tables manually
- Contact support if you need a formal data export for compliance purposes

---

## 17. Legal Basis for Processing (GDPR)

For EU users, we process data under:

- **Legitimate Interest** (Article 6(1)(f)) - Storage optimization and instance management
- **Contract Performance** (Article 6(1)(b)) - Providing the app service you subscribed to
- **Legal Obligation** (Article 6(1)(c)) - Audit logging for compliance

**Balancing Test:** Our legitimate interest in providing storage optimization does not override your rights, as we:
- Minimize data collection
- Provide transparency
- Offer easy deletion options
- Do not use data for unrelated purposes

---

## 18. Data Protection Officer

For organizations requiring a DPO contact:

**Atlassian's DPO:** privacy@atlassian.com  
**Our Privacy Contact:** Via support portal (https://drinkits.atlassian.net/servicedesk/customer/portal/34)

---

## 19. Dispute Resolution

If you have concerns about our data practices:

1. **Contact us first** - Via support portal
2. **Escalate to Atlassian** - If unresolved (privacy@atlassian.com)
3. **Regulatory authority** - File a complaint with your local data protection authority
4. **EU users** - Contact your national supervisory authority

---

## 20. Acknowledgment

By installing and using Attachment Architect, you acknowledge that you have read and understood this Privacy Policy and agree to the data practices described herein.

**For Administrators:** You are responsible for ensuring that your use of this app complies with your organization's data protection policies and applicable laws.

---

## Appendix A: Jira API Scopes Used

Our app requests the following Forge scopes:

| Scope | Purpose | Data Accessed |
|-------|---------|---------------|
| `read:jira-work` | Read issue and attachment metadata | Issues, attachments, projects |
| `write:jira-work` | Delete attachments | Attachment deletion |
| `read:jira-user` | Get user information | Display names, account IDs |
| `storage:app` | Store app data | Scan results, settings, audit logs |

**Principle:** We request only the minimum scopes necessary for app functionality.

---

## Appendix B: Data Flow Diagram

```
┌───────────���─────────────────────────────────────────────────┐
│                     Your Jira Instance                       │
│  ┌──────────────┐         ┌──────────────┐                 │
│  │  Attachments │────────▶│  Jira APIs   │                 │
│  │  (Files)     │         │  (Metadata)  │                 │
│  └──────────────┘         └──────┬───────┘                 │
│                                   │                          │
└───────────────────────────────────┼──────────────────────────┘
                                    │
                                    ▼
                    ┌───────────────────────────┐
                    │   Atlassian Forge         │
                    │   (Secure Sandbox)        │
                    │                           │
                    │  ┌─────────────────────┐ │
                    │  │ Attachment Architect│ │
                    │  │ (Our App Code)      │ │
                    │  └──────────┬──────────┘ │
                    │             │             │
                    │             ▼             │
                    │  ┌─────────────────────┐ │
                    │  │  Forge Storage      │ │
                    │  │  (Your Data Only)   │ │
                    │  └─────────────────────┘ │
                    └───────────────────────────┘
                                    │
                                    ▼
                    ┌───────────────────────────┐
                    │   Your Browser            │
                    │   (Dashboard UI)          │
                    └───────────────────────────┘

Legend:
────▶  Data flow (metadata only, never file contents)
│      No external data transmission
│      All processing within Atlassian infrastructure
```

---

## Appendix C: Incident Response

In the event of a security incident:

1. **Detection** - Atlassian monitors Forge platform security
2. **Notification** - Atlassian notifies app developers of platform issues
3. **Response** - We will investigate and patch within 24-48 hours
4. **User notification** - We will notify affected users within 72 hours
5. **Regulatory reporting** - We will comply with GDPR breach notification requirements

**Contact for security issues:** Via support portal (mark as "Security Issue")

---

**End of Privacy Policy**

*This policy is effective as of January 2025 and applies to Attachment Architect version 2.0.0 and later.*
