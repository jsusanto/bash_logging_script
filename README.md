# bash_logging_script
Bash Script to Log all activities

If you want to log every activities in your bash script.
Please include the following script at the beginning of your bash script.

<pre>
#!/bin/bash
exec 3>&1 4>&2
trap 'exec 2>&4 1>&3' 0 1 2 3
exec 1>log.out 2>&1
# Everything below will go to the file 'log.out':
</pre>
Explanation:

    exec 3>&1 4>&2

    Saves file descriptors so they can be restored to whatever they were before redirection or used themselves to output to whatever they were before the following redirect.

    trap 'exec 2>&4 1>&3' 0 1 2 3

    Restore file descriptors for particular signals. Not generally necessary since they should be restored when the sub-shell exits.

    exec 1>log.out 2>&1

    Redirect stdout to file log.out then redirect stderr to stdout. Note that the order is important when you want them going to the same file. stdout must be redirected before stderr is redirected to stdout.

References: https://serverfault.com/questions/103501/how-can-i-fully-log-all-bash-scripts-actions
