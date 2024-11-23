# Needle/UnionLib [![Minecraft Version](https://img.shields.io/badge/minecraft-1.21-blue.svg)](#)

## What is the purpose of this mod
This mod only does two things, first is making developing multi-loader mods as simple as possible and the second is a configuration system that's very intuitive to use and lacks complexity.

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

## How to setup
This is not intended for anyone using the configuration system alone. Go to the config section to see how to implement the config system this mod provides. For the rest of you, you're going to need to follow the required steps to get your mod working on your mod loader. This mod isn't so advanced to get your mod seen by the loader.
Once you've got it running, we're going to make our main mod class extend `MinecraftMod`. This class contains all we'll ever need, besides mixins.

## Configuration
Firstly, I'd like to explain what a configuration system is. It's a system that allows a developer to use user input to modify the way a mod behaves. Let's take an example: Imagine you created a magical sword in your mod and you would like the user to change how much damage the sword should do. This is where a configuration system comes in, you can allow the user to specify that number in a file and you (well the mod) will read the file and apply that number.
In order to set up our configuration file, you'll need to create a new class and add the `@UnionConfig` annotation:
```
@UnionConfig(name = "unionlib")
public class Config implements ConfigObject {
}
```
