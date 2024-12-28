# Prerequisites for Pedro Pathing

---

## Robot and Drive Type

Pedro Pathing is designed to work with **omnidirectional drives**, such as **mecanum drive**. Currently, there is no support for swerve drives. 

---

## Project Setup

#### 1. If you want to use the quickstart, clone it: ```https://github.com/Pedro-Pathing/Quickstart.git```. Then move on to [Constants Setup.](#constants-setup)
#### 2. If you want to add Pedro to your existing repository, add these two to your `repositories {}` block in `build.dependencies.gradle`:
```groovy
    maven { url = 'https://maven.brott.dev/' }
    maven { url= 'https://maven.pedropathing.com/' } 
```

#### 3. Then add these two to your `dependencies{}` block in `build.dependencies.gradle`:
```groovy
    implementation 'com.pedropathing:pedro:[VERSION]'
    implementation 'com.acmerobotics.dashboard:dashboard:0.4.16'
```
#### 4. Below, there is the latest version of Pedro, replace [VERSION] with it.

![Latest Pedro Version](https://img.shields.io/badge/dynamic/xml?url=https%3A%2F%2Fpedro-pathing.github.io%2Fmaven.pedropathing.com%2Fcom%2Fpedropathing%2Fpedro%2Fmaven-metadata.xml&query=%2Fmetadata%2Fversioning%2Flatest&style=for-the-badge&label=Build&labelColor=111111&color=7b39ab)

#### 5. Lastly, you will have to create a `PedroPathing` package. Within this you will store the tuners and your two constants files. Download the tuners from the [Pedro Pathing Quickstart](https://github.com/Pedro-Pathing/Quickstart). Place the tuners into your package and then continue to learn how to setup your `constants` files.

---

## Constants Setup

#### 1. Create a Class that has a static block. 
#### 2. We need to make sure to select our localizer type from the Localizers enum.

```java 
// This acts as a method of updating FollowerConstants without direct access to it.
public FConstants { // This is how we change Follower Constants.
    static {
        // Select our localizer
        FollowerConstants.localizers = Localizers.THREE_WHEEL;
        
        // We can change the value of each variable/constant of FollowerConstants.
        FollowerConstants.mass = 10; // In kg
    }
}
```

#### 3. Then, we need to create another class with a static block for our specific localizer's constants.
#### 4. We need to change the values for the localizer.

```java 
// This acts as a method of updating ThreeWheelConstants without direct access to it.
public LConstants { // This is how we change ThreeWheelConstants.
    static {
        ThreeWheelConstants.forwardTicksToInches = .001989436789;
        ThreeWheelConstants.strafeTicksToInches = .001989436789;
        ThreeWheelConstants.turnTicksToInches = .001989436789;
        ThreeWheelConstants.leftY = 1;
        ThreeWheelConstants.rightY = -1;
        ThreeWheelConstants.strafeX = -2.5;
        ThreeWheelConstants.leftEncoder_HardwareMapName = "leftFront";
        ThreeWheelConstants.rightEncoder_HardwareMapName = "rightRear";
        ThreeWheelConstants.strafeEncoder_HardwareMapName = "rightFront";
        ThreeWheelConstants.leftEncoderDirection = Encoder.REVERSE;
        ThreeWheelConstants.rightEncoderDirection = Encoder.REVERSE;
        ThreeWheelConstants.strafeEncoderDirection = Encoder.FORWARD;
    }
}
```
#### 5. There are default values saved within the library, you override them by changing their values in the ```static {}``` block in, for example, ```LConstants``` or ```FConstants```.
### **Note:** If you are ***not*** using the quickstart, you will have to adapt the tuners by inputting your classes that have the ```static{}``` blocks into the PoseUpdater or into the Follower, depending on which one the tuner/test uses.