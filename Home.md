Welcome to the Subworld Library wiki!

# Getting Started

Before you begin using Subworld Library, it is highly recommended that you download [SubworldLibrary.dll](https://github.com/jjohnsnaill/SubworldLibrary/blob/master/SubworldLibrary.dll), and add it as a dependency to your project, by right-clicking on `Dependencies`, clicking on `Add Reference...`, then `Browse...`, selecting the dll, and clicking `OK`. This will allow you to reference Subworld Library in Visual Studio.

# Creating a Subworld

Classes that derive from `Subworld` are automatically registered as subworlds. Below is a list of fields that can be overridden. Fields that are required are marked in **bold.**

| Field | Description |
| --- | --- |
| **width** | The subworld's width. Cannot be above 8400. |
| **height** | The subworld's height. Cannot be above 2400. |
| **modWorld** | If not set to null, only the specified ModWorld can update inside the subworld. |
| **tasks** | An array of the subworld's generation tasks. |
| **Load()** | Called after the subworld has loaded or generated. |
| Unload() | Called when exiting the subworld. |
| saveSubworld | Whether the subworld is saved or not. Defaults to `false`. |
| disablePlayerSaving | Whether players should save inside the subworld or not. Defaults to `false`. |
| saveModData | Whether ModWorld data should save inside the subworld or not. If `modWorld` is not null, only the specified ModWorld's data will save. Defaults to `false`. |
| loadingUI | Change this to your own `UserInterface` if you want the subworld's custom UI to persist after the subworld loads/unloads. |
| loadingUIState | Change this if you want the subworld to have a custom UI, rather than the default. |

# Entering and Exiting a Subworld

To enter a subworld, simply call `SLWorld.EnterSubworld("<mod name>_<subworld name>")`. Exiting a subworld is even simpler; just call `SLWorld.ExitSubworld()`.

# Examples

```
public class Blank : Subworld
{
    public override int width => 8400;
    public override int height => 2400;
    public override ModWorld modWorld => null;
    public override SubworldGenPass[] tasks => new SubworldGenPass[]
    {
        new SubworldGenPass("Loading", 1f, progress =>
        {
            progress.Message = "Loading";
            Main.worldSurface = Main.maxTilesY - 42;
            Main.rockLayer = Main.maxTilesY;
        })
    };

    public override void Load()
    {
        Main.dayTime = true;
        Main.time = 27000;
        Main.worldRate = 0;
    }
}