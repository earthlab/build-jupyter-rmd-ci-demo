# Remote Debugging & SSH with CircleCI

Remote debugging refers to debugging performed on the CircleCI build.

#### Interactive debugging via SSH

Debugging can be performed interactively via CLI, using SSH to acess a build after it is run. This can be handy for checking the content of intermediate files generated within the build, whether files updated as expected, etc.

You will need a local RSA key to access the build via SSH. See [Authenticating SSH](https://hackmd.io/psb27zRdTHqJfHtNG8kRXw?view#Authenticating-SSH) for instuctions on setting up an RSA key on your machine.

On the status page for your CircleCI job, select the drop-down menu next to the button at the upper-right that says `Rebuild` and select `Rerun job with SSH`. The job will rerun _without deploying changes_ and when finished will instead list a remote address where the job can be accessed. In the terminal, enter the command

```
ssh -p XXXXX xx.xxx.xxx.xx
```

using the values given at the end of the CircleCI build after `-p`. These represent the unique ID and address of the remote CircleCI job, respectively. Answer `yes` to the prompt about the remote RSA key.

Once you are finished debugging, leave the job with the command `exit`. The job will remain active for another 10 minutes, then time out. **Note** that you can SSH into a job more than once, but it _will not_ have the same ID and address as last time.

#### Debugging an R Lesson knit job

It is not possible to interactively debug an `.rmd` as it is knitting. However, variables in the notebook may be viewed from the knit progress report once the build completes by inserting this code chunk (uncommented):

```
# ```{r message = F}
# message(print(...))
# ```
```

where `...` is some variable or value you are interested in viewing from the knit job. The nested `print` function should coerce whatever data type the target variable/value is to a string that can be output by `message`.


## Authenticating SSH

CircleCI provides [these instructions](https://circleci.com/docs/2.0/ssh-access-jobs/) for authenticating SSH with your account.

You will need to set up a local RSA key before being able to enter a build. This is device-specific, so if you are working on multiple machines, you will need to run through these steps several times.

1. Checking whether a local SSH key exists:

    https://help.github.com/en/articles/error-permission-denied-publickey

2. Generating a new local SSH key if one is needed:

    https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

3. Adding the new SSH key to GitHub account:

    https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account

    **Note** that you will need to copy the SSH key you generated _from the terminal_ to your clipboard. There are [different ways to do this](https://www.digitalocean.com/community/questions/copy-ssh-key-to-clipboard) based on your OS.

4. Finally, verify your connection to GitHub:

    ```
    ssh -T git@github.com
    ```

    Enter `yes` if prompted. Then you should see a message like:

    ```
    Hi jvtcl! You've successfully authenticated...
    ```
