# docker-rpm-buildhost-el6
## Centos 6 RPM Build Host

This is an rpm building environment for RHEL 6 and its derivatives (CentOS 6, Oracle Linux 6, etc).  

You may want to edit the ~builder/.rpmmacros file to suit your details.  Below, I map my personal copy of it into the container.  Without, you can get a generic one there and copy it out to make your own personalization. (packager, distribution, and vendor tags, specifically)

Put your sources in ~builder/rpms/SOURCES, specs in ~builder/rpms/SPECS, and away you go.  It's a good idea to mount ~builder/rpms on an external volume, since these containers are temporary use and you might want to keep these around.

"sudo su -" is set up to add additional packages as needed when building RPMs, and "wget" is included for getting updated sources without exiting the container.

Finally, http://www.rpm.org/max-rpm-snapshot/ is a great reference for learning about building RPMs with rpm-build.

I typically run this container with command similar to:

```
docker run --rm -it \
        --hostname=buildhost_el6 \
        -v /usr/local/src/rpms/SPECS:/home/builder/rpms/SPECS \
        -v /usr/local/src/rpms/SOURCES:/home/builder/rpms/SOURCES \
        -v /usr/local/src/rpms/RPMS:/home/builder/rpms/RPMS \
        -v /usr/local/src/rpms/SRPMS:/home/builder/rpms/SRPMS \
        -v /usr/local/src/rpms/rpmmacros:/home/builder/.rpmmacros \
        guyton/rpm-buildhost-el6
```

Once up, you should start in your SPECS dir, and away you go.

## Things to do

- Get set up for gpg signing
- Better linking with yumrepo container
- Add git if might start needing for source fetching


- Nat

