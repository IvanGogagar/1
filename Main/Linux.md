 Расширение для терминала китти  
`For Kitty just set cursor_trail in kitty.conf`

 Почему то у меня не работает :( 
`"$(curl -fsSL https://raw.githubusercontent.com/Snowy-Fluffy/zapret.installer/refs/heads/main/installer.sh)"`  ~~одной командой запрет~~

 Вроде на иксах так запускать с гибридной графикой приложения на нвидиа 
`env NV_PRIME_RENDER_OFFLOAD=1 GLX_VENDOR_LIBRARY_NAME=nvidia <имя_приложения>`

[[linux это кайф]]

https://github.com/JaKooLit/Hyprland-v3?tab=readme-ov-file

**source** = *~/.config/hypr/config/animations.conf*
**source** = *~/.config/hypr/config/autostart.conf*
**source** = *~/.config/hypr/config/decorations.conf*
**source** = *~/.config/hypr/config/environment.conf*
**source** = *~/.config/hypr/config/input.conf*
**source** = *~/.config/hypr/config/keybinds.conf*
**source** = *~/.config/hypr/config/monitor.conf*
**source** = *~/.config/hypr/config/variables.conf*
**source** = *~/.config/hypr/config/windowrules.conf*
**source** = *~/.config/hypr/config/user-config.conf*
**source** = *~/.config/hypr/config/defaults.conf*


1. Открой пользовательский GRUB-файл

`sudo nano /etc/grub.d/40_custom`

Добавь в конец (или замени всё этим):

`menuentry "Windows (sda2)" {`
    `set root=(hd0,1)`
    `chainloader +1`
`}`

Объяснение:

(hd0,2) — это диск 0, раздел 2 → соответствует /dev/sda2

chainloader +1 — передаёт управление загрузчику Windows



---

2. Сохрани и сделай GRUB-конфигурацию заново

`sudo grub-mkconfig -o /boot/grub/grub.cfg`


---

3. Перезагрузи и выбери Windows

`reboot`

В меню GRUB должен появиться пункт "Windows (sda2)" — выбираешь его, и должна загрузиться Windows.
