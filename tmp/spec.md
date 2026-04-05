Nice — this is exactly how real devs do it 👏
You’re basically building a **mini cloud setup at home first** (smart move).

I’ll keep it **simple + step-by-step + real-world style**.

---

# 🧠 Big Picture (your setup)

```id="u2m4e6"
MacBook → (code + GitHub)  
        ↓
GitHub repo  
        ↓
Ubuntu Lenovo (server via SSH)
```

---

# ⚠️ SUPER IMPORTANT (sudo question)

👉 Can you do it without sudo?

* **YES (mostly)** ✅ → Minecraft server itself
* **NO (for setup stuff)** ❌ → installing Java

👉 So:

* Your dad (or admin) must do **ONE TIME setup**
* After that → you can run everything without sudo

---

# 🧱 STEP 0 — One-time setup (Dad does this)

On Ubuntu machine:

```bash
sudo apt install openjdk-25-jdk -y
```

Set Java 25 as default:

```bash
export PATH=/usr/lib/jvm/java-25-openjdk-amd64/bin:$PATH
```

Check:

```bash
java -version
```

✅ If you see version 25 → good

---

# 🧱 STEP 0b — Open Firewall (One-time setup)

Allow Minecraft server port:

```bash
sudo ufw allow 25565/tcp
sudo ufw reload
```

Check status:

```bash
sudo ufw status
```

---

# 🗂️ STEP 1 — Create your GitHub project (on Mac)

Go to your GitHub:
👉 [https://github.com/ar0sh](https://github.com/ar0sh)

Create repo:

```id="l9g3o1"
Name: minecraft-server
Public
Add README
```

---

# 📁 STEP 2 — Setup project locally (Mac)

Open Windsurf / terminal:

```bash
git clone https://github.com/ar0sh/minecraft-server.git
cd minecraft-server
```

Create files:

```id="xk7t2p"
minecraft-server/
 ├── server.jar   (later)
 ├── start.sh
 └── README.md
```

---

# ▶️ STEP 3 — Create start script

Create `start.sh`:

```bash
nano start.sh
```

Paste:

```bash
#!/bin/bash
java -Xmx2G -Xms1G -jar server.jar nogui
```

Save + make executable:

```bash
chmod +x start.sh
```

---

# 📥 STEP 4 — Download Minecraft server

Go here:
👉 [https://www.minecraft.net/en-us/download/server](https://www.minecraft.net/en-us/download/server)

Download `server.jar`
Move it into your project folder

---

# 💾 STEP 5 — Push to GitHub

```bash
git add .
git commit -m "initial minecraft server setup"
git push
```

---

# 🖥️ STEP 6 — Connect to Ubuntu (Lenovo)

From your Mac:

```bash
ssh arosh@<your-lenovo-ip>
```

---

# 📦 STEP 7 — Pull project on Ubuntu

```bash
git clone https://github.com/ar0sh/minecraft-server.git
cd minecraft-server
```

---

# ▶️ STEP 8 — First run (IMPORTANT)

Run:

```bash
./start.sh
```

❌ It will FAIL (expected)

It creates:

```id="g1v8r2"
eula.txt
```

---

# ✅ STEP 9 — Accept EULA

```bash
nano eula.txt
```

Change:

```id="q2d5zp"
eula=false → eula=true
```

---

# 🚀 STEP 10 — Start server

Make sure Java 25 is in PATH:

```bash
export PATH=/usr/lib/jvm/java-25-openjdk-amd64/bin:$PATH
```

Start server:

```bash
./start.sh
```

✅ You should see:

```id="h7z9kp"
Done (X.Xs)! For help, type "help"
```



---

# 🌐 STEP 11 — Join your server

On your Minecraft (Windows/Mac):

Use your Ubuntu server's **private IP** (find it with `ip addr` on Ubuntu):

```id="m4p8yc"
<your-lenovo-ip>:25565
```

Example: `192.168.123.45:25565`

Note: Both machines must be on the same WiFi/network.

---

# 🔁 STEP 12 — Update workflow (REAL DEV STYLE)

When you change something on Mac:

```bash
git add .
git commit -m "update"
git push
```

On Ubuntu:

```bash
git pull
```

---

# ☁️ How this matches Oracle Cloud

| Thing         | Your Setup | Oracle Cloud |
| ------------- | ---------- | ------------ |
| SSH           | ✅ same     | ✅ same       |
| Ubuntu        | ✅ same     | ✅ same       |
| No GUI        | ✅ yes      | ✅ yes        |
| GitHub deploy | ✅ same     | ✅ same       |
| Public IP     | ❌ local    | ✅ internet   |

👉 You are basically doing **cloud practice already**

---

# ⚡ Important Tips

### 1. Keep server running after SSH

Use:

```bash
screen -S mc
./start.sh
```

Detach:

```bash
Ctrl + A, then D
```

---

### 2. RAM control

```bash
-Xmx2G
```

👉 Change if laptop is weak:

```bash
-Xmx1G
```

---

### 3. If it’s slow (old laptop)

* Use **PaperMC** instead of vanilla (better performance)

---

# 🎯 Quick Recap

* Install Java (needs sudo once)
* GitHub = your “code hub”
* Ubuntu = your “server”
* SSH = your control panel
* start.sh = your launcher

---

# 🧠 Mini Challenge (quick check)

1. Why did the server fail first time?
2. What does `git pull` do on the server?
3. Why is Linux used instead of Windows for servers?

---

If you want next step:
👉 I can help you **upgrade this into a 24/7 Oracle Cloud server** (same setup, just public) 🚀
