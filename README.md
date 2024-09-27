# Needle/UnionLib [![Minecraft Version](https://img.shields.io/badge/minecraft-1.21-blue.svg)](#)

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
