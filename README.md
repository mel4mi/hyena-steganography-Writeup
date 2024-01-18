# Hyena CTF Writeup

Hello everyone! Today, I will guide you through the process of solving the Hyena CTF challenge. First, I downloaded the CTF file and inspected it using ExifTool.

```bash
exiftool stage.jpg
```

![Step 1](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/1.ad%C4%B1m.jpg)

Here, we discover our first flag.

Next, I decided to examine some photos using the 29a Forensic Tool, a valuable resource for steganography. I applied the Error Level Analysis filter and reduced the JPEG quality.

![Step 2](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/2.ad%C4%B1m.png)

While doing this, I noticed an encrypted message within the photo. The encryption appeared unique, prompting further investigation on the [Dcode](https://www.dcode.fr/marquage-alpha-angle) website.

![Step 3](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/3.ad%C4%B1m.png)

I documented the resulting password for future use.

To explore what's inside the photo, I used Binwalk.

```bash
binwalk stage.jpg
```

![Step 4](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/4.ad%C4%B1m.png)

Binwalk revealed hidden content in the photo. Despite initial extraction attempts failing, remembering the password allowed me to successfully extract the files using Steghide.

```bash
steghide extract -sf stage.jpg -p password
```

![Step 6](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/6.ad%C4%B1m.png)

Inside the extracted zip file were two files: `chat.txt` and `lpdf.pdf`.

```bash
cat chat.txt
```

![Step 7](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/7.ad%C4%B1m.png)

The second flag was found in the chat file. Next, I needed to crack the PDF file. The chat file suggested using John the Ripper for this.

Using `pdf2john`, I obtained the PDF's hash.

```bash
pdf2john lpdf.pdf
```

![Step 8](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/8.ad%C4%B1m.png)

I then cracked the hash using John the Ripper and a wordlist.

```bash
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

![Step 9](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/9.ad%C4%B1m.png)

The PDF password was successfully cracked.

To unlock the PDF, I used Soda PDF.

![Step 10](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/10.ad%C4%B1m.png)

After unlocking, the last flag was revealed in the PDF.

![Step 11](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/11.ad%C4%B1m.png)

Feel free to view the file at your convenience. This concludes the Hyena CTF challenge write-up.
