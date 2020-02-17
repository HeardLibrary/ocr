# Assignment 2

Let's make sure Tesseract up and running for everyone, so feel free to reach out directly if you are not getting it to work after trying the tips below.

Once you have it, try it out by following the instructions at the end.

---
## Installation for Mac Users

#### Getting to know the command line

If you need some more practice with using the command line, please check out this tutorial for using the Bash command line on Macs:  https://programminghistorian.org/en/lessons/intro-to-bash.

#### Install Homebrew
Homebrew is a package manager for Macs. It helps you install extra things that don't come pre-installed. Go to the homepage: [https://brew.sh/](https://brew.sh/) and cut and paste the long command into your Terminal.

#### Install xpdf

The xpdf tool is a PDF viewer that will help us convert PDFs to image files to be read in Tesseract. Install it by typing this in the command line:  ```brew install xpdf```

#### Install ImageMagick

ImageMagick is a useful image manipulation tool that helps us convert file formats like TIFF to JPG or to deskew or fix contrast. This helps our image files to be read in Tesseract. Install it by typing this in the command line:  ```brew install ImageMagick```

#### Install Ghostscript
Ghostscript is another image manipulation tool that is especially useful when reading and converting PDFs. Install it by typing this in the command line:  ```brew install ghostscript```

#### Install Tesseract

Install it by typing this in the command line:  ```brew install tesseract-lang```

---
## Installation for PC Users

#### Getting to know the command line

If you need some more practice with using the command line, please check out this tutorial for using PowerShell https://programminghistorian.org/en/lessons/intro-to-powershell. You can stop when you reach the 'Doing More' section.

#### Install AppGet
AppGet is a package manager for Windows. It helps you install extra things that don't come pre-installed. Go to the homepage: [https://appget.net/](https://appget.net/) and hit the download button and follow instructions.

#### Install ImageMagick

ImageMagick is a useful image manipulation tool that helps us convert file formats like TIFF to JPG or to deskew or fix contrast. This helps our image files to be read in Tesseract. Install it by typing this in the command line:  ```appget install ImageMagick```

#### Install Ghostscript
Ghostscript is another image manipulation tool that is especially useful when reading and converting PDFs. Install it by typing this in the command line:  ```appget install ghostscript```

#### Install Tesseract

Go here https://github.com/UB-Mannheim/tesseract/wiki and select the 64-bit version.


This will download an .exe file that will add Tesseract to your Program Files directory. You will need to include the full file path when invoking tesseract from the command line. What does that mean?  If the Tesseract instructions say to do this:

```tesseract [input image filename] [output txt filename]```

> Warning: You will need to do this if you are using Windows PowerShell:

```& "C:\Program Files\Tesseract-OCR\tesseract” [input image filename] [output txt filename]```

You will need to put the full path in quotation marks because the folder name has a space. [PS, this is why it's a very bad idea to have folder or file names with a space in them. Use _underscore_ instead.]

---

## Using Tesseract

#### Converting from PDFs
First thing to remember is that Tesseract only works on image files (.png, .jpg, or tiff all work). It won’t work on a pdf.

So if you have a pdf, you need to convert it to an image file. You can use an online converter, or you can use the ImageMagick package we just downloaded.  

Just type in the command line: ```convert inputfile.pdf outputfile.png```

Your output file can be .tiff, .png, or .jpg, but for OCR, let's use .png or .

This only works if your pdf is one page. If you have a multipage pdf, you'll need to do this instead:  ```convert inputfile.pdf output-%d.png```. This will give you multiple tiff files with the names in the format of ```output-0.png```, ```output-1.png```, etc.

#### Or grab an image file

You can take a picture on your phone or grab an image from the web using the  ```wget``` function on  the command line. Easy to remember if you think web-get. ```wget [full image url]```

**Example**

```wget –O example1.jpg http://www.earlyprintedbooks.com/wp-content/uploads/10397998-maximum-768x1198.jpg```

In this example, the -O (that's a capital letter O not a zero) is a flag that tells the computer that the next word is going to be an output file name. I added an output file name ```example1.jpg``` so that the file had a more meaningful file name than ```10397998-maximum-768x1198.jpg```.

The website [http://www.earlyprintedbooks.com/](http://www.earlyprintedbooks.com/) has some examples of texts that will be tricky for Tesseract.

You can also find examples at HathiTrust, like this one: [https://babel.hathitrust.org/cgi/pt?id=nyp.33433074972401&view=1up&seq=388](https://babel.hathitrust.org/cgi/pt?id=nyp.33433074972401&view=1up&seq=388).

#### Run Tesseract

Remember the folder where you put your images.

To run Tesseract, you just write this in the command line: ```tesseract inputfilename outputfile.txt```

Example:  ```tesseract example1.png example1.txt```

> See Windows instructions above for Windows variation.

If you have multiple images in your folder, you can iterate through the images like this:

```for i in *.png; do tesseract $i [insert_output_folder_name_here]/$i; done```

This command generates a .txt file for each .png image and places it into a new output folder with the same name as the image.
