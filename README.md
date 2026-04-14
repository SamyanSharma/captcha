# CAPTCHA-Bypass Brute Force Tool

A Python-based security research tool designed to demonstrate the vulnerabilities of text-based CAPTCHAs using **OCR-assisted automation**. This project illustrates how traditional image-based verification can be bypassed by integrating Optical Character Recognition into a credential brute-force workflow.

---

## 🚀 Overview

This tool automates the full lifecycle of a login attempt on platforms protected by simple text CAPTCHAs. Instead of "blind" guessing, it uses machine learning to "read" the challenge, significantly increasing the efficiency of the brute-force attack.

### How It Works
The script executes a persistent automated loop:
1. **Session Persistence:** Initializes a `requests.Session()` to maintain cookies and state between the CAPTCHA fetch and the login submission.
2. **OCR Processing:** Fetches the CAPTCHA image via HTTP, processes the byte stream using `Pillow`, and utilizes the `Tesseract` engine to extract the text.
3. **Automated Submission:** Pairs the solved CAPTCHA with credentials from a wordlist and performs a POST request to the target login endpoint.
4. **Intelligent Retries:** - If the CAPTCHA is identified as incorrect by the server, the script refreshes the challenge and retries the *same* credential set.
   - If the CAPTCHA passes but credentials fail, it moves to the next entry in the wordlist.

---

## 🛠️ Technical Stack

* **Python 3.x**
* **Requests:** For persistent HTTP session management.
* **PyTesseract (Tesseract OCR):** The core engine used to translate image patterns into string data.
* **Pillow (PIL):** For image manipulation and conversion of raw bytes into readable formats.
* **Jupyter/Colab:** Optimized for interactive testing and visual debugging of OCR accuracy.

---

## 🛡️ Defensive Insights

This project is a **Proof of Concept (PoC)** to help developers understand why simple text CAPTCHAs are no longer a primary security line. Recommended defenses include:

* **Behavioral Analysis:** Implementing non-interactive challenges like reCAPTCHA v3 or Cloudflare Turnstile.
* **Rate Limiting:** Restricting the number of attempts per IP address or session.
* **WAF Integration:** Using Web Application Firewalls to detect automated "bot-like" request patterns.
* **Account Lockout:** Implementing temporary lockouts after consecutive failed attempts.

---

## ⚠️ Setup & Disclaimer

### Configuration
Before running the notebook, ensure you update the `HOME_URL` in the setup cell. The current placeholder will result in an `InvalidURL` error:
```python
HOME_URL = "[https://your-authorized-test-target.com](https://your-authorized-test-target.com)"
```

## 📋 Prerequisites
Aside from the Python libraries, the Tesseract OCR Engine must be installed on your system:

Linux: sudo apt install tesseract-ocr

macOS: brew install tesseract

Windows: Download the binary from UB Mannheim and add it to your System PATH.

## ⚖️ Disclaimer
IMPORTANT: This project is for educational and authorized security testing purposes only. Unauthorized access to or testing of computer systems is illegal and unethical. The author is not responsible for any misuse of this software. By using this tool, you agree to do so at your own risk and only on systems you own or have explicit permission to test.

## 📄 License
This project is licensed under the MIT License - see the LICENSE file for details.
