## Introduction

In this tutorial we're going to run a classic experiment to classify images of hand-written digits. The implementation parts of this tutorial follow [this introduction to TensorFlow](https://www.tensorflow.org/get_started/get_started).

## Setup

Let's set up a python project with TensorFlow. CBMM has a [template project](https://github.com/CBMM/tensorflow-template) already set up that we can import. We'll call our project `digits`:

```bash
$ toolkit/new-project digits
```

NOTE: You will have to set up your GitHub account with an SSH key first. You'll also need the [CBMM toolkit](https://github.com/CBMM/toolkit) cloned locally. Check the [[UROP-Checklist]] for a full list of prerequisites.

If you want to use virtual-env, which this tutorial assumes, there is a script for initializing an environment for a folder:

```bash
$ toolkit/init-virtualenv digits
```

We can enter the virtual environment like this:

```bash
$ cd digits

# activate the environment
$ source venv/bin/activate

```

### Sanity check

Run `nose2` and make sure the tests pass. If they do, great! We can start developing on our machine.

## Softmax Example

As the introduction mentioned, the code we're working with is part of [this introduction to TensorFlow](https://www.tensorflow.org/get_started/get_started). It's encouraged to read the tutorial and implement it in `digits/example.py`. You can implement the tutorial by replacing the definition of the function `tensorflow_example` with the softmax trainer. Here is an example:

```python
'''
TensorFlow digits tutorial
'''

import tempfile

# Import the tensorflow module so that its definitions are in scope
import tensorflow as tf

# The MNIST data comes packaged with tensorflow
from tensorflow.examples.tutorials.mnist import input_data

# Define a function that trains and validates a softmax regression on the MNIST data
def softmax_digits():
    # lets first load the mnist data
    # one_hot means that we are representing the digits 0-9 as 10-element vectors
    # where exactly one element is 1 and all the others are 0.
    # e.g. 0 = [1, 0, 0, 0, 0, 0, 0, 0, 0, 0]
    #      3 = [0, 0, 0, 1, 0, 0, 0, 0, 0, 0]
    tmpdir = tempfile.mkdtemp()
    mnist = input_data.read_data_sets(tmpdir, one_hot=True)

    # This is an input tensor to the computation graph. It has two dimensions,
    # one of them has unknown size and the other a size of 784 entries, one for each pixel.
    # The dimension of unknown size means that we can pass in any number of images each comprising
    # 784 pixels.
    x = tf.placeholder(tf.float32, [None, 784])

    # The weights of our network: we have 10 outputs for each of 784 input pixels.
    W = tf.Variable(tf.zeros([784, 10]))
    # The bias of our network: 1 element for each digit 0-9
    b = tf.Variable(tf.zeros([10]))

    # Note: Our weights and biases are specified as variables, so they have a definite
    # value within our computation graph which can be updated by tensorflow calculations.
    # Contrast with the placeholder which is an input we supply for each calculation.

    # The pieces of the computation graph we've defined so far compose our model:
    y = tf.matmul(x, W) + b

    # To check our model we need to test it against correct labels
    # Again, each answer is represented as a 10-element vector.
    # When we run a training or validation batch we supply the training data in `x`
    # and the labels we expect in `y_`.
    y_ = tf.placeholder(tf.float32, [None, 10])

    # We evaluate our model by computing its cross-entropy with the correct labels
    # `y` is a tensor of shape [None, 10] just like `y_`.
    # 1. softmax normalization of our current guess
    # 2. cross-entropy is multiply, sum across the second axis and negate
    # 3. error is average over all the examples (the first axis)
    #
    # cross_entropy = tf.reduce_mean(-tf.reduce_sum(y_ * tf.log(tf.nn.softmax(y)), axis=[1]))
    #
    # However that is numerically unstable so we do this instead:
    cross_entropy = tf.reduce_mean(
        tf.nn.softmax_cross_entropy_with_logits(labels=y_, logits=y))

    # Now we finish defining our computational graph by specifying how we want to run the
    # optimization step. We use gradient descent to minimize cross_entropy, our error function.
    train_step = train_step = tf.train.GradientDescentOptimizer(0.5).minimize(cross_entropy)

    # having defined our computational graph, let's run it, print out the result, and return it
    sess = tf.InteractiveSession()
    tf.global_variables_initializer().run()

    # training phase. We use batches of 100 images, 1000 times.
    for _ in range(1000):
        # fetch a batch of test images and their labels
        batch_xs, batch_ys = mnist.train.next_batch(100);
        # run the computational graph, making sure to provide the inputs
        # we promised TensorFlow we would provide
        sess.run(train_step, feed_dict={x: batch_xs, y_: batch_ys})

    # validation phase. we use a variant of the computational graph here
    # since each answer label is a one_hot vector, we just find the indexes
    # of the predicted and correct label and compare them for equality.
    #
    # The accuracy is just the average number of correct answers we got.
    # Note that we have to cast the true/false answer in correct_prediction to
    # a floating point number.
    correct_prediction = tf.equal(tf.argmax(y, 1), tf.argmax(y_,1))
    accuracy = tf.reduce_mean(tf.cast(correct_prediction, tf.float32))

    # We test against all of the validation data
    result = sess.run(accuracy, feed_dict={x: mnist.test.images, y_: mnist.test.labels})
    print("Result of tensorflow computation: " + str(result))
    return result
```

---

##### running the code

We've written the function, but we want to run it! We can do so from the command line:

```bash
$ python -c 'from digits import example; example.softmax_digits();'
# Some warnings from tensorflow might appear about CPU instructions you could
# enable from source.
# Your result will vary but it'll probably be between 0.91 and 0.93.
> Result of tensorflow computation: 0.9186
```

We will want to use a more robust method of invocation at some point but this is good for now!

##### fixing the test

The test that came with this repository is now broken. That makes sense because we changed the name of the function the test was invoking.

```bash
$ nose2
> ======================================================================
> ERROR: test_example (tests.test_example.SampleTestSuite)
> ----------------------------------------------------------------------
```

This test wasn't very useful but we should fix it as a matter of habit. When writing far more complicated programs tests will become essential to keeping all the details in order. To fix this trivial test:

Replace this test:

```python
class SampleTestSuite(unittest.TestCase):
    """Basic test cases."""

    def test_example(self):
        result = example.softmax_digits()
        assert result >= 0.91 and result <=0.93
```

With this test:

```python
class SoftmaxTestSuite(unittest.TestCase):
    """Make sure softmax on MNIST data has the expected accuracy. (0.91 <= accuracy <= 0.93)"""

    def test_softmax_digits(self):
        result = example.softmax_digits()
        assert result >= 0.91 and result <=0.93
```

Make sure this succeeds:

```bash
$ nose2
> Ran 1 test in 0.931s
>
> OK
```

##### check in the changes

If you've gotten to this point, great! Time to commit our progress to the `git` repository. We're making a simple commit here but we'll take a closer look at working with `git`.

Let's get a quick summary of what's going on in our directory:

```bash
$ git status
> On branch master
> Changes not staged for commit:
>   (use "git add <file>..." to update what will be committed)
>   (use "git checkout -- <file>..." to discard changes in working directory)
>
>   modified:   digits/example.py
>   modified:   tests/test_example.py
>
> no changes added to commit (use "git add" and/or "git commit -a")
```

Now we'll look at the details:

```bash
$ git diff
# This will put you in a screen where you can press space to scroll page by page
# It will show you all of the changes that haven't been staged to commit so far.
```

The `git status` prompt suggested that we can use `git commit -a`. This would stage all of our outstanding changes and commit them. This is pretty bad practice! It's easy to commit scraps of code that should be cleaned up before commit.

A good way to commit is `git add -p`. This will prompt you to examine every change that isn't staged and decide what you want to do with it. There are a lot of options but the most important ones are:

| cmd | Function |
|:---:| --- |
| y   | Add this hunk |
| n   | Don't stage this hunk |
| q   | Don't stage this hunk and quit |
| d   | Don't stage this hunk or any others in this file |
| s   | Split this hunk into smaller units |

Even though we know the changes we've made are the ones we want and it's a simple commit, it's still good to be in the habit of examining each set of changes at least a little bit when commiting it.

---

Once you've committed the code, examine the output of `git status`:

```bash
$ git status
> On branch master
> Changes to be committed:
>   (use "git reset HEAD <file>..." to unstage)
>
>   modified:   digits/example.py
>   modified:   tests/test_example.py
```

You can also try `git diff`, but you'll notice it's empty! By default `git diff` shows _unstaged_ changes, not staged ones. You can look at staged indexes with `git diff --cached`.

Now that our changes are staged, let's commit them!

```bash
$ git commit -m "implement softmax digit classification"
> [master 2b624ae] implement softmax digit classification
>  2 files changed, 94 insertions(+), 27 deletions(-)
>  rewrite digits/example.py (78%)
```

`git commit -m` takes a parameter that describes the contents of the commit. If you use `git commit` instead, your text editor will be opened for you to type out a commit message.

### Deploying your code

We'll use GitHub to coordinate our code across environments. First [create a new GitHub repository](https://github.com/new) for the project. You can name it `digits` here as well. Do not add a `.gitignore`, `README` or `license`. Once that is done we will add the GitHub repository as a [remote](https://help.github.com/articles/about-remote-repositories/) of our local project and push our code:

```bash
$ git remote add origin git@github.com:<Github-Username>/digits.git
$ git push -u origin master
```

## Run the code on Polestar

Now you can log on to Polestar and clone your repository there:

```bash
# ssh -A lets you use your local private key to authenticate inside of an SSH session
$ ssh -A <Kerberos-Username>@polestar.mit.edu

# if you don't already have the toolkit cloned, do it here
$ git clone git@github.com:CBMM/toolkit.git --recursive

# gpu-16 is a polestar node with a more modern version of glibc, required for tensorflow
# any sufficiently up-to-date node is usable
polestar$ ssh -A gpu-16

gpu-16$ toolkit/clone-project <Github-Username> digits master
gpu-16$ cd digits
gpu-16$ source venv/bin/activate
gpu-16$ python -c 'from digits import example; example.softmax_digits();'
```

## Run the code on OpenMind

Running on OpenMind is a little different. We can't use virtualenv out of the box. In fact, we shouldn't be doing  dependency management on OpenMind at all. The recommended way to run code on OpenMind is to use Singularity. We've packaged up some singularity containers with some common sets of tools which you can find on the [[OpenMind]] page. Here we'll be using TensorFlow with Python 3.5.

OpenMind uses SLURM to allocate its resources to user jobs. To use SLURM we have to use a script that tells it what to do. Save this file into bin/slurm-job:

```bash
#!/usr/bin/env bash
#SBATCH --job-name=softmax_digits
#SBATCH --output digits.out
#SBATCH --ntasks=1
#SBATCH --gres=gpu:1

set -euxo pipefail

# allows us to use modules within a script
source ${MODULESHOME}/init/bash

module add openmind/singularity/2.2.1

singularity exec --bind /om:/om ./py35-tf.img python -c 'from digits import example; example.softmax_digits();'
```

Once that is saved, you need to mark it as executable with `chmod +x bin/slurm-job`. Having done that, commit the script to your repository and push it. Now we can log into openmind and run the job:

```bash
$ ssh -A <Kerberos-Username>@openmind7.mit.edu

# /om is where you should put all of your work. Your home directory is only allowed 5GB of space
# /om has a much laxer limit.
openmind$ cd /om/user/<Kerberos-Username>
openmind$ git clone git@github.com:<Github-Username>/digits
openmind$ cd digits

# the following line fetches the image, decompresses it, and saves it
openmind$ wget -O - https://resolution.cbmm.obsidian.systems/assets/py35-tf.img.gz | gunzip -c > py35-tf.img

openmind$ sbatch bin/slurm-job
```

To check on the status of your queued jobs you can use this command:

```bash
openmind$ squeue --user=$USER
# Sample output
-bash-4.2$ squeue --user=$USER
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
           8526071 om_all_no softmax_ danharaj  R       0:03      1 node003

```

To check on the status of a particular job, like the one we just ran, you can do:

```bash
openmind$ scontrol show job <JOBID>
# Sample output
-bash-4.2$ scontrol show job 8526071
JobId=8526071 JobName=softmax_digits
   UserId=danharaj(155530) GroupId=cbmm(88891) MCS_label=N/A
   Priority=55627 Nice=0 Account=cbmm QOS=normal
   JobState=COMPLETED Reason=None Dependency=(null)
   Requeue=1 Restarts=0 BatchFlag=1 Reboot=0 ExitCode=0:0
   RunTime=00:00:30 TimeLimit=00:10:00 TimeMin=N/A
   SubmitTime=2017-05-08T11:55:19 EligibleTime=2017-05-08T11:55:19
   StartTime=2017-05-08T11:55:20 EndTime=2017-05-08T11:55:50 Deadline=N/A
   PreemptTime=None SuspendTime=None SecsPreSuspend=0
   Partition=om_all_nodes AllocNode:Sid=openmind7:41400
   ReqNodeList=(null) ExcNodeList=(null)
   NodeList=node003
   BatchHost=node003
   NumNodes=1 NumCPUs=2 NumTasks=1 CPUs/Task=1 ReqB:S:C:T=0:0:*:*
   TRES=cpu=2,mem=4G,node=1,gres/gpu=1
   Socks/Node=* NtasksPerN:B:S:C=0:0:*:* CoreSpec=*
   MinCPUsNode=1 MinMemoryCPU=2G MinTmpDiskNode=0
   Features=(null) Gres=gpu:1 Reservation=(null)
   OverSubscribe=OK Contiguous=0 Licenses=(null) Network=(null)
   Command=/om/user/danharaj/digits/bin/slurm-job
   WorkDir=/om/user/danharaj/digits
   StdErr=/om/user/danharaj/digits/digits.out
   StdIn=/dev/null
   StdOut=/om/user/danharaj/digits/digits.out
   Power=
```

Note that the console output of our job was saved to `digits.out`. For more serious experiments you'll want to save your results to files formatted for consumption by data analysis tools.

## Conclusion

What we've gone over is the basic set up for writing and running an experiment. This template can serve as a model for more sophisticated experiments: The overall infrastructure does not change that much. Let us know about any questions you have in #tech on Slack!
