# rcS scripts
In Full System mode, you have to supply the commands you want to execute after the system has booted up its own kernel. 
This task can be simplified by supplying ```.rcS``` files.

For example, Python scripts for [generate_rcs_scripts/genscripts.py](generate_rcs_scripts/genscripts.py) will create all the necessary scripts for different PARSEC applications. It uses a PERL script [generate_rcs_scripts/writescripts.pl](generate_rcs_scripts/writescripts.pl) and input data from PARSEC to create necessary rcS file. You can also specify number of threads you want to utilize. 

One example of rcS file is as below 

```
#!/bin/sh

# File to run the blackscholes benchmark from existing checkpoints

cd /parsec/install/bin.ckpts  # this is where checkpoints are saved
/sbin/m5 dumpstats            # dump gem5 stats before executing the programs  
/sbin/m5 resetstats           # reset stats
./blackscholes 64 /parsec/install/inputs/blackscholes/in_16.txt /parsec/install/inputs/blackscholes/prices.txt # execute actual program
echo "Done :D"                # we are done
/sbin/m5 exit                 # exit needs to be twice
/sbin/m5 exit

```

