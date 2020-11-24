# LibVLCSharp.Android.AWindow
Small android binding project

Setting up `libvlc` for Android requires, amongst other things, calling this C function
```
LIBVLC_API void libvlc_media_player_set_android_context( 	
    libvlc_media_player_t *  	p_mi,
		void *  	p_awindow_handler 
	) 		
```

The documentation for the second parameter explains `p_awindow_handler: org.videolan.libvlc.AWindow jobject owned by the org.videolan.libvlc.MediaPlayer class from the libvlc-android project.`

So we will create an automatically generated binding for this class only, and pass a pointer to it to C code from C#.

_TODO: check Android API the Java code is compiled against._

## How to make your own binding

### Compile the relevant java code

- Get the sources (3.3.8): https://bintray.com/videolan/Android/download_file?file_path=org%2Fvideolan%2Fandroid%2Flibvlc-all%2F3.3.8%2Flibvlc-all-3.3.8-sources.jar
- Get the .so files https://bintray.com/videolan/Android/download_file?file_path=org%2Fvideolan%2Fandroid%2Flibvlc-all%2F3.3.8%2Flibvlc-all-3.3.8.aar

As of libvlc 3.0, you need to extract 3 Java files.
- `AndroidUtil`
- `AWindow`
- `IVLCVout`

- Put them at this location `MyApplication\org.videolan.libvlc\src\main\java`.

- Install gradle from choco https://chocolatey.org/packages/gradle

- run `gradle wrapper`

- finally run `.\gradlew assembleRelease` from `LibVLCSharp.Android.AWindow\MyApplication`

Extract the aar file from 

`LibVLCSharp.Android.AWindow\MyApplication\org.videolan.libvlc\build\outputs\aar` 

and copy it to

`LibVLCSharp.Android.AWindow\LibVLCSharp.Android.AWindow\Jars`.

On the C#, make sure the .aar file is referenced in your `csproj` file and the build action is marked as `LibraryProjectZip`.

-> Build.

The resulting dll is part of `LibVLCSharp.Android`.
