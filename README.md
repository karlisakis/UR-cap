# Aim Robotics Dispenser URcap

## Notes

The password for the UR virtualbox image is `easybot`

You don't necessary need to compile and package the application every time you make an update.

## How to install install the project locally

### Clone the repository

Navigate to the folder you want to store the code and enter the following command:

```
git clone https://github.com/rimvydaszilinskas/aimr_head.git
```

### Compiling the application

#### Compiling

Currently the naming is as follows: ```dispenser_head.aimr-<version-number>```. There are two files named identically, use .urcap for uploading to the robot.

#### Environment

To compile the application we need to have JDK, Maven and Universal Robot dependencies installed, therefore it is better if you use their own supplied Virtual Machine image. You can downlaod it [here](https://plus.universal-robots.com/download-center/urcaps-starter-package/). To use it, simply extract it and when creating a new virtual machine choose the file called `URCaps Starter Package.vmdk`.

#### GIT

To clone the repository first you will have to install GIT on the Virtual Machine. Run the following command to do so:

```sh
sudo apt-get install git
```

To verify that it works:

```sh
git --version
```

It should show you something similar to:

```
git version 2.17.1
```

If all is good, continue.

#### Installation

After you cloned the repository with:

```sh
git clone https://github.com/rimvydaszilinskas/aimr_head.git
```

Navigate to the folder using:

```sh
cd aimr_head/URcap
```

Before installing you also need to edit where is the simulator located. To do that use the following command:

```sh
nano ./URcap/pom.xml
```

Then find a line with the tag 

```xml
<ursim.home> ... </ursim.home>
```

Add the path instead of ```...```

If you're using the UR image the path should be

```xml
<ursim.home>/home/ur/ursim/ursim-5.3.0.64176</ursim.home>
```

NOTE that the version may vary.

After editing the path you are ready to install it:

```sh
mvn install -P ursim
```

Then navigate to the folder where simulator is:

```sh
cd ~/ursim/ursim-5.3.0.64176
```

And run the simulator

```sh
./start-ursim.sh
```

## How to install the URcap on the robot

After installation to the local simulator, there should be a file in ```./target/``` directory named something like ```dispenser_head.aimr-0.1.urcap```.
Copy that file to a flash drive and then plug it in to the robot.

On the robot enter manual mode by entering the password and then go to `settings > System > URcaps`. Press `'+'` sign to a new URcap, select the corresponding USB drive and select the URcap in question. After that you will be prompted to restart the robot again.

If you see our URCap already installed, please select it press `'-'` sign and restart the robot.

## Running

The app relies on RS485 communication using `/dev/ttyTool` serial port using tool 8-pin connector. And it has to be initialized beforehand. 

On the top menu choose `Installation`, then on the left hand side choose URcaps and then on the dropdown choose our URcap. The screen will show an installation. Press `Open Serial` button and wait until it turns to `Close Serial`. Then navigate back to the program and you are good to go!

# Arduino code

Arduino is currently just listening for RS485 signals and not responding.

We are utilizing:

```
RS485 to serial converter module
LM2596 buck converter module
A4988 Stepper Motor Driver module
```

# Licensing

To edit license for the URcap edit file `URcap/src/main/resources/META-INF/LICENSE

# Updating the repository

If you would like to edit the repository, please follow the following steps:

1. Pull for updates
    ```
    git pull
    ```
2. Edit the files you want to edit. If you need to run compile, do so.
3. Add all the files for commiting them to repository:
    ```
    git add .
    ```
4. Commit changes
    ```
    git commit "<YOUR MESSAGE GOES HERE>
    ```
    
    Note: The message should reflect what you have changed
5. Push the changes to the repository
    ```
    git push
    ```