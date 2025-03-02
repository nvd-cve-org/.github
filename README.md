# **🚀 Contribution Guidelines**

This document defines the **Commit Message Convention** and **Pull Request (PR) Guidelines** for this organization. Following these conventions ensures a **clean, readable, and structured Git history**. 

---

## **📌 Commit Message Convention**
We follow a structured commit message format to improve readability, collaboration, and changelog automation.

### **✨ Commit Format**
Each commit should follow this format:

```bash
<type>: <short description>
```

🔹 **Example:**
```bash
feat: setup basic Nest.js application structure
```

---

### **✅ Commit Types**
| Type       | Description |
|------------|-------------|
| **feat**   | A new feature |
| **fix**    | A bug fix |
| **chore**  | Minor updates (config, docs, dependencies) |
| **docs**   | Documentation changes |
| **style**  | Code style changes (whitespace, formatting) |
| **refactor** | Code improvements that don’t change functionality |
| **perf**   | Performance optimizations |
| **test**   | Adding or updating tests |
| **ci**     | Changes to CI/CD pipeline |

---

### **✅ Example Commits**
```bash
feat: implement CVE API fetcher
fix: resolve unique constraint issue in database
chore: update .gitignore to exclude logs
docs: add setup instructions to README
test: add unit tests for CVE service
```

---

### **✅ How to Write a Commit**
1️⃣ **Stage your changes**
```bash
git add .
```

2️⃣ **Write a commit message**
```bash
git commit -m "feat: setup basic Nest.js application structure"
```

3️⃣ **Push to GitHub**
```bash
git push origin main
```

---

## **📌 Pull Request (PR) Guidelines**
To maintain **consistent and high-quality PRs**, follow these guidelines.

### **✅ PR Title Format**
```
[type] <short summary>
```
🔹 **Example PR Titles:**
```
[feat] Add CVE API fetcher
[fix] Resolve unique constraint issue in database
[docs] Update README with setup instructions
[test] Add unit tests for CVE service
```

---

### **✅ PR Description Template**
Every PR should include the following sections:

```
## 📌 Summary
Briefly explain what this PR does.

## 🛠️ Changes
- List all the key changes made in this PR.

## 🔍 How to Test
1. Steps to test the feature/fix.
2. Expected behavior.

## ✅ Checklist
- [ ] My code follows the coding style.
- [ ] I have written necessary unit tests.
- [ ] I have updated relevant documentation.

## 🔗 Related Issues
Closes #<issue-number> (if applicable)
```

🔹 **Example PR Description:**
```
## 📌 Summary
This PR adds an API fetcher for CVE data from NVD.

## 🛠️ Changes
- Implemented `fetchCVEData` function in `cves.service.ts`.
- Added error handling for API failures.

## 🔍 How to Test
1. Run `yarn start` and check `/cves` endpoint.
2. Ensure CVE data is fetched from NVD API.

## ✅ Checklist
- [x] My code follows the coding style.
- [x] I have written necessary unit tests.
- [x] I have updated relevant documentation.

## 🔗 Related Issues
Closes #15
```
