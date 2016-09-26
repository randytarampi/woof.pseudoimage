#ʕつ◕ᴥ◕ʔつ 📷 → Your application's pseudolocales' image folders

[![Build Status](https://img.shields.io/travis/randytarampi/pseudoimage.woof.svg?style=flat-square)](https://travis-ci.org/randytarampi/pseudoimage.woof) [![Coverage Status](https://img.shields.io/coveralls/randytarampi/pseudoimage.woof.svg?style=flat-square)](https://coveralls.io/github/randytarampi/pseudoimage.woof?branch=master) [![Dependency Status](https://img.shields.io/david/randytarampi/pseudoimage.woof.svg?style=flat-square)](https://david-dm.org/randytarampi/pseudoimage.woof.svg) [![Backlog](https://img.shields.io/waffle/label/randytarampi/pseudoimage.woof/Backlog.svg?style=flat-square)](http://waffle.io/randytarampi/pseudoimage.woof) [![Ready](https://img.shields.io/waffle/label/randytarampi/pseudoimage.woof/Ready.svg?style=flat-square)](http://waffle.io/randytarampi/pseudoimage.woof) [![In Progress](https://img.shields.io/waffle/label/randytarampi/pseudoimage.woof/In%20Progress.svg?style=flat-square)](http://waffle.io/randytarampi/pseudoimage.woof)

This uses [lwip](https://github.com/EyalAr/lwip) to modify your images to create a fake, which gets saved somewhere.

##Usage

```javascript
let Pseudoimage = require("pseudoimage.woof");
let sourceDirectory = "/Users/randy.tarampi/Desktop/images";
let destinationDirectory = "/Users/randy.tarampi/Desktop/fakeImages";
let expect = require("chai").expect;

let pseudoimage = new Pseudoimage(sourceDirectory, destinationDirectory);
pseudoimage.generatePseudoImages();

// There should be a copy for each supported image in `sourceDirectory` in `destinationDirectory`
let files = fs.readdirSync(sourceDirectory);
files.map((file) => {
	openImage(file)
		.then((image) => {
			expect(images[0].width()).to.eql(images[1].width());
			expect(images[0].height()).to.eql(images[1].height());
		})
		.catch((error) => {
			console.error(error); // Shouldn't see any errors
		});
});

function openImage(imagePath) {
	return new Promise((resolve, reject) => {
		lwip.open(imagePath, (error, image) => {
			if (error) {
				reject(error);
				return;
			}
			resolve(image);
		})
	});
}
```
