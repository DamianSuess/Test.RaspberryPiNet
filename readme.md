## Intro
This example uses C# for Raspberry Pi 3 and demonstrates remote debugging.

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

## Resources
* [VSMonoDebugger](https://marketplace.visualstudio.com/items?itemName=GordianDotNet.VSMonoDebugger0d62)
  * https://github.com/GordianDotNet/VSMonoDebugger
  * Tested and does upload but failed to debug out of the box. (vs2019, RPi3 w/ Raspbian 9)
* [Mono Remote Debugger](https://marketplace.visualstudio.com/items?itemName=Bongho.MonoRemoteDebugger)
  * https://github.com/techl/MonoRemoteDebugger
  * [MSDN Thread](https://social.msdn.microsoft.com/Forums/vstudio/en-US/0654a5e4-42ba-4ebd-95b0-1a729d41f4d3/debugging-mono-apps-from-visual-studio?forum=vsdebug)
* MonoDevelop Remote Debugger
  * https://addins.monodevelop.com/Project/Index/205
  * https://github.com/logicethos/SSHDebugger
