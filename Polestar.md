## Polestar

Log on to Polestar and clone your repository there:

```bash
# ssh -A lets you use your local private key to authenticate inside of an SSH session
$ ssh -A <Kerberos-Username>@polestar.mit.edu

# if you don't already have the toolkit cloned, do it here
$ git clone git@github.com:CBMM/toolkit.git --recursive

# gpu-16 is a polestar node with a more modern version of glibc, required for tensorflow
# any sufficiently up-to-date node is usable
polestar$ ssh -A gpu-16

gpu-16$ toolkit/init-virtualenv tf_venv
gpu-16$ cd tf_venv
gpu-16$ source venv/bin/activate
gpu-16$ python -c 'import tensorflow as tf; print(tf.__version__);'
```