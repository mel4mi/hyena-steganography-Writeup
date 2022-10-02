# hyena-steganography-Writeup


Hello everyone today we will look up hyena ctf. First i download the ctf file and I put it in exiftool.


```
  exiftool file.jpg
  ```
  
  ![1.adım](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/1.ad%C4%B1m.jpg)
  
  
  here is our first flag.
  
  Then we need to examine some photos.I prefer the 29a[Forensic-tool](https://29a.ch/photo-forensics/) site for steganography. There are lots of useful effects in it.
  
  ![2.adım](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/2.ad%C4%B1m.png)
  
  
  I swtich the filter Error Level Analysis and i lower the jpeg quality.
  
  ![3.adım](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/3.ad%C4%B1m.png)
  
  and i found some encrypted message in photo
  
  this encryption looks different from other encryption methods. so I started doing research on the [Dcode](https://www.dcode.fr/chiffres-symboles) site.
  
  
  [that encryption](https://www.dcode.fr/marquage-alpha-angle)
  
  
  
  ![4.adım](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/4.ad%C4%B1m.png)
  
  I make a note of the resulting password for future use.
  
  and I want to see what's inside the photo,
  
  so i use binwalk
  
  ```
  binwalk stage.jpg
  ```

![5.adım](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/5.ad%C4%B1m.png)

there is something hidden in the photo. I tried to extract it with binwalk but the files were corrupt.
then I remembered the password which i found and using that password I extracted the files with steghide

```
steghide extract -sf stage.jpg -p password
```
![6.adım](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/6.ad%C4%B1m.png)

i found a zip file and unzip them
after the unzip i found 2 file:
1-chat.txt
2-lpdf.pdf

```
cat chat.txt
```
![7.adım](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/7.ad%C4%B1m.png)
there is the second flag here

and i have to crack pdf file. In the chat file it told us that we should use john for the cracking pdf
first i use pdf2john to get pdf's hash
```
pdf2john lpdf.pdf
```
![8.adım](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/8.ad%C4%B1m.png)

and note it as hash.txt

for cracking hash :

```
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

![9.adım](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/9.ad%C4%B1m.png)

We found the pdf password

You can view the file wherever you want.
but i want to unlock password. So i used [Sodapdf](https://www.sodapdf.com/unlock-pdf/)

![10.adım](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/10.ad%C4%B1m.png)

after the unlock i found the last flag in pdf

![11.adım](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/11.ad%C4%B1m.png)
