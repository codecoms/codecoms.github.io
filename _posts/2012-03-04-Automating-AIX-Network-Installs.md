---
layout: post
title:  "Automating AIX Network Installs"
subtitle: "Example script used to build out a new AIX p770 environment using IBM Hardware Management Console (HMC)"
author: "Kevin"
date:   2012-03-04 18:27:17
tags:
  - Unix Administration
  - AIX
  - Shell Scripting
categories: UNIX

---


The UNIX gurus at IBM in Austin, Texas developed a useful but barely-known utility on the Hardware Management Console (HMC) used to control IBM System-p servers.

Here is an example script we've recently used to build out a new AIX p770 environment.

You will need a Network Installation Management (NIM) server and I would suggest setting up public/private keys from an administration server to the HMC and the NIM server.

Normally you would login to the NIM server, set up a network installation session, then login to the console and go through a series of BIOS-like menus to boot and install the software image.

Using <a href="https://www.ibm.com/developerworks/wikis/display/virtualization/lpar_netboot">lpar_netboot</a>, the following script does this manual procedure in one line:


`# flash-lpar.sh hmc1 p770-a jabba.codecoms.com 10.1.1.150 10.1.1.1`


{% highlight sh %}

#!/bin/sh
# flash-lpar.sh

# setvar allows spacing in our variable definitions
setvar() {
  variable="$1"; shift
  value="$@";    eval $variable=\"$value\"
}

if [ "$#" -ne 6 ]; then
  echo "usage $0 hmc frame lpar hostname ip gw" 1>2
  exit 1
fi

setvar aix_level  6100-06-06

setvar nim        nim
setvar nim_ip     10.1.1.10
setvar hmc_user   hscroot

setvar hmc        "$1"
setvar frame      "$2"
setvar lpar       "$3"
setvar profile    default

setvar hostname   "$4"
setvar hostip     "$5"
setvar hostgw     "$6"

setvar nim_resolv   resolv_conf
setvar nim_spot     ${aix_level}-spot
setvar nim_lpp      ${aix_level}-lpp_source
setvar nim_bosinst  ${aix_level}-bosinst
setvar nim_mksysb   mksysb-${host}
setvar nim_imgdata  image_data-${host}

# reset host for new network install...

ssh ${nim} "
  nim -F -o reset client-${hostname};
  nim -o deallocate -a subclass=all client-${hostname};"


# prepare host for network install...

ssh ${nim} "
  nim -o bos_inst                         \
         -a source=mksysb                 \
         -a accept_licenses=yes           \
         -a boot_client=no                \
         -a bosinst_data=${nim_bosinst}   \
         -a resolv_conf=${nim_resolv}     \
         -a spot=${nim_spot}              \
         -a lpp_source=${nim_lpp}         \
         -a mksysb=${nim_mksysb}          \
         -a image_data=${nim_imgdata}     \
         client-${hostname}"

# network install host and create a virtual terminal...

ssh ${hmc_user}@${hmc} \
  "lpar_netboot -x -D -f -i -t ent -s auto -d auto \
   -S ${nim_ip} -G ${client_gw} -C ${client_ip}  \
   ${lpar} ${profile} ${frame}"

ssh -t ${hmc_user}@${hmc} \
  "mkvterm -m ${frame} -p ${lpar}"

{% endhighlight %}


<p>&nbsp;</p>
{% include twitter_plug.html %}