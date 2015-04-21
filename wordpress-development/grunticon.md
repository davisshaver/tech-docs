# Adding new icons with Grunticon
1. Icons can be downloaded from [The Noun Project](http://thenounproject.com/). Download the SVG version.
1. Rename the downloaded SVG to an appropriate name with `icon-` prefix. e.g. `icon-arrow`. This is the name that will be used for the CSS classes being created by Grunticon.  
1. The SVG file will need a little editing in vector editing software like Illustrator - make sure it's on a 100px by 100px canvas to keep it consistent with the rest of the icons. Change the color to what you need it to be and ensure that the file is in RGB mode. 
1. Drop the SVG file into: `assets/images/svg`
1. Run `grunt` in the terminal. All CSS files and PNG fallback images will be created. You can see a list of all icons from the file `assets/images/svg-fallback/preview.html`.

Optional step: If you need the icon to be in more colors than the original, you can rename the SVG file with color options. e.g. `icon-arrow.svg` will become `icon-arrow.colors-black.sv` More than one additional colors can be added by separating with `-`. The following color definitions have been added to gruntfile and can be used:  

    white: "#ffffff", gray: "#979ca0", black: "#0f0f13", hover: "#ed7a48", green: "#2ae699", blue: "#4284b4"
  
[More info about colors in Grunticon.](https://github.com/filamentgroup/grunticon#automating-color-variations)

Finally, since the icons are now background images, you'll have to set the width & height to scale the SVG image to what you want it to be. 
