# ViaLWJGL

***LWJGLX "plus version", integrated into LWJGL3 for full compatibility***

### Install

- build.gradle
```groovy
repositories {
    maven {
        url "https://jitpack.io"
    }
}

dependencies {
    implementation 'com.github.ChengF3ng233:ViaLWJGL:-SNAPSHOT'
}
```

### Error fixes

Replace following methods with the code below.

- Minecraft.createDisplay()

```java
private void createDisplay() throws LWJGLException {
    Display.setResizable(true);
    Display.setTitle("Minecraft 1.8.9");
    Display.create((new PixelFormat()).withDepthBits(24));
}
```

- Config.checkDisplaySettings()

```java
public static void checkDisplaySettings() {
    int i = getAntialiasingLevel();
    if (i <= 0) return;

    DisplayMode displaymode = Display.getDisplayMode();
    dbg("FSAA Samples: " + i);

    Display.destroy();
    Display.setDisplayMode(displaymode);
    Display.create((new PixelFormat()).withDepthBits(24).withSamples(i));

    if (Util.getOSType() == Util.EnumOS.WINDOWS) {
        Display.setResizable(false);
        Display.setResizable(true);
    }

    if (!Minecraft.isRunningOnMac && getDefaultResourcePack() != null) {
        InputStream icon16 = null;
        InputStream icon32 = null;

        try {
            icon16 = getDefaultResourcePack().getInputStreamAssets(new ResourceLocation("icons/icon_16x16.png"));
            icon32 = getDefaultResourcePack().getInputStreamAssets(new ResourceLocation("icons/icon_32x32.png"));

            if (icon16 != null && icon32 != null) {
                Display.setIcon(new ByteBuffer[]{readIconImage(icon16), readIconImage(icon32)});
            }
        } catch (IOException ioexception) {
            warn("Error setting window icon: " + ioexception.getClass().getName() + ": " + ioexception.getMessage());
        } finally {
            IOUtils.closeQuietly(icon16);
            IOUtils.closeQuietly(icon32);
        }
    }
}
```