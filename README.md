
# Odoo 16.0 Docker Compose

**Deploy Odoo 16.0 in seconds — with support for multiple instances on the same server**

## 🚀 Quick Installation

Install [Docker](https://docs.docker.com/get-docker/) dan [Docker Compose](https://docs.docker.com/compose/install/), ini onelinernya:
```
sudo apt update && sudo apt install -y ca-certificates curl gnupg lsb-release && curl -fsSL https://get.docker.com | sh
```


lalu jalankan perintah ini untuk setup instance pertama di `localhost:16001` (default master password: `rezahandsome123`):

```bash
curl -s https://raw.githubusercontent.com/rezak400/odoo-docker-compose/master/run.sh | bash -s odoo-one 16001 26001
```

Untuk membuat instance tambahan (misalnya di port `11018`):

```bash
curl -s https://raw.githubusercontent.com/rezak400/odoo-docker-compose/master/run.sh | bash -s odoo-two 18002 28002
```

**Parameter:**
- `odoo-one` → Nama folder instance Odoo
- `16001` → Port Odoo
- `26001` → Port live chat

Jika `curl` belum terpasang:

```bash
sudo apt install curl
# atau
sudo yum install curl
```

<p>
<img src="screenshots/odoo-18-docker-compose.gif" width="100%">
</p>

---

## 🧰 Usage

**Menjalankan container:**

```bash
docker-compose up
```

Lalu buka: [http://localhost:16001](http://localhost:16001)

---

### 🔧 Permission Issues?

Jalankan perintah ini jika terjadi error permission saat Odoo dijalankan:

```bash
sudo chmod -R 777 addons
sudo chmod -R 777 etc
sudo chmod -R 777 postgresql
```

---

### 🔁 Mengganti Port Odoo

Edit file `docker-compose.yml` dan ubah bagian:

```yaml
ports:
 - "16001:8069"
```

---

### 📦 Detached Mode

Jalankan container tanpa membuka terminal terus-menerus:

```bash
docker-compose up -d
```

---

### 🔄 Restart Policy (Opsional)

Atur di file `docker-compose.yml`:

```yaml
restart: always
```

Opsi lainnya:
- `no`
- `on-failure[:max-retries]`
- `always`
- `unless-stopped`

---

### 📈 Menambah Limit Watcher File (Opsional)

Untuk mencegah error saat banyak instance Odoo aktif:

```bash
if grep -qF "fs.inotify.max_user_watches" /etc/sysctl.conf; then echo $(grep -F "fs.inotify.max_user_watches" /etc/sysctl.conf); else echo "fs.inotify.max_user_watches = 524288" | sudo tee -a /etc/sysctl.conf; fi
sudo sysctl -p
```

---

## 🧩 Custom Addons

Letakkan modul kustom kamu ke dalam folder `addons/`.

---

## ⚙️ Konfigurasi & Log Odoo

- Edit konfigurasi Odoo: `etc/odoo.conf`
- Cek log Odoo: `etc/odoo-server.log`
- Ubah master password di bagian ini:

  ```ini
  [options]
  admin_passwd = minhng.info
  ```

---

## 🐳 Docker Commands

**Menjalankan Odoo:**

```bash
docker-compose up -d
```

**Restart Odoo:**

```bash
docker-compose restart
```

**Stop Odoo:**

```bash
docker-compose down
```

---

## 💬 Live Chat Support

Port `26001` disediakan khusus untuk fitur live chat (long polling).

Jika menggunakan Nginx di production, tambahkan di konfigurasi:

```nginx
location /longpolling/ {
    proxy_pass http://0.0.0.0:26001/longpolling/;
}
```

---

## 📦 docker-compose.yml Summary

- **Odoo**: versi 18
- **PostgreSQL**: versi 17

---

## 📸 Screenshots

<p align="center">
<img src="screenshots/odoo-18-welcome-screenshot.png" width="50%">
</p>

<p>
<img src="screenshots/odoo-18-apps-screenshot.png" width="100%">
</p>

<p>
<img src="screenshots/odoo-18-sales-screen.png" width="100%">
</p>

<p>
<img src="screenshots/odoo-18-product-form.png" width="100%">
</p>

---

## 🧑‍💻 Author

Forked & maintained by [rezak400](https://github.com/rezak400)  
Based on original work by [minhng92](https://github.com/minhng92)
