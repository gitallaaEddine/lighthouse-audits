# Lighthouse Batch Audit

**🚀 Automated Google Lighthouse audits for multiple websites using GitHub Actions**

Run full Lighthouse performance, accessibility, SEO, and best practices reports on dozens of URLs in one click. Perfect for agencies, SEO teams, developers, and performance monitoring.

---

## ✨ Features

- **One-click batch auditing** — no local installation needed
- Full Google Lighthouse reports (Performance, Accessibility, Best Practices, SEO, PWA)
- Supports **hundreds of URLs** at once
- Beautiful interactive HTML reports + JSON data
- Automatically uploaded as downloadable GitHub Artifact
- Clean and simple workflow
- Runs on Ubuntu with Node.js 20 (latest stable)

---

## 🚀 How to Use

### 1. Setup the Repository
1. Fork or clone this repo
2. Add your websites to `urls.txt` (one URL per line)

### 2. Run the Audit
1. Go to the **Actions** tab in your GitHub repository
2. Click on **Lighthouse Batch Audit** workflow
3. Click **Run workflow**
4. Click the green **Run workflow** button

The workflow will start immediately and usually finish in 2–10 minutes depending on the number of URLs.

---

## 📝 Configuration

### `urls.txt` (Required)

Create a file called `urls.txt` in the root of your repository with one URL per line:

```txt
https://yourwebsite.com
https://example.com
https://google.com
https://competitor-site.com
https://another-project.com
Tips:
	•	You can add as many URLs as you want
	•	HTTP and HTTPS are both supported
	•	Order doesn’t matter

📊 What You Get
After the workflow completes:
	•	Go to Actions → Click on the latest workflow run
	•	Scroll down to Artifacts section
	•	Download lighthouse-reports
Inside the zip you will find:
	•	One .html report per URL (open in any browser)
	•	One .json report per URL (for further analysis)

🔧 Workflow File (`.github/workflows/lighthouse-batch-audit.yml`)
This is the exact workflow included in the repo:
name: Lighthouse Batch Audit

on:
  workflow_dispatch:

jobs:
  audit:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repo
        uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Install lighthouse-batch
        run: npm install -g lighthouse-batch

      - name: Run lighthouse-batch
        run: |
          URLS=$(tr -d '\r' < urls.txt | tr '\n' ',' | sed 's/,$//')
          echo "Running on: $URLS"
          lighthouse-batch -s "$URLS"

      - name: Collect reports
        run: |
          mkdir -p reports
          mv report/lighthouse/* reports/

      - name: Upload reports
        uses: actions/upload-artifact@v4
        with:
          name: lighthouse-reports
          path: reports

🛠️ Customization Options
You can easily edit the workflow file to:
	•	Run on a schedule (add cron trigger)
	•	Change Node version
	•	Add extra Lighthouse flags (e.g., --chrome-flags, --quiet, etc.)
	•	Change artifact name
	•	Send reports to Slack/Discord (extra steps)

📌 Requirements
	•	GitHub account (free)
	•	urls.txt file with your list of websites
No local tools or Chrome needed — everything runs 100% in the cloud.

Perfect for:
	•	SEO audits
	•	Competitor analysis
	•	Website performance monitoring
	•	Client reporting
	•	Pre-launch checks

Happy auditing! 🔥
Simple, powerful, and completely free Google Lighthouse batch runner using GitHub Actions
**✅ Ready to copy-paste!**  
Just copy everything above and save it as `README.md` in your repository.  

Would you like me to also create a sample `urls.txt` example or add badges (like GitHub Actions status) to the README?
