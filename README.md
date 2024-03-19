# FNF-psych-engine-Shader-tutorial

This tutorial is to explain the basics of using the OFFICIAL Psych Engine's Softcoded/Lua shaders. This tutorial is NOT for OS engine or whatever shitty Psych Engine fork you play.

Step 1 : Obtain a shader from shadertoy
To do this, find the shader you want, then click on it, I'm going to be using this one here.
Copy the code from the right side of the screen.

Step 2 : Putting a shader in a .frag file
Make a new file with the .frag file type, name it whatever you want, and put it in mods/shaders. Paste the shadertoy code you have in your file, but you're gonna need to do a few extra things to make sure the shader doesn't give you any errors while compiling.

Firstly, you have to paste this on top of your shader code :

```
#pragma header
vec2 fragCoord = openfl_TextureCoordv*openfl_TextureSize;
vec2 iResolution = openfl_TextureSize;
uniform float iTime;
#define iChannel0 bitmap
#define texture texture2D
#define fragColor gl_FragColor
```

delete the void mainImage( out vec4 fragColor, in vec2 fragCoord) 
and make it into this
```
void main() 
```

if your shader turns black even tho you did everything right you need to add this code. this code adds alpha support so you can see your sprites 
```
gl_FragColor.a = texture2D(bitmap, openfl_TextureCoordv).a;
```
make sure to put this code on the bottom of something like this fragColor = vec4(col,1.0);

now, find the mainImage void in the shader, and remove it's parameters.

And that should be your shader file done.

Step 3 : Putting the shader on a sprite
This is probably the easiest part of this tutorial. Create a new .LUA file in your song's data folder, and inside any function, put :
```
initLuaShader('shaderName')
setSpriteShader('objName', 'shaderName')
```
Obviously replace "shaderName" with the name of your shader, and replace "objName", with the object you want the shader to be applied to.

If you've done everything correctly, your shader should give no errors and your shader should be applied to the object you specified.

If you're wondering how to remove a shader from an object, just use 
```
removeSpriteShader('objName')
```
