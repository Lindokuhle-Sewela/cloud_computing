# Tennis Project — AWS, Built in Stages

A tennis-themed site used as a practice project to demonstrate seven core
AWS services, one at a time. Each stage builds on the last and is pushed
as its own commit, so the repo history documents the build-up.

**Target skills:** S3 · VPC · EC2 · RDS · IAM · Lambda · CloudWatch

## Live demo

`http://<your-bucket-name>.s3-website-<region>.amazonaws.com`
*(add your live URL here once Stage 1 is deployed)*

## Architecture (once all stages are done)

```
                     ┌────────────────────────┐
   Visitor  ───────▶ │  S3 static site         │
                     │  (tennis.html + css)     │
                     └───────────┬─────────────┘
                                 │ calls
                                 ▼
                     ┌────────────────────────┐
                     │  Lambda (API Gateway)   │  ← serverless feature
                     └───────────┬─────────────┘
                                 │
                     ┌───────────▼─────────────┐
                     │        VPC               │
                     │  ┌─────────────────┐    │
                     │  │ EC2 (public      │    │
                     │  │ subnet) — small   │    │
                     │  │ backend / API     │    │
                     │  └────────┬──────────┘    │
                     │           │               │
                     │  ┌────────▼──────────┐    │
                     │  │ RDS (private       │    │
                     │  │ subnet) — tennis   │    │
                     │  │ data                │    │
                     │  └────────────────────┘    │
                     └────────────────────────────┘

   IAM roles/policies govern every arrow above.
   CloudWatch collects logs/metrics/alarms from EC2, RDS, and Lambda.
```

## Stack

- HTML5 / CSS3
- Amazon S3 — static website hosting
- Amazon VPC — custom network, public + private subnets
- Amazon EC2 — backend compute
- Amazon RDS — relational database
- AWS IAM — roles and policies
- AWS Lambda — serverless function
- Amazon CloudWatch — logs, metrics, alarms
- Git & GitHub for version control

## Project structure

```
.
├── tennis.html
├── css/
│   └── style.css
└── README.md
```

## Progress

- [x] **Stage 1 — S3**: static site hosting
- [x] **Stage 2 — VPC**: custom network for the backend
- [x] **Stage 3 — EC2**: backend server inside the VPC
- [ ] **Stage 4 — RDS**: database inside the VPC
- [ ] **Stage 5 — IAM**: least-privilege roles/policies
- [ ] **Stage 6 — Lambda**: serverless function called from the frontend
- [ ] **Stage 7 — CloudWatch**: monitoring/alarms across the stack

---

## Stage 1: S3 — static hosting

1. **Create a bucket** — AWS Console → S3 → *Create bucket*, globally
   unique name.
2. **Turn off "Block all public access"** — *Permissions* tab, uncheck
   and confirm.
3. **Add a bucket policy**:

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Sid": "PublicReadGetObject",
         "Effect": "Allow",
         "Principal": "*",
         "Action": "s3:GetObject",
         "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
       }
     ]
   }
   ```

4. **Enable static website hosting** — *Properties → Static website
   hosting → Enable*. Set `tennis.html` as the index document.
5. **Upload files** — `tennis.html` and `css/style.css`, keeping the
   `css/` folder structure intact.
6. **Visit the endpoint URL** shown under *Static website hosting*.

## Stage 2–7

Instructions for VPC, EC2, RDS, IAM, Lambda, and CloudWatch will be
added here as each stage is built.

## Pushing each stage to GitHub

```bash
git add .
git commit -m "Stage 2: VPC network setup"
git push
```