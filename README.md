# Needle/UnionLib [![Minecraft Version](https://img.shields.io/badge/minecraft-1.21-blue.svg)](#)

## What is the purpose of this mod
It's one and only goal is to allow me, Stereowalker, to make back ports and release for multiple mod loaders with ease.

## How to add to your Project:

Insert the following text to your `build.gradle` file:
```
repositories {
    maven {
        url = "https://modmaven.dev/"
    }
}
dependencies {
	//replace ${unionlib_version} with the version of UnionLib you want to use, ${minecraft_version} with the version of Minecraft and ${loader} with the mod loader
    implementation fg.deobf("com.stereowalker.unionlib:UnionLib:${minecraft_version}-${unionlib_version}-${loader}")
}
```
please note for fabric, you'll need the forge config API port mod. This is only temporary as I'm currently working on a config system for this mod. It won't be anything revolutionary, just an alternative

## How to setup
You're going to need to follow the required steps to get your mod working on your mod loader. This mod isn't so advanced to get your mod seen by the loader.