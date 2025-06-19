## 🔧 Step-by-Step Setup for Persistent Custom Nodes

1. Create a folder on your host machine:

```bash
mkdir -p /home/ubuntu/n8n_custom_nodes
```

2. Install the custom node there manually (outside of Docker):
```bash
cd /home/ubuntu/n8n_custom_nodes
npm install n8n-nodes-discord @discordjs/rest discord.js
```
