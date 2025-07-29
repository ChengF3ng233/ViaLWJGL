# ViaLWJGL

***LWJGLX "plus version", integrated into LWJGL3 for full compatibility***

### Usage
1. Download the latest build from `Github Release` to the folder `libs` in your project.
2. Add `implementation fileTree(dir: 'libs', include: ['*.jar'])` to the `dependencies` block in `build.gradle`
3. Remove try-catch errors in `Minecraft.java` and `Config.java` (Just remove the LWJGLException catch blocks). 