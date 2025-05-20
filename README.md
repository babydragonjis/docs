# 🐉 Baby Dragon Architecture Docs

> A fully operational, **\$0-cost** architecture powering Baby Dragon and [Indonesiaku](https://www.indonesiaku.com).

![Architecture Diagram](Indonesiaku.com%20Network%20Architecture.png)
[View in Figma](https://www.figma.com/board/Z5a7dxo8xd5znl1pcx5upl/Indonesiaku.com-Network-Architecture?node-id=0-1&t=ETCHrOWELcw7Ohoy-1)

---

## 📌 Overview

**Baby Dragon** serves two primary functions:

1. **GPU workspace** for students — accessible via JupyterLab for compute-heavy projects (e.g., ML).
2. **Model inference server** for [Indonesiaku.com](https://www.indonesiaku.com) — powering the **NusaMT-7B** translation model.

---

## 🔗 References

* [Indonesiaku GitHub Repository](https://github.com/williammtan/indonesiaku)
* [keys.env](https://drive.google.com/file/d/1JCQsiRQxCU_GCqp9mrtfm7pU5-ZNH7da/view?usp=sharing)
* [Access Form Responder](https://docs.google.com/forms/d/e/1FAIpQLSfvlJqrv6Em6VPw-1pI_ilwl0HDb3-UWCaZAiy1WfKIlqLYug/viewform?usp=header) / [Access Form Editing](https://docs.google.com/forms/d/1qJTUD0DSu1W9u21dESVB9UI2AymGifoX1FLiQkf1zek/edit)
* [Email Template](https://github.com/babydragon/docs)

---

## 🔐 Access Instructions

### Users

* **Indonesiaku Web App**: [https://www.indonesiaku.com](https://www.indonesiaku.com)
* **JupyterHub on Baby Dragon**

  * Within @JIS Network:
    `http://babydragon.jisedu.or.id:8080` or `172.16.100.13:8080`
  * Outside @JIS Network:
    `https://www.babydragon.indonesiaku.com`

### Admins

* **Inside @JIS Network**
  SSH Access:

  ```bash
  ssh baby@172.16.100.13
  # or
  ssh baby@babydragon.jisedu.or.id
  ```

  Use credentials: `$BABYDRAGON_USERNAME` / `$BABYDRAGON_PASSWORD`

* **Outside @JIS Network**
  Visit: `https://www.babydragon.indonesiaku.com`
  Log in with admin credentials → Start a Jupyter terminal session with `sudo` access.

---

## Admin Worflow
1. User submits a form.
2. Review the request.
3. Create a user by logging into jupyterhub: go to File > Hub Control Panel > Admin > Add User. The username is up to you.
4. Set the password of this user by logging in as the assigned username and setting the new password 
    * Generate a random generated strong password ([Password Generator](https://www.lastpass.com/features/password-generator))
5. Send the confirmation email using the [Email Template](https://github.com/babydragon/docs).

---

## 🔧 Services & Integrations

> **Note:** All credentials are stored in `keys.env` and referenced like `${VARIABLE}` (e.g. `$CLOUDFLARE_EMAIL`).
> You can also sync via the linked Google account for autofill access.

---

### 💻 JupyterHub

* Powered by [The Littlest JupyterHub](https://tljh.jupyter.org/en/latest/)
* Admin users can manage sessions and user permissions (File > Hub Control Panel > Admin)

---

### 🌐 Netlify

* Hosts the [Indonesiaku Next.js app](https://www.indonesiaku.com).
* Auto-deploys on push to `main` branch of `williammtan/indonesiaku`.

**Credentials**: `$NETLIFY_EMAIL` / `$NETLIFY_PASSWORD`

---

### 🗄️ Supabase

* Manages DB + authentication for Indonesiaku.com.
* Connected via `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_ANON_KEY`.

*Note: Auth is currently under revision.*

**Credentials**: `$SUPABASE_EMAIL` / `$SUPABASE_PASSWORD`

---

### 🛡️ Cloudflare

* Manages:

  1. DNS for `indonesiaku.com`
  2. Zero Trust Tunneling → `babydragon.indonesiaku.com` → JupyterHub

![Cloudflare DNS Setup](./Cloudflare%20DNS%20Setup.png)

**Credentials**: `$CLOUDFLARE_EMAIL` / `$CLOUDFLARE_PASSWORD`

---

### 🌉 Ngrok

* Secure tunneling for model inference (`NLLB_ENDPOINT`)
* Uses [Basic Auth](https://ngrok.com/docs/traffic-policy/actions/basic-auth/)

**Credentials**:

* URL: stored in `$NGROK_ENDPOINT`
* Username/Password: `$NGROK_TUNNEL_USERNAME` / `$NGROK_TUNNEL_PASSWORD`

---

### 🧬 Google Account

**Credentials**: `$GOOGLE_EMAIL` / `$GOOGLE_PASSWORD`

---

### 🐙 GitHub

* Primary repo: `williammtan/indonesiaku`

**Credentials**: `$GITHUB_EMAIL` / `$GITHUB_PASSWORD`

---

## ✅ To-Do List

* [x] Enable secure JupyterHub via Cloudflare Zero Trust
* [x] Proxy `babydragon.indonesiaku.com` via ngrok
* [x] Migrate frontend to Netlify
* [x] Write internal ops + secrets doc (logins, flow, etc.)
* [x] Build access request form
* [x] Automate access approval emails
* [ ] Shut down all GCP services → reach \$0 infra

---

## 🧪 Potential Add-Ons

* [ ] RStudio Server
* [ ] Remote Blender Rendering
  *(Ref: [Reddit Thread](https://www.reddit.com/r/blender/comments/1csvg6l/how_can_i_render_on_a_server/))*
