# Hardware Issues

* Remove all external devices. Test each.
* Test each RAM.
* Test RAM with [MemTest86](http://www.memtest86.com) Test 5 and/or 8.
* Test HDD via SMART and Checksum.
* Reset [PRAM](http://support.apple.com/kb/HT1379): Press and hold the Command-Option-P-R keys before the gray screen appears (3 times).
* Reset [SMC](http://support.apple.com/kb/HT3964): Press Shift-Control-Option keys and the power button at the same time.
* Use the [Apple Hardware Test](http://support.apple.com/kb/HT1509).


# OS Issues

* Repair permissions via the Disk Utility.
* Try a new user account.
* Check login items and boot without them: Press Shift while you login.
* Install latest [Combo Update](http://support.apple.com/downloads/).
* Delete system- and user-caches.
* Check Console.app logs.
* Try a [safe boot](http://support.apple.com/kb/HT1455).
* Try a [verbose boot](https://support.apple.com/kb/ht1492).

## Fix Sleep Mode

* Let your Mac on over night. Often times background jobs are overdue and prevent Mac OS from sleep.
* Check Login Items at `/Library/~StartupItems`, `/Library/~LaunchDaemons`, `/System/Library/~LaunchDaemons` and `/System/Library/~LaunchAgents`.
* Use the Application [SmartSleep](http://www.jinx.de/SmartSleep.html) if nothing else is successful.