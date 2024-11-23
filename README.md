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
@UnionConfig(name = "yourconfigfilename")
public class Config implements ConfigObject {
}
```
You can omit `ConfigObject` if you want to statically reference your config options. There are a few options you have in `@UnionConfig`.
1) `name`: This is what the config file would be named when it's generated and will be read. So if you set the name to "yourconfigfilename", the file generated will be "yourconfigfilename-common.toml", depending on the environment
2) `translatableName`: Use this if you're using the config gui to change the name depending on the language
3) `folder`: If you want the file to be in a folder in the config folder
4) `appendWithType`: Set this to false if you don't want the type of config to be appended to your file. Essentially, your file will no longer be "yourconfigfilename-common.toml", but instead "yourconfigfilename.toml". Please be careful of using 2 different types of config in the same file when using this option
5) `autoReload`: Whether or not you want the config file to reload itself after a change is made. Enabled by default and only really useful if you want to ensure the config doesn't change after it's loaded

Now for the entries, only primitives, strings, and collections are supported. You'll have to figure out any other data types yourself. To add an entry, you'll just have to add these annotations to your values
```
@UnionConfig.Entry(group = "Any Group" , name = "Magical Sword Damage", translatable = "config.any.sworddamage", side = ConfigSide.Shared)
@UnionConfig.Comment(translatable = {"config.any.sworddamage.comment.1", "config.any.sworddamage.comment.2"}, comment = {"Each entry is one line in the comment of your config","You can also use \n to add a new line. It's all up to preference"})
@UnionConfig.Range(min = 1, max = 100, useSlider = true)
public int magicalSwordDamage = 20;
```
Let's go through each annotation one by one
`@UnionConfig.Entry`
1) `group`: Only useful for organizing your entries in its file. Can be omitted
2) `name`: This is the name of the option in the file and what will be read
3) `translatable`: Same deal as the `translatableName` from earlier. Can be omitted
4) `side`: This determines when the file will be read Your options are `ConfigSide.Shared`, `ConfigSide.Server`, and `ConfigSide.Client`. `ConfigSide.Shared` is loaded when the client is started and when the world is loaded and synced to all connected clients. `ConfigSide.Server` is only loaded when the world is loaded, any attempts to read this value on the client will only result in what you set as the default. `ConfigSide.Client` is only read when the client is started and will only result in the default value when read by a server

`@UnionConfig.Comment`. Can be omitted
1) `comment`: The comment that will be generated in your file. Use it to convey important information about the option to your users
2) `translatable`: Same deal as the `translatableName` from earlier. Can be omitted

`@UnionConfig.Range`. For numerical entries, can be omitted
1) `min`: The minimum value of the entry. If the user specifies a number lower than this, it'll be corrected to this value
2) `max`: The maximum value of the entry. If the user specifies a number higher than this, it'll be corrected to this value
3) `useSlider`: Only useful if you're using the gui, it uses a slider instead of a text box for your entry
