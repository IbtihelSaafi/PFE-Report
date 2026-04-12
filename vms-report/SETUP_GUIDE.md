# VMS Setup & Installation Guide

## 1. Prerequisites

### System Requirements
- Python 3.11+
- PostgreSQL 16+
- 8GB RAM minimum (16GB recommended for Ollama)
- Tenable Nessus 10.x (Essentials or Professional)

---

## 2. Application Installation (Linux/macOS)

```bash
# Clone repository
git clone https://github.com/bahagmar/Vulnerability-Management-Tool.git
cd Vulnerability-Management-Tool

# Create virtual environment
python3.11 -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

---

## 3. PostgreSQL Setup

```bash
# Install PostgreSQL
sudo apt install postgresql-16     # Ubuntu/Debian
# brew install postgresql@16       # macOS

# Start service
sudo systemctl start postgresql

# Create database and user
sudo -u postgres psql << 'EOF'
CREATE USER vms_user WITH PASSWORD 'your_secure_password';
CREATE DATABASE vms_db OWNER vms_user;
GRANT ALL PRIVILEGES ON DATABASE vms_db TO vms_user;
EOF
```

---

## 4. Environment Configuration

```bash
cp .env.example .env
nano .env
```

Fill in the required values (see `appendix.tex` or `.env.example` for all variables).

---

## 5. Database Initialization

```bash
# Run migrations
flask db upgrade

# (Optional) Seed default admin user
flask shell
>>> from models import User, db
>>> from werkzeug.security import generate_password_hash
>>> admin = User(username='admin', email='admin@company.com',
...              password=generate_password_hash('Admin@1234'), role='admin')
>>> db.session.add(admin)
>>> db.session.commit()
>>> exit()
```

---

## 6. Ollama Setup

```bash
# Install Ollama
curl -fsSL https://ollama.ai/install.sh | sh

# Start Ollama service
systemctl enable --now ollama
# OR: ollama serve &

# Pull Mistral 7B model (~4GB download)
ollama pull mistral

# Verify installation
ollama run mistral "Hello, test"
```

---

## 7. Tenable Nessus Integration

1. Open Nessus web interface: `https://your-nessus-server:8834`
2. Go to **Settings → My Account → API Keys**
3. Click **Generate** to create Access Key and Secret Key
4. Copy both keys to your `.env` file:
   ```
   NESSUS_ACCESS_KEY=your_access_key_here
   NESSUS_SECRET_KEY=your_secret_key_here
   NESSUS_URL=https://your-nessus-server:8834
   ```

---

## 8. Running the Application

```bash
# Development
flask run --host=0.0.0.0 --port=5000

# Production (with Gunicorn)
gunicorn -w 4 -b 0.0.0.0:5000 app:app
```

Access the application at: `http://localhost:5000`

---

## 9. Docker Deployment (Recommended)

```bash
# Build and start all services
docker compose up -d

# Check logs
docker compose logs -f

# Stop services
docker compose down
```

---

## 10. Troubleshooting

| Issue | Solution |
|-------|---------|
| `Connection refused` to Nessus | Check SSL: set `NESSUS_VERIFY_SSL=False` for self-signed certs |
| Ollama timeout | Increase `OLLAMA_TIMEOUT=180` in `.env` |
| DB connection error | Verify `DATABASE_URL` format in `.env` |
| Email not sending | Check SMTP credentials and port (587 for TLS) |
| Dashboard slow | Add database indexes: `flask db upgrade` |

---

## 11. Default Login

After seeding the database:
- **URL**: http://localhost:5000
- **Username**: admin
- **Password**: Admin@1234 *(change immediately!)*
