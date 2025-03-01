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

---

## Main Critique  

Currently, most sites still rely on the **DNS backbone**. However, it is possible to resolve them via **gateways hosted over TOR**.  

The primary goal is to create websites that can resolve **natively over the clearnet**.  
