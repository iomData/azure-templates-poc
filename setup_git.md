**Let’s unlock Git with SSH keys! 🗝️**
Below you’ll find step-by-step instructions—in English y español—para generar tu par de llaves SSH, agregarla al agente y configurar un repositorio Git por SSH.

---

## 🔐 English: Configure SSH Key & Initialize Git

1. **Check for existing SSH keys**

   ```bash
   ls ~/.ssh/id_*.pub
   ```

   If you see files like `id_rsa.pub` or `id_ed25519.pub`, you’ve already got keys; you can skip to step 3 (or back them up and regenerate).

2. **Generate a new SSH key**
   Use Ed25519 (more secure & faster):

   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```

   * When prompted, accept the default file location (`~/.ssh/id_ed25519`).
   * Enter a passphrase (highly recommended) or leave empty for no passphrase (less secure).

3. **Start the ssh-agent & add your key**

   ```bash
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_ed25519
   ```

   This “agent” remembers your unlocked key so you don’t type your passphrase every time.

4. **Copy your public key to the clipboard**

   * **macOS / Linux**:

     ```bash
     cat ~/.ssh/id_ed25519.pub | pbcopy     # macOS
     cat ~/.ssh/id_ed25519.pub | xclip -sel clip  # Linux with xclip
     ```
   * **Windows (Git Bash)**:

     ```bash
     cat ~/.ssh/id_ed25519.pub | clip
     ```

5. **Add the key to your Git host**

   * **GitHub**: Settings → SSH and GPG keys → New SSH key → paste → Save.
   * **GitLab**: User Settings → SSH Keys → Add key → paste → Add key.
   * **Bitbucket**: Personal Settings → SSH Keys → Add key → paste → Add key.

6. **Test the connection**

   ```bash
   ssh -T git@github.com
   ```

   You should see:

   > “Hi username! You’ve successfully authenticated…”

7. **Initialize & connect your repo**

   ```bash
   mkdir my-project && cd my-project
   git init
   git remote add origin git@github.com:username/my-project.git
   git add .
   git commit -m "Initial commit"
   git push -u origin main
   ```

   Voilà! Your repo is live over SSH—no passwords, just pure key magic.

---

## 🔐 Español: Configurar llave SSH e iniciar Git

1. **Verifica si ya tienes llaves SSH**

   ```bash
   ls ~/.ssh/id_*.pub
   ```

   Si aparecen `id_rsa.pub` o `id_ed25519.pub`, ya tienes llaves; puedes ir al paso 3 (o respaldarlas y regenerar).

2. **Genera una nueva llave SSH**
   Con Ed25519 (más segura y rápida):

   ```bash
   ssh-keygen -t ed25519 -C "tu_email@ejemplo.com"
   ```

   * Al pedir ruta, acepta la ubicación por defecto (`~/.ssh/id_ed25519`).
   * Ingresa una frase de paso (recomendado) o déjalo vacío para no usar frase (menos seguro).

3. **Inicia el ssh-agent y agrega tu llave**

   ```bash
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_ed25519
   ```

   El agente “recuerda” tu llave desbloqueada para no pedirte frase cada vez.

4. **Copia tu llave pública al portapapeles**

   * **macOS / Linux**:

     ```bash
     cat ~/.ssh/id_ed25519.pub | pbcopy     # macOS
     cat ~/.ssh/id_ed25519.pub | xclip -sel clip  # Linux con xclip
     ```
   * **Windows (Git Bash)**:

     ```bash
     cat ~/.ssh/id_ed25519.pub | clip
     ```

5. **Agrega la llave a tu servicio Git**

   * **GitHub**: Configuración → SSH and GPG keys → New SSH key → pega → Guardar.
   * **GitLab**: Configuración de usuario → SSH Keys → Add key → pega → Add key.
   * **Bitbucket**: Configuración personal → SSH Keys → Add key → pega → Add key.

6. **Prueba la conexión**

   ```bash
   ssh -T git@github.com
   ```

   Deberías ver:

   > “Hi username! You’ve successfully authenticated…”

7. **Inicia tu repositorio y conéctalo**

   ```bash
   mkdir mi-proyecto && cd mi-proyecto
   git init
   git remote add origin git@github.com:usuario/mi-proyecto.git
   git add .
   git commit -m "Initial commit"
   git push -u origin main
   ```

   ¡Listo! Tu repo corriendo con SSH—sin contraseñas, solo la magia de las llaves.

---

💡 **Tip / Consejo**: Si cambias de clave o de máquina, repite solo los pasos 2–5 para mantener la puerta siempre abierta.
