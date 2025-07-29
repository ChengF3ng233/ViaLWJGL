# ViaLWJGL

***LWJGLX "plus version", integrated into LWJGL3 for full compatibility***

### Usage
1. Download the latest build from `Github Release` to the folder `libs` in your project.
2. Add `implementation fileTree(dir: 'libs', include: ['*.jar'])` to the `dependencies` block in `build.gradle`
3. Fix try-catch errors in `Minecraft.createDisplay()` and `Config.checkDisplaySettings()` (Just remove the try-catch stucture and keep the codes in `try` block). 