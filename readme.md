# Flask + Express AWS Deployment

This repository shows how to deploy a Flask backend + Express frontend on AWS.

## Project Structure

- `backend/` — Flask app, `app.py`, `requirements.txt`
- `frontend/` — Express app, `index.js`, `package.json`
- `README.md` — This deployment guide
- `.gitignore`

---

## 1️⃣ Single EC2 Deployment

1. Launch EC2 instance (Ubuntu 22.04, t2.micro / t3.micro)  
2. Security group inbound rules:
   - SSH (22) → My IP  
   - HTTP (80) → 0.0.0.0/0  
   - Custom TCP (5000) → 0.0.0.0/0  
   - Custom TCP (3000) → 0.0.0.0/0  
3. SSH into instance:
   ```bash
   ssh -i mohdsahal924.pem ubuntu@<EC2-Public-IP>
