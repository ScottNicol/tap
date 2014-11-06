tap
===

tee(1) that you can turn on or off at will

tap is a tool for copying output along a command pipeline, similar to tee.
The difference, however, is that the replicated output can be turned on or
off at any time, without affecting the rest of the pipeline.  When off,
tap still passes stdin through to stdout, but the replicated output
is bypassed.

Usage:

    tap <tapname>
    opentap <tapname>

Where tapname is the name of the tap you want to assign (tap) or use (opentap).


Environment Variables:
<pre>
HOME - user's home directory
TAPLOG - location where tap names are stored.  If not set, tap names are
    stored in $HOME/.tap
</pre>


Examples:

The following shows tap and opentap used to check the progress of
a command line that might take a lot of time and produce a lot of
output.  Whenever opentap is used, the current output is replicated
on opentap's stdout.

<pre>
$ find / -type f 2>/dev/null | tap bf | xargs grep xyzzy | tap grepmagic >grep.out &
$ opentap bf
[current output from find]
^C
$ opentap grepmagic
[current output from grep]
^C
$ opentap bf
[current output from find]
^C
...etc
</pre>
