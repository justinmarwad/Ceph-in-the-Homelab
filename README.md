# Ceph in the Homelab # 

Let's be honest, learning ceph is hard for newbies. I wrote this documentation to document the process of me learning ceph and to hopefully help anyone else who is also trying to learn ceph to implement it in their homelab. 

## Install

It's as simple as `sudo snap install microceph` 

## Configure 

Configuration is as simple as `sudo microceph init` and then enter the correct information. Enter yes to adding nodes and get the token. Then run `sudo microceph cluster add $TOKEN` on the other nodes where $TOKEN is your token.

## Questions 

### Can I use Ceph with a directory? 

Yes, but only by tricking Ceph into thinking it's a block device. See this Reddit for more information: https://www.reddit.com/r/ceph/comments/cjucgz/use_a_directory_for_ceph_osd_location/.  In short: 

```bash
dd if=/dev/zero of=/var/local/osd/blockfile bs=1M count=1024
losetup /dev/loop0 /var/local/osd/blockfile
``` 

And then point ceph to /dev/loop0. Warning: Docker might be using this, so you may have to use loop1 or loop2 if docker is also using loop0. 
