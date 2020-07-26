#### What is this?

This is a simple Android Studio native C++ project, generated
from the template in the starting wizard. However, the `cpp` part
of the project was improved to include the `"source"` folder
from https://github.com/Unity-Technologies/NativeRenderingPlugin (full
path in the repo is NativeRenderingPlugin/PluginSource/source/ ), taken
from commit `cd54d6c389a0f79fde9407b93ed87e3a9ac1f0ca`.

#### Why?

I needed to experiment with having access to a Unity texture from native C++.

#### What happened?

The NativeRenderingPlugin source was changed to:
- fix the compilation errors (comment out the dependency on glx, this might have broken something, but I don't care)
- the Android part now firmly targets GLES-3 instead of GLES-2
- fix Android Vulkan support: now Vulkan builds for Android as well, and the order of renderer choice was altered so that Vulkan would be attempted before the GLES-3 fallback
- the code on changing the geometries is commented out, only the texture altering code works now

Also, the `CMakeLists.txt` build instruction was changed to properly build
the NativeRenderingPlugin for Android.

#### What to do next?

To get the built libraries, build the project and go to

```app\build\intermediates\stripped_native_libs\debug\out\lib\```

folder of this repo. Take the folders for the CPU architectures you need
from the folder and copy the folders to your Unity project into

```Assets/Plugins/Android/Libs/```

After that the plugin should be available on Unity side.

Be sure that the rendering backends are set to "Vulkan" and "GLES 3"
in player settings in your Unity project.

#### And?

And it also works inside the Unity Editor and maybe on other platforms
as well.

To make it work in the Unity Editor go to https://github.com/Unity-Technologies/NativeRenderingPlugin
and find the `Assets/Plugins/Windows` folder there and copy the structure and
the contents into your project. I guess it would be a similar procedure for
other platforms.