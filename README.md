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
