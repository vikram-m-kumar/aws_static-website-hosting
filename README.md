# 🌐 AWS Static Website Hosting

This project demonstrates how to host a static website on AWS with a custom domain, HTTPS, and continuous deployment from GitHub using CodePipeline.

## 🧰 Services Used

- **Amazon S3** – Stores static files (HTML, CSS, JS)
- **Amazon CloudFront** – CDN for global content delivery
- **Amazon Route 53** – Domain registration and DNS routing
- **AWS Certificate Manager (ACM)** – Manages SSL/TLS certificates
- **AWS CodePipeline + CodeBuild** – Automates CI/CD from GitHub

## 🔐 Domain & HTTPS

- Custom Domain: `www.static-website-hosting.org`
- SSL: Managed via ACM
- HTTPS supported through CloudFront distribution

## 🔁 CI/CD Pipeline

1. **GitHub** → Push commits
2. **CodePipeline** detects changes in the GitHub repo
3. **Deploy Stage (S3)** automatically syncs new files to the static S3 bucket
4. **CloudFront** serves the updated content over HTTPS globally

## 🛠️ Setup Steps

1. Upload static files to GitHub repo  
2. Set up S3 bucket (private) with website files  
3. Configure CloudFront with custom domain and ACM cert  
4. Register domain in Route 53 and point to CloudFront  
5. Use CodePipeline to deploy directly from GitHub to S3  

## 📝 License

This project is for educational purposes.

