## Jsteg is a package for hiding data inside JPEG files with a technique known as steganography. This is accomplished by copying each bit of the data into the least-significant bits (LSB) of the image. The amount of data that can be hidden depends on the file size of the jpeg; it takes about 10-14 bytes of jpeg to store each byte of the hidden data.

## Installation of jsteg-

`sudo wget -O /usr/bin/jsteg https://github.com/lukechampine/jsteg/releases/download/v0.1.0/jsteg-linux-amd64`

![image](https://github.com/ananthan05/Steganography/assets/140697378/f12e3127-9642-4a3e-a3da-00ea5d28bc8c)

`sudo chmod +x /usr/bin/jsteg`

`sudo wget -O /usr/bin/slink https://github.com/lukechampine/jsteg/releases/download/v0.2.0/slink-linux-amd64`

![image](https://github.com/ananthan05/Steganography/assets/140697378/02e8bf3d-1857-4c76-b2fa-01898079b629)

`chmod +x /usr/bin/slink`

![image](https://github.com/ananthan05/Steganography/assets/140697378/5a07b9d4-5be9-4c85-845d-d2459c7360c3)

Download an image of any format and store it in the current directory `pngtree.jpg`

And Create a sample txt file which contains the secret message which is to be embeded with the image.

![image](https://github.com/ananthan05/Steganography/assets/140697378/7becfece-5790-4571-8239-e1b54560fb8b)

Usage-

Jsteg tool can be initialised by typing the following command.

`jsteg`

![image](https://github.com/ananthan05/Steganography/assets/140697378/06097512-3c6a-4316-825e-c62c7c164db0)


### Commands to embed a file in the JPEG image is as follows.


`jsteg hide <in.jpg> <secret file name> <out.jpg>`


![image](https://github.com/ananthan05/Steganography/assets/140697378/be5035e6-2413-4578-a87d-7834594a18ea)

where in.jpg is our original file, secret file name is the name of text file and out.jpg is name of modified image file

### Revealing data

The syntax for revealing data is as follows.

 `jsteg reveal <in.jpg> <output file name>`

 ![image](https://github.com/ananthan05/Steganography/assets/140697378/f874bfaa-5d00-4e73-898b-8df325fa0f85)

 successfully decoded.
 

