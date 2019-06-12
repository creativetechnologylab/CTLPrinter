# CTL Printer

A simple starter example/module for using the Star TSP100 FuturePRNT thermal printers that are currently stocked in the CTL.

The module currently works as a node script for MacOS. You need to just install the driver which you can find here: <http://www.starmicronics.com/support/default.aspx?printerCode=futurePRNT>

## Installation

For this module to work, you need to install PDFKit: `npm install pdfkit`

You also need to install the drivers necessary if using a USB printer. See the **Drivers** section

## Drivers

### Mac OS

Install the .pkg file found in /Drivers/MacOS

### Raspberry Pi

Download the zip folder found in /Drivers/RaspberryPi

## Usage

This example is a bare minimum to print some text to the printer.

```
const CTLPrinter = require('../CTLPrinter');

// Very important. See FINDING YOUR PRINTER
const printerName = 'Star_TSP143__STR_T_001_';
const options = {};

const printer = new CTLPrinter(printerName, options);
printer.printImage("This is some text");
```

## API

**CTLPrinter(printerName, options)**
- *printerName* - The name of the printer
- *options* - Any options to override the defaults

**options**

| Key             | Value                                          | Default |
|-----------------|------------------------------------------------|---------|
| file            | The file name to save. Mainly temporary        | tmp.pdf |
| width           | The width of the document                      | 612.0   |
| height          | The height of the document                     | 792.0   |
| margins         | The margins of the document (Number or Object) | 0       |
| deleteGenerated | Delete the generated PDF after use             | true    |
| fontSize        | The default font size for text                 | 36      |
| cutPage         | Whether to cut the page each time              | false   |
| cutDocument     | Whether to cut the document                    | true    |


**printText**
- *text* The text to print
- *options* (Optional) Override options temporarily
- *@returns Promise*

**printImage**
- *image* The image to print
- *options* (Optional) Override options temporarily
- *@returns Promise*

**printCustom**
- *drawFunction* A function that allows you to add custom PDFKit code, for full custimation
- *options* (Optional) Override options temporarily
- *@returns Promise*

*drawFunction* Is a function that gives you `(doc, width, height)` to work with


## Good-to-knows

Under the hood it uses PDFKit to generate a pdf to print. This is an opinionated choice, but it allows the code to have a level playing field, while also allowing for all of the immense catalogue that PDFKit brings.

## Finding your printer

To use the script you need to know the name of your printer according to your computer. To get the name, run `node getPrinters.js` and it should list them all. You will want to find the one that resembles `Star_TSP143__STR_T`