## Intro
This example uses C# for Raspberry Pi 3 and demonstrates remote debugging.

Fore note, all tests are performed using vs2019 (v16.4), RaspberryPi 3b v1.2 w/ Raspbian v9.

## Linux - Launching the app
To launch your app using a clickable link on Desktop Linux.

We uploaded ours using [WinSCP](https://winscp.net/eng/downloads.php) portable app to a new folder called ``TestApps`` under ``/home/pi/Desktop``, and renamed the exe to ``test-pinet.exe`` to keep things simple.

Next, we'll create the clicking file. Open a console window and navigate to our new folder. Now, type ``sudo nano TestPi.sh`` and input the following content

```bash
#!/bin/bash
mono /home/pi/Desktop/TestApps/test-pinet.exe
```

Now give the ``TestPi.sh`` file executable rights

```bash
sudo chmod +x TestPi.sh
```

Give it a try by double clicking your file via the Desktop.

## Raspberry Pi GPIO
* https://elinux.org/RPi_Low-level_peripherals#General_Purpose_Input.2FOutput_.28GPIO.29

### .NET Core IoT
The C# snip below can be found at the [.NET Core IoT samples](https://github.com/dotnet/iot/blob/master/samples/led-blink/README.md).

**Requires:**
* Red LED (1.8 - 2.2 Vf)
* 100K resistor
* GPIO pin 17 and GND.

```cs
int pin = 17;
GpioController controller = new GpioController();
controller.OpenPin(pin, PinMode.Output);

// Blink the LED
int lightTimeInMilliseconds = 1000;
int dimTimeInMilliseconds = 200;

while (true)
{
  Console.WriteLine($"Light for {lightTimeInMilliseconds}ms");
  controller.Write(pin, PinValue.High);

  Thread.Sleep(lightTimeInMilliseconds);
  Console.WriteLine($"Dim for {dimTimeInMilliseconds}ms");

  controller.Write(pin, PinValue.Low);
  Thread.Sleep(dimTimeInMilliseconds);
}
```

## Resources
**Raspberry Pi GPIO**
* .NET Core IoT [System.Device.Gpio](https://github.com/dotnet/iot) - 2019-12-22
  * [Samples](https://github.com/dotnet/iot/blob/master/samples/README.md) for .NET Core 2.1 and 3.0.
  * Supports Raspberry Pi 2B, 3, and 4 models (ARMv7/v8).
  * Raspberry Pi Zero or Arduino is not supported at this time (2019-12-27)
* [Raspberry-GPIO-Manager](https://github.com/AlexSartori/Raspberry-GPIO-Manager) - 2018-01-20
* [RaspberryPi.Net](https://github.com/cypherkey/RaspberryPi.Net) - 2017-05-06
* http://raspberrypi-aa.github.io/session2/led_control.html
* https://www.hanselman.com/blog/InstallingTheNETCore2xSDKOnARaspberryPiAndBlinkingAnLEDWithSystemDeviceGpio.aspx


**Remote Debugging:**
* [Connect VS to remote Linux](https://docs.microsoft.com/en-us/cpp/linux/connect-to-your-remote-linux-computer?view=vs-2019)
* [VSMonoDebugger](https://marketplace.visualstudio.com/items?itemName=GordianDotNet.VSMonoDebugger0d62)
  * https://github.com/GordianDotNet/VSMonoDebugger
  * Tested uploading EXE works
  * Tested remote debugging and it fails out of the box.
* [Mono Remote Debugger](https://marketplace.visualstudio.com/items?itemName=Bongho.MonoRemoteDebugger)
  * https://github.com/techl/MonoRemoteDebugger
  * [MSDN Thread](https://social.msdn.microsoft.com/Forums/vstudio/en-US/0654a5e4-42ba-4ebd-95b0-1a729d41f4d3/debugging-mono-apps-from-visual-studio?forum=vsdebug)
* MonoDevelop Remote Debugger
  * https://addins.monodevelop.com/Project/Index/205
  * https://github.com/logicethos/SSHDebugger
