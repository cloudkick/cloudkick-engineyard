Installing the Cloudkick Agent on Engine Yard
=============================================

Step 1: Retrieving the Cloudkick Engine Yard Overlay
----------------------------------------------------

Make sure that /usr/portage/local exists, then clone the overlay into it

    mkdir -p /usr/portage/local
    cd /usr/portage/local
    git clone git://github.com/cloudkick/cloudkick-engineyard.git

Step 2: Adding the Cloudkick Engine Yard Overlay
------------------------------------------------

Open up /etc/make.conf and add a line to the end:

    PORTDIR_OVERLAY="${PORTDIR_OVERLAY}
                      /usr/portage/local/cloudkick-engineyard"

Step 3: Installing the Cloudkick Agent
--------------------------------------

You should now be able to install the Cloudkick Agent by running

    emerge -a cloudkick-agent

This will also pull in the cloudkick-config tool which helsp you configure the
agent. When they are done installing run.

    cloudkick-config

And provide your Cloudkick username and password when prompted. This will
generate a basic /etc/cloudkick.conf. If this node already appears on your
Cloudkick dashboard then this is all the configuration needed. Otherwise you
will need to specify a node name in /etc/cloudkick.conf as described at
https://support.cloudkick.com/Agent/Cloudkick.conf.

You probably also want to add the agent to the default runlevel:

    rc-update add cloudkick-agent default

Now start the agent

    /etc/init.d/cloudkick-agent start

And log into Cloudkick and make sure the agent is shown as connected in the
Dashboard. If not, check /var/log/cloudkick-agent.log for troubleshooting
information.

Receiving Updates
=================

To update the Cloudkick Agent for Engine Yard, you will need to first pull in any updates to the overlay, then install any available updates.

    cd /usr/portage/local/cloudkick-engineyard
    git pull
    emerge -a cloudkick-agent

Then, once the update is installed

    /etc/init.d/cloudkick-agent restart

At this point you should be running the updated version of the agent.
