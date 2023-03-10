# Checkpoints
Checkpoints are just saved states that can be used later to load. For example, if we can save the memory contents after the machine boots up, then we do not have to wait longer for each step of the kernel operation to bootup if we can just read from that saved checkpoint. 
Gem5 employs similar method. 
It saves the content into a ckpt file and can read the memory directly from there. 
However, __only MOESI__ cache protocol can be used to take the checkpoint as of v22.1.0.0 
So, we need to build the gem5 with new options. 

```
scons build/X86/gem5.opt PROTOCOL=MOESI_hammer --default=X86 
```
This should build a gem5 binary that can take checkpoint. 
We can use this binary in fs mode to take checkpoint after the system boots up using the hack_back_ckpts script or some other mechanism. 

## ```Hack Back Ckpts```
This is a [hack_back_ckpt.rcS](hack_back_ckpt.rcS) script given by gem5 software. This will take a checkpoint after booting up the system. Or it will execute a different script if there exists a checkpoint. Name of the script can be supplied in the file.

## ```genscripts.py``` 
The given [genscripts.py](generate_rcs_scripts/genscripts.py) will generate both checkpoint taking and restoring from checkpoint scripts. Checkpoint taking files will have ```_ckpts``` suffix before their ```.rcS``` file extensions. 

## ```/sbin/m5 checkpoint```
You can use ```telnet``` or other TTY program to connect while the gem5 simulation is running as it emits information on port 3456. So, you can directly get access to TTY by using ```telnet localhost 3456```

Once the kernel bootup is complete, you can execute the checkpoint command ```/sbin/m5 checkpoint``` 


## Using config parameters
You can take checkpoint by using ```--take-checkpoints``` parameters. This can be used to take multiple checkpoints from the same execution. Check the ```configs/common/Options.py``` for more details about this method
