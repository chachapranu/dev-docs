## ⚙️ Step 1: Install NVM on WSL2

WSL2 acts like a Linux system, so treat it as such:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

Then activate NVM by adding this to your shell config:

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
```

> For Bash: Edit `~/.bashrc`  
> For Zsh: Edit `~/.zshrc`

Finally, reload your shell:

```bash
source ~/.bashrc   # or ~/.zshrc depending on what you're using
```

---

## 📥 Step 2: Install Node.js via NVM

Once NVM is working:

```bash
nvm ls-remote              # List available versions
nvm install 18.17.0        # Or any version you want
nvm use 18.17.0            # Sets the active version
nvm alias default 18.17.0  # Makes it default every time
```

Check your setup:

```bash
node -v   # Node version
npm -v    # npm version
```

> Everything stays inside WSL2 — independent of Windows-native Node installations

---

## 📦 Step 3: Use npm in Your Projects

Inside your project folder:

```bash
mkdir my-node-app
cd my-node-app
npm init -y
```

Install packages:

```bash
npm install express
```

Create a file like `index.js`:

```js
const express = require('express');
const app = express();
app.get('/', (req, res) => res.send('Hello from WSL2!'));
app.listen(3000, () => console.log('Server running on port 3000'));
```

Run it:

```bash
node index.js
```

Then visit `http://localhost:3000` from your Windows browser — WSL2 ports are forwarded!

---

## 🔄 Useful Extras

- To list installed Node versions:
```bash
nvm ls
```

- To update npm globally:
```bash
npm install -g npm
```

- To uninstall a Node version:
```bash
nvm uninstall 18.17.0
```

---

Would you like me to help you format this into a polished tutorial write-up next? I can include friendly headings, clear code blocks, and comments to guide learners step by step.
