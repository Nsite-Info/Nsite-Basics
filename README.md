# Nsite Basics

## What is an Nsite?

The concept of **Nsite** was born during the second cohort of [Sovereign Engineering](https://sovereignengineering.io/). It utilizes **Nostr** and **Blossom servers** to deploy static websites and clients.  

Nsite makes it easy to deploy websites to multiple hosts in a **non-KYC** way, allowing payments via Bitcoin while ensuring redundancy is built-in.  

Another key feature is **Nsite Gateways**:  
Even if your website is blocked on one domain, it remains accessible through different gateways because these sites resolve via **Nostr**.

### Summary:
- **Censorship Resistance** through redundancy  
- **Non-KYC Hosting Solutions**  
- **Multi-Gateway Resolution**  
- **No Need for GitHub** – Store, edit, and deploy your website directly to **Blossom servers**  

---

## Where Do I Get Started?  

We have compiled a list of tools to help you deploy your website. You can find them here:  
🔗 [Nsite Tools](https://nsite.info/tools)  

If you're experiencing deployment issues, visit:  
🔗 [Nsite Debug](https://nsite.info/debug)  

---

## Technical Implementation  

1. **Generate a Nostr Key Pair**  
   - The **private key** is used to upload your website’s public folder to one or multiple **Blossom servers** (e.g., `BUD-03`, `10063`).  

2. **Upload & Broadcast**  
   - Once uploaded, **notes** (`Kind: 34128`) containing the **filename** and **file hash** are broadcasted to your **Nostr Outbox Relays** (`NIP 65`, `Kind: 10002`).  

3. **No More GitHub Needed**  
   - Since the website’s code is stored on **Blossom servers**, there’s no need for GitHub.  
   - You can **edit, deploy, and store** your website **directly on Blossom servers**, eliminating dependency on centralized version control platforms.  

---

## Main Critique  

Currently, most sites still rely on the **DNS backbone**. However, it is possible to resolve them via **gateways hosted over TOR**.  

The primary goal is to create websites that can resolve **natively over the clearnet**.  

# Nsite Deploy Instructions  
**~ 30 min guide**  

## Introduction  
The Nsite setup consists of two components/repositories:  
1. **The Nsite** – Contains the GitHub action deploy script.  
2. **The Nsite Gateway** – Resolves the site through its `npub` and connects the domain.  

---

## Prerequisites  
- GitHub Account  
- `Nsec` in Hex format  
- Domain name *(optional)*  
- Cloudflare or Vercel Account *(GitHub Pages may also work)*  

---

## 1) Nsite Repository  

### 1.1) Clone the Repository  
Go to the [Nsite-Upload GitHub Repo](https://github.com/Nsite-Info/Nsite-Upload) and select **Use this template** to clone it.  

![Clone Repo](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/1.png)

### 1.2) Set Your Nsec Hex as an Action Secret  
1. Navigate to **Settings** in your repo.  
2. Under **Secrets and variables**, select **Actions**.  

![Nav Secrets](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/2.png)

3. Click **Add a New Repository Secret**.  

![Add Secret](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/3.png)

4. Name it: `NSITE_KEY`  Set the secret as your `Nsec` in hex format.  

![Add Name - Hex Key](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/4.png)


### 1.3) Redeploy the Action  
Once the secret is set:  
1. Go to the **Actions** tab in the repo.  

![Actions Menu](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/5.png)

2. Because the deployment failed, click **Re-run jobs** to redeploy with the newly set `Nsec`.  

![Retrigger Action](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/6.png)

![Running Action](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/7.png)

### 1.4) 🎉 Successfully Deployed! 🎉  
After deployment, the `npx` command will show the deployment details, including the live URL on **Nsite.lol Gateway**.  

![Succes Message](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/8.png)

- Any changes made to `index.html` will be deployed automatically when pushed.  

---

### 1.5) FAQ & Debugging  

#### **Q: My Deployment Failed**  
You might not have set any Blossom servers for your **BUD-03 List**.  
1. Visit [Nsite Debug](https://nsite.info/debug), enter your `npub`, and check for missing configurations.  
2. Set your Blossom Server List via [Bouquet](https://bouquet.slidestr.net).  

Alternatively, try deploying locally:  
1. Download the repo to your local machine.  
2. Install [Node.js](https://nodejs.org/en).  
3. Set your `Nsec` in `.nsite/project.json`. *(Modify other settings if needed)*  
4. Run in the terminal from the root directory:  

   ```sh
   npx nsite-cli upload www
   ```  

#### **Q: My Changes Are Not Visible**  
- **Nsite.lol has caching**, so updates may not appear immediately.  
- **Try Nsite.cloud**, which does not have caching and should reflect updates immediately. *(Note: Nsite.cloud only supports simple single-page HTML sites.)*  
- **The Blossom server might not serve the blob via public access.**  

---

## 2) Gateway Repository  

There are several ways to connect a domain, ordered from easiest to hardest:  

### 2.0) Redirect to Nsite.lol *(Easiest & Recommended)*  
Simply redirect your domain to:  

```
https://<your-npub>.nsite.lol
```

### 2.1) Not Resolving Over Nostr *(Alternative Fast Loading Method)*  
This is a workaround since the repo contains the `index.html` file.  
- On **GitHub Pages**, set the `www` folder as the website root.  
- This method loads faster but does not resolve over Nostr.  

### 2.2) Hosting Your Own Nsite Gateway *(Advanced & Slower)*  

#### **2.2.1) Clone the Gateway Repository**  
Go to the [Nsite-Gateway GitHub Repo](https://github.com/Nsite-Info/Nsite-Gateway) and select **Use this template** to clone it.  

![Clone Repo](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/1.png)

#### **2.2.2) Deploy on Cloudflare or Vercel** *(Cloudflare Example Below)*  
1. Log in to your **Cloudflare** or **Vercel** account.  
2. Navigate to **Workers & Pages** in the left menu.  

![Workers & Pages ](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/9.png)

3. Click **Create** in the Worker or Page modal.  

![Click create](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/10.png)

4. Select **Pages** and connect the cloned Gateway repo via Git.  

![Select Pages](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/11.png)

5. Select the gateway repo and start the setup.  

![Select Github Repo](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/12.png)

6. Choose **Nuxt.js** as the framework preset, then **Save & Deploy**.  

![Select Nuxt Framework](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/13.png)

*⏳ This may take a few minutes to fully propagate, even when deployed it might take a couple minutes*  

![Cloudflare Deployed](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/14.png)

When you visit the newly deployed page it might take a little bit for cloudflare to display but you should be greeted with this black page.

![Empty Gateway](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/15.png)

#### **2.2.3) Configure npub in Your Repo**  
1. In your cloned **GitHub repo**, open the required config file.  
2. Click the **pencil icon** to edit.  

![Config Gateway](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/16.png)

3. Replace the `npub` value with yours, set gateway to false and singlesite to true.  

![Clone Repo](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/16.png)

4. Commit the changes and redeploy, should look like this but also with your npub filled in.

![Clone Repo](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/17.png)  

#### **2.2.4) Add a Custom Domain**  
- Both **Cloudflare** & **Vercel** will prompt you to set your domain’s **NameServers**.  
- Once propagated, you can attach the domain to the project.  

![Clone Repo](https://raw.githubusercontent.com/Nsite-Info/Nsite-Basics/refs/heads/main/images/18.png)

---

🚀 **You’re now set up with Nsite!** 🚀  
Your Nsite should be accessible via the gateway and any connected custom domain.


