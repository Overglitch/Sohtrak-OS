# 🌌 **Sothrak-OS**  
*"Yog-Sothoth knows the gate. Yog-Sothoth is the gate. Yog-Sothoth is the key and guardian of the gate. Past, present, future, all are one in Yog-Sothoth."*  

Sothrak-OS es una configuración personalizada de **Arch Linux** optimizada para alto rendimiento y experiencia fluida con **Hyprland** en Wayland.  

---

## 💪 **Componentes Principales**  

### **🖥️ Base del Sistema**  
- **Distro:** Arch Linux 🏹 (minimalista y rolling-release)  
- **Kernel:** `linux-zen` (optimizado para baja latencia y mejor rendimiento)  
- **Gestor de arranque:** `GRUB` (soporte para dualboot)  
- **Sistema de archivos:** `Btrfs` (con snapshots y compresión opcional)  
- **Archivos clave:** `/etc/pacman.conf`, `/etc/mkinitcpio.conf`, `/etc/environment`  

### **🎨 Interfaz Gráfica (Wayland)**  
- **Compositor:** `Hyprland` 🌊 (rápido, modular y ligero)  
- **Lanzador de aplicaciones:** `fuzzel` (minimalista y nativo en Wayland)  
- **Barra de estado:** `Waybar` (altamente personalizable con JSON + CSS)  
- **Panel de notificaciones:** `Mako` (sencillo y estético)  
- **Gestor de inicio de sesión:** `SDDM` (con tema `chili-sddm`)  
- **Pantalla de bloqueo:** `Swaylock-effects` (blur y transparencias)  

### **🖥️ Terminal & Herramientas**  
- **Terminal:** `WezTerm` (rápido, GPU-accelerated, soporte Wayland)  
- **Shell:** `Fish` 🐟 (con `Starship` para un prompt moderno)  
- **Monitor del sistema:** `Btop` (potente TUI)  
- **Gestor de archivos:** `yazi` (rápido y minimalista, reemplazo de `ranger`)  
- **Editor de texto:** `Neovim` (configurado en Lua)  
- **Selector de ventanas:** `Tofi` (alternativa moderna a Rofi en Wayland)  

### **🎭 Estética y Theming**  
- **Gestor de fondos:** `Swww` (transiciones suaves en Wayland)  
- **Gestión de colores:** `Pywal` (sincroniza colores con fondo)  
- **Tipografía:** `FiraCode Nerd Font` (con ligaduras para desarrollo)  
- **Íconos:** `Papirus` (temática moderna y completa)  

### **📺 Aplicaciones y Multimedia**  
- **Navegador:** `Firefox` (con `pywalfox` para temas dinámicos)  
- **Música:** `Spotify` (con `spicetify` para personalización)  
- **Correo:** `Thunderbird`  
- **Captura de pantalla:** `Grim + Slurp` (CLI nativo en Wayland)  
- **Grabación de pantalla:** `wf-recorder` (alternativa a OBS en Wayland)  

### **⚡ Automatización y Configuración**  
- **Gestor de paquetes:** `Pacman` + `Paru` (AUR helper)  
- **Gestión de servicios:** `systemd`  
- **Sincronización de dotfiles:** `Ansible`  

---

## 🚀 **Instalación de Sothrak-OS**  

### 1️⃣ **Instalar Arch Linux con Btrfs y GRUB**  
```bash
lsblk  # Listar discos y particiones

cfdisk /dev/sda  # Crear particiones
# sda1 - 1G  -> EFI
# sda2 - 16G -> Swap
# sda3 - 60G -> Root (/)

mkfs.btrfs /dev/sda3  # Formatear partición root con Btrfs
mkswap /dev/sda2  && swapon /dev/sda2
mkfs.fat -F 32 /dev/sda1  # Formatear EFI como FAT32

mount /dev/sda3 /mnt
mount --mkdir /dev/sda1 /mnt/efi

# Instalar Arch con paquetes esenciales
pacstrap -K /mnt base base-devel linux-zen linux-firmware linux-headers grub efibootmgr networkmanager nano man-db man-pages sof-firmware

genfstab -U /mnt >> /mnt/etc/fstab
arch-chroot /mnt

ln -sf /usr/share/zoneinfo/America/Lima /etc/localtime
timedatectl set-timezone America/Lima
hwclock --systohc

# Configuración de idioma y teclado
echo "LANG=en_US.UTF-8" >> /etc/locale.conf
echo "KEYMAP=la-latin1" >> /etc/vconsole.conf
echo "glitch" >> /etc/hostname

locale-gen
mkinitcpio -P

# Configurar GRUB
grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=GRUB
grub-mkconfig -o /boot/grub/grub.cfg

exit
umount -R /mnt
poweroff
```

### 2️⃣ **Clonar y aplicar la configuración con Ansible**  
```bash
git clone https://github.com/Overglitch/Sohtrak-OS/dotfiles ~/.dotfiles
cd ~/.dotfiles
ansible-playbook setup.yml
```

### 3️⃣ **Habilitar servicios esenciales**  
```bash
systemctl enable sddm
systemctl --user enable pipewire wireplumber
```

---

## 📸 **Capturas de Pantalla**  
| ![Sothrak-OS](https://github.com/user-attachments/assets/c1360f23-3db6-4de1-866e-c9bbbf827e7c) |
|:--:|
| *Sothrak-OS* |
