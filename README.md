# 1-Natours
What if there was one resource, one place, where you could learn all the advanced and modern CSS techniques and properties




IF YOU HAVE V U L N E R A B I L I T Y PROBLEM WITH Package-lock.json---TRY this!


                                               V U L N E R A B I L I T Y
If a tar file contains a hardlink to an existing file on the filesystem, and then a subsequent regular file with the same name as this hardlink, the contents of the regular file will overwrite the contents of the original file.

For example, the attached file, hardlink_exploit.tar.gz, contains two relevant files. First, a hardlink to /tmp/overwriteme called hardboi/yyy, and second, a regular file called hardboi/yyy containing oops.

To demonstrate this vulnerability:

Make a file called /tmp/overwriteme with whatever contents
Extract the attached tar archive using the following code:
tar = require('tar')

tar.x(
  {
    file: 'hardlink_exploit.tar.gz'
  }
).then(_=> { console.log("done") })
Observe the contents of /tmp/overwriteme are now "oops"
I'm not sure what the best way to resolve this vulnerability is. My local copy of GNU Tar isn't vulnerable because by default it doesn't allow hardlinks that point to an absolute file or that try to directory traverse above the parent:

$ tar -xvf hardlink_pkg.tar.gz
hardboi/
tar: Removing leading `/' from hard link targets
hardboi/yyy
tar: hardboi/yyy: Cannot hard link to ‘tmp/overwriteme’: No such file or directory
hardboi/yyy
hardboi/package.json
tar: Exiting with failure status due to previous errors
Impact
Applications, of which there are probably many, that rely on node-tar to be secure-by-default when extracting a tar file are in fact vulnerable. Unless hardlinks are explicitly disabled as in pacote, arbitrary files can be overwritten with the permissions of the user running node-tar.
