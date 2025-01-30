## 🔑 **Generar y agregar una clave SSH en GitHub desde Windows**  

---

### ✅ **Paso 1: Verificar si ya tienes una clave SSH**  
Antes de generar una nueva clave, revisa si ya tienes una. Para hacerlo:  

1. Abre **PowerShell** o **Git Bash**.  
2. Escribe el siguiente comando y presiona **Enter**:  

   ```bash
   ls ~/.ssh
   ```
3. Si ves archivos como `id_rsa` y `id_rsa.pub`, significa que ya tienes una clave SSH.  

   - Si quieres usar esta clave, ve al **Paso 4**.  
   - Si no tienes una clave o quieres crear una nueva, sigue al **Paso 2**.  

---

### 🔑 **Paso 2: Generar una nueva clave SSH**  
Si no tienes una clave SSH o quieres una nueva, sigue estos pasos:  

1. En **PowerShell** o **Git Bash**, escribe:  

   ```bash
   ssh-keygen -t ed25519 -C "tu-correo@ejemplo.com"
   ```

   - Reemplaza `"tu-correo@ejemplo.com"` con tu correo de GitHub.  
   - Si tu sistema no admite `ed25519`, usa `rsa`:  

     ```bash
     ssh-keygen -t rsa -b 4096 -C "tu-correo@ejemplo.com"
     ```

2. Presiona **Enter** cuando te pregunte dónde guardar la clave (usará la ubicación predeterminada `C:\Users\TU_USUARIO\.ssh\id_ed25519`).  
3. Puedes establecer una **contraseña** para mayor seguridad o dejarlo en blanco y presionar **Enter**.  

---

### 📂 **Paso 3: Agregar la clave SSH al agente SSH**  
1. Inicia el agente SSH escribiendo en **PowerShell** o **Git Bash**:  

   ```bash
   eval $(ssh-agent -s)
   ```

2. Agrega la clave privada al agente:  

   ```bash
   ssh-add ~/.ssh/id_ed25519
   ```

   - Si usaste `rsa`, reemplaza `id_ed25519` por `id_rsa`.  
   - Si ves un error como **"Could not open a connection to your authentication agent"**, inicia el servicio manualmente:  

     ```bash
     Start-Service ssh-agent
     ```

     Luego, repite el comando `ssh-add`.  

---

### 📋 **Paso 4: Copiar la clave pública**  
Para copiar la clave pública y agregarla a GitHub:  

1. Ejecuta en **PowerShell** o **Git Bash**:  

   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```

   - Si usaste `rsa`, cambia `id_ed25519.pub` por `id_rsa.pub`.  

2. **Copia el contenido completo** de la clave pública que aparece en pantalla.  

---

### 🛠️ **Paso 5: Agregar la clave a GitHub**  
1. Ve a [GitHub → Configuración SSH](https://github.com/settings/keys).  
2. Haz clic en **New SSH Key**.  
3. Pon un nombre en "Title" (ejemplo: "Mi PC personal").  
4. Pega la clave pública copiada en "Key".  
5. Haz clic en **Add SSH Key**.  

---

### 🏗 **Paso 6: Probar la conexión con GitHub**  
Para verificar que todo funciona correctamente:  

```bash
ssh -T git@github.com
```

Si todo está bien, verás un mensaje como:  

```bash
Hi TU_USUARIO! You've successfully authenticated, but GitHub does not provide shell access.
```

¡Eso significa que tu clave SSH está funcionando! 🎉  

---

### 🚀 **Paso 7: Configurar Git para usar SSH (Opcional)**  
Si quieres que Git use SSH en lugar de HTTPS para clonar repositorios, puedes configurar tu usuario globalmente:  

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu-correo@ejemplo.com"
```

Y al clonar un repositorio, usa la URL SSH en lugar de la HTTPS:  

```bash
git clone git@github.com:usuario/repo.git
```

---

## 🎯 **Resumen rápido**  
✅ **Verificar si tienes una clave SSH:** `ls ~/.ssh`  
✅ **Generar una clave SSH:** `ssh-keygen -t ed25519 -C "tu-correo@ejemplo.com"`  
✅ **Agregar la clave al agente SSH:** `ssh-add ~/.ssh/id_ed25519`  
✅ **Copiar la clave pública:** `cat ~/.ssh/id_ed25519.pub`  
✅ **Agregar la clave a GitHub:** [GitHub SSH Keys](https://github.com/settings/keys)  
✅ **Probar la conexión:** `ssh -T git@github.com`  

Ahora ya puedes trabajar con GitHub de forma segura usando SSH en Windows. 🚀🔐
