# LibreOffice buildpack for heroku-24 stack

Particularly useful if you use the `libreconv` gem for document conversion to PDF in Ruby on Rails applications, and results in a manageable slug size (which will likely keep you under heroku's soft limit as an added bonus) when compared with other options.


Add the `heroku-buildpack-apt` buildpack:
```
heroku buildpacks:add --index 1 https://github.com/heroku/heroku-buildpack-apt.git
```

Add the LibreOffice buildpack:
```
heroku buildpacks:add --index 2 https://github.com/KaleidoscopeGroupPBC/heroku-buildpack-libreoffice.git
```

Optionally, add the `heroku/jvm` buildpack to install Java Runtime Environment (only for non-java apps):
```
heroku buildpacks:add --index 3 heroku/jvm
```

Create an `Aptfile` file at the root with the following content (do **not** include libreoffice here):
```
libsm6
libice6
libxinerama1
libdbus-glib-1-2
libharfbuzz0b
libharfbuzz-icu0
libx11-xcb1
libxcb1
libcups2
```

Optionally, create a `LibreOfficeAppImage` file in your application repository to change the installed version to something other than the latest `fresh`.
The file should contain only the full URL of a LibreOffice AppImage, from the [official links found here](https://www.libreoffice.org/download/appimage/).
For example the latest `still` can be installed with:
```
https://appimages.libreitalia.org/LibreOffice-still.basic-x86_64.AppImage
```

Redeploy after committing the above.
