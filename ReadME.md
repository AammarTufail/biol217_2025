# Biol217-2025 



## Here is how to use srun for ANVIO interactive:

### Displaying stuff
```
srun --pty --x11 --partition=interactive --nodes=1 --tasks-per-node=1 --cpus-per-task=1 --mem=10G --time=01:00:00 /bin/bash

module load gcc12-env/12.1.0
module load micromamba
micromamba activate $WORK/.micromamba/envs/00_anvio/

```
`Run the command to display what you want`
Then open a new terminal
```
ssh -L 8060:localhost:8080 sunam###@caucluster.rz.uni-kiel.de
```
```
ssh -L 8080:localhost:8080 n#
```
http://127.0.0.1:8060/
Then close the connection with `ctrl c`
```
exit
```
# if the host is busy, try 8080 instead of 8060
