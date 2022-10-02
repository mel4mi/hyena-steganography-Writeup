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
  
  '''
  binwalk filename.jpg
  ''''

![5.adım](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/5.ad%C4%B1m.png)

there is something hidden in the photo. I tried to extract it with binwalk but the files were corrupt.
then I remembered the password which i found and using that password I extracted the files with steghide

'''
steghide extract -sf stage.jpg -p password
'''
![6.adım](https://github.com/mel4mi/hyena-steganography-Writeup/blob/main/6.ad%C4%B1m.png)
