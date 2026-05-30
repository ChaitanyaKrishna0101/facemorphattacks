# 🎭 Morphy — Face Morphing Attack Generation & Detection System

> A full-stack web application that both **generates** and **detects** face morphing attacks — the kind used to fool passport scanners, border security systems, and banking KYC checks.

🌐 **Live Demo:** [https://facemorphattacks.onrender.com](https://facemorphattacks.onrender.com)
📦 **GitHub:** [ChaitanyaKrishna0101/facemorphattacks](https://github.com/ChaitanyaKrishna0101/facemorphattacks)

---

## 🧠 What is a Face Morphing Attack?

Imagine two people — a criminal and an innocent person. A face morphing attack **blends their faces together** into one image. This blended image:

- Looks like the criminal to a human eye
- But also matches the innocent person's passport photo
- Fools facial recognition systems used at airports and banks

This is a **real security threat** used in identity fraud worldwide.

```
Person A 😊 + Person B 😐 = Morphed Face 😶 → Fools the system!
```

This project **generates** such morphed faces (for research) and **detects** them (for security).

---

## ⚡ Why This Project Runs Differently

Most AI/security projects take hours to set up — downloading models, fixing CUDA errors, running out of RAM. This project is intentionally built to avoid all of that.

### ⚡ Why This Project Stands Out

<div align="center">

<table>
<tr>
<td valign="top" width="50%">

### ⚡ Why This Project Stands Out

<div align="center">

| | 🏠 Local Setup — Under 5 Minutes | 🚀 Deployment — One Push |
|---|---|---|
| **Problem** | **How we solved it** | **How we solved it** |
| Heavy model downloads | No model downloads — uses SSIM algorithm | Dockerfile handles everything automatically |
| Needs GPU | Runs on any laptop, even low-end ones | Just add environment variables on Render |
| Complex dependencies | Pure Python, one `pip install -r requirements.txt` | GitHub push → Render auto-deploys in 3 minutes |
| Hard to run | Just `python manage.py runserver` | Zero downtime rolling deploys |

</div>

### 🐳 Why Docker Makes This Smarter

Unlike projects that ship raw Python scripts, this project uses **Docker** — which means:

- **Same behavior everywhere** — works identically on Windows, Mac, Linux, and the cloud
- **No "works on my machine" problems** — the entire environment is packaged
- **One command to run anywhere** — `docker run` and it's live
- **Reliable deployments** — if it works locally in Docker, it works in production
- **Easy scaling** — spin up multiple containers if traffic grows

> The Docker container packages Python 3.9, all system libraries (OpenCV dependencies, MySQL client), and your Django app — all in one portable unit. No setup. No surprises.

---

## 🎯 The Problem This Solves

### Real World Threat
Face morphing attacks are used to:
- 🛂 Bypass **airport passport checks** — one morphed passport, two people can travel
- 🏦 Fool **banking KYC systems** — criminals use innocent people's face-blended IDs
- 🪪 Compromise **national ID verification** — identity fraud at scale

### The Gap
Most security systems **verify** faces but cannot **detect if the face itself is morphed**. This project fills that gap.

---

## Snapshots

<div align="center">

| | | |
|:---:|:---:|:---:|
| <img width="270" src="https://github.com/user-attachments/assets/8631ff21-ad87-48c7-a86b-acda9857fb13" /> | <img width="270" src="https://github.com/user-attachments/assets/6e0ffb7e-e6fa-4fe9-8a5b-018d4b1c7a43" /> | <img width="270" src="https://github.com/user-attachments/assets/d6c38d14-d741-4cdc-89c6-7ab355453156" /> |
| <img width="270" src="https://github.com/user-attachments/assets/b43733d9-a416-49c9-afea-0a9f47bbd066" /> | <img width="270" src="https://github.com/user-attachments/assets/2d31cf9b-4786-4661-bbd8-fe2bb70b6667" /> | <img width="270" src="https://github.com/user-attachments/assets/ce5d4b75-e108-46af-8bbd-b1f8397e0f9b" /> |
| <img width="270" src="https://github.com/user-attachments/assets/5ad83083-0cde-454e-85f5-dd65f3701c86" /> | <img width="270" src="https://github.com/user-attachments/assets/da54ee6e-8daa-4eb3-8803-7a9af0819404" /> | <img width="270" src="https://github.com/user-attachments/assets/d472af0e-d2ef-4744-8823-63371bf6e64d" /> |

</div>

---

## ✨ Key Features

### 👤 User Side
| Feature | What it does |
|---|---|
| 🔐 Register & Login | Secure user authentication |
| 🎭 Generate Morphed Faces | Upload 2-3 photos → get a morphed face |
| 📋 Submit Application | Apply with a photo for identity verification |
| 📊 Analysis Dashboard | View your morphing results and history |
| 👤 Profile Management | Manage your account |

### 🛡️ Admin Side
| Feature | What it does |
|---|---|
| 📊 Dashboard | Real-time counts of pending/verified/invalid applications |
| 👥 View All Users | See all registered users |
| 🔍 Detect Morph Attacks | Run detection on pending applications |
| ✅ Verified Applications | Applications that passed detection |
| ❌ Invalid Applications | Applications flagged as morphed |
| 📈 Graph Analysis | Visual charts of detection results |

---

## 🏗️ System Design

```
┌─────────────────────────────────────────────────────┐
│                   MORPHY SYSTEM                     │
├─────────────┬───────────────────┬───────────────────┤
│  USER LAYER │   DJANGO BACKEND  │   ADMIN LAYER     │
│             │                   │                   │
│  Register   │   URL Routing     │  Admin Login      │
│  Login      │   Views           │  Dashboard        │
│  Morph      │   Models          │  Detect Morphs    │
│  Apply      │   FaceMatch.py    │  Manage Apps      │
│  Profile    │   Static Files    │  Graph Analysis   │
└─────┬───────┴────────┬──────────┴───────┬───────────┘
      │                │                  │
      ▼                ▼                  ▼
┌──────────┐    ┌─────────────┐    ┌──────────────┐
│PostgreSQL│    │  Media      │    │  WhiteNoise  │
│Database  │    │  Storage    │    │  Static CDN  │
│(Supabase)│    │  (Images)   │    │  (CSS/JS)    │
└──────────┘    └─────────────┘    └──────────────┘
```

---

## 🔄 User Flow

```
User Visits Site
      │
      ▼
  Register / Login
      │
      ├──────────────────────────┐
      ▼                          ▼
Generate Morphed Face      Submit Application
      │                          │
      │ Upload 2-3 photos         │ Upload ID photo
      │ System blends faces       │ Enter personal details
      │ Download morphed image    │ Status: Pending
      │                          │
      ▼                          ▼
  View Results              Wait for Admin Review
                                 │
                    ┌────────────┴────────────┐
                    ▼                         ▼
              ✅ Verified               ❌ Invalid
              (Clean image)        (Morphed image detected)
```

---

## 🔬 Detection & Generation Flow

### 🎭 Generation Flow

```
Input: Photo A + Photo B (+ optional Photo C)
              │
              ▼
    Load images with OpenCV
              │
              ▼
    Convert to grayscale
              │
              ▼
    Blend pixel values (alpha blending)
              │
              ▼
    Save morphed image to /media/morphed/
              │
              ▼
    Output: One morphed face image
```

### 🔍 Detection Flow

```
Admin clicks "Verify Application"
              │
              ▼
    Load applicant's uploaded photo
              │
              ▼
    Load ALL known morphed images from database
              │
              ▼
    For each morphed image:
    ┌─────────────────────────────────────────┐
    │  Compare using SSIM Algorithm           │
    │  (Structural Similarity Index Measure)  │
    │                                         │
    │  SSIM Score = 0.0 → completely different│
    │  SSIM Score = 1.0 → identical images   │
    └────────────────┬────────────────────────┘
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
    Score ≥ 0.9           Score < 0.9
    (90% similar)         (Not similar)
          │                     │
          ▼                     ▼
    ❌ INVALID            Continue checking
    Mark as morphed        next image
    attack detected              │
                                 ▼
                    All images checked → ✅ VERIFIED
```

### 🧮 Why SSIM?

SSIM (Structural Similarity Index Measure) is better than simple pixel comparison because it measures:
- **Luminance** — how bright is the image?
- **Contrast** — how different are light and dark areas?
- **Structure** — what do the shapes and edges look like?

This makes it robust against minor lighting changes and compression artifacts.

**Threshold: 0.9 (90% similarity)**
- If SSIM ≥ 0.9 → morphed attack detected → application rejected
- If SSIM < 0.9 → no match found → application approved

---

## 💡 Real Use Cases

### 🛂 Airport / Border Security
```
Traveller presents passport
        │
        ▼
System scans face
        │
        ▼
Morphy checks if face is morphed
        │
        ▼
✅ Real person → board the plane
❌ Morphed face → flagged for manual check
```

### 🏦 Banking KYC (Know Your Customer)
```
Customer submits ID photo for account opening
        │
        ▼
Bank runs Morphy detection
        │
        ▼
✅ Clean image → account approved
❌ Morphed image → fraud prevented
```

### 🏛️ Government ID Verification
```
Citizen applies for national ID card
        │
        ▼
Government runs photo through Morphy
        │
        ▼
✅ Genuine face → ID issued
❌ Morphed face → application rejected, flagged
```

---

## 🌍 Real World Applications

| Sector | Application |
|---|---|
| ✈️ Aviation | Passenger identity verification at check-in |
| 🏦 Banking | Fraud prevention in remote account opening |
| 🏥 Healthcare | Patient identity verification |
| 🎓 Education | Online exam proctoring identity checks |
| 🏛️ Government | E-passport and national ID verification |
| 🔐 Enterprise | Secure access control systems |

---

## 🗄️ Database Design

### UserModel
| Field | Type | Description |
|---|---|---|
| name | CharField | User's full name |
| email | EmailField | Login email |
| mobile | CharField | Phone number |
| city | CharField | City of residence |
| picture | ImageField | Profile photo |
| password | CharField | Hashed password |

### ApplicationModel
| Field | Type | Description |
|---|---|---|
| fullname | CharField | Applicant's first name |
| surname | CharField | Applicant's last name |
| dob | DateField | Date of birth |
| picture | ImageField | ID photo for verification |
| email | EmailField | Contact email |
| mobile | CharField | Phone number |
| gender | CharField | Gender |
| marital_status | CharField | Marital status |
| citizenship_by | CharField | How citizenship was obtained |
| education | CharField | Education level |
| status | CharField | Pending / Verified / Invalid |

### MorphedImages
| Field | Type | Description |
|---|---|---|
| image1 | ImageField | First source image |
| image2 | ImageField | Second source image |
| image3 | ImageField | Optional third source image |
| morphedimage | ImageField | Generated morphed output |
| user | ForeignKey | Who generated this morphed image |
| data | DateField | Auto-generated creation date |

---

## 🛠️ Tech Stack

### Backend
| Technology | Version | Purpose |
|---|---|---|
| Python | 3.9 | Core programming language |
| Django | 4.1.5 | Web framework |
| Gunicorn | 23.0.0 | Production WSGI server |
| python-dotenv | 1.2.1 | Environment variable management |

### Computer Vision & AI
| Technology | Version | Purpose |
|---|---|---|
| OpenCV (Headless) | 4.5.5.64 | Image loading and processing |
| scikit-image | 0.19.3 | SSIM similarity computation |
| NumPy | 1.24.1 | Numerical image operations |
| Pillow | 9.4.0 | Image file handling |
| SciPy | 1.10.0 | Scientific computations |
| Matplotlib | 3.3.3 | Analysis graphs and charts |

### Database
| Technology | Purpose |
|---|---|
| PostgreSQL | Production database (Render/Supabase) |
| MySQL | Local development database |
| psycopg2-binary | PostgreSQL Python driver |
| dj-database-url | Database URL parsing |

### Frontend
| Technology | Purpose |
|---|---|
| HTML5 / CSS3 | Page structure and styling |
| Bootstrap | Responsive UI components |
| jQuery | DOM manipulation |
| Chart.js | Analysis graphs |
| AOS | Scroll animations |

### DevOps & Deployment
| Technology | Purpose |
|---|---|
| Docker | Containerization |
| Render | Cloud hosting (free tier) |
| WhiteNoise | Static file serving in production |
| GitHub | Version control and CI/CD |

---

## 🚀 Getting Started

### 🗄️ Step 1 — Set Up Your Free Database (Required First)

Before running the project, you need a free database. Use **Supabase** — free forever, no credit card!

**1. Go to** 👉 [supabase.com](https://supabase.com) → Sign up with GitHub

**2. Create a new project:**
- Click **New Project**
- Name: `facemorphattacks`
- Set a database password (remember it!)
- Region: **Southeast Asia**
- Click **Create Project** → wait 2 minutes ⏳

**3. Get your Database URL:**
- Go to **Project Settings** (gear icon) → **Database**
- Scroll to **Connection String** → Select **URI** tab
- Copy the URL — it looks like:
```
postgresql://postgres:yourpassword@db.xxxx.supabase.co:5432/postgres
```

---

### 🔒 Step 2 — Create .env File

Create a `.env` file in the project root:

```dotenv
# Generate from https://djecrety.ir
SECRET_KEY="your-secret-key-here"

DEBUG=True

# Paste your Supabase URL here
DATABASE_URL=postgresql://postgres:yourpassword@db.xxxx.supabase.co:5432/postgres

# Admin panel login credentials (choose your own)
ADMIN_USERNAME=admin
ADMIN_PASSWORD=Admin@123
```

> 💡 **How to get SECRET_KEY:** Go to [djecrety.ir](https://djecrety.ir) → Click Generate → Copy and paste it above.

---

### 🐳 Option A — Docker (Recommended, 2 minutes)

No Python, no MySQL, no virtual environment needed!

```bash
# 1. Clone the repository
git clone https://github.com/ChaitanyaKrishna0101/facemorphattacks.git
cd facemorphattacks

# 2. Create .env file (Step 2 above)

# 3. Build the Docker image
docker build -t facemorphattacks .

# 4. Run the container
docker run -p 8000:8000 --env-file .env facemorphattacks
```

Visit: **http://localhost:8000** ✅ Done!

> Docker automatically installs Python, all libraries, OpenCV dependencies, and starts the server — all in one command.

---

### 🐍 Option B — Manual Setup (5 minutes)

Requires Python 3.9+ and Git installed.

```bash
# 1. Clone the repository
git clone https://github.com/ChaitanyaKrishna0101/facemorphattacks.git
cd facemorphattacks

# 2. Create virtual environment
python -m venv faceenv
faceenv\Scripts\activate        # Windows
source faceenv/bin/activate     # Mac/Linux

# 3. Install dependencies
pip install -r requirements.txt

# 4. Create .env file (Step 2 above)

# 5. Run migrations
python manage.py migrate

# 6. Start the server
python manage.py runserver
```

Visit: **http://127.0.0.1:8000** ✅ Done!

---

### 📊 Quick Comparison

| | Docker | Manual |
|---|---|---|
| Install Python | ❌ Not needed | ✅ Required |
| Install MySQL | ❌ Not needed | ❌ Not needed (uses Supabase) |
| Commands to run | 4 | 6 |
| Time to setup | 2 minutes | 5 minutes |
| Recommended for | Everyone | Developers |

---

## 📁 Project Structure

```
facemorphattacks/
│
├── 📁 adminapp/              # Admin module
│   ├── views.py              # Admin views (login, dashboard, detection)
│   ├── models.py             # Admin models
│   └── urls.py               # Admin URL routes
│
├── 📁 userapp/               # User module
│   ├── views.py              # User views (register, morph, apply)
│   ├── models.py             # User, Application, MorphedImages models
│   └── urls.py               # User URL routes
│
├── 📁 mainapp/               # Main/landing module
│   └── views.py              # Home, about, contact pages
│
├── 📁 facemorphattacks/      # Django project settings
│   ├── settings.py           # Configuration
│   ├── urls.py               # Root URL configuration
│   └── wsgi.py               # WSGI entry point
│
├── 📁 assets/
│   ├── static/               # CSS, JS, images
│   └── templates/            # HTML templates
│       ├── main/             # Landing page templates
│       ├── user/             # User dashboard templates
│       └── admin/            # Admin dashboard templates
│
├── 📁 staticfiles/           # Collected static files (production)
├── 📁 media/                 # User uploaded images
├── 🐳 Dockerfile             # Docker configuration
├── 📄 requirements.txt       # Python dependencies
├── 🔒 .env                   # Environment variables (not in git)
└── 📄 .gitignore             # Git ignore rules
```

---

## 🔐 Security Features

- ✅ Environment variables for all secrets (never hardcoded)
- ✅ `.env` file excluded from git
- ✅ CSRF protection on all forms
- ✅ SSL/TLS enforced on database connections
- ✅ DEBUG=False in production
- ✅ Secret key rotatable via environment variable

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📄 License

This project is for educational and research purposes only.

---

## 👨‍💻 Developer

**Chaitanya Krishna**
- GitHub: [@ChaitanyaKrishna0101](https://github.com/ChaitanyaKrishna0101)
- Live Project: [facemorphattacks.onrender.com](https://facemorphattacks.onrender.com)

---

> ⚠️ **Disclaimer:** This project is built strictly for academic research and security awareness. The face morphing generation feature is intended to help researchers understand the threat — not to facilitate identity fraud.
