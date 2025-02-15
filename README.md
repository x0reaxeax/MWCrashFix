# MWCrashFix - Experimental

### ⚠️ WARNING: EXPERIMENTAL BUILD, PROCEED AT YOUR OWN RISK ⚠️
This experimental version basically "swallows" crashes and forces the game to continue running, while leaving it in an [Undefined Behavior](https://en.wikipedia.org/wiki/Undefined_behavior) state, in which anything can theoretically happen.
  
In practice, the crashes should only stem from invalid `CALL` instructions, which are most likely the results of incorrect offset calculations caused by the initial patching, and recovering should be straightforward.  
**TL;DR:** Everything should be okay. source: trust me bro.

**However**, please keep in mind that this is a super "hacky" solution, comparable to patching a leaking lifeboat with band-aids.  
I'm **NOT RESPONSIBLE** for **ANYTHING** that might happen by using this fix, whether it's harmless in-game glitches, cosmic horrors manifesting in your RAM, or your PC becoming sentient and hijacking your car's ECU to do donuts in the parking lot.  

This build creates a file named `mwcrashfix.log` in the `scripts` folder of your NFS:MW folder. If you by some inconceivable chance still crash, please do send me this file, so I can hopefully fix whatever is even left to fix, I don't know at this point.

### Description
Fixes `Debug Error: R6025 - pure virtual function call` crash in Need for Speed Most Wanted 2005 1.3 BE.  
  
A widely used fix for this crash is implemented in [@GrimMaple](https://github.com/GrimMaple)'s [mwfixes](https://github.com/GrimMaple/mwfixes) project,
however, MWCrashFix (this mod) takes on a different approach for fixing this error, and that is by replacing the erroneous event with a different one, which should in theory not affect the spawn amount of pursuit events.  

This mod **CAN be used** along with the [mwfixes](https://github.com/GrimMaple/mwfixes) project, however, the **'Roadblock spawn problem fix'** in mwfixes will become **obsolete**. 

### Usage
Copy `MWCrashFix.asi` to `scripts` folder, which is located inside the main `Need For Speed Most Wanted Black Edition` game folder.

You can grab the compiled ASI file from the [Releases](https://github.com/x0reaxeax/MWCrashFix/releases) page, or compile it on your own.

### Troubleshooting
* `Instruction Check` error when starting the game:  
  * You're using an unsupported version of NFS MW. This mod was made for v1.3 RELOADED patch only.


### Additional information
* All instances of offending `MOV r/m32, imm32` instruction in `speed.exe`, where `imm32` is the erroneous address `0x00890970`, are replaced with a `MOV r/m32, 0x8aa828`, with `0x8aa828` being an address of a non-offending pursuit event.  
* A Vectored Exception Handler is registered and utilized to evaluate segmentation faults caused by erroneous `CALL` instructions, with backing from [Zydis-Amalgamated](https://github.com/zyantific/zydis).

### Possible improvements
* Add more non-offending event addresses to provide a variety in pursuit event spawning. 


### Credits
Special thanks to [Zydis](https://github.com/zyantific/zydis) for Zydis-Amalgamated.
