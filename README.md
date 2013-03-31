graphite-zenossMetrics
======================

Automatically creates symlinks to Zenoss performance data rrd files for visualisation and analysis in Graphite.

Zenoss is a unified monitoring solution, available in Enterprise and Open Source versions. Zenoss collects performance metric values and stored them in rrd files.

Graphite natively supports rrd. By symlinking to Zenoss rrd files from a Graphite server, Graphite's powerful visualisation, analytics and dashboarding may be applied to Zenoss metrics for free.

*Note: graphite-zenossMetrics is currently designed to symlink metrics for Linux servers. However adding Windows, Network and other devices would be trivial.

Requirements
----------------------

* A Zenoss installation, with Zenoss performance data directory, (/opt/zenoss/perf/ by default) exported as an NFS share.
* A Graphite installation, with rrd enabled and the Zenoss performance data NFS share mounted.

Configuration
----------------------

Configuration is set in config.py.

Set zenossRoot to the location of the Zenoss performance data NFS mount:

'''
# root directory of Zenoss metric RRD files
# this should be an nfs mount to /opt/zenoss/perf on the Zenoss server
zenossRoot = '/mnt/zenossPerf'
'''

Set graphiteRoot to the location under which the Zenoss metrics will be symlinked:

'''
# root path of Zenoss metrics
graphiteRoot = '/opt/grahite/storage/rrd/Zenoss/Linux'
'''

Add regexes that match the hostnames of the Linux devices whose metrics you wish to symlink to:

'''
# regexes to match Zenoss Linux server device names
devicePatterns = [
    '.*'
]
'''

Usage
----------------------

Once configuration is complete, simply run graphite-zenossMetrics.py with Python:

'''>python graphite-zenossMetrics.py'''

To keep your symlinks up to date, create a cron job to run this regularly. Any new devices will be added and any devices no longer in Zenoss will be removed.