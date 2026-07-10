# Dotfiles - Arch Linux + Hyprland

Configurações minimalistas de sistema e ferramentas de desenvolvimento.

---

## Como fazer o Backup (Atualizar este repositório)

Sempre que eu fizer alterações visuais ou modificar arquivos na minha pasta .config, posso atualizar este repositório com os comandos abaixo:

<br><br>

### 1. Sincroniza as configurações locais para a pasta do backup
rsync -a --exclude='.git' ~/.config/{hypr,waybar,alacritty,nvim,yazi,starship,fastfetch} ~/dotfiles/.config/

### 2. Atualiza a lista de pacotes explícitos do sistema
pacman -Qe | awk '{print $1}' > ~/dotfiles/pacman-basics.txt

### 3. Envia as alterações para o GitHub
```bash
cd ~/dotfiles
git add .
git commit -m "update: atualizando minhas configurações"
git push origin main
```

---

## Como Restaurar em uma Máquina Nova (Recovery)

Se eu formatar o PC, após fazer a instalação básica do Arch a restauração do meu setup é feita em 3 passos:

### 1. Clonar este repositório
```bash
cd ~
git clone git@github.com:marcelotaparelli/arch-hyprland-backup.git dotfiles
```
---------------

### 2. Instalar todos os programas de uma vez
```bash
sudo pacman -S --needed $(cat ~/dotfiles/pacotes_arch.txt)
```
---------------

### 3. Sincronizar as configurações para a pasta do sistema
#### Cria a pasta .config do sistema se ela não existir
```bash
mkdir -p ~/.config
```
#### Copia tudo de volta do backup para o computador
```bash
rsync -a ~/dotfiles/.config/ ~/.config/
```
----------------

Feito isso, basta reiniciar o sistema para o visual completo voltar a funcionar exatamente como estava antes.
