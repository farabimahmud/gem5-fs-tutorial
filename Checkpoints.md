# Checkpoints
Checkpoints are just saved states that can be used later to load. For example, if we can save the memory contents after the machine boots up, then we do not have to wait longer for each step of the kernel operation to bootup if we can just read from that saved checkpoint. 
Gem5 employs similar method. 
It saves the content into a ckpt file and can read the memory directly from there. 
However, __only MOESI__ cache protocol can be used to take the checkpoint as of v22.1.0.0 
So, we need to build the gem5 with new options. 

```
scons build/X86/gem5.opt PROTOCOL=MOESI_Hammer --default=X86 
```
This should build a gem5 binary that can take checkpoint. 
We can use this binary in fs mode to take checkpoint after the system boots up using the hack_back_ckpts script or some other mechanism. 

## Hack Back Ckpts
This is a [hack_back_ckpt.rcS](hack_back_ckpt.rcS) script given by gem5 software. This will take a checkpoint after booting up the system. Or it will execute a different script if there exists a checkpoint. Name of the script can be supplied in the file.


