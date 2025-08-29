
# Odoo 18.0 Docker Compose

**Deploy Odoo 18.0 in seconds — with support for multiple instances on the same server**

## 🚀 Quick Installation

Install [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/), here's the oneliner:
```
sudo apt update && sudo apt install -y ca-certificates curl gnupg lsb-release && curl -fsSL https://get.docker.com | sh
```


then run this command to setup the first instance at `localhost:18001` (default master password: `rezahandsome123`):

```bash
curl -s https://raw.githubusercontent.com/rezak400/odoo-docker-compose/master/run.sh | bash -s odoo-one 18001 28001
```

To create additional instances (for example at port `11018`):

```bash
curl -s https://raw.githubusercontent.com/rezak400/odoo-docker-compose/master/run.sh | bash -s odoo-two 18002 28002
```

**Parameters:**
- `odoo-one` → Odoo instance folder name
- `18001` → Odoo port
- `28001` → Live chat port

If `curl` is not installed:

```bash
sudo apt install curl
# or
sudo yum install curl
```

<p>
<img src="screenshots/odoo-18-docker-compose.gif" width="100%">
</p>

---

## 🧰 Usage

**Running the container:**

```bash
docker-compose up
```

Then open: [http://localhost:18001](http://localhost:18001)

---

### 🔧 Permission Issues?

Run this command if you get permission errors when running Odoo:

```bash
sudo chmod -R 777 addons
sudo chmod -R 777 etc
sudo chmod -R 777 postgresql
```

---

### 🔁 Changing Odoo Port

Edit the `docker-compose.yml` file and change this part:

```yaml
ports:
 - "10018:8069"
```

---

### 📦 Detached Mode

Run the container without keeping the terminal open continuously:

```bash
docker-compose up -d
```

---

### 🔄 Restart Policy (Optional)

Set in the `docker-compose.yml` file:

```yaml
restart: always
```

Other options:
- `no`
- `on-failure[:max-retries]`
- `always`
- `unless-stopped`

---

### 📈 Adding File Watcher Limit (Optional)

To prevent errors when many Odoo instances are active:

```bash
if grep -qF "fs.inotify.max_user_watches" /etc/sysctl.conf; then echo $(grep -F "fs.inotify.max_user_watches" /etc/sysctl.conf); else echo "fs.inotify.max_user_watches = 524288" | sudo tee -a /etc/sysctl.conf; fi
sudo sysctl -p
```

---

## 🧩 Custom Addons

Place your custom modules in the `custom_addons/` folder.

The custom addons are mounted to the container at `/mnt/extra-addons` and will be automatically loaded by Odoo.

---

## 🏢 Enterprise Addons

Place your enterprise modules in the `enterprise_addons/` folder.

The enterprise addons are mounted to the container at `/mnt/enterprise-addons` and will be automatically loaded by Odoo.

---

## ⚙️ Odoo Configuration & Logs

- Edit Odoo configuration: `etc/odoo.conf`
- Check Odoo logs: `etc/odoo-server.log`
- Change master password in this section:

  ```ini
  [options]
  admin_passwd = minhng.info
  ```

---

## 🐳 Docker Commands

**Running Odoo:**

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

Port `28001` is specifically provided for live chat features (long polling).

If using Nginx in production, add this to the configuration:

```nginx
location /longpolling/ {
    proxy_pass http://0.0.0.0:28001/longpolling/;
}
```

---

## 📦 docker-compose.yml Summary

- **Odoo**: version 18
- **PostgreSQL**: version 17

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
