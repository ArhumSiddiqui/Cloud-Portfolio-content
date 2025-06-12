# Cloud Portfolio

A modern, end-to-end personal portfolio website built with **Next.js** and **TypeScript**, featuring seamless DevOps and cloud infrastructure integration.

---

## 🚀 Overview

This project is a fully responsive, production-grade portfolio site designed to showcase your skills, projects, and professional background. It’s not just a static site—this portfolio demonstrates real-world software engineering practices, including:

- **Modern front-end development** (React, Next.js, TypeScript)
- **UI/UX best practices** (responsive design, accessibility, smooth animations)
- **Cloud-native deployment** (AWS S3, CloudFront)
- **Automated CI/CD** (GitHub Actions)

---

## ✨ Features

- **Dynamic Portfolio:** Projects, skills, and about sections are all easily customizable.
- **Project Filtering:** Users can filter projects by category for a better browsing experience.
- **Smooth Animations:** Framer Motion is used for subtle, professional transitions.
- **Mobile-First Design:** Looks great on all devices.
- **Downloadable Resume:** Resume is served from the public directory for easy access.
- **Accessible & SEO-Friendly:** Uses semantic HTML, alt text, and best practices.

---

## 🛠️ Tech Stack

- **Framework:** Next.js (React, TypeScript)
- **Styling:** Tailwind CSS
- **Animation:** Framer Motion
- **Image Optimization:** Next.js `<Image />`
- **Cloud Hosting:** AWS S3 (static site), AWS CloudFront (CDN)
- **CI/CD:** GitHub Actions

---

## ⚙️ DevOps & Infrastructure

This project is set up for **continuous deployment** to AWS using a GitHub Actions workflow:

- **Automatic Deployment:**  
  Every push to the `main` branch triggers the workflow defined in `.github/workflows/front-end-cicd.yml`.
- **S3 Sync:**  
  The workflow uses the `jakejarvis/s3-sync-action` to upload the built site to an S3 bucket.
- **CloudFront Invalidation:**  
  After deployment, the workflow invalidates the CloudFront cache to ensure users always see the latest version.
- **AWS Credentials:**  
  All AWS credentials and configuration are securely managed using GitHub Secrets.

**Workflow Highlights:**
```yaml
on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - uses: jakejarvis/s3-sync-action@master
        with:
          args: --follow-symlinks --delete
        env:
          AWS_S3_BUCKET: ${{ secrets.AWS_S3_BUCKET }}
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_REGION: 'us-west-1'
          SOURCE_DIR: "website"
      - name: Invalidate CloudFront Distribution
        run: |
          aws cloudfront create-invalidation \
            --distribution-id ${{ secrets.CLOUDFRONT_DISTRIBUTION_ID }} \
            --paths "/*"
```

---

## 📁 Project Structure

```
/public
  /img
  Arham Siddiqui Resume 2025.pdf
/src
  /components
    /About
    /Skills
    /Projects
    /Hero
    /Header
    /Footer
  /app
    page.tsx
    globals.css
tailwind.config.js
tsconfig.json
.github/workflows/front-end-cicd.yml
```

---


## 🏆 Why This Project Stands Out

- **End-to-End Solution:** From code to cloud, this project demonstrates the full lifecycle of a modern web application.
- **DevOps Integration:** Automated, zero-downtime deployments with cache invalidation.
- **Cloud Native:** Built for scalability and performance using AWS infrastructure.
- **Professional Polish:** Clean design, smooth UX, and production-ready code.

---

**Feel free to fork, customize, and use this as a template for your own portfolio or cloud projects!**

---
