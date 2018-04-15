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

```cmd
git clone https://code.videolan.org/videolan/vlc-android
```

Checkout the revision you target on vlc-android: 3.0.0, 3.0.1, 3.0.2, etc...

As of libvlc 3.0, you need to extract 3 Java files.
- `AndroidUtil`
- `AWindow`
- `IVLCVout`

To get the .aar file, run `assemblyRelease` in the Gradle window of Android Studio.

Extract the aar file from 

`LibVLCSharp.Android.AWindow\MyApplication\org.videolan.libvlc\build\outputs\aar` 

and copy it to

`LibVLCSharp.Android.AWindow\LibVLCSharp.Android.AWindow\Jars`.

On the C#, make sure the .aar file is referenced in your `csproj` file and the build action is marked as `LibraryProjectZip`.

-> Build.

The resulting dll is part of `LibVLCSharp.Android`.
