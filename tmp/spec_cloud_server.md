Love it — now we’re leveling up to **real cloud deployment** 🚀
I’ll keep this **careful + simple + real-world accurate**.

---

# ☁️ PART 1 — Move your server to Oracle Cloud (step-by-step)

## 🧠 What you’re building

```id="flow1"
Mac → GitHub → Oracle Cloud (Ubuntu VM) → Minecraft server (public)
```

---

## 🟢 STEP 1 — Create Oracle Cloud account

Go to: [https://www.oracle.com/cloud/free/](https://www.oracle.com/cloud/free/)

👉 Choose **“Always Free”**

---

## 🟢 STEP 2 — Create a VM (server)

Inside Oracle dashboard:

* Go to **Compute → Instances → Create**
* Name: `minecraft-server`
* Image:
  👉 **Ubuntu 22.04**
* Shape:
  👉 Choose **Always Free (Ampere ARM)**
  (best free option)

---

## 🔑 STEP 3 — SSH key (IMPORTANT)

When creating VM:

* Click **Generate SSH key pair**
* Download private key

On your Mac:

```bash
chmod 600 your-key.pem
```

---

## 🌐 STEP 4 — Connect via SSH

```bash
ssh -i your-key.pem ubuntu@<public-ip>
```

👉 This is EXACTLY like your Lenovo — just remote

---

## 🧱 STEP 5 — Install Java (needs sudo here)

```bash
sudo apt update
sudo apt install openjdk-21-jdk -y
```

Check:

```bash
java -version
```

---

## 🔥 STEP 6 — Open Minecraft port (CRITICAL)

Oracle blocks ports by default.

### A. In Oracle dashboard:

* Go to **Networking → VCN → Security List**
* Add rule:

```id="rule"
Port: 25565  
Source: 0.0.0.0/0  
Protocol: TCP
```

### B. On the server:

```bash
sudo ufw allow 25565
```

---

## 📦 STEP 7 — Pull your GitHub project

```bash
git clone https://github.com/<your-username>/minecraft-server.git
cd minecraft-server
```

---

## ▶️ STEP 8 — Run server

```bash
chmod +x start.sh
./start.sh
```

Accept EULA again if needed.

---

## 🧠 STEP 9 — Keep server running

```bash
sudo apt install screen -y
screen -S mc
./start.sh
```

Detach:

```id="detach"
Ctrl + A, then D
```

---

## 🌍 STEP 10 — Join from Minecraft

Use:

```id="join"
<oracle-public-ip>:25565
```

🎉 Now anyone can join

---

# ⚠️ PART 2 — Local vs Oracle limits (REAL answer)

## 🖥️ Your Local Server (Lenovo)

### Limits (NOT hardware):

* ❌ Friends can’t join unless port forwarding
* ❌ Server stops when PC off
* ❌ Internet upload speed matters

### Practical player count:

👉 Usually:

```id="localplayers"
2–8 players (stable)
```

---

## ☁️ Oracle Free Server (Ampere ARM)

Typical free specs:

* 4 CPU cores
* 24 GB RAM (shared limit pool)

### BUT real Minecraft usable:

👉 You should use:

```id="ram"
2–6 GB RAM
```

---

## 🎮 Player limits (REALISTIC)

### Vanilla server:

```id="vanilla"
5–10 players smooth
```

### With PaperMC (optimized):

```id="paper"
10–20 players possible
```

---

# ⚠️ Hidden limitations (IMPORTANT)

## 🧊 1. CPU speed

* ARM CPU ≠ super strong per core
* Minecraft likes **strong single-core**

👉 So:

* Many players = lag

---

## 🌐 2. Network rules

* Must open ports (you did)
* Some ISPs block stuff (rare)

---

## 🔌 3. Idle shutdown risk

* Oracle may reclaim inactive VMs (rare but possible)

---

## 💾 4. Storage limits

* ~200 GB total free

---

# ⚖️ Final Comparison

| Feature          | Local      | Oracle Cloud |
| ---------------- | ---------- | ------------ |
| 24/7             | ❌          | ✅            |
| Public access    | ❌ (hard)   | ✅            |
| Setup difficulty | Easy       | Medium       |
| Performance      | Depends PC | Stable       |
| Best for         | Testing    | Real server  |

---

# 🧠 Pro Tips (VERY IMPORTANT)

### 1. Use PaperMC (huge boost)

👉 I recommend switching later

---

### 2. Lower render distance

In `server.properties`:

```id="render"
view-distance=6
```

---

### 3. Limit players

```id="players"
max-players=10
```

---

# 🎯 What you just built

👉 You now understand:

* Local vs cloud
* Dev → deploy workflow
* Real server architecture

That’s actually **junior developer level knowledge** 🔥

---

# 🧠 Mini challenge

1. Why do we open port 25565?
2. Why is PaperMC better than vanilla?
3. What’s the biggest weakness of Oracle free tier?

---

If you want next:
👉 I can help you **make auto-deploy (push to GitHub → server updates automatically)**
That’s how real companies do it 😄
