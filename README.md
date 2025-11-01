
## 🛡️ Password Leak Checker Bot (n8n Automation)

### 🔍 Overview

The **Password Leak Checker Bot** is an automated workflow built using **n8n** to detect whether an email or password has been compromised in known data breaches. When a form submission occurs, the bot checks multiple APIs for leaked credentials and automatically sends an alert email to the user.

This no-code/low-code version replaces manual scripting with a fully automated, visual workflow powered by **n8n**, integrated with **HaveIBeenPwned API**, **BreachDirectory API**, and **Gmail**.

---

### ⚙️ Tools & Technologies

| Component               | Purpose                                           |
| ----------------------- | ------------------------------------------------- |
| **n8n Cloud**           | Workflow automation and orchestration             |
| **HTTP Request Node**   | To call HaveIBeenPwned and BreachDirectory APIs   |
| **AI Agent Node**       | To interpret and summarize API responses          |
| **Gmail Node**          | To send email alerts for detected breaches        |
| **HaveIBeenPwned API**  | Checks for known compromised emails/passwords     |
| **BreachDirectory API** | Expands search to additional breach databases     |
| **Form Trigger Node**   | Captures user input (email/password) for checking |

---

### 🧩 Workflow Design

Below is the logical flow of the automation:

1. **📝 On Form Submission**

   * Captures the user's email or password input.

2. **🌐 HTTP Request**

   * Sends a GET request to `HaveIBeenPwned` or `BreachDirectory` APIs to check for leaks.
   * Example endpoint:

     ```
     GET https://email-breach-search.api/{email_or_hash}
     ```

3. **🤖 AI Agent**

   * Parses and interprets the API response.
   * Generates a human-readable breach summary (e.g., sites affected, type of leak, etc.).
   * Uses contextual understanding to decide if an alert should be sent.

4. **📧 Gmail**

   * Sends an automated alert email to the user summarizing the breach findings.

---

### 🧠 Example Workflow (Screenshot)



**Workflow Description:**

* The workflow starts with the **Form Submission trigger**.
* The input is sent to the **HTTP Request node** for breach lookup.
* The **AI Agent node** processes results using the configured model.
* If breaches are detected, an **email alert** is sent via **Gmail** to the user.

---

### 🧰 Setup Instructions

1. **Create n8n Cloud Account**

   * Sign up at [n8n.io](https://n8n.io).
   * Create a new workflow named `Password Leak Checker`.

2. **Add the Following Nodes**

   * **Trigger:** Form Submission
   * **HTTP Request:** API call to HaveIBeenPwned or BreachDirectory
   * **AI Agent:** Summarize results
   * **Gmail:** Send results to the user

3. **Connect API Endpoints**

   * Add API URLs and credentials for:

     * [HaveIBeenPwned API](https://haveibeenpwned.com/API/v3)
     * [BreachDirectory API](https://breachdirectory.org/api)
   * Securely store API keys using n8n’s **Credentials** feature.

4. **Configure Gmail Node**

   * Authorize with your Gmail account.
   * Set up the email message template (subject, body, and recipient).

5. **Execute Workflow**

   * Test using a sample email or password (non-sensitive data).
   * Check execution logs for results.

---

### 📬 Example Email Alert

**Subject:** ⚠️ Breach Alert: Your Email May Have Been Compromised

**Body:**

```
Hello [User],

We detected potential breaches linked to your credentials.
Here’s a summary:

- Breached Sites: 3
- Exposed Data: Email, Password, Phone
- Last Seen: July 2023

Please update your passwords immediately and enable 2FA.

— Password Leak Checker Bot (n8n)
```

---

### ✅ Key Features

* 🔒 No sensitive data stored or logged.
* 🤖 Fully automated from input to email notification.
* 📡 Integrates multiple APIs for higher accuracy.
* 🧠 Uses AI Agent node for natural-language summaries.
* 📬 Real-time email alerts via Gmail.

---

### 🚀 Future Enhancements

* Add database logging for analytics (MongoDB or Google Sheets node).
* Enable Telegram or Slack notifications.
* Include domain-wide leak scanning for enterprise users.

---

