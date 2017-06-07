## OpenMind

### SLURM

SLURM is the system used to allocate OpenMind resources to particular jobs. You can check out the [[Digits]] tutorial for a simple example of running a job. Here are some more resources on using SLURM:

[The Slurm documentation](https://slurm.schedmd.com/)

[Summary of Slurm commands](https://slurm.schedmd.com/pdfs/summary.pdf)

[NCCS Slurm info](https://www.nccs.nasa.gov/user_info/slurm)

[CBMM tutorial on working on OpenMind](https://www.youtube.com/watch?v=NGHlPNiYJcA) by Evan Remington


### Singularity

[Singularity is a container system designed for scientific computing.](http://singularity.lbl.gov/) The recommended way to run your code on OpenMind is through singularity.

In order to use Singularity you will need to add the singularity module when you log into Openmind. Note that modules do not persist between sessions:

```bash
$ module add openmind/singularity/2.2.1
```

If you want a version of singularity that's more cutting edge, for example if you want to use containers found on [Singularity Hub]() then you ought to do:

```bash
$ module add openmind/singularity/dev-8g4384538
```

#### Tutorials

[Here is an in-house tutorial on Singularity on OpenMind.](https://www.youtube.com/watch?v=tNRBRgNw2eM)

[Here is an example SLURM script that uses Singularity.](https://www.melbournebioinformatics.org.au/documentation/running_jobs/singularity/#using-singularity-containers-inside-a-slurm-job)

#### Where to get containers

Singularity can pull docker containers. If you use the dev version of singularity you can also use Singularity Hub. We also maintain a cache of some singularity images that you can download with `wget`. If you want an image that you can't find on docker or singularity hub and is difficult to build on your own, you can request a custom image on #tech in Slack. An engineer will build it for you and add it to our cache.

This is a list of containers we currently host:

| packages | url |
|:---:| --- |
| Python 3.6   | [Right click to copy link](https://resolution.cbmm.obsidian.systems/assets/py36.img.gz) |
| Python 3.6, Theano, and Keras   | [Right click to copy link](https://resolution.cbmm.obsidian.systems/assets/py36-theano-keras.img.gz) |
| Python 3.5, Tensorflow | [Right click to copy link](https://resolution.cbmm.obsidian.systems/assets/py35-tf.img.gz) |
| Python 3.5, PyTorch | [Right click to copy link](https://resolution.cbmm.obsidian.systems/assets/py35-torch.img.gz) |

For example, to download, unpack and shell into the container with Theano and Keras on it:

```bash
/om/user/$USER $ wget https://resolution.cbmm.obsidian.systems/assets/py36-theano-keras.img.gz
/om/user/$USER $ gunzip py36-theano-keras.img.gz
/om/user/$USER $ singularity shell -B /om:/om py36-theano-keras.img
```
