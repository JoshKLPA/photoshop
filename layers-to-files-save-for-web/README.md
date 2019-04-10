# Export Layers to Files in Photoshop using Save for Web and without underscore/number prefixes

This script is intended to replace the Photoshop script file "Export Layers to Files.jsx," to allow the script to use "Save for Web" instead of "Save," and to remove the underscore and number prefixes that come 

## Getting Started

Replace the "Export Layers To Files.jsx" file on your machine and replace it with the file in this repository. Note: be sure to save a backup of your original .jsx file under a modified file name in case this version doesn't work for some reason.

MacOS: `/Applications/Adobe Photoshop [VERSION]/Presets/Scripts/`

Windows: `C:/Program Files/Adobe/Adobe Photoshop [VERSION]/Presets/Scripts/`


Within the file, you can find the edited code in the locations listed below. To assist people who want to learn more about how .jsx works or to customize their own scripts, I've only commented out the original code so it can be compared with the revisions:

#### Line 1501 - JPG Save for Web:

```javascript

case jpegIndex:

fileExtension = "jpg";

// docRef.bitsPerChannel = BitsPerChannelType.EIGHT;

// var saveFile = new File(exportInfo.destination + "/" + fileNameBody + ".jpg");

// jpgSaveOptions = new JPEGSaveOptions();

// jpgSaveOptions.embedColorProfile = exportInfo.icc;

// jpgSaveOptions.quality = exportInfo.jpegQuality;

// docRef.saveAs(saveFile, jpgSaveOptions, true, Extension.LOWERCASE);

docRef.bitsPerChannel = BitsPerChannelType.EIGHT;

var saveFile = new File(exportInfo.destination + "/" + fileNameBody + ".jpg");

var exportOpts = new ExportOptionsSaveForWeb( );

exportOpts.format = SaveDocumentType.JPEG;

exportOpts.includeProfile = exportInfo.icc;

exportOpts.quality = Math.round( exportInfo.jpegQuality / 12 * 100 ); // exportInfo.jpegQuality is 0 to 12, SFW uses 0 to 100. this converts

if ( saveFile.exists ) saveFile.remove( );// avoid file exists overwrite dialog

docRef.exportDocument( saveFile, ExportType.SAVEFORWEB, exportOpts );

break;

```

#### Line 2207 - Remove numerical prefixes 1:

```javascript

var fileNameBody = fileNamePrefix;

// fileNameBody += "_" + zeroSuppress(i, 4);

// fileNameBody += "_" + layerName;

fileNameBody += layerName;

```

#### Line 2245: - Remove numerical prefixes 2:

```javascript

var fileNameBody = fileNamePrefix;

// fileNameBody += "_" + zeroSuppress(i, 4) + "s";

```

### Prerequisites

Adobe Photoshop CC 2019 (20.0.4)

This script should work with older and newer versions of Photoshop, but is untested with anything but the above version. Again, please be sure to backup a copy of your old "Export Layers to Files.jsx" file in case this one doesn't work.

* **Josh KLPA** - *Initial work* - [Github](https://github.com/JoshKLPA) [Dribbble](https://dribbble.com/KLPA)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

Many thanks to Michael L. Hale who wrote the original snippet way back in 2010: [Adobe Forum Post](https://forums.adobe.com/thread/572458)

Also, thanks to Srikar Appalaraju who wrote the instructions for removing/adjusting the numerical prefixes: [Stack Exchange Post](https://graphicdesign.stackexchange.com/questions/10669/cs5-export-layers-as-files-with-no-number-sequence)