# 🧠 Super ShopBoss Agent

A Flowise-powered AI assistant that answers questions about your infrastructure using real-time data from structured YAML files.

---

## 🔍 What It Can Do
- Answer questions like:
  - "What servers run PHP 7.4.6?"
  - "Which subnets are used for Redis?"
  - "How do I access the production MySQL bastion?"
- Understands your actual infrastructure layout
- Reads and indexes YAML files from this repo
- Uses Pinecone to store and retrieve embeddings
- Works inside Flowise (hosted on Render)

---

## 🧱 Architecture
| Component     | Stack                                      |
|---------------|---------------------------------------------|
| File Loader   | `combined.txt` in `/data/`                 |
| Embeddings    | HuggingFace (`all-MiniLM-L6-v2`)           |
| Vector DB     | Pinecone (`infra-yaml`)                    |
| Agent UI      | Flowise (via Render deployment)            |

---

## 📂 Project Structure

```
shopboss/
├── data/
│   └── combined.txt         # Flattened YAML config used for embedding
├── flowise/
│   └── super-shopboss.flow.json   # Ready-to-import agent flow
├── README.md
```

---

## 🔁 Updating Instructions

> Keep the agent up to date as your infra evolves.

### 1. Update your YAML files locally

### 2. Rebuild `combined.txt`
Run this script:

```bash
python scripts/load_yamls.py
```

Or re-export it however you're maintaining your infra docs.

### 3. Commit and push

```bash
git add data/combined.txt
git commit -m "update infra context"
git push origin main
```

The Flowise agent will automatically fetch the latest version from GitHub.

---

## 🧪 Live Testing (for team use)
- Open Flowise via [your Render URL]
- Use the Super ShopBoss Agent flow
- Ask any infra question — it will search, retrieve, and answer using context from `combined.txt`

---

## ✅ Next Steps
- Add `runbooks/` to guide provisioning, access, and recovery
- Optionally convert to multi-file vector search later
- Add Slack or CLI integration

---

Maintained by @bigredcoder
