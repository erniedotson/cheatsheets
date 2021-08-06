# Linux Commands

## Table of Contents

<!-- markdownlint-disable MD004 -->

<!-- toc -->

- [System Information](#system-information)
- [File Permissions](#file-permissions)
- [Archives](#archives)
  * [Tar and GZip/BZip2 Archives](#tar-and-gzipbzip2-archives)
  * [Zip Archives](#zip-archives)
- [Misc](#misc)
- [Installing software from source](#installing-software-from-source)
- [References](#references)

<!-- tocstop -->

<!-- markdownlint-enable MD004 -->

## System Information

| Action | Command |
| ------ | ------- |
| Print all system information | `uname -a` |
| Print the kernel release | `uname -r` |
| Show which version of redhat installed | `cat /etc/redhat-release` |
| Get distro information for modern releases | `cat /etc/os_release` |
| Show how long the system has been running + load | `uptime` |
| Show system host name | `hostname` |
| Display the IP addresses of the host | `hostname -I` or `ifconfig` or `ip addr` |
| Show system reboot history | `last reboot` |
| Show the current date and time | `date` |
| Show this month's calendar | `cal` |
| Show who is logged on and what they are doing | `w` |

## File Permissions

| Action | Command |
| ------ | ------- |
| Change owner and group | `chown user:group file` |
| Change mode (permissions) | `chmod octal file` |
| Make file executable for all | `chmod +x file` |

```text
        PERMISSION      EXAMPLE

         U   G   W
        rwx rwx rwx     chmod 777 filename
        rwx rwx r-x     chmod 775 filename
        rwx r-x r-x     chmod 755 filename
        rw- rw- r--     chmod 664 filename
        rw- r-- r--     chmod 644 filename

        LEGEND
        U = User
        G = Group
        W = World

        r = Read (4)
        w = write (2)
        x = execute (1)
        - = no access
```

## Archives

### Tar and GZip/BZip2 Archives

| Action | Command |
| ------ | ------- |
| Create tar archive | `tar -cf archive.tar dir-to-tar` |
| Extract tar archive | `tar -xf archive.tar` |
| List contents of a tar archive | `tar -tvf archive.tar` |
| Create gzip compressed tar | `tar -czf archive.tar.gz files` |
| Extract gzip compressed tar | `tar -xzf archive.tar.gz dir` |
| List contents of a gzip compressed tar | `tar -ztvf archive.tar.gz` |
| Create bzip2 compresssed tar | `tar -cjf archive.tar.bz2 dir-to-tar` |
| Extract bzip2 compressed tar | `tar -xjf archive.tar.gz2` |
| List contents of a bzip2 compressed tar | `tar -jtvf archive.tar.bz2` |
| Create compressed gzip file (file.txt will be removed) | `gzip file.txt` |
| Create compressed gzip file (keeping file.txt) | `gzip -c file.txt > file.txt.gz` |

### Zip Archives

| Action | Command |
| ------ | ------- |
| Unzip zip archive | `unzip archive.zip` |
| Unzip zip archive to destination | `unzip archive.zip -d /dest/dir` |
| Unzip password protected zip archive | `unzip -P password archive.zip` |
| List contents of zip archive | `unzip -l archive.zip` |

## Misc

| Action | Command |
| ------ | ------- |
| Find all .sh scripts and make them executable | `find . -name "*.sh" \| xargs chmod +x` |
| Find all .sh scripts and convert to LF endings | `find . -name "*.sh" \| xargs dos2unix` |
| Find all .sh files and search for string | `find . -name '*.sh' \| xargs grep 'echo'` |
| Find all .sh files and copy | `find . -name '*.sh' -exec cp {} /dest/dir/ \;`
| Run programs and summarize system resource usage | `time ls -l` |
| Create symlink | `ln -s the-file mylink` |
| Remove symlink | `rm mylink` |

## Installing software from source

| Action | Command |
| ------ | ------- |
| Build from source | `./configure && make && make install` |
| Install a Debian package | `dpkg -i package.deb` |
| Install a RPM package | `rpm -Uvh package.rpm` |

## References

- [/etc/os_release Documentation](https://www.freedesktop.org/software/systemd/man/os-release.html)
- [Linux Commands Cheat Sheet](https://www.linuxtrainingacademy.com/linux-commands-cheat-sheet/)
- [Package Management Cheat Sheet](https://distrowatch.com/dwres.php?resource=package-management)
