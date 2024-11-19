# Mimic

Mimic is the 13th stable release of Ceph. It is named after the Mimic
Octopus (Thaumoctopus mimicus).

## v13.2.10 Mimic

This is the tenth bugfix release of Ceph Mimic, this release fixes an
RGW vulnerability, and we recommend that all Mimic users upgrade.

### Notable Changes

-   CVE 2020 12059: Fix an issue with Post Object Requests with Tagging
    ([issue#44967](http://tracker.ceph.com/issues/44967), Lei Cao,
    Abhishek Lekshmanan)

## v13.2.9 Mimic

This is the ninth and very likely the last stable release in the Ceph
Mimic series. This release fixes bugs across all components and also
contains a RGW security fix. We recommend all Mimic users to upgrade to
this version.

### Notable Changes

-   CVE-2020-1760: Fixed XSS due to RGW GetObject header-splitting
-   The configuration value `osd_calc_pg_upmaps_max_stddev` used for
    upmap balancing has been removed. Instead use the mgr balancer
    config `upmap_max_deviation` which now is an integer number of PGs
    of deviation from the target PGs per OSD. This can be set with a
    command like
    `ceph config set mgr mgr/balancer/upmap_max_deviation 2`. The
    default `upmap_max_deviation` is 1. There are situations where crush
    rules would not allow a pool to ever have completely balanced PGs.
    For example, if crush requires 1 replica on each of 3 racks, but
    there are fewer OSDs in 1 of the racks. In those cases, the
    configuration value can be increased.
-   The `cephfs-data-scan scan_links` command now automatically repair
    inotables and snaptable.

### Changelog

-   bluestore: os/bluestore: fix improper setting of STATE_KV_SUBMITTED
    ([pr#31673](https://github.com/ceph/ceph/pull/31673), Igor Fedotov)
-   ceph-volume/batch: check lvs list before access
    ([pr#34479](https://github.com/ceph/ceph/pull/34479), Jan Fajerski)
-   ceph-volume/batch: fail on filtered devices when non-interactive
    ([pr#33201](https://github.com/ceph/ceph/pull/33201), Jan Fajerski)
-   ceph-volume/batch: return success when all devices are filtered
    ([pr#34476](https://github.com/ceph/ceph/pull/34476), Jan Fajerski)
-   ceph-volume/lvm/activate.py: clarify error message: fsid refers to
    osd_fsid ([pr#32865](https://github.com/ceph/ceph/pull/32865), Yaniv
    Kaul)
-   ceph-volume/test: patch VolumeGroups
    ([pr#32559](https://github.com/ceph/ceph/pull/32559), Jan Fajerski)
-   ceph-volume: Dereference symlink in lvm list
    ([pr#32876](https://github.com/ceph/ceph/pull/32876), Benoît Knecht)
-   ceph-volume: add db and wal support to raw mode
    ([pr#33622](https://github.com/ceph/ceph/pull/33622), Sébastien Han)
-   ceph-volume: add methods to pass filters to pvs, vgs and lvs
    commands ([pr#33215](https://github.com/ceph/ceph/pull/33215),
    Rishabh Dave)
-   ceph-volume: add proper size attribute to partitions
    ([pr#32529](https://github.com/ceph/ceph/pull/32529), Jan Fajerski)
-   ceph-volume: add raw mode
    ([pr#33580](https://github.com/ceph/ceph/pull/33580), Jan Fajerski,
    Sage Weil, Guillaume Abrioux)
-   ceph-volume: add sizing arguments to prepare
    ([pr#33578](https://github.com/ceph/ceph/pull/33578), Jan Fajerski)
-   ceph-volume: add utility functions
    ([pr#32544](https://github.com/ceph/ceph/pull/32544), Mohamad Gebai)
-   ceph-volume: allow raw block devices everywhere
    ([pr#32869](https://github.com/ceph/ceph/pull/32869), Jan Fajerski)
-   ceph-volume: allow to skip restorecon calls
    ([pr#32530](https://github.com/ceph/ceph/pull/32530), Alfredo Deza)
-   ceph-volume: avoid calling zap_lv with a LV-less VG
    ([pr#33610](https://github.com/ceph/ceph/pull/33610), Jan Fajerski)
-   ceph-volume: batch bluestore fix create_lvs call
    ([pr#33579](https://github.com/ceph/ceph/pull/33579), Jan Fajerski)
-   ceph-volume: batch bluestore fix create_lvs call
    ([pr#33623](https://github.com/ceph/ceph/pull/33623), Jan Fajerski)
-   ceph-volume: check if we run in an selinux environment
    ([pr#32866](https://github.com/ceph/ceph/pull/32866), Jan Fajerski)
-   ceph-volume: check if we run in an selinux environment, now also in
    py2 ([pr#32867](https://github.com/ceph/ceph/pull/32867), Jan
    Fajerski)
-   ceph-volume: devices/simple/scan: Fix string in log statement
    ([pr#34444](https://github.com/ceph/ceph/pull/34444), Jan Fajerski)
-   ceph-volume: don\'t create osd\[\'block.db\'\] by default
    ([pr#33626](https://github.com/ceph/ceph/pull/33626), Jan Fajerski)
-   ceph-volume: don\'t remove vg twice when zapping filestore
    ([pr#33615](https://github.com/ceph/ceph/pull/33615), Jan Fajerski)
-   ceph-volume: finer grained availability notion in inventory
    ([pr#33606](https://github.com/ceph/ceph/pull/33606), Jan Fajerski)
-   ceph-volume: fix is_ceph_device for lvm batch
    ([pr#33608](https://github.com/ceph/ceph/pull/33608), Jan Fajerski,
    Dimitri Savineau)
-   ceph-volume: fix the integer overflow
    ([pr#32872](https://github.com/ceph/ceph/pull/32872), dongdong tao)
-   ceph-volume: import mock.mock instead of unittest.mock (py2)
    ([pr#32871](https://github.com/ceph/ceph/pull/32871), Jan Fajerski)
-   ceph-volume: lvm deactivate command
    ([pr#33208](https://github.com/ceph/ceph/pull/33208), Jan Fajerski)
-   ceph-volume: lvm/deactivate: add unit tests, remove \--all
    ([pr#32862](https://github.com/ceph/ceph/pull/32862), Jan Fajerski)
-   ceph-volume: lvm: get_device_vgs() filter by provided prefix
    ([pr#33617](https://github.com/ceph/ceph/pull/33617), Jan Fajerski,
    Yehuda Sadeh)
-   ceph-volume: make get_devices fs location independent
    ([pr#33124](https://github.com/ceph/ceph/pull/33124), Jan Fajerski)
-   ceph-volume: minor clean-up of \"simple scan\" subcommand help
    ([pr#32557](https://github.com/ceph/ceph/pull/32557), Michael
    Fritch)
-   ceph-volume: mokeypatch calls to lvm related binaries
    ([pr#31406](https://github.com/ceph/ceph/pull/31406), Jan Fajerski)
-   ceph-volume: pass journal_size as Size not string
    ([pr#33611](https://github.com/ceph/ceph/pull/33611), Jan Fajerski)
-   ceph-volume: rearrange api/lvm.py
    ([pr#31407](https://github.com/ceph/ceph/pull/31407), Rishabh Dave)
-   ceph-volume: refactor listing.py + fixes
    ([pr#33603](https://github.com/ceph/ceph/pull/33603), Jan Fajerski,
    Rishabh Dave, Theofilos Mouratidis, Guillaume Abrioux)
-   ceph-volume: reject disks smaller then 5GB in inventory
    ([issue#40776](http://tracker.ceph.com/issues/40776),
    [pr#32528](https://github.com/ceph/ceph/pull/32528), Jan Fajerski)
-   ceph-volume: silence \'ceph-bluestore-tool\' failures
    ([pr#33605](https://github.com/ceph/ceph/pull/33605), Sébastien Han)
-   ceph-volume: skip missing interpreters when running tox tests
    ([pr#33489](https://github.com/ceph/ceph/pull/33489), Andrew Schoen)
-   ceph-volume: skip osd creation when already done
    ([pr#33607](https://github.com/ceph/ceph/pull/33607), Guillaume
    Abrioux)
-   ceph-volume: strip \_dmcrypt suffix in simple scan json output
    ([pr#33618](https://github.com/ceph/ceph/pull/33618), Jan Fajerski)
-   ceph-volume: use correct extents if using db-devices and \>1
    osds_per_device
    ([pr#32875](https://github.com/ceph/ceph/pull/32875), Fabian
    Niepelt)
-   ceph-volume: use fsync for dd command
    ([pr#31552](https://github.com/ceph/ceph/pull/31552), Rishabh Dave)
-   ceph-volume: use get_device_vgs in has_common_vg
    ([pr#33609](https://github.com/ceph/ceph/pull/33609), Jan Fajerski)
-   ceph-volume: util: look for executable in \$PATH
    ([pr#32861](https://github.com/ceph/ceph/pull/32861), Shyukri
    Shyukriev)
-   cephfs: cephfs: osdc/objecter: Fix last_sent in scientific format
    and add age to ops
    ([pr#31384](https://github.com/ceph/ceph/pull/31384), Varsha Rao)
-   cephfs: cephfs: test_volume_client: declare only one default for
    python version ([issue#40460](http://tracker.ceph.com/issues/40460),
    [pr#30110](https://github.com/ceph/ceph/pull/30110), Rishabh Dave)
-   cephfs: client: more precise CEPH_CLIENT_CAPS_PENDING_CAPSNAP
    ([pr#31283](https://github.com/ceph/ceph/pull/31283), \"Yan,
    Zheng\")
-   cephfs: client: remove Inode.dir_contacts field and handle bad
    whence value to llseek gracefully
    ([pr#31380](https://github.com/ceph/ceph/pull/31380), Jeff Layton)
-   cephfs: mds: avoid calling clientreplay_done() prematurely
    ([pr#31282](https://github.com/ceph/ceph/pull/31282), \"Yan,
    Zheng\")
-   cephfs: mds: fix assert(omap_num_objs \<= MAX_OBJECTS) of
    OpenFileTable ([pr#32757](https://github.com/ceph/ceph/pull/32757),
    \"Yan, Zheng\")
-   cephfs: mds: fix infinite loop in Locker::file_update_finish
    ([pr#31284](https://github.com/ceph/ceph/pull/31284), \"Yan,
    Zheng\")
-   cephfs: mds: mds returns -5(EIO) error when the deleted file does
    not exist ([pr#31381](https://github.com/ceph/ceph/pull/31381),
    huanwen ren)
-   cephfs: mds: split the dir if the op makes it oversized, because
    some ops maybe in flight
    ([pr#31379](https://github.com/ceph/ceph/pull/31379), simon gao)
-   cephfs: tools/cephfs: make \'cephfs-data-scan scan_links\'
    reconstruct snaptable
    ([pr#31281](https://github.com/ceph/ceph/pull/31281), \"Yan,
    Zheng\")
-   common/config: parse \--log-early option
    ([pr#33130](https://github.com/ceph/ceph/pull/33130), Sage Weil)
-   common: common/admin_socket: Increase socket timeouts
    ([pr#33323](https://github.com/ceph/ceph/pull/33323), Brad Hubbard)
-   common: common/config: update values when they are removed via mon
    ([pr#33327](https://github.com/ceph/ceph/pull/33327), Sage Weil)
-   common: common/util: use ifstream to read from /proc files
    ([pr#32902](https://github.com/ceph/ceph/pull/32902), Kefu Chai,
    songweibin)
-   core,mgr,tests: mgr: Release GIL and Balancer fixes
    ([pr#31957](https://github.com/ceph/ceph/pull/31957), Neha Ojha,
    Kefu Chai, Noah Watkins, David Zafman)
-   core,mgr: mgr/prometheus: assign a value to osd_dev_node when
    obj_store is not filestore or bluestore
    ([pr#31557](https://github.com/ceph/ceph/pull/31557), jiahuizeng)
-   core,tests: qa/tasks/cbt: install python3 deps
    ([pr#34193](https://github.com/ceph/ceph/pull/34193), Sage Weil)
-   core: mon/OSDMonitor: fix format error ceph osd stat \--format json
    ([pr#33322](https://github.com/ceph/ceph/pull/33322), Zheng Yin)
-   core: mon: Don\'t put session during feature change
    ([pr#33154](https://github.com/ceph/ceph/pull/33154), Brad Hubbard)
-   core: osd/PeeringState.cc: don\'t let num_objects become negative
    ([pr#33331](https://github.com/ceph/ceph/pull/33331), Neha Ojha)
-   core: osd/PeeringState.cc: skip peer_purged when discovering all
    missing ([pr#33329](https://github.com/ceph/ceph/pull/33329), Neha
    Ojha)
-   core: osd/PeeringState.h: ignore MLogRec in Peering/GetInfo
    ([pr#33594](https://github.com/ceph/ceph/pull/33594), Neha Ojha)
-   core: osd/PeeringState: do not exclude up from
    acting_recovery_backfill
    ([pr#33324](https://github.com/ceph/ceph/pull/33324), Nathan Cutler,
    xie xingguo)
-   core: osd: Allow 64-char hostname to be added as the \"host\" in
    CRUSH ([pr#33145](https://github.com/ceph/ceph/pull/33145), Michal
    Skalski)
-   core: osd: Diagnostic logging for upmap cleaning
    ([pr#32717](https://github.com/ceph/ceph/pull/32717), David Zafman)
-   core: osd: backfill_toofull seen on cluster where the most full OSD
    is at 1% ([pr#32361](https://github.com/ceph/ceph/pull/32361), David
    Zafman)
-   core: osd: set collection pool opts on collection create, pg load
    ([pr#32125](https://github.com/ceph/ceph/pull/32125), Sage Weil)
-   core: selinux: Allow ceph to read udev db
    ([pr#32258](https://github.com/ceph/ceph/pull/32258), Boris Ranto)
-   core: selinux: Allow ceph-mgr access to httpd dir
    ([pr#34458](https://github.com/ceph/ceph/pull/34458), Brad Hubbard)
-   doc: remove invalid option mon_pg_warn_max_per_osd
    ([pr#31875](https://github.com/ceph/ceph/pull/31875), zhang daolong)
-   doc: doc/\_templates/page.html: redirect to etherpad
    ([pr#32249](https://github.com/ceph/ceph/pull/32249), Neha Ojha)
-   doc: doc/cephfs/client-auth: description and example are
    inconsistent ([pr#32782](https://github.com/ceph/ceph/pull/32782),
    Ilya Dryomov)
-   doc: wrong datatype describing crush_rule
    ([pr#32255](https://github.com/ceph/ceph/pull/32255), Kefu Chai)
-   mgr,pybind: mgr/prometheus: report per-pool pg states
    ([pr#33158](https://github.com/ceph/ceph/pull/33158), Aleksei
    Zakharov)
-   mgr,pybind: mgr/telemetry: check get_metadata return val
    ([pr#33096](https://github.com/ceph/ceph/pull/33096), Yaarit Hatuka)
-   mount.ceph: give a hint message when no mds is up or cluster is
    laggy ([pr#32911](https://github.com/ceph/ceph/pull/32911), Xiubo
    Li)
-   pybind: pybind/mgr: Cancel output color control
    ([pr#31805](https://github.com/ceph/ceph/pull/31805), Zheng Yin)
-   qa: get rid of iterkeys for py3 compatibility
    ([pr#33999](https://github.com/ceph/ceph/pull/33999), Kyr Shatskyy)
-   rbd: creating thick-provision image progress percent info exceeds
    100% ([pr#33318](https://github.com/ceph/ceph/pull/33318), Xiangdong
    Mu)
-   rbd: librbd: diff iterate with fast-diff now correctly includes
    parent ([pr#32470](https://github.com/ceph/ceph/pull/32470), Jason
    Dillaman)
-   rbd: librbd: don\'t call refresh from mirror::GetInfoRequest state
    machine ([pr#32952](https://github.com/ceph/ceph/pull/32952), Mykola
    Golub)
-   rbd: librbd: fix rbd_open_by_id, rbd_open_by_id_read_only
    ([pr#33315](https://github.com/ceph/ceph/pull/33315), yangjun)
-   rbd: nautilus: rbd-mirror: fix \'rbd mirror status\' asok command
    output ([pr#32714](https://github.com/ceph/ceph/pull/32714), Mykola
    Golub)
-   rbd: rbd-mirror: clone v2 mirroring improvements
    ([pr#31520](https://github.com/ceph/ceph/pull/31520), Mykola Golub)
-   rbd: rbd-mirror: improve detection of blacklisted state
    ([pr#33598](https://github.com/ceph/ceph/pull/33598), Mykola Golub)
-   rbd: rbd-mirror: make logrotate work
    ([pr#32598](https://github.com/ceph/ceph/pull/32598), Mykola Golub)
-   rgw: add bucket permission verify when copy obj
    ([pr#31377](https://github.com/ceph/ceph/pull/31377), NancySu05)
-   rgw: add list user admin OP API
    ([pr#31754](https://github.com/ceph/ceph/pull/31754), Oshyn Song)
-   rgw: add missing admin property when sync user info
    ([pr#30804](https://github.com/ceph/ceph/pull/30804), zhang Shaowen)
-   rgw: add num_shards to radosgw-admin bucket stats
    ([pr#31183](https://github.com/ceph/ceph/pull/31183), Paul Emmerich)
-   rgw: adding mfa code validation when bucket versioning status is
    changed ([pr#33303](https://github.com/ceph/ceph/pull/33303), Pritha
    Srivastava)
-   rgw: allow reshard log entries for non-existent buckets to be
    cancelled ([pr#33302](https://github.com/ceph/ceph/pull/33302), J.
    Eric Ivancich)
-   rgw: auto-clean reshard queue entries for non-existent buckets
    ([pr#33300](https://github.com/ceph/ceph/pull/33300), J. Eric
    Ivancich)
-   rgw: change the \"rgw admin status\" \'num_shards\' output to signed
    int ([issue#37645](http://tracker.ceph.com/issues/37645),
    [pr#33305](https://github.com/ceph/ceph/pull/33305), Mark Kogan)
-   rgw: crypt: permit RGW-AUTO/default with SSE-S3 headers
    ([pr#31861](https://github.com/ceph/ceph/pull/31861), Matt Benjamin)
-   rgw: find oldest period and update RGWMetadataLogHistory()
    ([pr#33309](https://github.com/ceph/ceph/pull/33309), Shilpa
    Jagannath)
-   rgw: fix a bug that bucket instance obj can\'t be removed after
    resharding completed
    ([pr#33306](https://github.com/ceph/ceph/pull/33306), zhang Shaowen)
-   rgw: fix bad user stats on versioned bucket after reshard
    ([pr#33304](https://github.com/ceph/ceph/pull/33304), J. Eric
    Ivancich)
-   rgw: fix memory growth while deleting objects with
    ([pr#31378](https://github.com/ceph/ceph/pull/31378), Mark Kogan)
-   rgw: get barbican secret key request maybe return error code
    ([pr#33966](https://github.com/ceph/ceph/pull/33966), Richard
    Bai(白学余))
-   rgw: make max_connections configurable in beast
    ([pr#33341](https://github.com/ceph/ceph/pull/33341), Tiago
    Pasqualini)
-   rgw: making implicit_tenants backwards compatible
    ([issue#24348](http://tracker.ceph.com/issues/24348),
    [pr#33748](https://github.com/ceph/ceph/pull/33748), Marcus Watts)
-   rgw: maybe coredump when reload operator happened
    ([pr#33313](https://github.com/ceph/ceph/pull/33313), Richard
    Bai(白学余))
-   rgw: move forward marker even in case of many rgw.none indexes
    ([pr#33311](https://github.com/ceph/ceph/pull/33311), Ilsoo Byun)
-   rgw: prevent bucket reshard scheduling if bucket is resharding
    ([pr#31299](https://github.com/ceph/ceph/pull/31299), J. Eric
    Ivancich)
-   rgw: update the hash source for multipart entries during resharding
    ([pr#33312](https://github.com/ceph/ceph/pull/33312), dongdong tao)

## v13.2.8 Mimic

This is the eighth release in the Ceph Mimic stable release series. Its
sole purpose is to fix a regression that found its way into the previous
release.

### Notable Changes

-   Due to a missed backport, clusters in the process of being upgraded
    from 13.2.6 to 13.2.7 might suffer an OSD crash in
    build_incremental_map_msg. This regression was reported in
    <https://tracker.ceph.com/issues/43106> and is fixed in 13.2.8 (this
    release). Users of 13.2.6 can upgrade to 13.2.8 directly - i.e.,
    skip 13.2.7 - to avoid this.

### Changelog

-   osd: fix sending incremental map messages (more)
    ([issue#43106](https://tracker.ceph.com/issues/43106),
    [pr#32000](https://github.com/ceph/ceph/pull/32000), Sage Weil)
-   tests: added missing point release versions
    ([pr#32087](https://github.com/ceph/ceph/pull/32087), Yuri
    Weinstein)
-   tests: rgw: add missing force-branch: ceph-mimic for swift tasks
    ([pr#32033](https://github.com/ceph/ceph/pull/32033), Casey Bodley)

## v13.2.7 Mimic

This is the seventh bugfix release of the Mimic v13.2.x long-term stable
release series. All Mimic users are advised to upgrade.

### Notable Changes

MDS:

-   Cache trimming is now throttled. Dropping the MDS cache via the
    \"ceph tell mds.\<foo\> cache drop\" command or large reductions in
    the cache size will no longer cause service unavailability.
-   Behavior with recalling caps has been significantly improved to not
    attempt recalling too many caps at once, leading to instability. MDS
    with a large cache (64GB+) should be more stable.
-   MDS now provides a config option \"mds_max_caps_per_client\"
    (default: 1M) to limit the number of caps a client session may hold.
    Long running client sessions with a large number of caps have been a
    source of instability in the MDS when all of these caps need to be
    processed during certain session events. It is recommended to not
    unnecessarily increase this value.
-   The \"mds_recall_state_timeout\" config parameter has been removed.
    Late client recall warnings are now generated based on the number of
    caps the MDS has recalled which have not been released. The new
    config parameters \"mds_recall_warning_threshold\" (default: 32K)
    and \"mds_recall_warning_decay_rate\" (default: 60s) set the
    threshold for this warning.
-   The \"cache drop\" admin socket command has been removed. The \"ceph
    tell mds.X cache drop\" remains.

OSD:

-   A health warning is now generated if the average osd heartbeat ping
    time exceeds a configurable threshold for any of the intervals
    computed. The OSD computes 1 minute, 5 minute and 15 minute
    intervals with average, minimum and maximum values. New
    configuration option \"mon_warn_on_slow_ping_ratio\" specifies a
    percentage of \"osd_heartbeat_grace\" to determine the threshold. A
    value of zero disables the warning. A new configuration option
    \"mon_warn_on_slow_ping_time\", specified in milliseconds, overrides
    the computed value, causing a warning when OSD heartbeat pings take
    longer than the specified amount. A new admin command \"ceph daemon
    mgr.# dump_osd_network \[threshold\]\" lists all connections with a
    ping time longer than the specified threshold or value determined by
    the config options, for the average for any of the 3 intervals. A
    new admin command \"ceph daemon osd.# dump_osd_network
    \[threshold\]\" does the same but only including heartbeats
    initiated by the specified OSD.
-   The default value of the
    \"osd_deep_scrub_large_omap_object_key_threshold\" parameter has
    been lowered to detect an object with large number of omap keys more
    easily.

RGW:

-   radosgw-admin introduces two subcommands that allow the managing of
    expire-stale objects that might be left behind after a bucket
    reshard in earlier versions of RGW. One subcommand lists such
    objects and the other deletes them. Read the troubleshooting section
    of the dynamic resharding docs for details.

### Changelog

-   bluestore: 50-100% iops lost due to bluefs_preextend_wal_files =
    false ([issue#40280](http://tracker.ceph.com/issues/40280),
    [pr#28574](https://github.com/ceph/ceph/pull/28574), Vitaliy
    Filippov)
-   bluestore: Change default for bluestore_fsck_on_mount_deep as false
    ([pr#29699](https://github.com/ceph/ceph/pull/29699), Neha Ojha)
-   bluestore: \_txc_add_transaction error (39) Directory not empty not
    handled on operation 21 (op 1, counting from 0)
    ([issue#39692](http://tracker.ceph.com/issues/39692),
    [pr#29217](https://github.com/ceph/ceph/pull/29217), Sage Weil)
-   bluestore: apply shared_alloc_size to shared device with log level
    change ([pr#30219](https://github.com/ceph/ceph/pull/30219), Vikhyat
    Umrao, Josh Durgin, Sage Weil, Igor Fedotov)
-   bluestore: avoid length overflow in extents returned by Stupid
    Allocator ([issue#40758](http://tracker.ceph.com/issues/40758),
    [issue#40703](http://tracker.ceph.com/issues/40703),
    [pr#29024](https://github.com/ceph/ceph/pull/29024), Igor Fedotov)
-   bluestore: common/options: Set concurrent bluestore rocksdb
    compactions to 2
    ([pr#30150](https://github.com/ceph/ceph/pull/30150), Mark Nelson)
-   bluestore: default to bitmap allocator for bluestore/bluefs
    ([pr#28970](https://github.com/ceph/ceph/pull/28970), Igor Fedotov)
-   bluestore: dump before \"no-spanning blob id\" abort
    ([pr#28029](https://github.com/ceph/ceph/pull/28029), Igor Fedotov)
-   bluestore: fix \>2GB bluefs writes
    ([pr#28967](https://github.com/ceph/ceph/pull/28967), Sage Weil,
    kungf)
-   bluestore: fix duplicate allocations in bmap allocator
    ([issue#40080](http://tracker.ceph.com/issues/40080),
    [pr#28645](https://github.com/ceph/ceph/pull/28645), Igor Fedotov)
-   bluestore: load OSD all compression settings unconditionally
    ([issue#40480](http://tracker.ceph.com/issues/40480),
    [pr#28894](https://github.com/ceph/ceph/pull/28894), Igor Fedotov)
-   build/ops: Cython 0.29 removed support for subinterpreters: raises
    ImportError: Interpreter change detected
    ([issue#39593](http://tracker.ceph.com/issues/39593),
    [issue#39592](http://tracker.ceph.com/issues/39592),
    [pr#27971](https://github.com/ceph/ceph/pull/27971), Kefu Chai, Tim
    Serong)
-   build/ops: admin/build-doc: use python3
    ([pr#30663](https://github.com/ceph/ceph/pull/30663), Kefu Chai)
-   build/ops: admin/build-doc: use python3 (follow-on fix)
    ([pr#30687](https://github.com/ceph/ceph/pull/30687), Nathan Cutler)
-   build/ops: backport miscellaneous install-deps.sh and ceph.spec.in
    fixes from master
    ([issue#37707](http://tracker.ceph.com/issues/37707),
    [pr#30718](https://github.com/ceph/ceph/pull/30718), Jeff Layton,
    Kefu Chai, Nathan Cutler, Brad Hubbard, Changcheng Liu, Sebastian
    Wagner, Yunchuan Wen, Tomasz Setkowski, Zack Cerza)
-   build/ops: ceph.spec.in: reserve 2500MB per build job
    ([pr#30355](https://github.com/ceph/ceph/pull/30355), Dan van der
    Ster)
-   build/ops: cmake,run-make-check.sh: disable SPDK by default
    ([pr#30183](https://github.com/ceph/ceph/pull/30183), Kefu Chai)
-   build/ops: cmake: detect armv8 crc and crypto feature using
    CHECK_C_COMPILER_FLAG
    ([issue#17516](http://tracker.ceph.com/issues/17516),
    [pr#30713](https://github.com/ceph/ceph/pull/30713), Kefu Chai)
-   build/ops: do_cmake.sh: source not found
    ([issue#39981](http://tracker.ceph.com/issues/39981),
    [issue#40005](http://tracker.ceph.com/issues/40005),
    [pr#28217](https://github.com/ceph/ceph/pull/28217), Nathan Cutler)
-   build/ops: fix build fail related to PYTHON_EXECUTABLE variable
    ([pr#30260](https://github.com/ceph/ceph/pull/30260), Ilsoo Byun)
-   build/ops: install-deps.sh: Remove CR repo
    ([issue#13997](http://tracker.ceph.com/issues/13997),
    [pr#30128](https://github.com/ceph/ceph/pull/30128), Alfredo Deza,
    Brad Hubbard)
-   build/ops: install-deps.sh: install [python\*-devel]{.title-ref} for
    python\*rpm-macros
    ([pr#30244](https://github.com/ceph/ceph/pull/30244), Kefu Chai)
-   build/ops: make \"patch\" build dependency explicit
    ([issue#40269](http://tracker.ceph.com/issues/40269),
    [issue#40175](http://tracker.ceph.com/issues/40175),
    [pr#29150](https://github.com/ceph/ceph/pull/29150), Nathan Cutler)
-   build/ops: python3-cephfs should provide python36-cephfs
    ([pr#30982](https://github.com/ceph/ceph/pull/30982), Kefu Chai)
-   build/ops: rpm: always build ceph-test package
    ([pr#30188](https://github.com/ceph/ceph/pull/30188), Nathan Cutler)
-   ceph-volume: PVolumes.filter shouldn\'t purge itself
    ([pr#30806](https://github.com/ceph/ceph/pull/30806), Rishabh Dave)
-   ceph-volume: VolumeGroups.filter shouldn\'t purge itself
    ([pr#30808](https://github.com/ceph/ceph/pull/30808), Rishabh Dave)
-   ceph-volume: add Ceph\'s device id to inventory
    ([pr#31211](https://github.com/ceph/ceph/pull/31211), Sebastian
    Wagner)
-   ceph-volume: api/lvm: check if list of LVs is empty
    ([pr#31229](https://github.com/ceph/ceph/pull/31229), Rishabh Dave)
-   ceph-volume: assume msgrV1 for all branches containing mimic
    ([pr#31615](https://github.com/ceph/ceph/pull/31615), Jan Fajerski)
-   ceph-volume: batch functional idempotency test fails since message
    is now on stderr
    ([pr#29688](https://github.com/ceph/ceph/pull/29688), Jan Fajerski)
-   ceph-volume: broken assertion errors after pytest changes
    ([pr#28948](https://github.com/ceph/ceph/pull/28948), Alfredo Deza)
-   ceph-volume: do not fail when trying to remove crypt mapper
    ([pr#30555](https://github.com/ceph/ceph/pull/30555), Guillaume
    Abrioux)
-   ceph-volume: does not recognize wal/db partitions created by
    ceph-disk ([pr#29463](https://github.com/ceph/ceph/pull/29463), Jan
    Fajerski)
-   ceph-volume: ensure device lists are disjoint
    ([pr#30334](https://github.com/ceph/ceph/pull/30334), Jan Fajerski)
-   ceph-volume: extend batch
    ([issue#40919](http://tracker.ceph.com/issues/40919),
    [pr#29243](https://github.com/ceph/ceph/pull/29243), Andrew Schoen,
    Jan Fajerski, Sébastien Han, Volker Theile)
-   ceph-volume: fix stderr failure to decode/encode when redirected
    ([pr#30301](https://github.com/ceph/ceph/pull/30301), Alfredo Deza)
-   ceph-volume: fix warnings raised by pytest
    ([pr#30678](https://github.com/ceph/ceph/pull/30678), Rishabh Dave)
-   ceph-volume: implement \_\_format\_\_ in Size to format sizes in py3
    ([pr#30333](https://github.com/ceph/ceph/pull/30333), Jan Fajerski)
-   ceph-volume: look for rotational data in lsblk
    ([pr#26991](https://github.com/ceph/ceph/pull/26991), Andrew Schoen)
-   ceph-volume: lvm.activate: Return an error if WAL/DB devices absent
    ([pr#29039](https://github.com/ceph/ceph/pull/29039), David Casier)
-   ceph-volume: lvm.zap fix cleanup for db partitions
    ([issue#40664](http://tracker.ceph.com/issues/40664),
    [pr#30303](https://github.com/ceph/ceph/pull/30303), Dominik Csapak)
-   ceph-volume: minor optimizations related to class Volumes\'s use
    ([pr#30096](https://github.com/ceph/ceph/pull/30096), Rishabh Dave)
-   ceph-volume: miscellaneous backports
    ([pr#31227](https://github.com/ceph/ceph/pull/31227), Mohamad Gebai,
    Andrew Schoen)
-   ceph-volume: missing string substitution when reporting mounts
    ([issue#40977](http://tracker.ceph.com/issues/40977),
    [pr#29350](https://github.com/ceph/ceph/pull/29350), Shyukri
    Shyukriev)
-   ceph-volume: more mimic backports
    ([pr#29631](https://github.com/ceph/ceph/pull/29631), Andrew Schoen,
    Alfredo Deza)
-   ceph-volume: more missing mimic backports
    ([pr#31362](https://github.com/ceph/ceph/pull/31362), Mohamad Gebai,
    Kefu Chai)
-   ceph-volume: pre-install python-apt and its variants before test
    runs ([pr#30295](https://github.com/ceph/ceph/pull/30295), Alfredo
    Deza)
-   ceph-volume: prints errors to stdout with \--format json
    ([issue#38548](http://tracker.ceph.com/issues/38548),
    [pr#29507](https://github.com/ceph/ceph/pull/29507), Jan Fajerski)
-   ceph-volume: prints log messages to stdout
    ([pr#29602](https://github.com/ceph/ceph/pull/29602), Jan Fajerski,
    Alfredo Deza, Kefu Chai)
-   ceph-volume: replace testinfra command with py.test
    ([pr#28930](https://github.com/ceph/ceph/pull/28930), Alfredo Deza)
-   ceph-volume: simple functional tests drop test for lvm zap
    ([pr#29661](https://github.com/ceph/ceph/pull/29661), Jan Fajerski)
-   ceph-volume: simple: when \'type\' file is not present activate
    fails ([pr#29417](https://github.com/ceph/ceph/pull/29417), Jan
    Fajerski, Alfredo Deza)
-   ceph-volume: tests add a sleep in tox for slow OSDs after booting
    ([pr#28947](https://github.com/ceph/ceph/pull/28947), Alfredo Deza)
-   ceph-volume: tests set the noninteractive flag for Debian
    ([pr#29900](https://github.com/ceph/ceph/pull/29900), Alfredo Deza)
-   ceph-volume: update testing playbook \'deploy.yml\'
    ([pr#29074](https://github.com/ceph/ceph/pull/29074), Andrew Schoen,
    Guillaume Abrioux)
-   ceph-volume: use the OSD identifier when reporting success
    ([pr#29770](https://github.com/ceph/ceph/pull/29770), Alfredo Deza)
-   ceph-volume: zap always skips block.db, leaves them around
    ([issue#40664](http://tracker.ceph.com/issues/40664),
    [pr#30306](https://github.com/ceph/ceph/pull/30306), Alfredo Deza)
-   ceph_detect_init: Add support for ALT Linux
    ([pr#27028](https://github.com/ceph/ceph/pull/27028), Andrey
    Bychkov)
-   cephfs: MDSTableServer.cc: 83: FAILED assert(version == tid)
    ([issue#39212](http://tracker.ceph.com/issues/39212),
    [issue#38835](http://tracker.ceph.com/issues/38835),
    [pr#29222](https://github.com/ceph/ceph/pull/29222), \"Yan, Zheng\")
-   cephfs: avoid map been inserted by mistake
    ([pr#29833](https://github.com/ceph/ceph/pull/29833),
    XiaoGuoDong2019)
-   cephfs: ceph-fuse: client hang because its bad session
    PipeConnection to mds
    ([issue#39305](http://tracker.ceph.com/issues/39305),
    [issue#39685](http://tracker.ceph.com/issues/39685),
    [pr#29200](https://github.com/ceph/ceph/pull/29200), Guan yunfei)
-   cephfs: client: EINVAL may be returned when offset is 0
    ([pr#30932](https://github.com/ceph/ceph/pull/30932), wenpengLi)
-   cephfs: client: \_readdir_cache_cb() may use the readdir_cache
    already clear ([issue#41148](http://tracker.ceph.com/issues/41148),
    [pr#30933](https://github.com/ceph/ceph/pull/30933), huanwen ren)
-   cephfs: client: add procession of SEEK_HOLE and SEEK_DATA in lseek
    ([pr#30918](https://github.com/ceph/ceph/pull/30918), Shen Hang)
-   cephfs: client: bump ll_ref from int32 to uint64_t
    ([pr#29187](https://github.com/ceph/ceph/pull/29187), Xiaoxi CHEN)
-   cephfs: client: ceph.dir.rctime xattr value incorrectly prefixes 09
    to the nanoseconds component
    ([issue#40168](http://tracker.ceph.com/issues/40168),
    [pr#28501](https://github.com/ceph/ceph/pull/28501), David
    Disseldorp)
-   cephfs: client: fix bad error handling in \_lookup_parent
    ([issue#40085](http://tracker.ceph.com/issues/40085),
    [pr#29609](https://github.com/ceph/ceph/pull/29609), Jeff Layton)
-   cephfs: client: nfs-ganesha with cephfs client, removing dir reports
    not empty ([issue#40746](http://tracker.ceph.com/issues/40746),
    [pr#30443](https://github.com/ceph/ceph/pull/30443), Peng Xie)
-   cephfs: client: return -EIO when sync file which unsafe reqs have
    been dropped ([issue#40877](http://tracker.ceph.com/issues/40877),
    [pr#30241](https://github.com/ceph/ceph/pull/30241), simon gao)
-   cephfs: client: set snapdir\'s link count to 1
    ([pr#30108](https://github.com/ceph/ceph/pull/30108), \"Yan,
    Zheng\")
-   cephfs: client: support the fallocate() when fuse version \>= 2.9
    ([issue#40615](http://tracker.ceph.com/issues/40615),
    [pr#30228](https://github.com/ceph/ceph/pull/30228), huanwen ren)
-   cephfs: client: unlink dentry for inode with llref=0
    ([issue#40960](http://tracker.ceph.com/issues/40960),
    [pr#29479](https://github.com/ceph/ceph/pull/29479), Xiaoxi CHEN)
-   cephfs: fix a memory leak
    ([pr#29915](https://github.com/ceph/ceph/pull/29915),
    XiaoGuoDong2019)
-   cephfs: getattr on snap inode stuck
    ([issue#40437](http://tracker.ceph.com/issues/40437),
    [pr#29230](https://github.com/ceph/ceph/pull/29230), \"Yan, Zheng\")
-   cephfs: kcephfs TestClientLimits.test_client_pin fails with client
    caps fell below min
    ([issue#38270](http://tracker.ceph.com/issues/38270),
    [issue#38687](http://tracker.ceph.com/issues/38687),
    [pr#29211](https://github.com/ceph/ceph/pull/29211), \"Yan, Zheng\")
-   cephfs: mds: Fix duplicate client entries in eviction list
    ([pr#30950](https://github.com/ceph/ceph/pull/30950), Sidharth
    Anupkrishnan)
-   cephfs: mds: avoid sending too many osd requests at once after mds
    restarts ([issue#40042](http://tracker.ceph.com/issues/40042),
    [issue#40028](http://tracker.ceph.com/issues/40028),
    [pr#28650](https://github.com/ceph/ceph/pull/28650), simon gao)
-   cephfs: mds: behind on trimming and \[dentry\] was purgeable but no
    longer is! ([issue#39223](http://tracker.ceph.com/issues/39223),
    [issue#38679](http://tracker.ceph.com/issues/38679),
    [pr#29224](https://github.com/ceph/ceph/pull/29224), \"Yan, Zheng\")
-   cephfs: mds: cannot switch mds state from standby-replay to active
    ([issue#40213](http://tracker.ceph.com/issues/40213),
    [pr#29232](https://github.com/ceph/ceph/pull/29232), \"Yan, Zheng\",
    simon gao)
-   cephfs: mds: change how mds revoke stale caps
    ([issue#38043](http://tracker.ceph.com/issues/38043),
    [issue#17854](http://tracker.ceph.com/issues/17854),
    [pr#28585](https://github.com/ceph/ceph/pull/28585), \"Yan, Zheng\",
    Rishabh Dave)
-   cephfs: mds: check dir fragment to split dir if mkdir makes it
    oversized ([issue#39689](http://tracker.ceph.com/issues/39689),
    [pr#28381](https://github.com/ceph/ceph/pull/28381), Erqi Chen)
-   cephfs: mds: cleanup unneeded client_snap_caps when splitting snap
    inode ([issue#39987](http://tracker.ceph.com/issues/39987),
    [pr#30234](https://github.com/ceph/ceph/pull/30234), \"Yan, Zheng\")
-   cephfs: mds: delay exporting directory whose pin value exceeds max
    rank id ([issue#40603](http://tracker.ceph.com/issues/40603),
    [pr#29940](https://github.com/ceph/ceph/pull/29940), Zhi Zhang)
-   cephfs: mds: destroy reconnect msg when it is from non-existent
    session to avoid memory leak
    ([issue#40588](http://tracker.ceph.com/issues/40588),
    [pr#28796](https://github.com/ceph/ceph/pull/28796), Shen Hang)
-   cephfs: mds: evict an unresponsive client only when another client
    wants its caps ([pr#30239](https://github.com/ceph/ceph/pull/30239),
    Rishabh Dave)
-   cephfs: mds: fix SnapRealm::resolve_snapname for long name
    ([issue#39472](http://tracker.ceph.com/issues/39472),
    [pr#28186](https://github.com/ceph/ceph/pull/28186), \"Yan, Zheng\")
-   cephfs: mds: fix corner case of replaying open sessions
    ([pr#28579](https://github.com/ceph/ceph/pull/28579), \"Yan,
    Zheng\")
-   cephfs: mds: high debug logging with many subtrees is slow
    ([issue#38875](http://tracker.ceph.com/issues/38875),
    [pr#29219](https://github.com/ceph/ceph/pull/29219), Rishabh Dave)
-   cephfs: mds: make MDSIOContextBase delete itself when shutting down
    ([pr#30417](https://github.com/ceph/ceph/pull/30417), Xuehan Xu)
-   cephfs: mds: mds_cap_revoke_eviction_timeout is not used to
    initialize Server::cap_revoke_eviction_timeout
    ([issue#38844](http://tracker.ceph.com/issues/38844),
    [issue#39210](http://tracker.ceph.com/issues/39210),
    [pr#29220](https://github.com/ceph/ceph/pull/29220), simon gao)
-   cephfs: mds: output lock state in format dump
    ([issue#39669](http://tracker.ceph.com/issues/39669),
    [issue#39645](http://tracker.ceph.com/issues/39645),
    [pr#28274](https://github.com/ceph/ceph/pull/28274), Zhi Zhang)
-   cephfs: mds: remove cache drop admin socket command
    ([issue#38020](http://tracker.ceph.com/issues/38020),
    [issue#38099](http://tracker.ceph.com/issues/38099),
    [pr#29210](https://github.com/ceph/ceph/pull/29210), Patrick
    Donnelly)
-   cephfs: mds: reset heartbeat during long-running loops in recovery
    ([issue#40222](http://tracker.ceph.com/issues/40222),
    [pr#28918](https://github.com/ceph/ceph/pull/28918), \"Yan, Zheng\")
-   cephfs: mds: stopping MDS with a large cache (40+GB) causes it to
    miss heartbeats
    ([issue#38022](http://tracker.ceph.com/issues/38022),
    [issue#38129](http://tracker.ceph.com/issues/38129),
    [issue#37723](http://tracker.ceph.com/issues/37723),
    [issue#38131](http://tracker.ceph.com/issues/38131),
    [pr#28452](https://github.com/ceph/ceph/pull/28452), Patrick
    Donnelly)
-   cephfs: mds: there is an assertion when calling Beacon::shutdown()
    ([issue#39215](http://tracker.ceph.com/issues/39215),
    [issue#38822](http://tracker.ceph.com/issues/38822),
    [pr#29223](https://github.com/ceph/ceph/pull/29223), huanwen ren)
-   cephfs: mount.ceph.c: do not pass nofail to the kernel
    ([issue#39233](http://tracker.ceph.com/issues/39233),
    [pr#28090](https://github.com/ceph/ceph/pull/28090), Kenneth
    Waegeman)
-   cephfs: mount.ceph: properly handle -o strictatime
    ([pr#30240](https://github.com/ceph/ceph/pull/30240), Jeff Layton)
-   cephfs: mount: key parsing fail when doing a remount
    ([issue#40165](http://tracker.ceph.com/issues/40165),
    [pr#29225](https://github.com/ceph/ceph/pull/29225), Luis Henriques)
-   cephfs: pybind: added lseek()
    ([issue#39679](http://tracker.ceph.com/issues/39679),
    [pr#28337](https://github.com/ceph/ceph/pull/28337), Xiaowei Chu)
-   cephfs: test_volume_client: fix test_put_object_versioned()
    ([issue#39405](http://tracker.ceph.com/issues/39405),
    [issue#39510](http://tracker.ceph.com/issues/39510),
    [pr#30236](https://github.com/ceph/ceph/pull/30236), Rishabh Dave)
-   common/ceph_context: avoid unnecessary wait during service thread
    shutdown ([pr#31096](https://github.com/ceph/ceph/pull/31096), Jason
    Dillaman)
-   common/options.cc: Lower the default value of
    osd_deep_scrub_large_omap_object_key_threshold
    ([pr#29174](https://github.com/ceph/ceph/pull/29174), Neha Ojha)
-   common/util: handle long lines in /proc/cpuinfo
    ([issue#39475](http://tracker.ceph.com/issues/39475),
    [issue#38296](http://tracker.ceph.com/issues/38296),
    [pr#28206](https://github.com/ceph/ceph/pull/28206), Sage Weil)
-   common: Keyrings created by ceph auth get are not suitable for ceph
    auth import ([issue#22227](http://tracker.ceph.com/issues/22227),
    [issue#40547](http://tracker.ceph.com/issues/40547),
    [pr#28741](https://github.com/ceph/ceph/pull/28741), Kefu Chai)
-   common: data race in OutputDataSocket
    ([issue#40268](http://tracker.ceph.com/issues/40268),
    [issue#40188](http://tracker.ceph.com/issues/40188),
    [pr#29201](https://github.com/ceph/ceph/pull/29201), Casey Bodley)
-   common: parse ISO 8601 datetime format
    ([issue#40088](http://tracker.ceph.com/issues/40088),
    [pr#28326](https://github.com/ceph/ceph/pull/28326), Sage Weil)
-   core: .mgrstat failed to decode mgrstat state; luminous dev version?
    ([issue#38852](http://tracker.ceph.com/issues/38852),
    [issue#38839](http://tracker.ceph.com/issues/38839),
    [pr#29249](https://github.com/ceph/ceph/pull/29249), Sage Weil)
-   core: Better default value for osd_snap_trim_sleep
    ([pr#29732](https://github.com/ceph/ceph/pull/29732), Neha Ojha)
-   core: Health warnings on long network ping times
    ([issue#40640](http://tracker.ceph.com/issues/40640),
    [issue#40586](http://tracker.ceph.com/issues/40586),
    [pr#30225](https://github.com/ceph/ceph/pull/30225), xie xingguo,
    David Zafman)
-   core: ceph daemon mon.a config set mon_health_to_clog false cause
    leader mon assert
    ([issue#39625](http://tracker.ceph.com/issues/39625),
    [pr#29741](https://github.com/ceph/ceph/pull/29741), huangjun)
-   core: crc cache should be invalidated when posting preallocated rx
    buffers ([issue#38437](http://tracker.ceph.com/issues/38437),
    [pr#29247](https://github.com/ceph/ceph/pull/29247), Ilya Dryomov)
-   core: lazy omap stat collection
    ([pr#29189](https://github.com/ceph/ceph/pull/29189), Brad Hubbard)
-   core: mon, osd: parallel clean_pg_upmaps
    ([issue#40104](http://tracker.ceph.com/issues/40104),
    [issue#40230](http://tracker.ceph.com/issues/40230),
    [pr#28619](https://github.com/ceph/ceph/pull/28619), xie xingguo)
-   core: mon,osd: limit MOSDMap messages by size as well as map count
    ([issue#38277](http://tracker.ceph.com/issues/38277),
    [issue#38040](http://tracker.ceph.com/issues/38040),
    [pr#29242](https://github.com/ceph/ceph/pull/29242), Sage Weil)
-   core: mon/AuthMonitor: fix initial creation of rotating keys
    ([issue#40634](http://tracker.ceph.com/issues/40634),
    [pr#30181](https://github.com/ceph/ceph/pull/30181), Sage Weil)
-   core: mon/MDSMonitor: use stringstream instead of dout for mds
    repaired ([issue#40472](http://tracker.ceph.com/issues/40472),
    [pr#30235](https://github.com/ceph/ceph/pull/30235), Zhi Zhang)
-   core: mon/MgrMonitor: fix null deref when invalid formatter is
    specified ([pr#29593](https://github.com/ceph/ceph/pull/29593), Sage
    Weil)
-   core: mon/OSDMonitor.cc: better error message about min_size
    ([pr#29618](https://github.com/ceph/ceph/pull/29618), Neha Ojha)
-   core: mon/OSDMonitor: trim not-longer-exist failure reporters
    ([pr#30903](https://github.com/ceph/ceph/pull/30903), NancySu05)
-   core: mon: C_AckMarkedDown has not handled the Callback Arguments
    ([pr#30213](https://github.com/ceph/ceph/pull/30213), NancySu05)
-   core: mon: ensure prepare_failure() marks no_reply on op
    ([pr#30481](https://github.com/ceph/ceph/pull/30481), Joao Eduardo
    Luis)
-   core: mon: paxos: introduce new reset_pending_committing_finishers
    for safety ([issue#39744](http://tracker.ceph.com/issues/39744),
    [issue#39484](http://tracker.ceph.com/issues/39484),
    [pr#28540](https://github.com/ceph/ceph/pull/28540), Greg Farnum)
-   core: mon: show pool id in pool ls command
    ([issue#40287](http://tracker.ceph.com/issues/40287),
    [pr#30485](https://github.com/ceph/ceph/pull/30485), Chang Liu)
-   core: osd beacon sometimes has empty pg list
    ([issue#40464](http://tracker.ceph.com/issues/40464),
    [issue#40377](http://tracker.ceph.com/issues/40377),
    [pr#29253](https://github.com/ceph/ceph/pull/29253), Sage Weil)
-   core: osd/OSD.cc: make osd bench description consistent with
    parameters ([issue#39374](http://tracker.ceph.com/issues/39374),
    [issue#39006](http://tracker.ceph.com/issues/39006),
    [pr#28097](https://github.com/ceph/ceph/pull/28097), Neha Ojha)
-   core: osd/OSDCap: Check for empty namespace
    ([issue#40835](http://tracker.ceph.com/issues/40835),
    [pr#30214](https://github.com/ceph/ceph/pull/30214), Brad Hubbard)
-   core: osd/OSDMap: Replace get_out_osds with get_out_existing_osds
    ([issue#39422](http://tracker.ceph.com/issues/39422),
    [issue#39154](http://tracker.ceph.com/issues/39154),
    [pr#28142](https://github.com/ceph/ceph/pull/28142), Brad Hubbard)
-   core: osd/OSDMap: do not trust partially simplified pg_upmap_item
    ([pr#30898](https://github.com/ceph/ceph/pull/30898), xie xingguo)
-   core: osd/PG: Add PG to large omap log message
    ([pr#30924](https://github.com/ceph/ceph/pull/30924), Brad Hubbard)
-   core: osd/PG: fix last_complete re-calculation on splitting
    ([issue#39538](http://tracker.ceph.com/issues/39538),
    [issue#26958](http://tracker.ceph.com/issues/26958),
    [pr#28259](https://github.com/ceph/ceph/pull/28259), xie xingguo)
-   core: osd/PeeringState: do not complain about past_intervals
    constrained by oldest epoch
    ([pr#30222](https://github.com/ceph/ceph/pull/30222), Sage Weil)
-   core: osd/PeeringState: recover_got - add special handler for empty
    log ([pr#30895](https://github.com/ceph/ceph/pull/30895), xie
    xingguo)
-   core: osd/PrimaryLogPG: Avoid accessing destroyed references in
    finish_degr... ([pr#30291](https://github.com/ceph/ceph/pull/30291),
    Tao Ning)
-   core: osd/PrimaryLogPG: skip obcs that don\'t exist during backfill
    scan_range ([pr#31029](https://github.com/ceph/ceph/pull/31029),
    Sage Weil)
-   core: osd/PrimaryLogPG: update oi.size on write op implicitly
    truncating ob...
    ([pr#30275](https://github.com/ceph/ceph/pull/30275), xie xingguo)
-   core: osd: Better error message when OSD count is less than
    osd_pool_default_size
    ([issue#38617](http://tracker.ceph.com/issues/38617),
    [pr#30180](https://github.com/ceph/ceph/pull/30180), Kefu Chai, Sage
    Weil, zjh)
-   core: osd: Don\'t evict after a flush if intersecting scrub range
    ([issue#38840](http://tracker.ceph.com/issues/38840),
    [issue#39518](http://tracker.ceph.com/issues/39518),
    [pr#28232](https://github.com/ceph/ceph/pull/28232), David Zafman)
-   core: osd: Don\'t include user changeable flag in snaptrim related
    assert ([issue#38124](http://tracker.ceph.com/issues/38124),
    [issue#39698](http://tracker.ceph.com/issues/39698),
    [pr#28202](https://github.com/ceph/ceph/pull/28202), David Zafman)
-   core: osd: Fix for compatibility of encode/decode of osd_stat_t
    ([pr#31275](https://github.com/ceph/ceph/pull/31275), Kefu Chai,
    David Zafman)
-   core: osd: Include dups in copy_after() and copy_up_to()
    ([issue#39304](http://tracker.ceph.com/issues/39304),
    [pr#28089](https://github.com/ceph/ceph/pull/28089), David Zafman)
-   core: osd: Output Base64 encoding of CRC header if binary data
    present ([issue#39737](http://tracker.ceph.com/issues/39737),
    [pr#28503](https://github.com/ceph/ceph/pull/28503), David Zafman)
-   core: osd: Remove unused osdmap flags full, nearfull from output
    ([pr#30901](https://github.com/ceph/ceph/pull/30901), David Zafman)
-   core: osd: clear PG_STATE_CLEAN when repair object
    ([pr#30243](https://github.com/ceph/ceph/pull/30243), Zengran Zhang)
-   core: osd: fix build_incremental_map_msg
    ([issue#38282](http://tracker.ceph.com/issues/38282),
    [pr#31236](https://github.com/ceph/ceph/pull/31236), Sage Weil)
-   core: osd: make project_pg_history handle concurrent osdmap publish
    ([issue#26970](http://tracker.ceph.com/issues/26970),
    [pr#29976](https://github.com/ceph/ceph/pull/29976), Sage Weil)
-   core: osd: merge replica log on primary need according to replica
    log\'s crt ([pr#30916](https://github.com/ceph/ceph/pull/30916),
    Zengran Zhang)
-   core: osd: pg stuck in backfill_wait with plenty of disk space
    ([issue#38034](http://tracker.ceph.com/issues/38034),
    [pr#28201](https://github.com/ceph/ceph/pull/28201), xie xingguo,
    David Zafman)
-   core: osd: report omap/data/metadata usage
    ([issue#40639](http://tracker.ceph.com/issues/40639),
    [pr#28852](https://github.com/ceph/ceph/pull/28852), Sage Weil)
-   core: osd: rollforward may need to mark pglog dirty
    ([issue#40403](http://tracker.ceph.com/issues/40403),
    [pr#31035](https://github.com/ceph/ceph/pull/31035), Zengran Zhang)
-   core: osd: scrub error on big objects; make bluestore refuse to
    start on big objects
    ([pr#30784](https://github.com/ceph/ceph/pull/30784), David Zafman,
    Sage Weil)
-   core: osd: take heartbeat_lock when calling heartbeat()
    ([issue#39513](http://tracker.ceph.com/issues/39513),
    [issue#39439](http://tracker.ceph.com/issues/39439),
    [pr#28220](https://github.com/ceph/ceph/pull/28220), Sage Weil)
-   core: osds allows to partially start more than N+2
    ([issue#38206](http://tracker.ceph.com/issues/38206),
    [issue#38076](http://tracker.ceph.com/issues/38076),
    [pr#29241](https://github.com/ceph/ceph/pull/29241), Sage Weil)
-   core: should report EINVAL in ErasureCode::parse() if m\<=0
    ([issue#38682](http://tracker.ceph.com/issues/38682),
    [issue#38751](http://tracker.ceph.com/issues/38751),
    [pr#28995](https://github.com/ceph/ceph/pull/28995), Sage Weil)
-   core: should set EPOLLET flag on del_event()
    ([issue#38856](http://tracker.ceph.com/issues/38856),
    [pr#29250](https://github.com/ceph/ceph/pull/29250), Roman Penyaev)
-   doc/ceph-fuse: mention -k option in ceph-fuse man page
    ([pr#30936](https://github.com/ceph/ceph/pull/30936), Rishabh Dave)
-   doc/rbd: s/guess/xml/ for codeblock lexer
    ([pr#31090](https://github.com/ceph/ceph/pull/31090), Kefu Chai)
-   doc/rgw: document use of \'realm pull\' instead of \'period pull\'
    ([issue#39655](http://tracker.ceph.com/issues/39655),
    [pr#30131](https://github.com/ceph/ceph/pull/30131), Casey Bodley)
-   doc: Document behaviour of fsync-after-close
    ([issue#24641](http://tracker.ceph.com/issues/24641),
    [pr#29765](https://github.com/ceph/ceph/pull/29765), Jos Collin,
    Jeff Layton)
-   doc: Object Gateway multisite document read-only argument error
    ([issue#40497](http://tracker.ceph.com/issues/40497),
    [pr#29289](https://github.com/ceph/ceph/pull/29289), Chenjiong Deng)
-   doc: default values for mon_health_to_clog\_\* were flipped
    ([pr#30227](https://github.com/ceph/ceph/pull/30227), James McClune)
-   doc: describe metadata_heap cleanup
    ([issue#18174](http://tracker.ceph.com/issues/18174),
    [pr#30070](https://github.com/ceph/ceph/pull/30070), Dan van der
    Ster)
-   doc: fix rgw_ldap_dnattr username token
    ([pr#30099](https://github.com/ceph/ceph/pull/30099), Thomas
    Kriechbaumer)
-   doc: rgw: CreateBucketConfiguration for s3 PUT Bucket request
    ([issue#39602](http://tracker.ceph.com/issues/39602),
    [issue#39597](http://tracker.ceph.com/issues/39597),
    [pr#29257](https://github.com/ceph/ceph/pull/29257), Casey Bodley)
-   doc: update bluestore cache settings and clarify data fraction
    ([issue#39522](http://tracker.ceph.com/issues/39522),
    [pr#31258](https://github.com/ceph/ceph/pull/31258), Jan Fajerski)
-   doc: wrong value of usage log default in logging section
    ([issue#37891](http://tracker.ceph.com/issues/37891),
    [issue#37856](http://tracker.ceph.com/issues/37856),
    [pr#29014](https://github.com/ceph/ceph/pull/29014), Abhishek
    Lekshmanan)
-   filestore: assure sufficient leaves in pre-split
    ([issue#39390](http://tracker.ceph.com/issues/39390),
    [pr#30182](https://github.com/ceph/ceph/pull/30182), Jeegn Chen)
-   krbd: avoid udev netlink socket overrun and retry on transient
    errors from udev_enumerate_scan_devices()
    ([pr#31322](https://github.com/ceph/ceph/pull/31322), Ilya Dryomov,
    Adam C. Emerson)
-   krbd: fix rbd map hang due to udev return subsystem unordered
    ([issue#39089](http://tracker.ceph.com/issues/39089),
    [pr#30176](https://github.com/ceph/ceph/pull/30176), Zhi Zhang)
-   mgr/balancer: fix fudge
    ([pr#28399](https://github.com/ceph/ceph/pull/28399), xie xingguo)
-   mgr/balancer: python3 compatibility issue
    ([pr#31013](https://github.com/ceph/ceph/pull/31013), Mykola Golub)
-   mgr/balancer: restrict automatic balancing to specific weekdays
    ([pr#26499](https://github.com/ceph/ceph/pull/26499), xie xingguo)
-   mgr/crash: fix python3 invalid syntax problems
    ([pr#29029](https://github.com/ceph/ceph/pull/29029), Ricardo Dias)
-   mgr/dashboard: Fix run-frontend-e2e-tests.sh
    ([issue#40707](http://tracker.ceph.com/issues/40707),
    [pr#28954](https://github.com/ceph/ceph/pull/28954), Kiefer Chang,
    Tiago Melo)
-   mgr/dashboard: Fix various RGW issues
    ([pr#28210](https://github.com/ceph/ceph/pull/28210), Volker Theile)
-   mgr/dashboard: RGW proxy can\'t handle self-signed SSL certificates
    ([pr#30543](https://github.com/ceph/ceph/pull/30543), Volker Theile)
-   mgr/dashboard: cephfs multimds graphs stack together
    ([issue#40660](http://tracker.ceph.com/issues/40660),
    [pr#28911](https://github.com/ceph/ceph/pull/28911), Kiefer Chang)
-   mgr/localpool: pg_num is an int arg to \'osd pool create\'
    ([pr#30447](https://github.com/ceph/ceph/pull/30447), Sage Weil)
-   mgr/prometheus: Cast collect_timeout (scrape_interval) to float
    ([pr#31108](https://github.com/ceph/ceph/pull/31108), Ben Meekhof)
-   mgr/prometheus: replace whitespaces in metrics\' names
    ([issue#39458](http://tracker.ceph.com/issues/39458),
    [pr#28165](https://github.com/ceph/ceph/pull/28165), Alfonso
    Martínez)
-   mgr/telemetry: Ignore crashes in report when module not enabled
    ([pr#30846](https://github.com/ceph/ceph/pull/30846), Wido den
    Hollander)
-   mgr: DaemonServer::handle_conf_change - broken locking
    ([issue#38899](http://tracker.ceph.com/issues/38899),
    [issue#38963](http://tracker.ceph.com/issues/38963),
    [pr#29197](https://github.com/ceph/ceph/pull/29197), xie xingguo)
-   mgr: deadlock ([issue#39040](http://tracker.ceph.com/issues/39040),
    [issue#39426](http://tracker.ceph.com/issues/39426),
    [pr#28161](https://github.com/ceph/ceph/pull/28161), xie xingguo)
-   mgr: do not reset reported if a new metric is not collected
    ([pr#30391](https://github.com/ceph/ceph/pull/30391), Ilsoo Byun)
-   radosgw-admin: bucket sync status not \'caught up\' during full sync
    ([issue#40806](http://tracker.ceph.com/issues/40806),
    [pr#30170](https://github.com/ceph/ceph/pull/30170), Casey Bodley)
-   rbd-mirror: cannot restore deferred deletion mirrored images
    ([pr#30828](https://github.com/ceph/ceph/pull/30828), Jason
    Dillaman, Mykola Golub)
-   rbd-mirror: clear out bufferlist prior to listing mirror images
    ([issue#39461](http://tracker.ceph.com/issues/39461),
    [issue#39407](http://tracker.ceph.com/issues/39407),
    [pr#28123](https://github.com/ceph/ceph/pull/28123), Jason Dillaman)
-   rbd-mirror: don\'t overwrite status error returned by replay
    ([pr#29872](https://github.com/ceph/ceph/pull/29872), Mykola Golub)
-   rbd-mirror: handle duplicates in image sync throttler queue
    ([issue#40519](http://tracker.ceph.com/issues/40519),
    [issue#40593](http://tracker.ceph.com/issues/40593),
    [pr#28815](https://github.com/ceph/ceph/pull/28815), Mykola Golub)
-   rbd-mirror: ignore errors relating to parsing the cluster config
    file ([pr#30117](https://github.com/ceph/ceph/pull/30117), Jason
    Dillaman)
-   rbd/action: fix error getting positional argument
    ([issue#40095](http://tracker.ceph.com/issues/40095),
    [pr#29294](https://github.com/ceph/ceph/pull/29294), songweibin)
-   rbd/tests: avoid hexdump skip and length options in krbd test
    ([pr#30569](https://github.com/ceph/ceph/pull/30569), Ilya Dryomov)
-   rbd: Reduce log level for cls/journal and cls/rbd expected errors
    ([issue#40865](http://tracker.ceph.com/issues/40865),
    [pr#29565](https://github.com/ceph/ceph/pull/29565), Jason Dillaman)
-   rbd: filter out group/trash snapshots from snap_list
    ([issue#38538](http://tracker.ceph.com/issues/38538),
    [issue#39186](http://tracker.ceph.com/issues/39186),
    [pr#28138](https://github.com/ceph/ceph/pull/28138), songweibin,
    Jason Dillaman)
-   rbd: journal: properly advance read offset after skipping invalid
    range ([pr#28814](https://github.com/ceph/ceph/pull/28814), Mykola
    Golub)
-   rbd: librbd: add missing shutdown states to managed lock helper
    ([issue#38387](http://tracker.ceph.com/issues/38387),
    [issue#38509](http://tracker.ceph.com/issues/38509),
    [pr#28151](https://github.com/ceph/ceph/pull/28151), Jason Dillaman)
-   rbd: librbd: async open/close should free ImageCtx before issuing
    callback ([issue#39429](http://tracker.ceph.com/issues/39429),
    [issue#39031](http://tracker.ceph.com/issues/39031),
    [pr#28125](https://github.com/ceph/ceph/pull/28125), Jason Dillaman)
-   rbd: librbd: avoid dereferencing an empty container during deep-copy
    ([issue#40368](http://tracker.ceph.com/issues/40368),
    [pr#30177](https://github.com/ceph/ceph/pull/30177), Jason Dillaman)
-   rbd: librbd: disable image mirroring when moving to trash
    ([pr#28150](https://github.com/ceph/ceph/pull/28150), Mykola Golub)
-   rbd: librbd: ensure compare-and-write doesn\'t skip compare after
    copyup ([issue#38383](http://tracker.ceph.com/issues/38383),
    [issue#38441](http://tracker.ceph.com/issues/38441),
    [pr#28133](https://github.com/ceph/ceph/pull/28133), Ilya Dryomov)
-   rbd: librbd: properly handle potential object map failures
    ([issue#39952](http://tracker.ceph.com/issues/39952),
    [issue#36074](http://tracker.ceph.com/issues/36074),
    [pr#30796](https://github.com/ceph/ceph/pull/30796), Jason Dillaman,
    Mykola Golub)
-   rbd: librbd: properly track in-flight flush requests
    ([issue#40573](http://tracker.ceph.com/issues/40573),
    [pr#28770](https://github.com/ceph/ceph/pull/28770), Jason Dillaman)
-   rbd: librbd: race condition possible when validating RBD pool
    ([issue#38500](http://tracker.ceph.com/issues/38500),
    [issue#38563](http://tracker.ceph.com/issues/38563),
    [pr#28139](https://github.com/ceph/ceph/pull/28139), Jason Dillaman)
-   rbd: use the ordered throttle for the export action
    ([issue#40435](http://tracker.ceph.com/issues/40435),
    [pr#30178](https://github.com/ceph/ceph/pull/30178), Jason Dillaman)
-   restful: Query nodes_by_id for items
    ([pr#31273](https://github.com/ceph/ceph/pull/31273), Boris Ranto)
-   rgw admin: disable stale instance delete in a multiste env
    ([pr#30340](https://github.com/ceph/ceph/pull/30340), Abhishek
    Lekshmanan)
-   rgw/OutputDataSocket: append_output(buffer::list&) says it will (but
    does not) discard output at data_max_backlog
    ([issue#40178](http://tracker.ceph.com/issues/40178),
    [issue#40351](http://tracker.ceph.com/issues/40351),
    [pr#29279](https://github.com/ceph/ceph/pull/29279), Matt Benjamin)
-   rgw/cls: keep issuing bilog trim ops after reset
    ([issue#40187](http://tracker.ceph.com/issues/40187),
    [pr#30074](https://github.com/ceph/ceph/pull/30074), Casey Bodley)
-   rgw/multisite: Don\'t allow certain radosgw-admin commands to run on
    non-master zone
    ([issue#39548](http://tracker.ceph.com/issues/39548),
    [pr#30133](https://github.com/ceph/ceph/pull/30133), Shilpa
    Jagannath)
-   rgw/rgw_op: Remove get_val from hotpath via legacy options
    ([pr#30141](https://github.com/ceph/ceph/pull/30141), Mark Nelson)
-   rgw: Add support for \--bypass-gc flag of radosgw-admin bucket rm
    command in RGW Multi-site
    ([issue#39748](http://tracker.ceph.com/issues/39748),
    [issue#24991](http://tracker.ceph.com/issues/24991),
    [pr#29262](https://github.com/ceph/ceph/pull/29262), Casey Bodley)
-   rgw: Don\'t crash on copy when metadata directive not supplied
    ([issue#40416](http://tracker.ceph.com/issues/40416),
    [pr#29500](https://github.com/ceph/ceph/pull/29500), Adam C.
    Emerson)
-   rgw: Fix bucket versioning vs. swift metadata bug
    ([pr#30140](https://github.com/ceph/ceph/pull/30140), Marcus Watts)
-   rgw: Fix rgw decompression log-print
    ([pr#30156](https://github.com/ceph/ceph/pull/30156), Han Fengzhe)
-   rgw: Multisite sync corruption for large multipart obj
    ([issue#40144](http://tracker.ceph.com/issues/40144),
    [pr#29273](https://github.com/ceph/ceph/pull/29273), Casey Bodley,
    Tianshan Qu, Xiaoxi CHEN)
-   rgw: RGWCoroutine::call(nullptr) sets retcode=0
    ([pr#30159](https://github.com/ceph/ceph/pull/30159), Casey Bodley)
-   rgw: Return tenant field in bucket_stats function
    ([issue#40038](http://tracker.ceph.com/issues/40038),
    [pr#28209](https://github.com/ceph/ceph/pull/28209), Volker Theile)
-   rgw: S3 policy evaluated incorrectly
    ([issue#38638](http://tracker.ceph.com/issues/38638),
    [issue#39274](http://tracker.ceph.com/issues/39274),
    [pr#29255](https://github.com/ceph/ceph/pull/29255), Pritha
    Srivastava)
-   rgw: Save an unnecessary copy of RGWEnv
    ([pr#29483](https://github.com/ceph/ceph/pull/29483), Mark Kogan)
-   rgw: Swift interface: server side copy fails if object name contains
    \'?\' ([issue#27217](http://tracker.ceph.com/issues/27217),
    [issue#40128](http://tracker.ceph.com/issues/40128),
    [pr#29267](https://github.com/ceph/ceph/pull/29267), Casey Bodley)
-   rgw: TempURL should not allow PUTs with the X-Object-Manifest
    ([issue#40133](http://tracker.ceph.com/issues/40133),
    [issue#20797](http://tracker.ceph.com/issues/20797),
    [pr#28711](https://github.com/ceph/ceph/pull/28711), Radoslaw
    Zarzynski)
-   rgw: abort multipart fix
    ([pr#29016](https://github.com/ceph/ceph/pull/29016), J. Eric
    Ivancich)
-   rgw: asio: check the remote endpoint before processing requests
    ([pr#30977](https://github.com/ceph/ceph/pull/30977), Abhishek
    Lekshmanan)
-   rgw: conditionally allow builtin users with non-unique email
    addresses ([issue#40089](http://tracker.ceph.com/issues/40089),
    [issue#40507](http://tracker.ceph.com/issues/40507),
    [pr#28716](https://github.com/ceph/ceph/pull/28716), Matt Benjamin)
-   rgw: data/bilogs are trimmed when no peers are reading them
    ([issue#39487](http://tracker.ceph.com/issues/39487),
    [pr#30130](https://github.com/ceph/ceph/pull/30130), Casey Bodley)
-   rgw: datalog/mdlog trim commands loop until done
    ([pr#30868](https://github.com/ceph/ceph/pull/30868), Casey Bodley)
-   rgw: do necessary checking of website configuration
    ([issue#40678](http://tracker.ceph.com/issues/40678),
    [pr#30980](https://github.com/ceph/ceph/pull/30980), Enming Zhang)
-   rgw: don\'t throw when accept errors are happening on frontend
    ([pr#30154](https://github.com/ceph/ceph/pull/30154), Yuval
    Lifshitz)
-   rgw: fix CreateBucket with BucketLocation parameter failed under
    default zonegroup
    ([pr#30171](https://github.com/ceph/ceph/pull/30171), Enming Zhang)
-   rgw: fix bucket may redundantly list keys after BI_PREFIX_CHAR
    ([issue#40147](http://tracker.ceph.com/issues/40147),
    [issue#39984](http://tracker.ceph.com/issues/39984),
    [pr#28409](https://github.com/ceph/ceph/pull/28409), Casey Bodley,
    Tianshan Qu)
-   rgw: fix cls_bucket_list_unordered() partial results
    ([pr#30253](https://github.com/ceph/ceph/pull/30253), Mark Kogan)
-   rgw: fix data sync start delay if remote haven\'t init data_log
    ([pr#30510](https://github.com/ceph/ceph/pull/30510), Tianshan Qu)
-   rgw: fix drain handles error when deleting bucket with bypass-gc
    option ([pr#29984](https://github.com/ceph/ceph/pull/29984),
    dongdong tao)
-   rgw: fix list bucket with delimiter wrongly skip some special keys
    ([issue#40905](http://tracker.ceph.com/issues/40905),
    [pr#30168](https://github.com/ceph/ceph/pull/30168), Tianshan Qu)
-   rgw: fix list versions starts with version_id=null
    ([pr#30775](https://github.com/ceph/ceph/pull/30775), Tianshan Qu)
-   rgw: fix potential realm watch lost
    ([issue#40991](http://tracker.ceph.com/issues/40991),
    [pr#30167](https://github.com/ceph/ceph/pull/30167), Tianshan Qu)
-   rgw: fix race b/w bucket reshard and ops waiting on reshard
    completion ([pr#29139](https://github.com/ceph/ceph/pull/29139), J.
    Eric Ivancich)
-   rgw: fix refcount tags to match and update object\'s idtag
    ([pr#30891](https://github.com/ceph/ceph/pull/30891), J. Eric
    Ivancich)
-   rgw: fixed \"unrecognized arg\" error when using \"radosgw-admin
    zone rm\" ([pr#30172](https://github.com/ceph/ceph/pull/30172),
    Hongang Chen)
-   rgw: gc remove tag after all sub io finish
    ([issue#40903](http://tracker.ceph.com/issues/40903),
    [pr#30173](https://github.com/ceph/ceph/pull/30173), Tianshan Qu)
-   rgw: housekeeping of reset stats operation in radosgw-admin and cls
    back-end ([pr#30165](https://github.com/ceph/ceph/pull/30165), J.
    Eric Ivancich)
-   rgw: increase beast parse buffer size to 64k
    ([pr#30450](https://github.com/ceph/ceph/pull/30450), Casey Bodley)
-   rgw: ldap auth: S3 auth failure should return InvalidAccessKeyId
    ([pr#30652](https://github.com/ceph/ceph/pull/30652), Matt Benjamin)
-   rgw: make dns hostnames matching case insensitive
    ([issue#40995](http://tracker.ceph.com/issues/40995),
    [pr#30166](https://github.com/ceph/ceph/pull/30166), Casey Bodley,
    Abhishek Lekshmanan)
-   rgw: mitigate bucket list with max-entries excessively high
    ([pr#30134](https://github.com/ceph/ceph/pull/30134), J. Eric
    Ivancich)
-   rgw: multisite: \'radosgw-admin bucket sync status\' should call
    syncs_from(source.name) instead of id
    ([issue#40022](http://tracker.ceph.com/issues/40022),
    [issue#40141](http://tracker.ceph.com/issues/40141),
    [pr#29270](https://github.com/ceph/ceph/pull/29270), Casey Bodley)
-   rgw: multisite: RGWListBucketIndexesCR for data full sync needs
    pagination ([issue#39551](http://tracker.ceph.com/issues/39551),
    [issue#40354](http://tracker.ceph.com/issues/40354),
    [pr#29284](https://github.com/ceph/ceph/pull/29284), Shilpa
    Jagannath)
-   rgw: multisite: data sync loops back to the start of the datalog
    after reaching the end
    ([issue#39033](http://tracker.ceph.com/issues/39033),
    [issue#39074](http://tracker.ceph.com/issues/39074),
    [pr#29021](https://github.com/ceph/ceph/pull/29021), Casey Bodley)
-   rgw: multisite: mismatch of bucket creation times from List Buckets
    ([issue#39635](http://tracker.ceph.com/issues/39635),
    [issue#39734](http://tracker.ceph.com/issues/39734),
    [pr#28483](https://github.com/ceph/ceph/pull/28483), Casey Bodley)
-   rgw: multisite: overwrites in versioning-suspended buckets fail to
    sync ([issue#38080](http://tracker.ceph.com/issues/38080),
    [issue#37792](http://tracker.ceph.com/issues/37792),
    [pr#29017](https://github.com/ceph/ceph/pull/29017), Casey Bodley)
-   rgw: multisite: period pusher gets 403 Forbidden against other
    zonegroups ([issue#39415](http://tracker.ceph.com/issues/39415),
    [issue#39287](http://tracker.ceph.com/issues/39287),
    [pr#29256](https://github.com/ceph/ceph/pull/29256), Casey Bodley)
-   rgw: non-existent mdlog failures logged at level 0
    ([issue#38747](http://tracker.ceph.com/issues/38747),
    [issue#40033](http://tracker.ceph.com/issues/40033),
    [pr#28757](https://github.com/ceph/ceph/pull/28757), Abhishek
    Lekshmanan)
-   rgw: perfcounters: add gc retire counter
    ([pr#30073](https://github.com/ceph/ceph/pull/30073), Matt Benjamin)
-   rgw: permit rgw-admin to populate user info by access-key
    ([pr#30105](https://github.com/ceph/ceph/pull/30105), Matt Benjamin,
    Marc Koderer)
-   rgw: provide admin-friendly reshard status output
    ([issue#37615](http://tracker.ceph.com/issues/37615),
    [issue#40357](http://tracker.ceph.com/issues/40357),
    [pr#29285](https://github.com/ceph/ceph/pull/29285), Mark Kogan)
-   rgw: remove_olh_pending_entries() does not limit the number of
    xattrs to remove
    ([issue#39179](http://tracker.ceph.com/issues/39179),
    [issue#39118](http://tracker.ceph.com/issues/39118),
    [pr#28348](https://github.com/ceph/ceph/pull/28348), Casey Bodley)
-   rgw: resharding of a versioned bucket causes a bucket stats
    discrepancy ([issue#39532](http://tracker.ceph.com/issues/39532),
    [pr#28249](https://github.com/ceph/ceph/pull/28249), J. Eric
    Ivancich)
-   rgw: return ERR_NO_SUCH_BUCKET early while evaluating bucket policy
    ([issue#38420](http://tracker.ceph.com/issues/38420),
    [issue#39697](http://tracker.ceph.com/issues/39697),
    [pr#28422](https://github.com/ceph/ceph/pull/28422), Abhishek
    Lekshmanan)
-   rgw: rgw_file: all directories are virtual with respect to contents
    ([issue#40262](http://tracker.ceph.com/issues/40262),
    [issue#40204](http://tracker.ceph.com/issues/40204),
    [pr#28887](https://github.com/ceph/ceph/pull/28887), Matt Benjamin)
-   rgw: set null version object issues
    ([issue#36763](http://tracker.ceph.com/issues/36763),
    [issue#40360](http://tracker.ceph.com/issues/40360),
    [pr#29288](https://github.com/ceph/ceph/pull/29288), Tianshan Qu)
-   rgw: support delimiter longer then one symbol
    ([issue#39989](http://tracker.ceph.com/issues/39989),
    [issue#38776](http://tracker.ceph.com/issues/38776),
    [pr#29018](https://github.com/ceph/ceph/pull/29018), Tianshan Qu,
    Matt Benjamin)
-   rgw: swift object expiry fails when a bucket reshards
    ([issue#39741](http://tracker.ceph.com/issues/39741),
    [pr#29258](https://github.com/ceph/ceph/pull/29258), Casey Bodley,
    Abhishek Lekshmanan, J. Eric Ivancich)
-   rgw: swift: refrain from corrupting static large objects when using
    nginx as a GET cache
    ([pr#30135](https://github.com/ceph/ceph/pull/30135), Andrey
    Groshev)
-   rgw: the Multi-Object Delete operation of S3 API wrongly handles the
    Code response element
    ([issue#18241](http://tracker.ceph.com/issues/18241),
    [issue#40136](http://tracker.ceph.com/issues/40136),
    [pr#29268](https://github.com/ceph/ceph/pull/29268), Radoslaw
    Zarzynski)
-   rgw: update resharding documentation
    ([issue#39047](http://tracker.ceph.com/issues/39047),
    [pr#29020](https://github.com/ceph/ceph/pull/29020), J. Eric
    Ivancich)
-   rgw_file: fix invalidation of top-level directories
    ([issue#40215](http://tracker.ceph.com/issues/40215),
    [pr#29276](https://github.com/ceph/ceph/pull/29276), Matt Benjamin)
-   rgw_file: advance_mtime() should consider namespace expiration
    ([issue#40415](http://tracker.ceph.com/issues/40415),
    [pr#30660](https://github.com/ceph/ceph/pull/30660), Matt Benjamin)
-   rgw_file: fix readdir eof() calc\--caller stop implies !eof and
    introduce fast S3 Unix stats (immutable)
    ([issue#40375](http://tracker.ceph.com/issues/40375),
    [issue#40456](http://tracker.ceph.com/issues/40456),
    [pr#30077](https://github.com/ceph/ceph/pull/30077), Matt Benjamin)
-   rgw_file: include tenant when hashing bucket names
    ([issue#40225](http://tracker.ceph.com/issues/40225),
    [issue#40118](http://tracker.ceph.com/issues/40118),
    [pr#29277](https://github.com/ceph/ceph/pull/29277), Matt Benjamin)
-   rgw_file: readdir: do not construct markers w/leading \'/\'
    ([pr#30157](https://github.com/ceph/ceph/pull/30157), Matt Benjamin)
-   rgw_file: save etag and acl info in setattr
    ([issue#39229](http://tracker.ceph.com/issues/39229),
    [pr#28073](https://github.com/ceph/ceph/pull/28073), Tao Chen)
-   rpm: missing dependency on python34-ceph-argparse from
    python34-cephfs (and others?)
    ([issue#24918](http://tracker.ceph.com/issues/24918),
    [issue#24919](http://tracker.ceph.com/issues/24919),
    [issue#37613](http://tracker.ceph.com/issues/37613),
    [pr#27949](https://github.com/ceph/ceph/pull/27949), Kefu Chai)
-   tests: cls_rbd: removed mirror peer pool test cases
    ([pr#31485](https://github.com/ceph/ceph/pull/31485), Jason
    Dillaman)
-   tests: librbd: set nbd timeout due to newer kernels defaulting it on
    ([pr#30424](https://github.com/ceph/ceph/pull/30424), Jason
    Dillaman)
-   tests: ceph-disk: use a Python2.7 compatible version of pytest
    ([pr#31254](https://github.com/ceph/ceph/pull/31254), Alfredo Deza)
-   tests: rgw: don\'t use ceph-ansible in s3a-hadoop suite
    ([issue#39706](http://tracker.ceph.com/issues/39706),
    [pr#30069](https://github.com/ceph/ceph/pull/30069), Casey Bodley)
-   tests/workunits/rbd: wait for rbd-nbd unmap to complete
    ([issue#39598](http://tracker.ceph.com/issues/39598),
    [issue#39674](http://tracker.ceph.com/issues/39674),
    [pr#28310](https://github.com/ceph/ceph/pull/28310), Jason Dillaman)
-   tests: fix issues in vstart runner
    ([pr#28208](https://github.com/ceph/ceph/pull/28208), Volker Theile)
-   tests: limit loops waiting for force-backfill/force-recovery to
    happen ([issue#38351](http://tracker.ceph.com/issues/38351),
    [issue#38309](http://tracker.ceph.com/issues/38309),
    [pr#29245](https://github.com/ceph/ceph/pull/29245), David Zafman)
-   tests: remove s3tests !
    ([pr#31640](https://github.com/ceph/ceph/pull/31640), Yuri
    Weinstein)
-   tests: cephfs: TestMisc.test_evict_client fails
    ([issue#40219](http://tracker.ceph.com/issues/40219),
    [pr#29228](https://github.com/ceph/ceph/pull/29228), \"Yan, Zheng\")
-   tests: do not take ceph.conf.template from ceph/teuthology.git
    ([pr#30841](https://github.com/ceph/ceph/pull/30841), Sage Weil)
-   tests: ignore expected MDS_CLIENT_LATE_RELEASE warning
    ([issue#40968](http://tracker.ceph.com/issues/40968),
    [pr#29812](https://github.com/ceph/ceph/pull/29812), Patrick
    Donnelly)
-   tests: install python3-cephfs for fs suite
    ([pr#31285](https://github.com/ceph/ceph/pull/31285), Kefu Chai)
-   tests: kclient unmount hangs after file system goes down
    ([issue#38709](http://tracker.ceph.com/issues/38709),
    [issue#38677](http://tracker.ceph.com/issues/38677),
    [pr#29218](https://github.com/ceph/ceph/pull/29218), Patrick
    Donnelly)
-   tests: krbd_msgr_segments.t: filter lvcreate output
    ([pr#31324](https://github.com/ceph/ceph/pull/31324), Ilya Dryomov)
-   tests: make get_mon_status use mon addr
    ([pr#31461](https://github.com/ceph/ceph/pull/31461), Sage Weil,
    Nathan Cutler)
-   tests: make: \*\*\* \[hello_world_cpp\] Error 127 in rados
    ([issue#40320](http://tracker.ceph.com/issues/40320),
    [pr#29203](https://github.com/ceph/ceph/pull/29203), Kefu Chai)
-   tests: qa/standalone/scrub/osd-scrub-snaps.sh sometimes fails
    ([issue#40179](http://tracker.ceph.com/issues/40179),
    [issue#40078](http://tracker.ceph.com/issues/40078),
    [pr#29251](https://github.com/ceph/ceph/pull/29251), David Zafman)
-   tests: qa/tasks/ceph.py: pass cluster_name to get_mons
    ([pr#31424](https://github.com/ceph/ceph/pull/31424), Nathan Cutler)
-   tests: qa/workunits/rbd: stress test \"rbd mirror pool status
    \--verbose\" ([pr#29873](https://github.com/ceph/ceph/pull/29873),
    Mykola Golub)
-   tests: remove \"1node\" and \"systemd\" tests as ceph-deploy is not
    actively developed
    ([pr#28457](https://github.com/ceph/ceph/pull/28457), Yuri
    Weinstein)
-   tests: sleep briefly after resetting kclient
    ([pr#29751](https://github.com/ceph/ceph/pull/29751), Patrick
    Donnelly)
-   tests: test_volume_client: print python version correctly
    ([issue#40317](http://tracker.ceph.com/issues/40317),
    [issue#40184](http://tracker.ceph.com/issues/40184),
    [pr#29208](https://github.com/ceph/ceph/pull/29208), Lianne)
-   tests: use curl in wait_for_radosgw() in util/rgw.py
    ([pr#28668](https://github.com/ceph/ceph/pull/28668), Ali Maredia)
-   tests: use hard_reset to reboot kclient
    ([issue#37681](http://tracker.ceph.com/issues/37681),
    [pr#30233](https://github.com/ceph/ceph/pull/30233), Patrick
    Donnelly)
-   tests: whitelisted \'application not enabled\'
    ([pr#28389](https://github.com/ceph/ceph/pull/28389), Yuri
    Weinstein)
-   tools/rados: list objects in a pg
    ([issue#36732](http://tracker.ceph.com/issues/36732),
    [pr#30893](https://github.com/ceph/ceph/pull/30893), Vikhyat Umrao,
    Li Wang)
-   tools/rbd-ggate: close log before running postfork
    ([pr#30121](https://github.com/ceph/ceph/pull/30121), Willem Jan
    Withagen)
-   tools: Add clear-data-digest command to objectstore tool
    ([issue#37749](http://tracker.ceph.com/issues/37749),
    [pr#29196](https://github.com/ceph/ceph/pull/29196), Li Yichao)
-   tools: ceph-objectstore-tool can\'t remove head with bad snapset
    ([pr#30081](https://github.com/ceph/ceph/pull/30081), David Zafman)
-   tools: ceph-objectstore-tool: return 0 if incmap is sane
    ([pr#31659](https://github.com/ceph/ceph/pull/31659), Kefu Chai)
-   tools: ceph-objectstore-tool: update-mon-db: do not fail if incmap
    is missing ([pr#30979](https://github.com/ceph/ceph/pull/30979),
    Kefu Chai)
-   tools: crushtool crash on Fedora 28 and newer
    ([issue#39174](http://tracker.ceph.com/issues/39174),
    [issue#39311](http://tracker.ceph.com/issues/39311),
    [pr#27986](https://github.com/ceph/ceph/pull/27986), Brad Hubbard)

## v13.2.6 Mimic

This is the sixth bugfix release of the Mimic v13.2.x long term stable
release series. We recommend all Mimic users upgrade.

### Notable Changes

-   Ceph v13.2.6 now packages python bindings for python3.6 instead of
    python3.4, because EPEL7 recently switched from python3.4 to
    python3.6 as the native python3. See the [announcement
    \<https://lists.fedoraproject.org/archives/list/epel-announce@lists.fedoraproject.org/message/EGUMKAIMPK2UD5VSHXM53BH2MBDGDWMO/\>\_]{.title-ref}
    for more details on the background of this change.

### Changelog

-   cephfs: MDSMonitor: do not assign standby-replay when degraded
    ([issue#36384](http://tracker.ceph.com/issues/36384),
    [pr#26643](https://github.com/ceph/ceph/pull/26643), Patrick
    Donnelly)
-   ceph-volume: add \--all flag to simple activate
    ([pr#26655](https://github.com/ceph/ceph/pull/26655), Jan Fajerski)
-   ceph-volume: use our own testinfra suite for functional testing
    ([pr#26702](https://github.com/ceph/ceph/pull/26702), Andrew Schoen)
-   cli: ability to change file ownership
    ([issue#38370](http://tracker.ceph.com/issues/38370),
    [pr#26760](https://github.com/ceph/ceph/pull/26760), Sébastien Han)
-   cli: better output of \'ceph health detail\'
    ([issue#39266](http://tracker.ceph.com/issues/39266),
    [pr#27847](https://github.com/ceph/ceph/pull/27847), Shen Hang)
-   cls/rgw: raise debug level of bi_log_iterate_entries output
    ([pr#27973](https://github.com/ceph/ceph/pull/27973), Casey Bodley)
-   common: ceph_timer: stop timer\'s thread when it is suspended
    ([issue#37766](http://tracker.ceph.com/issues/37766),
    [pr#26583](https://github.com/ceph/ceph/pull/26583), Peng Wang)
-   common/str_map: fix trim() on empty string
    ([issue#38329](http://tracker.ceph.com/issues/38329),
    [pr#26810](https://github.com/ceph/ceph/pull/26810), Sage Weil)
-   core: ENOENT in collection_move_rename on EC backfill target
    ([issue#36739](http://tracker.ceph.com/issues/36739),
    [pr#27943](https://github.com/ceph/ceph/pull/27943), Neha Ojha)
-   core: Fix recovery and backfill priority handling
    ([issue#38041](http://tracker.ceph.com/issues/38041),
    [pr#27081](https://github.com/ceph/ceph/pull/27081), David Zafman)
-   crush: add root_bucket to identify underfull buckets
    ([issue#38826](http://tracker.ceph.com/issues/38826),
    [pr#27257](https://github.com/ceph/ceph/pull/27257), huangjun)
-   crush: backport recent upmap fixes
    ([issue#37968](http://tracker.ceph.com/issues/37968),
    [issue#38897](http://tracker.ceph.com/issues/38897),
    [issue#37940](http://tracker.ceph.com/issues/37940),
    [pr#27963](https://github.com/ceph/ceph/pull/27963), xie xingguo)
-   crush/CrushWrapper: ensure crush_choose_arg_map.size == max_buckets
    ([issue#38664](http://tracker.ceph.com/issues/38664),
    [pr#27082](https://github.com/ceph/ceph/pull/27082), Sage Weil)
-   doc: Fix incorrect mention of \'osd_deep_mon_scrub_interval\'
    ([pr#26860](https://github.com/ceph/ceph/pull/26860), Ashish Singh)
-   doc: Minor rados related documentation fixes
    ([issue#38896](http://tracker.ceph.com/issues/38896),
    [pr#27188](https://github.com/ceph/ceph/pull/27188), David Zafman)
-   doc: osd_recovery_priority is not documented (but
    osd_recovery_op_priority is)
    ([issue#23999](http://tracker.ceph.com/issues/23999),
    [pr#26901](https://github.com/ceph/ceph/pull/26901), David Zafman)
-   doc/radosgw: Document mappings of S3 Operations to ACL grants
    ([issue#38523](http://tracker.ceph.com/issues/38523),
    [pr#26968](https://github.com/ceph/ceph/pull/26968), Adam C.
    Emerson)
-   doc/rgw: document placement target configuration
    ([issue#24508](http://tracker.ceph.com/issues/24508),
    [pr#27032](https://github.com/ceph/ceph/pull/27032), Casey Bodley)
-   doc: Update bluestore config docs - fix typo (as -\> has)
    ([pr#27845](https://github.com/ceph/ceph/pull/27845), Yaniv Kaul)
-   doc: updated reference link for log based PG
    ([issue#38465](http://tracker.ceph.com/issues/38465),
    [pr#26829](https://github.com/ceph/ceph/pull/26829), James McClune)
-   include/intarith: enforce the same type for p2\*() arguments
    ([pr#27318](https://github.com/ceph/ceph/pull/27318), Ilya Dryomov)
-   librbd: avoid aggregate-initializing any static_visitor
    ([issue#38659](http://tracker.ceph.com/issues/38659),
    [pr#27041](https://github.com/ceph/ceph/pull/27041), Willem Jan
    Withagen)
-   librbd: avoid aggregate-initializing IsWriteOpVisitor
    ([issue#38660](http://tracker.ceph.com/issues/38660),
    [pr#27039](https://github.com/ceph/ceph/pull/27039), Willem Jan
    Withagen)
-   mds: drop reconnect message from non-existent session
    ([issue#39026](http://tracker.ceph.com/issues/39026),
    [pr#27916](https://github.com/ceph/ceph/pull/27916), Shen Hang)
-   mds: inode filtering on \'dump cache\' asok
    ([issue#11172](http://tracker.ceph.com/issues/11172),
    [pr#27058](https://github.com/ceph/ceph/pull/27058), dongdong tao)
-   mds/server: check directory split after rename
    ([issue#38994](http://tracker.ceph.com/issues/38994),
    [pr#27917](https://github.com/ceph/ceph/pull/27917), Shen Hang)
-   mds: wait for client to release shared cap when re-acquiring xlock
    ([issue#38491](http://tracker.ceph.com/issues/38491),
    [pr#27023](https://github.com/ceph/ceph/pull/27023), \"Yan, Zheng\")
-   mgr/balancer: blame if upmap won\'t actually work
    ([issue#38780](http://tracker.ceph.com/issues/38780),
    [pr#26497](https://github.com/ceph/ceph/pull/26497), xie xingguo)
-   mgr/BaseMgrModule: drop GIL for ceph_send_command
    ([issue#38537](http://tracker.ceph.com/issues/38537),
    [pr#26833](https://github.com/ceph/ceph/pull/26833), Sage Weil)
-   mgr: crashdump feature backport
    ([pr#24639](https://github.com/ceph/ceph/pull/24639), Noah Watkins,
    Sage Weil, Dan Mick)
-   mgr/dashboard: fix for using \'::\' on hosts without ipv6
    ([issue#38575](http://tracker.ceph.com/issues/38575),
    [pr#26750](https://github.com/ceph/ceph/pull/26750), Noah Watkins)
-   mgr/dashboard: Manager should complain about wrong dashboard
    certificate ([issue#24453](http://tracker.ceph.com/issues/24453),
    [pr#27747](https://github.com/ceph/ceph/pull/27747), Volker Theile,
    Ricardo Dias)
-   mgr/dashboard: Search broken for entries with null values
    ([issue#38583](http://tracker.ceph.com/issues/38583),
    [pr#26944](https://github.com/ceph/ceph/pull/26944), Patrick
    Nawracay)
-   mgr/dashboard: show I/O stats in Pool list
    ([pr#27053](https://github.com/ceph/ceph/pull/27053), Alfonso
    Martínez)
-   mgr/dashboard: Update npm packages
    ([issue#39080](http://tracker.ceph.com/issues/39080),
    [pr#26670](https://github.com/ceph/ceph/pull/26670), Tiago Melo)
-   mgr/dashboard: Use human readable units on the OSD I/O graphs
    ([issue#25075](http://tracker.ceph.com/issues/25075),
    [pr#27558](https://github.com/ceph/ceph/pull/27558), Tiago Melo)
-   mgr: drop GIL in get_config
    ([pr#26612](https://github.com/ceph/ceph/pull/26612), John Spray)
-   mgr: enable inter-module calls
    ([pr#27638](https://github.com/ceph/ceph/pull/27638), John Spray)
-   mgr/prometheus: add interface and objectstore to osd metadata
    ([pr#26537](https://github.com/ceph/ceph/pull/26537), Jan Fajerski,
    Konstantin Shalygin)
-   mgr/PyModule: put mgr_module_path first in sys.path
    ([issue#38469](http://tracker.ceph.com/issues/38469),
    [pr#26777](https://github.com/ceph/ceph/pull/26777), Tim Serong)
-   mon/OSDMonitor: fix osd boot check
    ([pr#27351](https://github.com/ceph/ceph/pull/27351), Sage Weil)
-   mon/OSDMonitor: further improve prepare_command_pool_set E2BIG error
    message ([issue#39353](http://tracker.ceph.com/issues/39353),
    [pr#27647](https://github.com/ceph/ceph/pull/27647), Nathan Cutler)
-   msg: output peer address when detecting bad CRCs
    ([issue#39367](http://tracker.ceph.com/issues/39367),
    [pr#27860](https://github.com/ceph/ceph/pull/27860), Greg Farnum)
-   multisite: bucket full sync does not handle delete markers
    ([issue#38007](http://tracker.ceph.com/issues/38007),
    [pr#26194](https://github.com/ceph/ceph/pull/26194), Casey Bodley)
-   multisite: rgw_data_sync_status json decode failure breaks automated
    datalog trimming
    ([issue#38373](http://tracker.ceph.com/issues/38373),
    [pr#26615](https://github.com/ceph/ceph/pull/26615), Casey Bodley)
-   os/bluestore: backport new bitmap allocator
    ([pr#26983](https://github.com/ceph/ceph/pull/26983), Igor Fedotov,
    Sage Weil)
-   os/bluestore: bitmap allocator might fail to return contiguous chunk
    despite having enough space
    ([pr#27298](https://github.com/ceph/ceph/pull/27298), Igor Fedotov)
-   os/bluestore: call fault_range properly prior to looking for blob to
    ... ([pr#27570](https://github.com/ceph/ceph/pull/27570), Igor
    Fedotov)
-   os/bluestore: fix improper backport for p2 macros for bmap allocator
    ([pr#27606](https://github.com/ceph/ceph/pull/27606), Igor Fedotov)
-   os/bluestore: fix length overflow
    ([issue#39245](http://tracker.ceph.com/issues/39245),
    [pr#27366](https://github.com/ceph/ceph/pull/27366), Jianpeng Ma)
-   os/bluestore: fix out-of-bound access in bmap allocator
    ([pr#27738](https://github.com/ceph/ceph/pull/27738), Igor Fedotov)
-   os/bluestore_tool: bluefs-bdev-expand: indicate bypassed for main
    dev ([pr#27447](https://github.com/ceph/ceph/pull/27447), Igor
    Fedotov)
-   osd: FAILED ceph_assert(attrs \|\|
    !pg_log.get_missing().is_missing(soid) \|\| (it_objects !=
    pg_log.get_log().objects.end() && it_objects-\>second-\>op ==
    pg_log_entry_t::LOST_REVERT)) in PrimaryLogPG::get_object_context()
    ([issue#38931](http://tracker.ceph.com/issues/38931),
    [issue#38784](http://tracker.ceph.com/issues/38784),
    [pr#27940](https://github.com/ceph/ceph/pull/27940), xie xingguo)
-   osd: fixup OpTracker destruct assert, waiting_for_osdmap take ref
    with OpRequest ([issue#38377](http://tracker.ceph.com/issues/38377),
    [pr#26862](https://github.com/ceph/ceph/pull/26862), linbing)
-   osd/PG: discover missing objects when an OSD peers and PG is
    degraded ([pr#27745](https://github.com/ceph/ceph/pull/27745), Jonas
    Jelten)
-   osd/PGLog.h: print olog_can_rollback_to before deciding to rollback
    ([issue#38894](http://tracker.ceph.com/issues/38894),
    [pr#27284](https://github.com/ceph/ceph/pull/27284), Neha Ojha)
-   osd/PGLog: preserve original_crt to check rollbackability
    ([issue#39023](http://tracker.ceph.com/issues/39023),
    [issue#36739](http://tracker.ceph.com/issues/36739),
    [pr#27629](https://github.com/ceph/ceph/pull/27629), Neha Ojha)
-   osd/PrimaryLogPG: handle object !exists in handle_watch_timeout
    ([issue#38432](http://tracker.ceph.com/issues/38432),
    [pr#26709](https://github.com/ceph/ceph/pull/26709), Sage Weil)
-   osd: process_copy_chunk remove obc ref before pg unlock
    ([issue#38842](http://tracker.ceph.com/issues/38842),
    [pr#27587](https://github.com/ceph/ceph/pull/27587), Zengran Zhang)
-   osd: shutdown recovery_request_timer earlier
    ([issue#38945](http://tracker.ceph.com/issues/38945),
    [pr#27938](https://github.com/ceph/ceph/pull/27938), Zengran Zhang)
-   pybind/rados: fixed Python3 string conversion issue on get_fsid
    ([issue#38381](http://tracker.ceph.com/issues/38381),
    [pr#27259](https://github.com/ceph/ceph/pull/27259), Jason Dillaman)
-   rbd: API list_images() Segmentation fault
    ([issue#38468](http://tracker.ceph.com/issues/38468),
    [pr#26707](https://github.com/ceph/ceph/pull/26707), songweibin)
-   rbd: krbd: return -ETIMEDOUT in polling
    ([issue#38792](http://tracker.ceph.com/issues/38792),
    [pr#27588](https://github.com/ceph/ceph/pull/27588), Dongsheng Yang)
-   rbd_mirror: don\'t report error if image replay canceled
    ([pr#26140](https://github.com/ceph/ceph/pull/26140), Mykola Golub)
-   rgw: Adding tcp_nodelay option to Beast
    ([issue#34308](http://tracker.ceph.com/issues/34308),
    [pr#27367](https://github.com/ceph/ceph/pull/27367), Or Friedmann)
-   rgw admin: add tenant argument to reshard cancel
    ([issue#38214](http://tracker.ceph.com/issues/38214),
    [pr#27603](https://github.com/ceph/ceph/pull/27603), Abhishek
    Lekshmanan)
-   rgw-admin: fix data sync report for master zone
    ([issue#38938](http://tracker.ceph.com/issues/38938),
    [pr#27421](https://github.com/ceph/ceph/pull/27421), cfanz)
-   rgw: admin: handle delete_at attr in object stat output
    ([pr#27828](https://github.com/ceph/ceph/pull/27828), Abhishek
    Lekshmanan)
-   rgw: allow radosgw-admin to list bucket w \--allow-unordered
    ([pr#28096](https://github.com/ceph/ceph/pull/28096), J. Eric
    Ivancich)
-   rgw: beast: set a default port for endpoints
    ([issue#39000](http://tracker.ceph.com/issues/39000),
    [pr#27661](https://github.com/ceph/ceph/pull/27661), Abhishek
    Lekshmanan)
-   rgw: bucket limit check misbehaves for \> max-entries buckets
    (usually 1000) ([pr#26945](https://github.com/ceph/ceph/pull/26945),
    Matt Benjamin)
-   rgw: bug in versioning concurrent, list and get have consistency
    issue ([issue#38060](http://tracker.ceph.com/issues/38060),
    [pr#26664](https://github.com/ceph/ceph/pull/26664), Wang Hao)
-   rgw: check for non-existent bucket in RGWGetACLs
    ([issue#38116](http://tracker.ceph.com/issues/38116),
    [pr#26529](https://github.com/ceph/ceph/pull/26529), Matt Benjamin)
-   rgw: cls_bucket_list_unordered lists a single shard
    ([issue#39393](http://tracker.ceph.com/issues/39393),
    [pr#28086](https://github.com/ceph/ceph/pull/28086), Casey Bodley)
-   rgw: data sync drains lease stack on lease failure
    ([issue#38479](http://tracker.ceph.com/issues/38479),
    [pr#26762](https://github.com/ceph/ceph/pull/26762), Casey Bodley)
-   rgw: don\'t crash on missing /etc/mime.types
    ([issue#38328](http://tracker.ceph.com/issues/38328),
    [pr#27354](https://github.com/ceph/ceph/pull/27354), Casey Bodley)
-   rgw: failed to pass test_bucket_create_naming_bad_punctuation in
    s3test ([issue#23587](http://tracker.ceph.com/issues/23587),
    [issue#26965](http://tracker.ceph.com/issues/26965),
    [pr#27666](https://github.com/ceph/ceph/pull/27666), yuliyang,
    Abhishek Lekshmanan)
-   rgw: fix bug of apply default quota, for this create new a user may
    core using beast
    ([issue#38847](http://tracker.ceph.com/issues/38847),
    [pr#27335](https://github.com/ceph/ceph/pull/27335), liaoxin01)
-   rgw: fix read not exists null version return wrong
    ([issue#38811](http://tracker.ceph.com/issues/38811),
    [pr#27304](https://github.com/ceph/ceph/pull/27304), Tianshan Qu)
-   rgw: Fix S3 compatibility bug when CORS is not found
    ([issue#37945](http://tracker.ceph.com/issues/37945),
    [pr#27356](https://github.com/ceph/ceph/pull/27356), Nick Janus)
-   rgw: GetBucketCORS API returns Not Found error code when CORS
    configuration does not exist
    ([issue#26964](http://tracker.ceph.com/issues/26964),
    [pr#27122](https://github.com/ceph/ceph/pull/27122), yuliyang,
    ashitakasam)
-   rgw: get or set realm zonegroup zone should check user\'s caps for
    security ([issue#37352](http://tracker.ceph.com/issues/37352),
    [pr#27948](https://github.com/ceph/ceph/pull/27948), yuliyang, Casey
    Bodley)
-   rgw: ldap: fix LDAPAuthEngine::init() when uri !empty()
    ([issue#38699](http://tracker.ceph.com/issues/38699),
    [pr#27174](https://github.com/ceph/ceph/pull/27174), Matt Benjamin)
-   rgw: multiple es related fixes and improvements
    ([issue#38028](http://tracker.ceph.com/issues/38028),
    [issue#22877](http://tracker.ceph.com/issues/22877),
    [issue#36233](http://tracker.ceph.com/issues/36233),
    [issue#38030](http://tracker.ceph.com/issues/38030),
    [issue#36092](http://tracker.ceph.com/issues/36092),
    [pr#26517](https://github.com/ceph/ceph/pull/26517), Yehuda Sadeh,
    Abhishek Lekshmanan, Willem Jan Withagen)
-   rgw: nfs: skip empty (non-POSIX) path segments
    ([issue#38744](http://tracker.ceph.com/issues/38744),
    [pr#27179](https://github.com/ceph/ceph/pull/27179), Matt Benjamin)
-   rgw: only update last_trim marker on ENODATA
    ([issue#38075](http://tracker.ceph.com/issues/38075),
    [pr#26641](https://github.com/ceph/ceph/pull/26641), Casey Bodley)
-   rgw: resolve bugs and clean up garbage collection code
    ([issue#38454](http://tracker.ceph.com/issues/38454),
    [pr#27796](https://github.com/ceph/ceph/pull/27796), J. Eric
    Ivancich)
-   rgw: rgw_file: use correct secret key to check auth
    ([issue#37855](http://tracker.ceph.com/issues/37855),
    [pr#26687](https://github.com/ceph/ceph/pull/26687), MinSheng Lin)
-   rgw: sse c fixes
    ([issue#38700](http://tracker.ceph.com/issues/38700),
    [pr#27297](https://github.com/ceph/ceph/pull/27297), Adam Kupczyk,
    Casey Bodley, Abhishek Lekshmanan)
-   rgw: sync module: avoid printing attrs of objects in log
    ([issue#37646](http://tracker.ceph.com/issues/37646),
    [pr#27029](https://github.com/ceph/ceph/pull/27029), Abhishek
    Lekshmanan)
-   rgw: use chunked encoding to get partial results out faster
    ([issue#12713](http://tracker.ceph.com/issues/12713),
    [pr#28014](https://github.com/ceph/ceph/pull/28014), Robin H.
    Johnson)
-   rgw: when exclusive lock fails due existing lock, log add\'l info
    ([issue#38171](http://tracker.ceph.com/issues/38171),
    [pr#26553](https://github.com/ceph/ceph/pull/26553), J. Eric
    Ivancich)
-   rgw: when using nfs-ganesha to upload file, rgw es sync module get
    failed ([issue#36233](http://tracker.ceph.com/issues/36233),
    [pr#27972](https://github.com/ceph/ceph/pull/27972), Abhishek
    Lekshmanan)
-   run-standalone.sh: Need double-quotes to handle \| in core_pattern
    on all distributions
    ([issue#38325](http://tracker.ceph.com/issues/38325),
    [pr#26811](https://github.com/ceph/ceph/pull/26811), David Zafman)
-   spdk: update to latest spdk-18.05 branch
    ([pr#27451](https://github.com/ceph/ceph/pull/27451), Kefu Chai)
-   test: run-standalone.sh set local library location so mgr can find
    li... ([issue#38262](http://tracker.ceph.com/issues/38262),
    [pr#26495](https://github.com/ceph/ceph/pull/26495), David Zafman)
-   test/store_test: fix/workaround for BlobReuseOnOverwriteUT and
    garbageCollection
    ([pr#27055](https://github.com/ceph/ceph/pull/27055), Igor Fedotov)
-   test: Verify a log trim trims the dup_index
    ([pr#26578](https://github.com/ceph/ceph/pull/26578), Brad Hubbard)
-   tools: ceph-disk/tests: use random unused port for CEPH_MON
    ([issue#39066](http://tracker.ceph.com/issues/39066),
    [pr#27228](https://github.com/ceph/ceph/pull/27228), Kefu Chai)
-   tools: ceph-objectstore-tool: rename dump-import to dump-export
    ([issue#39284](http://tracker.ceph.com/issues/39284),
    [pr#27635](https://github.com/ceph/ceph/pull/27635), David Zafman)

## v13.2.5 Mimic

This is the fifth bugfix release of the Mimic v13.2.x long term stable
release series. We recommend all Mimic users upgrade.

### Notable Changes

-   This release fixes the pg log hard limit bug that was introduced in
    13.2.2, <https://tracker.ceph.com/issues/36686>. A flag called
    [pglog_hardlimit]{.title-ref} has been introduced, which is off by
    default. Enabling this flag will limit the length of the pg log. In
    order to enable that, the flag must be set by running [ceph osd set
    pglog_hardlimit]{.title-ref} after completely upgrading to 13.2.2.
    Once the cluster has this flag set, the length of the pg log will be
    capped by a hard limit. Once set, this flag *must not* be unset
    anymore. In luminous, this feature was introduced in 12.2.11. Users
    who are running 12.2.11, and want to continue to use this feature,
    should upgrade to 13.2.5 or later.
-   This release also fixes a CVE on civetweb, CVE-2019-3821 where SSL
    file descriptors were not closed in civetweb in case the initial
    negotiation fails.
-   There have been fixes to RGW dynamic and manual resharding, which no
    longer leaves behind stale bucket instances to be removed manually.
    For finding and cleaning up older instances from a reshard a
    radosgw-admin command [reshard stale-instances list]{.title-ref} and
    [reshard stale-instances rm]{.title-ref} should do the necessary
    cleanup. These commands should *not* be used on a multisite setup as
    the stale instances may be unlikely to be from a reshard and can
    have consequences. In the next version the admin CLI will prevent
    this command to be run on a multisite cluster, however for the
    current release users are urged not to use the delete command on a
    multisite cluster.

### Changelog

-   build/ops: Destruction of basic_string \_GLIBCXX_USE_CXX11_ABI=0 and
    C++17 mode results in invalid delete
    ([issue#38177](http://tracker.ceph.com/issues/38177),
    [pr#26593](https://github.com/ceph/ceph/pull/26593), Kefu Chai,
    Jason Dillaman)
-   build/ops: rpm: require ceph-base instead of ceph-common
    ([issue#37620](http://tracker.ceph.com/issues/37620),
    [pr#25809](https://github.com/ceph/ceph/pull/25809), Sébastien Han)
-   build/ops: run-make-check.sh ccache tweaks
    ([issue#24817](http://tracker.ceph.com/issues/24817),
    [issue#24777](http://tracker.ceph.com/issues/24777),
    [pr#25153](https://github.com/ceph/ceph/pull/25153), Nathan Cutler,
    Jonathan Brielmaier, Erwan Velu)
-   ceph-create-keys: fix octal notation for Python 3 without losing
    compatibility with Python 2
    ([issue#37641](http://tracker.ceph.com/issues/37641),
    [pr#25531](https://github.com/ceph/ceph/pull/25531), James Page)
-   cephfs: MDCache::finish_snaprealm_reconnect() create and drop
    MClientSnap message
    ([issue#38285](http://tracker.ceph.com/issues/38285),
    [pr#26472](https://github.com/ceph/ceph/pull/26472), \"Yan, Zheng\")
-   cephfs: mgr/status: fix fs status subcommand did not show
    standby-replay MDS\' perf info
    ([issue#36399](http://tracker.ceph.com/issues/36399),
    [pr#25031](https://github.com/ceph/ceph/pull/25031), Zhi Zhang)
-   ceph-objectstore-tool: Dump hashinfo
    ([issue#37597](http://tracker.ceph.com/issues/37597),
    [pr#25721](https://github.com/ceph/ceph/pull/25721), David Zafman)
-   ceph-volume-client: allow setting mode of CephFS volumes
    ([issue#36651](http://tracker.ceph.com/issues/36651),
    [pr#25413](https://github.com/ceph/ceph/pull/25413), Tom Barron)
-   ceph-volume: enable device discards
    ([issue#36532](http://tracker.ceph.com/issues/36532),
    [pr#25749](https://github.com/ceph/ceph/pull/25749), Jonas Jelten)
-   ceph-volume: fix JSON output in [inventory]{.title-ref}
    ([issue#37390](http://tracker.ceph.com/issues/37390),
    [pr#25923](https://github.com/ceph/ceph/pull/25923), Sebastian
    Wagner)
-   ceph-volume: Fix TypeError: join() takes exactly one argument (2
    given) ([issue#37595](http://tracker.ceph.com/issues/37595),
    [pr#25771](https://github.com/ceph/ceph/pull/25771), Sebastian
    Wagner)
-   ceph-volume normalize comma to dot for string to int conversions
    ([issue#37442](http://tracker.ceph.com/issues/37442),
    [pr#25775](https://github.com/ceph/ceph/pull/25775), Alfredo Deza)
-   ceph-volume: revert partition as disk
    ([issue#37506](http://tracker.ceph.com/issues/37506),
    [pr#26294](https://github.com/ceph/ceph/pull/26294), Jan Fajerski)
-   ceph-volume: set permissions right before prime-osd-dir
    ([issue#37486](http://tracker.ceph.com/issues/37486),
    [pr#25777](https://github.com/ceph/ceph/pull/25777), Andrew Schoen,
    Alfredo Deza)
-   ceph-volume tests/functional declare ceph-ansible roles instead of
    importing them ([issue#37805](http://tracker.ceph.com/issues/37805),
    [pr#25837](https://github.com/ceph/ceph/pull/25837), Alfredo Deza)
-   ceph-volume zap: improve zapping to remove all partitions and all
    LVs, encrypted or not
    ([issue#37449](http://tracker.ceph.com/issues/37449),
    [pr#25351](https://github.com/ceph/ceph/pull/25351), Alfredo Deza)
-   cli: dump osd-fsid as part of osd find \<id\>
    ([issue#37966](http://tracker.ceph.com/issues/37966),
    [pr#26035](https://github.com/ceph/ceph/pull/26035), Noah Watkins)
-   client: do not move f-\>pos untill success write
    ([issue#37546](http://tracker.ceph.com/issues/37546),
    [pr#25683](https://github.com/ceph/ceph/pull/25683), Junhui Tang)
-   client: fix failure in quota size limitation when using samba
    ([issue#37547](http://tracker.ceph.com/issues/37547),
    [pr#25678](https://github.com/ceph/ceph/pull/25678), Junhui Tang)
-   client: fix fuse client hang because its pipe to mds is not ok
    ([issue#36079](http://tracker.ceph.com/issues/36079),
    [pr#25903](https://github.com/ceph/ceph/pull/25903), Guan yunfei)
-   client: retry remount on dcache invalidation failure
    ([issue#27657](http://tracker.ceph.com/issues/27657),
    [pr#24695](https://github.com/ceph/ceph/pull/24695), Venky Shankar)
-   client: session flush does not cause cap release message flush
    ([issue#38009](http://tracker.ceph.com/issues/38009),
    [pr#26424](https://github.com/ceph/ceph/pull/26424), Patrick
    Donnelly)
-   cmake: do not pass -B{symbolic,symbolic-functions} to linker on
    FreeBSD ([issue#36717](http://tracker.ceph.com/issues/36717),
    [pr#25525](https://github.com/ceph/ceph/pull/25525), Willem Jan
    Withagen)
-   common: fix memory leaks in WeightedPriorityQueue
    ([issue#36248](http://tracker.ceph.com/issues/36248),
    [pr#25295](https://github.com/ceph/ceph/pull/25295), Radoslaw
    Zarzynski)
-   common: fix missing include boost/noncopyable.hpp
    ([issue#38178](http://tracker.ceph.com/issues/38178),
    [pr#26277](https://github.com/ceph/ceph/pull/26277), Willem Jan
    Withagen)
-   core: list-inconsistent-obj output truncated, causing
    osd-scrub-repair.sh failure
    ([issue#37653](http://tracker.ceph.com/issues/37653),
    [pr#25603](https://github.com/ceph/ceph/pull/25603), David Zafman)
-   core: luminous-\>(mimic,nautilus): PGMapDigest decode error on
    luminous end ([issue#38295](http://tracker.ceph.com/issues/38295),
    [pr#26451](https://github.com/ceph/ceph/pull/26451), Sage Weil)
-   core: Objecter::calc_op_budget: Fix invalid access to extent union
    member ([issue#37932](http://tracker.ceph.com/issues/37932),
    [pr#26066](https://github.com/ceph/ceph/pull/26066), Simon Ruggier)
-   core: scrub warning check incorrectly uses mon scrub interval
    ([issue#37264](http://tracker.ceph.com/issues/37264),
    [pr#26493](https://github.com/ceph/ceph/pull/26493), David Zafman)
-   deep fsck fails on inspecting very large onodes
    ([issue#38065](http://tracker.ceph.com/issues/38065),
    [pr#26291](https://github.com/ceph/ceph/pull/26291), Igor Fedotov)
-   doc: pin the version for \"breathe\" to 4.1.11
    ([issue#38229](http://tracker.ceph.com/issues/38229),
    [pr#26333](https://github.com/ceph/ceph/pull/26333), Alfredo Deza)
-   doc: rados/configuration: refresh osdmap section
    ([issue#38051](http://tracker.ceph.com/issues/38051),
    [pr#26373](https://github.com/ceph/ceph/pull/26373), Ilya Dryomov)
-   doc: updated Ceph documentation links
    ([issue#37793](http://tracker.ceph.com/issues/37793),
    [pr#26180](https://github.com/ceph/ceph/pull/26180), James McClune)
-   doc/user-management: Remove obsolete reset caps command
    ([issue#37663](http://tracker.ceph.com/issues/37663),
    [pr#25607](https://github.com/ceph/ceph/pull/25607), Brad Hubbard)
-   journal: max journal order is incorrectly set at 64
    ([issue#37541](http://tracker.ceph.com/issues/37541),
    [pr#25957](https://github.com/ceph/ceph/pull/25957), Mykola Golub)
-   librbd: fix missing unblock_writes if shrink is not allowed
    ([issue#36778](http://tracker.ceph.com/issues/36778),
    [pr#25252](https://github.com/ceph/ceph/pull/25252), runsisi)
-   librbd: reset snaps in rbd_snap_list()
    ([issue#37508](http://tracker.ceph.com/issues/37508),
    [pr#25459](https://github.com/ceph/ceph/pull/25459), Kefu Chai)
-   mds: broadcast quota message to client when disable quota
    ([issue#38054](http://tracker.ceph.com/issues/38054),
    [pr#26292](https://github.com/ceph/ceph/pull/26292), Junhui Tang)
-   mds: create separate config for heartbeat timeout
    ([issue#37674](http://tracker.ceph.com/issues/37674),
    [pr#26010](https://github.com/ceph/ceph/pull/26010), Patrick
    Donnelly)
-   mds: directories pinned keep being replicated back and forth between
    exporting mds and importing mds
    ([issue#37368](http://tracker.ceph.com/issues/37368),
    [pr#25521](https://github.com/ceph/ceph/pull/25521), Xuehan Xu)
-   mds: disallow dumping huge caches to formatter
    ([issue#36703](http://tracker.ceph.com/issues/36703),
    [pr#25642](https://github.com/ceph/ceph/pull/25642), Venky Shankar)
-   mds: do not call Journaler::\_trim twice
    ([issue#37566](http://tracker.ceph.com/issues/37566),
    [pr#25561](https://github.com/ceph/ceph/pull/25561), Tang Junhui)
-   mds: fix bug filelock stuck at LOCK_XSYN leading client can\'t read
    data ([issue#37333](http://tracker.ceph.com/issues/37333),
    [pr#25676](https://github.com/ceph/ceph/pull/25676), Guan yunfei)
-   mds: fix incorrect l_pq_executing_ops statistics when meet an
    invalid item in purge queue
    ([issue#37567](http://tracker.ceph.com/issues/37567),
    [pr#25559](https://github.com/ceph/ceph/pull/25559), Junhui Tang)
-   mds: fix potential re-evaluate stray dentry in \_unlink_local_finish
    ([issue#38263](http://tracker.ceph.com/issues/38263),
    [pr#26474](https://github.com/ceph/ceph/pull/26474), Zhi Zhang)
-   mds: fix races of updating wanted caps
    ([issue#37464](http://tracker.ceph.com/issues/37464),
    [pr#25680](https://github.com/ceph/ceph/pull/25680), \"Yan, Zheng\")
-   mds: handle fragment notify race
    ([issue#36035](http://tracker.ceph.com/issues/36035),
    [pr#26252](https://github.com/ceph/ceph/pull/26252), \"Yan, Zheng\")
-   mds: handle state change race
    ([issue#37594](http://tracker.ceph.com/issues/37594),
    [pr#26051](https://github.com/ceph/ceph/pull/26051), \"Yan, Zheng\")
-   mds: log evicted clients to clog/dbg
    ([issue#37639](http://tracker.ceph.com/issues/37639),
    [pr#25857](https://github.com/ceph/ceph/pull/25857), Patrick
    Donnelly)
-   MDSMonitor: allow beacons from stopping MDS that was laggy
    ([issue#37724](http://tracker.ceph.com/issues/37724),
    [pr#25685](https://github.com/ceph/ceph/pull/25685), Patrick
    Donnelly)
-   MDSMonitor: missing osdmon writeable check
    ([issue#37929](http://tracker.ceph.com/issues/37929),
    [pr#26069](https://github.com/ceph/ceph/pull/26069), Patrick
    Donnelly)
-   mds: purge queue recovery hangs during boot if PQ journal is damaged
    ([issue#37543](http://tracker.ceph.com/issues/37543),
    [pr#26055](https://github.com/ceph/ceph/pull/26055), Patrick
    Donnelly)
-   mds: PurgeQueue write error handler does not handle EBLACKLISTED
    ([issue#37394](http://tracker.ceph.com/issues/37394),
    [pr#25523](https://github.com/ceph/ceph/pull/25523), Patrick
    Donnelly)
-   mds: remove duplicated l_mdc_num_strays perfcounter set
    ([issue#37516](http://tracker.ceph.com/issues/37516),
    [pr#25681](https://github.com/ceph/ceph/pull/25681), Zhi Zhang)
-   mds: remove wrong assertion in Locker::snapflush_nudge
    ([issue#37721](http://tracker.ceph.com/issues/37721),
    [pr#25885](https://github.com/ceph/ceph/pull/25885), \"Yan, Zheng\")
-   mds: runs out of file descriptors after several respawns
    ([issue#35850](http://tracker.ceph.com/issues/35850),
    [pr#25822](https://github.com/ceph/ceph/pull/25822), Patrick
    Donnelly)
-   mds: severe internal fragment when decoding xattr_map from log event
    ([issue#37399](http://tracker.ceph.com/issues/37399),
    [pr#25519](https://github.com/ceph/ceph/pull/25519), \"Yan, Zheng\")
-   mds: trim cache after journal flush
    ([issue#38010](http://tracker.ceph.com/issues/38010),
    [pr#26214](https://github.com/ceph/ceph/pull/26214), Patrick
    Donnelly)
-   mds: wait shorter intervals if beacon not sent
    ([issue#36367](http://tracker.ceph.com/issues/36367),
    [pr#25980](https://github.com/ceph/ceph/pull/25980), Patrick
    Donnelly)
-   mgr: add get_latest_counter() to C++ -\> Python interface
    ([issue#38138](http://tracker.ceph.com/issues/38138),
    [pr#26074](https://github.com/ceph/ceph/pull/26074), Jan Fajerski)
-   mgr/balancer: add cmd to list all plans
    ([issue#37418](http://tracker.ceph.com/issues/37418),
    [pr#25293](https://github.com/ceph/ceph/pull/25293), Yang Honggang)
-   mgr/balancer: add crush_compat_metrics param to change optimization
    keys ([issue#37412](http://tracker.ceph.com/issues/37412),
    [pr#25291](https://github.com/ceph/ceph/pull/25291), Dan van der
    Ster)
-   mgr/dashboard: Set mirror_mode to None
    ([issue#37870](http://tracker.ceph.com/issues/37870),
    [pr#26009](https://github.com/ceph/ceph/pull/26009), Sebastian
    Wagner)
-   mgr: deadlock: \_check_auth_rotating possible clock skew, rotating
    keys expired way too early
    ([issue#23460](http://tracker.ceph.com/issues/23460),
    [pr#26426](https://github.com/ceph/ceph/pull/26426), Yan Jun)
-   mgr: prometheus: added bluestore db and wal devices to
    ceph_disk_occupation metric
    ([issue#36627](http://tracker.ceph.com/issues/36627),
    [pr#25218](https://github.com/ceph/ceph/pull/25218), Konstantin
    Shalygin)
-   mgr: race between daemon state and service map in \'service status\'
    ([issue#36656](http://tracker.ceph.com/issues/36656),
    [pr#25368](https://github.com/ceph/ceph/pull/25368), Mykola Golub)
-   mgr/restful: fix py got exception when get osd info
    ([issue#38182](http://tracker.ceph.com/issues/38182),
    [pr#26200](https://github.com/ceph/ceph/pull/26200), Boris Ranto,
    zouaiguo)
-   mgr: various python3 fixes
    ([issue#37415](http://tracker.ceph.com/issues/37415),
    [pr#25292](https://github.com/ceph/ceph/pull/25292), Noah Watkins)
-   mgr will refuse connection from the monitor who starts behind it
    ([issue#37753](http://tracker.ceph.com/issues/37753),
    [pr#26235](https://github.com/ceph/ceph/pull/26235), Xinying Song)
-   mgr/zabbix: Send more PG information to Zabbix
    ([issue#38180](http://tracker.ceph.com/issues/38180),
    [pr#25944](https://github.com/ceph/ceph/pull/25944), Wido den
    Hollander)
-   mon: A PG with PG_STATE_REPAIR doesn\'t mean damaged data,
    PG_STATE_IN... ([issue#38070](http://tracker.ceph.com/issues/38070),
    [pr#26304](https://github.com/ceph/ceph/pull/26304), David Zafman)
-   mon: log last command skips latest entry
    ([issue#36679](http://tracker.ceph.com/issues/36679),
    [pr#25526](https://github.com/ceph/ceph/pull/25526), John Spray)
-   mon: mark REMOVE_SNAPS messages as no_reply
    ([issue#37568](http://tracker.ceph.com/issues/37568),
    [pr#25782](https://github.com/ceph/ceph/pull/25782), \"Yan, Zheng\")
-   mon/OSDMonitor: do not populate void pg_temp into nextmap
    ([issue#37784](http://tracker.ceph.com/issues/37784),
    [pr#25844](https://github.com/ceph/ceph/pull/25844), Aleksei
    Zakharov)
-   mon: shutdown messenger early to avoid accessing deleted logger
    ([issue#37780](http://tracker.ceph.com/issues/37780),
    [pr#25846](https://github.com/ceph/ceph/pull/25846), ningtao)
-   msg/async: backport recent messenger fixes
    ([issue#36497](http://tracker.ceph.com/issues/36497),
    [issue#37778](http://tracker.ceph.com/issues/37778),
    [pr#25958](https://github.com/ceph/ceph/pull/25958), xie xingguo)
-   msg/async: crashes when authenticator provided by verify_authorizer
    not implemented
    ([issue#36443](http://tracker.ceph.com/issues/36443),
    [pr#25299](https://github.com/ceph/ceph/pull/25299), Sage Weil)
-   multisite: es sync null versioned object failed because of olh info
    ([issue#23842](http://tracker.ceph.com/issues/23842),
    [issue#23841](http://tracker.ceph.com/issues/23841),
    [pr#25578](https://github.com/ceph/ceph/pull/25578), Tianshan Qu,
    Shang Ding)
-   os/bluestore: fixup access a destroy cond cause deadlock or undefine
    ([issue#37733](http://tracker.ceph.com/issues/37733),
    [pr#26260](https://github.com/ceph/ceph/pull/26260), linbing)
-   os/bluestore: KernelDevice::read() does the EIO mapping now
    ([issue#36455](http://tracker.ceph.com/issues/36455),
    [pr#25854](https://github.com/ceph/ceph/pull/25854), Radoslaw
    Zarzynski)
-   os/bluestore: rename does not old ref to replacement onode at old
    name ([issue#36541](http://tracker.ceph.com/issues/36541),
    [pr#25313](https://github.com/ceph/ceph/pull/25313), Sage Weil)
-   osd: Add support for osd_delete_sleep configuration value
    ([issue#36474](http://tracker.ceph.com/issues/36474),
    [pr#25507](https://github.com/ceph/ceph/pull/25507), Jianpeng Ma,
    David Zafman)
-   osd-backfill-stats.sh fails in rados/standalone/osd.yaml
    ([issue#37393](http://tracker.ceph.com/issues/37393),
    [issue#35982](http://tracker.ceph.com/issues/35982),
    [pr#26329](https://github.com/ceph/ceph/pull/26329), Sage Weil,
    David Zafman)
-   osd: backport recent upmap fixes
    ([issue#37940](http://tracker.ceph.com/issues/37940),
    [issue#37881](http://tracker.ceph.com/issues/37881),
    [pr#26128](https://github.com/ceph/ceph/pull/26128), huangjun, xie
    xingguo)
-   osdc/Objecter: update op_target_t::paused in \_calc_target
    ([issue#37398](http://tracker.ceph.com/issues/37398),
    [pr#25718](https://github.com/ceph/ceph/pull/25718), Song Shun,
    runsisi)
-   osd: failed assert when osd_memory_target options mismatch
    ([issue#37507](http://tracker.ceph.com/issues/37507),
    [pr#25605](https://github.com/ceph/ceph/pull/25605), xie xingguo)
-   osd: force-backfill sets forced_recovery instead of forced_backfill
    in 13.2.1 ([issue#27985](http://tracker.ceph.com/issues/27985),
    [pr#26324](https://github.com/ceph/ceph/pull/26324), xie xingguo)
-   osd/mon: fix upgrades for pg log hard limit
    ([issue#36686](http://tracker.ceph.com/issues/36686),
    [pr#26206](https://github.com/ceph/ceph/pull/26206), Neha Ojha)
-   osd/OSDMap: cancel mapping if target osd is out
    ([issue#37501](http://tracker.ceph.com/issues/37501),
    [pr#25699](https://github.com/ceph/ceph/pull/25699), ningtao, xie
    xingguo)
-   osd/OSD: OSD::mkfs asserts when reusing disk with existing
    superblock ([issue#37404](http://tracker.ceph.com/issues/37404),
    [pr#25385](https://github.com/ceph/ceph/pull/25385), Igor Fedotov)
-   osd/PG.cc: account for missing set irrespective of last_complete
    ([issue#37919](http://tracker.ceph.com/issues/37919),
    [pr#26239](https://github.com/ceph/ceph/pull/26239), Neha Ojha)
-   osd/PrimaryLogPG: fix the extent length error of the sync read
    ([issue#37680](http://tracker.ceph.com/issues/37680),
    [pr#25708](https://github.com/ceph/ceph/pull/25708), Xiaofei Cui)
-   osd: Prioritize user specified scrubs
    ([issue#37269](http://tracker.ceph.com/issues/37269),
    [pr#25513](https://github.com/ceph/ceph/pull/25513), David Zafman)
-   os/filestore: ceph_abort() on fsync(2) or fdatasync(2) failure
    ([issue#38258](http://tracker.ceph.com/issues/38258),
    [pr#26438](https://github.com/ceph/ceph/pull/26438), Sage Weil)
-   pybind/mgr: drop unnecessary iterkeys usage to make py-3 compatible
    ([issue#37581](http://tracker.ceph.com/issues/37581),
    [pr#25759](https://github.com/ceph/ceph/pull/25759), Mykola Golub)
-   pybind/mgr/status: fix ceph fs status in py3 environments
    ([issue#37573](http://tracker.ceph.com/issues/37573),
    [pr#25694](https://github.com/ceph/ceph/pull/25694), Jan Fajerski)
-   qa: pjd test appears to require more than 3h timeout for some
    configurations ([issue#36594](http://tracker.ceph.com/issues/36594),
    [pr#25557](https://github.com/ceph/ceph/pull/25557), Patrick
    Donnelly)
-   qa/rados/upgrade: align thrashing with upgrade suite, don\'t
    import/export pgs
    ([issue#37665](http://tracker.ceph.com/issues/37665),
    [pr#25856](https://github.com/ceph/ceph/pull/25856), Sage Weil)
-   qa/tasks/radosbench: default to 64k writes
    ([issue#37797](http://tracker.ceph.com/issues/37797),
    [pr#26354](https://github.com/ceph/ceph/pull/26354), Sage Weil)
-   qa: test_damage needs to silence MDS_READ_ONLY
    ([issue#37944](http://tracker.ceph.com/issues/37944),
    [pr#26072](https://github.com/ceph/ceph/pull/26072), Patrick
    Donnelly)
-   qa: test_damage performs truncate test on same object repeatedly
    ([issue#37836](http://tracker.ceph.com/issues/37836),
    [issue#37837](http://tracker.ceph.com/issues/37837),
    [pr#26047](https://github.com/ceph/ceph/pull/26047), Patrick
    Donnelly)
-   qa: teuthology may hang on diagnostic commands for fuse mount
    ([issue#36390](http://tracker.ceph.com/issues/36390),
    [pr#25515](https://github.com/ceph/ceph/pull/25515), Patrick
    Donnelly)
-   qa: whitelist cap revoke warning
    ([issue#25188](http://tracker.ceph.com/issues/25188),
    [pr#26496](https://github.com/ceph/ceph/pull/26496), Patrick
    Donnelly)
-   qa/workunits/rados/test_health_warnings: prevent out osds
    ([issue#37776](http://tracker.ceph.com/issues/37776),
    [pr#25850](https://github.com/ceph/ceph/pull/25850), Sage Weil)
-   qa: wrong setting for msgr failures
    ([issue#36676](http://tracker.ceph.com/issues/36676),
    [pr#25517](https://github.com/ceph/ceph/pull/25517), Patrick
    Donnelly)
-   rbd: fix delay time calculation for trash move
    ([issue#37861](http://tracker.ceph.com/issues/37861),
    [pr#25954](https://github.com/ceph/ceph/pull/25954), Mykola Golub)
-   rgw: debug logging for v4 auth does not sanitize encryption keys
    ([issue#37847](http://tracker.ceph.com/issues/37847),
    [pr#26003](https://github.com/ceph/ceph/pull/26003), Casey Bodley)
-   rgw: Don\'t treat colons specially in resource part of ARN
    ([issue#23817](http://tracker.ceph.com/issues/23817),
    [pr#25386](https://github.com/ceph/ceph/pull/25386), Adam C.
    Emerson)
-   rgw: fails to start on Fedora 28 from default configuration
    ([issue#24228](http://tracker.ceph.com/issues/24228),
    [pr#26129](https://github.com/ceph/ceph/pull/26129), Matt Benjamin)
-   rgw: feature \-- log successful bucket resharding events
    ([issue#37647](http://tracker.ceph.com/issues/37647),
    [pr#25740](https://github.com/ceph/ceph/pull/25740), J. Eric
    Ivancich)
-   rgw_file: user info never synced since librgw init
    ([issue#37527](http://tracker.ceph.com/issues/37527),
    [pr#25485](https://github.com/ceph/ceph/pull/25485), Tao Chen)
-   rgw: fix max-size in radosgw-admin and REST Admin API
    ([issue#37517](http://tracker.ceph.com/issues/37517),
    [pr#25449](https://github.com/ceph/ceph/pull/25449), Nick Erdmann)
-   rgw: fix version bucket stats
    ([issue#21429](http://tracker.ceph.com/issues/21429),
    [pr#25643](https://github.com/ceph/ceph/pull/25643), Shasha Lu)
-   rgw: handle S3 version 2 pre-signed urls with meta-data
    ([issue#23470](http://tracker.ceph.com/issues/23470),
    [pr#25899](https://github.com/ceph/ceph/pull/25899), Matt Benjamin)
-   rgw: master zone deletion without a zonegroup rm would break rgw
    rados init ([issue#37328](http://tracker.ceph.com/issues/37328),
    [pr#25511](https://github.com/ceph/ceph/pull/25511), Abhishek
    Lekshmanan)
-   rgw: multisite: sync gets stuck retrying deletes that fail with
    ERR_PRECONDITION_FAILED
    ([issue#37448](http://tracker.ceph.com/issues/37448),
    [pr#25505](https://github.com/ceph/ceph/pull/25505), Casey Bodley)
-   rgw: Object can still be deleted even if s3:DeleteObject policy is
    set ([issue#37403](http://tracker.ceph.com/issues/37403),
    [pr#26309](https://github.com/ceph/ceph/pull/26309), Enming.Zhang)
-   rgw: \"radosgw-admin bucket rm \... \--purge-objects\" can hang
    ([issue#38134](http://tracker.ceph.com/issues/38134),
    [pr#26266](https://github.com/ceph/ceph/pull/26266), J. Eric
    Ivancich)
-   rgw: radosgw-admin: translate reshard status codes (trivial)
    ([issue#36486](http://tracker.ceph.com/issues/36486),
    [pr#25198](https://github.com/ceph/ceph/pull/25198), Matt Benjamin)
-   rgw: rgwgc: process coredump in some special case
    ([issue#23199](http://tracker.ceph.com/issues/23199),
    [pr#25624](https://github.com/ceph/ceph/pull/25624), zhaokun)
-   rpm: Use hardened LDFLAGS
    ([issue#36316](http://tracker.ceph.com/issues/36316),
    [pr#25171](https://github.com/ceph/ceph/pull/25171), Boris Ranto)

## v13.2.4 Mimic

This is the fourth bugfix release of the Mimic v13.2.x long term stable
release series. This release includes two security fixes that were
tested but inadvertently excluded from the final v13.2.3 release build.

### Changelog

-   CVE-2018-16846: rgw: enforce bounds on
    max-keys/max-uploads/max-parts
    ([issue#35994](http://tracker.ceph.com/issues/35994))
-   CVE-2018-14662: mon: limit caps allowed to access the config store

## v13.2.3 Mimic

This is the third bugfix release of the Mimic v13.2.x long term stable
release series. This release contains many fixes across all components
of Ceph. We recommend that all users upgrade.

-   The default memory utilization for the mons has been increased
    somewhat. Rocksdb now uses 512 MB of RAM by default, which should be
    sufficient for small to medium-sized clusters; large clusters should
    tune this up. Also, the [mon_osd_cache_size]{.title-ref} has been
    increase from 10 OSDMaps to 500, which will translate to an
    additional 500 MB to 1 GB of RAM for large clusters, and much less
    for small clusters.
-   Ceph v13.2.2 includes a wrong backport, which may cause mds to go
    into \'damaged\' state when upgrading Ceph cluster from previous
    version. The bug is fixed in v13.2.3. If you are already running
    v13.2.2, upgrading to v13.2.3 does not require special action.
-   The [bluestore_cache]()\* options are no longer needed. They are
    replaced by osd_memory_target, defaulting to 4GB. BlueStore will
    expand and contract its cache to attempt to stay within this limit.
    Users upgrading should note this is a higher default than the
    previous bluestore_cache_size of 1GB, so OSDs using BlueStore will
    use more memory by default. For more details, see the [BlueStore
    docs](http://docs.ceph.com/docs/mimic/rados/configuration/bluestore-config-ref/#automatic-cache-sizing).
-   This version contains an upgrade bug,
    <http://tracker.ceph.com/issues/36686>, due to which upgrading
    during recovery/backfill can cause OSDs to fail. This bug can be
    worked around, either by restarting all the OSDs after the upgrade,
    or by upgrading when all PGs are in \"active+clean\" state. If you
    have already successfully upgraded to 13.2.2, this issue should not
    impact you. Going forward, we are working on a clean upgrade path
    for this feature.

### Changelog

-   build/ops: Can\'t compile Ceph on Fedora 29 as it doesn\'t recognize
    python\*3\*-tox as an install Tox
    ([issue#18163](http://tracker.ceph.com/issues/18163),
    [issue#37301](http://tracker.ceph.com/issues/37301),
    [issue#37422](http://tracker.ceph.com/issues/37422),
    [pr#25294](https://github.com/ceph/ceph/pull/25294), Nathan Cutler,
    Brad Hubbard)
-   build/ops: debian: correct ceph-common relationship with older
    radosgw package
    ([pr#25115](https://github.com/ceph/ceph/pull/25115), Matthew
    Vernon)
-   ceph-bluestore-tool: fix set label functionality for specific keys
    ([pr#24352](https://github.com/ceph/ceph/pull/24352), Igor Fedotov)
-   ceph fs add_data_pool applies pool application metadata incorrectly
    ([issue#36203](http://tracker.ceph.com/issues/36203),
    [issue#36028](http://tracker.ceph.com/issues/36028),
    [pr#24470](https://github.com/ceph/ceph/pull/24470), John Spray)
-   cephfs: client: explicitly show blacklisted state via asok status
    command ([issue#36457](http://tracker.ceph.com/issues/36457),
    [issue#36352](http://tracker.ceph.com/issues/36352),
    [pr#24993](https://github.com/ceph/ceph/pull/24993), Jonathan
    Brielmaier, Zhi Zhang)
-   cephfs: client: request next osdmap for blacklisted client
    ([issue#36668](http://tracker.ceph.com/issues/36668),
    [issue#36690](http://tracker.ceph.com/issues/36690),
    [pr#24987](https://github.com/ceph/ceph/pull/24987), Zhi Zhang)
-   cephfs-journal-tool: wrong layout info used
    ([issue#24933](http://tracker.ceph.com/issues/24933),
    [issue#24644](http://tracker.ceph.com/issues/24644),
    [pr#24583](https://github.com/ceph/ceph/pull/24583), Gu Zhongyan)
-   cephfs: some tool commands silently operate on only rank 0, even if
    multiple ranks exist
    ([issue#36218](http://tracker.ceph.com/issues/36218),
    [pr#25036](https://github.com/ceph/ceph/pull/25036), Venky Shankar)
-   ceph-fuse: add to selinux profile
    ([issue#36103](http://tracker.ceph.com/issues/36103),
    [issue#36197](http://tracker.ceph.com/issues/36197),
    [pr#24439](https://github.com/ceph/ceph/pull/24439), Patrick
    Donnelly)
-   ceph-volume: activate option \--auto-detect-objectstore respects
    \--no-systemd ([issue#36249](http://tracker.ceph.com/issues/36249),
    [pr#24357](https://github.com/ceph/ceph/pull/24357), Alfredo Deza)
-   ceph-volume add device_id to inventory listing
    ([pr#25349](https://github.com/ceph/ceph/pull/25349), Jan Fajerski)
-   ceph-volume: add inventory command
    ([issue#24972](http://tracker.ceph.com/issues/24972),
    [pr#25013](https://github.com/ceph/ceph/pull/25013), Jan Fajerski)
-   ceph-volume Additional work on ceph-volume to add some choose_disk
    capabilities ([issue#36446](http://tracker.ceph.com/issues/36446),
    [pr#24782](https://github.com/ceph/ceph/pull/24782), Erwan Velu)
-   ceph-volume add new ceph-handlers role from ceph-ansible
    ([issue#36251](http://tracker.ceph.com/issues/36251),
    [pr#24337](https://github.com/ceph/ceph/pull/24337), Alfredo Deza)
-   ceph-volume: adds a \--prepare flag to [lvm batch]{.title-ref}
    ([issue#36363](http://tracker.ceph.com/issues/36363),
    [pr#24760](https://github.com/ceph/ceph/pull/24760), Andrew Schoen)
-   ceph-volume: allow to specify \--cluster-fsid instead of reading
    from ceph.conf ([issue#26953](http://tracker.ceph.com/issues/26953),
    [pr#25116](https://github.com/ceph/ceph/pull/25116), Alfredo Deza)
-   ceph_volume_client: py3 compatible
    ([issue#26850](http://tracker.ceph.com/issues/26850),
    [issue#17230](http://tracker.ceph.com/issues/17230),
    [pr#24443](https://github.com/ceph/ceph/pull/24443), Rishabh Dave,
    Patrick Donnelly)
-   ceph-volume custom cluster names fail on filestore trigger
    ([issue#27210](http://tracker.ceph.com/issues/27210),
    [pr#24279](https://github.com/ceph/ceph/pull/24279), Alfredo Deza)
-   ceph-volume: do not send (lvm) stderr/stdout to the terminal, use
    the logfile ([issue#36492](http://tracker.ceph.com/issues/36492),
    [pr#24740](https://github.com/ceph/ceph/pull/24740), Alfredo Deza)
-   ceph-volume enable \--no-systemd flag for simple sub-command
    ([issue#36470](http://tracker.ceph.com/issues/36470),
    [pr#25011](https://github.com/ceph/ceph/pull/25011), Alfredo Deza)
-   ceph-volume: fix journal and filestore data size in [lvm batch
    \--report]{.title-ref}
    ([issue#36242](http://tracker.ceph.com/issues/36242),
    [pr#24306](https://github.com/ceph/ceph/pull/24306), Andrew Schoen)
-   ceph-volume: lsblk can fail to find PARTLABEL, must fallback to
    blkid ([issue#36098](http://tracker.ceph.com/issues/36098),
    [pr#24334](https://github.com/ceph/ceph/pull/24334), Alfredo Deza)
-   ceph-volume lvm.prepare update help to indicate partitions are
    needed, not devices
    ([issue#24795](http://tracker.ceph.com/issues/24795),
    [pr#24449](https://github.com/ceph/ceph/pull/24449), Alfredo Deza)
-   ceph-volume: make [lvm batch]{.title-ref} idempotent
    ([pr#24588](https://github.com/ceph/ceph/pull/24588), Andrew Schoen)
-   ceph-volume: patch Device when testing
    ([issue#36768](http://tracker.ceph.com/issues/36768),
    [pr#25066](https://github.com/ceph/ceph/pull/25066), Alfredo Deza)
-   ceph-volume: reject devices that have existing GPT headers
    ([issue#27062](http://tracker.ceph.com/issues/27062),
    [pr#25103](https://github.com/ceph/ceph/pull/25103), Andrew Schoen)
-   ceph-volume: remove LVs when using zap \--destroy
    ([pr#25100](https://github.com/ceph/ceph/pull/25100), Alfredo Deza)
-   ceph-volume remove version reporting from help menu
    ([issue#36386](http://tracker.ceph.com/issues/36386),
    [pr#24753](https://github.com/ceph/ceph/pull/24753), Alfredo Deza)
-   ceph-volume: rename Device property valid to available
    ([issue#36701](http://tracker.ceph.com/issues/36701),
    [pr#25133](https://github.com/ceph/ceph/pull/25133), Jan Fajerski)
-   ceph-volume: skip processing devices that don\'t exist when scanning
    system disks ([issue#36247](http://tracker.ceph.com/issues/36247),
    [pr#24381](https://github.com/ceph/ceph/pull/24381), Alfredo Deza)
-   ceph-volume systemd import main so console_scripts work for
    executable ([issue#36648](http://tracker.ceph.com/issues/36648),
    [pr#24852](https://github.com/ceph/ceph/pull/24852), Alfredo Deza)
-   ceph-volume tests install ceph-ansible\'s requirements.txt
    dependencies ([issue#36672](http://tracker.ceph.com/issues/36672),
    [pr#24959](https://github.com/ceph/ceph/pull/24959), Alfredo Deza)
-   ceph-volume tests.systemd update imports for systemd module
    ([issue#36704](http://tracker.ceph.com/issues/36704),
    [pr#24957](https://github.com/ceph/ceph/pull/24957), Alfredo Deza)
-   ceph-volume: use console_scripts
    ([issue#36601](http://tracker.ceph.com/issues/36601),
    [pr#24838](https://github.com/ceph/ceph/pull/24838), Mehdi Abaakouk)
-   ceph-volume util.encryption don\'t push stderr to terminal
    ([issue#36246](http://tracker.ceph.com/issues/36246),
    [pr#24826](https://github.com/ceph/ceph/pull/24826), Alfredo Deza)
-   ceph-volume util.encryption robust blkid+lsblk detection of lockbox
    ([pr#24980](https://github.com/ceph/ceph/pull/24980), Alfredo Deza)
-   client: fix use-after-free in Client::link()
    ([issue#35841](http://tracker.ceph.com/issues/35841),
    [issue#24557](http://tracker.ceph.com/issues/24557),
    [pr#24187](https://github.com/ceph/ceph/pull/24187), \"Yan, Zheng\")
-   client: statfs inode count odd
    ([issue#35940](http://tracker.ceph.com/issues/35940),
    [issue#24849](http://tracker.ceph.com/issues/24849),
    [pr#24377](https://github.com/ceph/ceph/pull/24377), Rishabh Dave)
-   client:two ceph-fuse client, one can not list out files created by
    an... ([issue#27051](http://tracker.ceph.com/issues/27051),
    [issue#35934](http://tracker.ceph.com/issues/35934),
    [pr#24295](https://github.com/ceph/ceph/pull/24295), Peng Xie)
-   client: update ctime when modifying file content
    ([issue#35945](http://tracker.ceph.com/issues/35945),
    [issue#36134](http://tracker.ceph.com/issues/36134),
    [pr#24385](https://github.com/ceph/ceph/pull/24385), \"Yan, Zheng\")
-   common: get real hostname from container/pod environment
    ([pr#23916](https://github.com/ceph/ceph/pull/23916), Sage Weil)
-   core: \_aio_log_start inflight overlap of 0x10000\~1000 with
    \[65536\~4096\]
    ([issue#36754](http://tracker.ceph.com/issues/36754),
    [issue#36625](http://tracker.ceph.com/issues/36625),
    [pr#25062](https://github.com/ceph/ceph/pull/25062), Jonathan
    Brielmaier, Yang Honggang)
-   core: FAILED assert(osdmap_manifest.pinned.empty()) in
    OSDMonitor::prune_init()
    ([issue#24612](http://tracker.ceph.com/issues/24612),
    [issue#35071](http://tracker.ceph.com/issues/35071),
    [pr#24918](https://github.com/ceph/ceph/pull/24918), Joao Eduardo
    Luis)
-   core: Interactive mode CLI prints no output since Mimic
    ([issue#36358](http://tracker.ceph.com/issues/36358),
    [issue#36432](http://tracker.ceph.com/issues/36432),
    [pr#24971](https://github.com/ceph/ceph/pull/24971), John Spray,
    Mohamad Gebai)
-   core: mgr crash on scrub of unconnected osd
    ([issue#36110](http://tracker.ceph.com/issues/36110),
    [issue#36465](http://tracker.ceph.com/issues/36465),
    [pr#25029](https://github.com/ceph/ceph/pull/25029), Sage Weil)
-   core: mon osdmap cash too small during upgrade to mimic
    ([issue#36505](http://tracker.ceph.com/issues/36505),
    [pr#25019](https://github.com/ceph/ceph/pull/25019), Sage Weil)
-   core: monstore tool rebuild does not generate creating_pgs
    ([issue#36306](http://tracker.ceph.com/issues/36306),
    [issue#36433](http://tracker.ceph.com/issues/36433),
    [pr#25016](https://github.com/ceph/ceph/pull/25016), Sage Weil)
-   core: Objecter: add ignore cache flag if got redirect reply
    ([issue#36658](http://tracker.ceph.com/issues/36658),
    [pr#25075](https://github.com/ceph/ceph/pull/25075), Iain Buclaw,
    Jonathan Brielmaier)
-   core: objecter cannot resend split-dropped op when racing with con
    reset ([issue#22544](http://tracker.ceph.com/issues/22544),
    [issue#35843](http://tracker.ceph.com/issues/35843),
    [pr#24970](https://github.com/ceph/ceph/pull/24970), Sage Weil)
-   core: os/bluestore: cache autotuning and memory limit
    ([issue#37340](http://tracker.ceph.com/issues/37340),
    [pr#25283](https://github.com/ceph/ceph/pull/25283), Josh Durgin,
    Mark Nelson)
-   core: rados rm \--force-full is blocked when cluster is in full
    status ([issue#36435](http://tracker.ceph.com/issues/36435),
    [pr#25017](https://github.com/ceph/ceph/pull/25017), Yang Honggang)
-   crush/CrushWrapper: fix crush tree json dumper
    ([issue#36150](http://tracker.ceph.com/issues/36150),
    [pr#24481](https://github.com/ceph/ceph/pull/24481), Oshyn Song)
-   debian/control: require fuse for ceph-fuse
    ([issue#21057](http://tracker.ceph.com/issues/21057),
    [pr#24037](https://github.com/ceph/ceph/pull/24037), Thomas Serlin)
-   doc: add ceph-volume inventory sections
    ([pr#25130](https://github.com/ceph/ceph/pull/25130), Jan Fajerski)
-   doc: fix broken fstab url in cephfs/fuse
    ([issue#36286](http://tracker.ceph.com/issues/36286),
    [issue#36313](http://tracker.ceph.com/issues/36313),
    [pr#24441](https://github.com/ceph/ceph/pull/24441), Jos Collin)
-   doc: Put command template into literal block
    ([pr#25000](https://github.com/ceph/ceph/pull/25000), Alexey
    Stupnikov)
-   doc: remove deprecated \'scrubq\' from ceph(8)
    ([issue#35813](http://tracker.ceph.com/issues/35813),
    [issue#35855](http://tracker.ceph.com/issues/35855),
    [pr#24210](https://github.com/ceph/ceph/pull/24210), Ruben Kerkhof)
-   docs: backport edit on github changes
    ([pr#25362](https://github.com/ceph/ceph/pull/25362), Neha Ojha,
    Noah Watkins)
-   doc: Typo error on cephfs/fuse/
    ([issue#36180](http://tracker.ceph.com/issues/36180),
    [issue#36308](http://tracker.ceph.com/issues/36308),
    [pr#24420](https://github.com/ceph/ceph/pull/24420), Karun Josy)
-   ec: src/common/interval_map.h: 161: FAILED assert(len \> 0)
    ([issue#21931](http://tracker.ceph.com/issues/21931),
    [issue#22330](http://tracker.ceph.com/issues/22330),
    [pr#24581](https://github.com/ceph/ceph/pull/24581), Neha Ojha)
-   fsck: cid is improperly matched to oid
    ([issue#36146](http://tracker.ceph.com/issues/36146),
    [issue#36551](http://tracker.ceph.com/issues/36551),
    [issue#36099](http://tracker.ceph.com/issues/36099),
    [issue#32731](http://tracker.ceph.com/issues/32731),
    [pr#24480](https://github.com/ceph/ceph/pull/24480), Kefu Chai, Sage
    Weil)
-   kernel_untar_build.sh: bison: command not found
    ([issue#36121](http://tracker.ceph.com/issues/36121),
    [pr#24241](https://github.com/ceph/ceph/pull/24241), Neha Ojha)
-   libcephfs: expose CEPH_SETATTR_MTIME_NOW and CEPH_SETATTR_ATIME_NOW
    ([issue#36205](http://tracker.ceph.com/issues/36205),
    [issue#35961](http://tracker.ceph.com/issues/35961),
    [pr#24464](https://github.com/ceph/ceph/pull/24464), Zhu Shangzhong)
-   librados application\'s symbol could conflict with the
    libceph-common ([issue#26839](http://tracker.ceph.com/issues/26839),
    [issue#25154](http://tracker.ceph.com/issues/25154),
    [pr#24708](https://github.com/ceph/ceph/pull/24708), Kefu Chai)
-   librbd: blacklisted client might not notice it lost the lock
    ([issue#34534](http://tracker.ceph.com/issues/34534),
    [pr#24401](https://github.com/ceph/ceph/pull/24401), Jason Dillaman)
-   librbd: ensure exclusive lock acquired when removing sync point
    snaps... ([issue#35714](http://tracker.ceph.com/issues/35714),
    [issue#24898](http://tracker.ceph.com/issues/24898),
    [pr#24137](https://github.com/ceph/ceph/pull/24137), Mykola Golub)
-   librbd: fixed assert when flattening clone with zero overlap
    ([issue#35957](http://tracker.ceph.com/issues/35957),
    [issue#35702](http://tracker.ceph.com/issues/35702),
    [pr#24356](https://github.com/ceph/ceph/pull/24356), Jason Dillaman)
-   librbd: journaling unable request can not be sent to remote lock
    owner ([issue#26939](http://tracker.ceph.com/issues/26939),
    [issue#35712](http://tracker.ceph.com/issues/35712),
    [pr#24122](https://github.com/ceph/ceph/pull/24122), Mykola Golub)
-   librbd: object map improperly flagged as invalidated
    ([issue#24516](http://tracker.ceph.com/issues/24516),
    [issue#36225](http://tracker.ceph.com/issues/36225),
    [pr#24413](https://github.com/ceph/ceph/pull/24413), Jason Dillaman)
-   librgw: crashes in multisite configuration
    ([issue#36302](http://tracker.ceph.com/issues/36302),
    [issue#36415](http://tracker.ceph.com/issues/36415),
    [pr#24908](https://github.com/ceph/ceph/pull/24908), Casey Bodley)
-   mds: allows client to create .. and . dirents
    ([issue#32104](http://tracker.ceph.com/issues/32104),
    [pr#24384](https://github.com/ceph/ceph/pull/24384), Venky Shankar)
-   mds: curate priority of perf counters sent to mgr
    ([issue#35938](http://tracker.ceph.com/issues/35938),
    [issue#26991](http://tracker.ceph.com/issues/26991),
    [issue#32090](http://tracker.ceph.com/issues/32090),
    [issue#35837](http://tracker.ceph.com/issues/35837),
    [pr#24467](https://github.com/ceph/ceph/pull/24467), Patrick
    Donnelly, Venky Shankar)
-   mds: evict cap revoke non-responding clients
    ([pr#24661](https://github.com/ceph/ceph/pull/24661), Venky Shankar)
-   mimic:mds: fix mds damaged due to unexpected journal length
    ([issue#36199](http://tracker.ceph.com/issues/36199),
    [pr#24463](https://github.com/ceph/ceph/pull/24463), Zhi Zhang)
-   mds: internal op missing events time \'throttled\', \'all_read\',
    \'dispatched\' ([issue#36114](http://tracker.ceph.com/issues/36114),
    [issue#36195](http://tracker.ceph.com/issues/36195),
    [pr#24411](https://github.com/ceph/ceph/pull/24411), Yanhu Cao)
-   mds: migrate strays part by part when shutdown mds
    ([issue#26926](http://tracker.ceph.com/issues/26926),
    [issue#32092](http://tracker.ceph.com/issues/32092),
    [pr#24435](https://github.com/ceph/ceph/pull/24435), \"Yan, Zheng\")
-   mds: optimize the way how max export size is enforced
    ([issue#25131](http://tracker.ceph.com/issues/25131),
    [pr#23952](https://github.com/ceph/ceph/pull/23952), \"Yan, Zheng\")
-   mds: print is_laggy message once
    ([issue#35250](http://tracker.ceph.com/issues/35250),
    [issue#35719](http://tracker.ceph.com/issues/35719),
    [pr#24161](https://github.com/ceph/ceph/pull/24161), Patrick
    Donnelly)
-   mds: rctime may go back
    ([issue#35916](http://tracker.ceph.com/issues/35916),
    [issue#36136](http://tracker.ceph.com/issues/36136),
    [pr#24379](https://github.com/ceph/ceph/pull/24379), \"Yan, Zheng\")
-   mds: rctime not set on system inode (root) at startup
    ([issue#36221](http://tracker.ceph.com/issues/36221),
    [issue#36461](http://tracker.ceph.com/issues/36461),
    [pr#25042](https://github.com/ceph/ceph/pull/25042), Patrick
    Donnelly)
-   mds: reset heartbeat map at potential time-consuming places
    ([issue#26858](http://tracker.ceph.com/issues/26858),
    [pr#23506](https://github.com/ceph/ceph/pull/23506), Yan, Zheng,
    \"Yan, Zheng\")
-   mds: src/mds/MDLog.cc: 281: FAILED ceph_assert(!capped) during
    max_mds thrashing
    ([issue#36350](http://tracker.ceph.com/issues/36350),
    [issue#37093](http://tracker.ceph.com/issues/37093),
    [pr#25095](https://github.com/ceph/ceph/pull/25095), \"Yan, Zheng\",
    Jonathan Brielmaier)
-   mgr/DaemonServer: fix Session leak
    ([pr#24233](https://github.com/ceph/ceph/pull/24233), Sage Weil)
-   mgr/dashboard: Add http support to dashboard
    ([issue#36069](http://tracker.ceph.com/issues/36069),
    [pr#24734](https://github.com/ceph/ceph/pull/24734), Boris Ranto,
    Wido den Hollander)
-   mgr/dashboard: Add support for URI encode
    ([issue#24621](http://tracker.ceph.com/issues/24621),
    [issue#26856](http://tracker.ceph.com/issues/26856),
    [issue#24907](http://tracker.ceph.com/issues/24907),
    [pr#24488](https://github.com/ceph/ceph/pull/24488), Tiago Melo)
-   mgr/dashboard: Progress bar does not stop in TableKeyValueComponent
    ([issue#35925](http://tracker.ceph.com/issues/35925),
    [pr#24258](https://github.com/ceph/ceph/pull/24258), Volker Theile)
-   mgr/dashboard: Remove fieldsets when using CdTable
    ([issue#27851](http://tracker.ceph.com/issues/27851),
    [issue#26999](http://tracker.ceph.com/issues/26999),
    [pr#24478](https://github.com/ceph/ceph/pull/24478), Tiago Melo)
-   mgr: hold lock while accessing the request list and submittin
    request ([pr#25113](https://github.com/ceph/ceph/pull/25113), Jerry
    Lee)
-   mgr: \[restful\] deep_scrub is not a valid OSD command
    ([issue#36720](http://tracker.ceph.com/issues/36720),
    [issue#36749](http://tracker.ceph.com/issues/36749),
    [pr#25040](https://github.com/ceph/ceph/pull/25040), Boris Ranto)
-   mon: mgr options not parse propertly
    ([issue#35076](http://tracker.ceph.com/issues/35076),
    [issue#35836](http://tracker.ceph.com/issues/35836),
    [pr#24176](https://github.com/ceph/ceph/pull/24176), Sage Weil)
-   mon/OSDMonitor: invalidate max_failed_since on cancel_report
    ([issue#35930](http://tracker.ceph.com/issues/35930),
    [issue#35860](http://tracker.ceph.com/issues/35860),
    [pr#24281](https://github.com/ceph/ceph/pull/24281), xie xingguo)
-   mon: test if gid exists in pending for prepare_beacon
    ([issue#35848](http://tracker.ceph.com/issues/35848),
    [pr#24272](https://github.com/ceph/ceph/pull/24272), Patrick
    Donnelly)
-   msg/async: clean up local buffers on dispatch
    ([issue#36127](http://tracker.ceph.com/issues/36127),
    [issue#35987](http://tracker.ceph.com/issues/35987),
    [pr#24386](https://github.com/ceph/ceph/pull/24386), Greg Farnum)
-   msg: ceph_abort() when there are enough accepter errors in msg
    server ([issue#36219](http://tracker.ceph.com/issues/36219),
    [pr#25045](https://github.com/ceph/ceph/pull/25045),
    <penglaiyxy@gmail.com>)
-   msg: challenging authorizer messages appear at debug_ms=0
    ([issue#35251](http://tracker.ceph.com/issues/35251),
    [issue#35717](http://tracker.ceph.com/issues/35717),
    [pr#24113](https://github.com/ceph/ceph/pull/24113), Patrick
    Donnelly)
-   multisite: data full sync does not limit concurrent bucket sync
    ([issue#26897](http://tracker.ceph.com/issues/26897),
    [issue#36216](http://tracker.ceph.com/issues/36216),
    [pr#24536](https://github.com/ceph/ceph/pull/24536), Casey Bodley)
-   multisite: data sync error repo processing does not back off on
    empty ([issue#35979](http://tracker.ceph.com/issues/35979),
    [issue#26938](http://tracker.ceph.com/issues/26938),
    [pr#24319](https://github.com/ceph/ceph/pull/24319), Casey Bodley)
-   multisite: incremental data sync makes unnecessary call to
    RGWReadRemoteDataLogShardInfoCR
    ([issue#35977](http://tracker.ceph.com/issues/35977),
    [issue#26952](http://tracker.ceph.com/issues/26952),
    [pr#24710](https://github.com/ceph/ceph/pull/24710), Casey Bodley)
-   multisite: intermittent test_bucket_index_log_trim failures
    ([issue#36201](http://tracker.ceph.com/issues/36201),
    [issue#36034](http://tracker.ceph.com/issues/36034),
    [pr#24400](https://github.com/ceph/ceph/pull/24400), Casey Bodley)
-   multisite: invalid read in RGWCloneMetaLogCoroutine
    ([issue#36208](http://tracker.ceph.com/issues/36208),
    [issue#35851](http://tracker.ceph.com/issues/35851),
    [pr#24414](https://github.com/ceph/ceph/pull/24414), Casey Bodley)
-   multisite: segfault on shutdown/realm reload
    ([issue#35857](http://tracker.ceph.com/issues/35857),
    [issue#35543](http://tracker.ceph.com/issues/35543),
    [pr#24235](https://github.com/ceph/ceph/pull/24235), Casey Bodley)
-   os/bluestore: fix bloom filter num entry miscalculation in repairer
    ([issue#25001](http://tracker.ceph.com/issues/25001),
    [pr#24339](https://github.com/ceph/ceph/pull/24339), Igor Fedotov)
-   os/bluestore: handle spurious read errors
    ([issue#22464](http://tracker.ceph.com/issues/22464),
    [pr#24647](https://github.com/ceph/ceph/pull/24647), Paul Emmerich)
-   osd: add creating to pg_string_state
    ([issue#36174](http://tracker.ceph.com/issues/36174),
    [issue#36298](http://tracker.ceph.com/issues/36298),
    [pr#24601](https://github.com/ceph/ceph/pull/24601), Dan van der
    Ster)
-   osd: backport recent upmap fixes
    ([pr#25419](https://github.com/ceph/ceph/pull/25419), ningtao, xie
    xingguo)
-   osdc/Objecter: possible race condition with connection reset
    ([issue#36183](http://tracker.ceph.com/issues/36183),
    [issue#36296](http://tracker.ceph.com/issues/36296),
    [pr#24600](https://github.com/ceph/ceph/pull/24600), Jason Dillaman)
-   osd: crash in OpTracker::unregister_inflight_op via
    OSD::get_health_metrics
    ([issue#24889](http://tracker.ceph.com/issues/24889),
    [pr#23026](https://github.com/ceph/ceph/pull/23026), Radoslaw
    Zarzynski)
-   osdc: reduce ObjectCacher\'s memory fragments
    ([issue#36192](http://tracker.ceph.com/issues/36192),
    [issue#36643](http://tracker.ceph.com/issues/36643),
    [pr#24873](https://github.com/ceph/ceph/pull/24873), \"Yan, Zheng\")
-   osd/ECBackend: don\'t get result code of subchunk-read overwritten
    ([issue#35959](http://tracker.ceph.com/issues/35959),
    [issue#21769](http://tracker.ceph.com/issues/21769),
    [pr#24298](https://github.com/ceph/ceph/pull/24298), songweibin)
-   OSDMapMapping does not handle active.size() \> pool size
    ([issue#26866](http://tracker.ceph.com/issues/26866),
    [issue#35936](http://tracker.ceph.com/issues/35936),
    [pr#24431](https://github.com/ceph/ceph/pull/24431), Sage Weil)
-   osd/PG: avoid choose_acting picking want with \> pool size items
    ([issue#35963](http://tracker.ceph.com/issues/35963),
    [issue#35924](http://tracker.ceph.com/issues/35924),
    [pr#24344](https://github.com/ceph/ceph/pull/24344), Sage Weil)
-   osd/PrimaryLogPG: fix potential pg-log overtrimming
    ([pr#24309](https://github.com/ceph/ceph/pull/24309), xie xingguo)
-   osd: race condition opening heartbeat connection
    ([issue#36637](http://tracker.ceph.com/issues/36637),
    [issue#36602](http://tracker.ceph.com/issues/36602),
    [pr#25026](https://github.com/ceph/ceph/pull/25026), Sage Weil)
-   osd: RBD client IOPS pool stats are incorrect (2x higher; includes
    IO hints as an op)
    ([issue#24909](http://tracker.ceph.com/issues/24909),
    [issue#36557](http://tracker.ceph.com/issues/36557),
    [pr#25024](https://github.com/ceph/ceph/pull/25024), Jason Dillaman)
-   osd: Remove old bft= which has been superceded by backfill
    ([issue#36292](http://tracker.ceph.com/issues/36292),
    [issue#36170](http://tracker.ceph.com/issues/36170),
    [pr#24573](https://github.com/ceph/ceph/pull/24573), David Zafman)
-   qa: add test that builds example librados programs
    ([issue#36228](http://tracker.ceph.com/issues/36228),
    [issue#15100](http://tracker.ceph.com/issues/15100),
    [pr#24537](https://github.com/ceph/ceph/pull/24537), Nathan Cutler)
-   qa/ceph-ansible: Specify stable-3.2 branch
    ([pr#25191](https://github.com/ceph/ceph/pull/25191), Brad Hubbard)
-   qa: extend timeout for SessionMap flush
    ([issue#36156](http://tracker.ceph.com/issues/36156),
    [pr#24438](https://github.com/ceph/ceph/pull/24438), Patrick
    Donnelly)
-   qa: fsstress workunit does not execute in parallel on same host
    without clobbering files
    ([issue#36278](http://tracker.ceph.com/issues/36278),
    [issue#24177](http://tracker.ceph.com/issues/24177),
    [issue#36323](http://tracker.ceph.com/issues/36323),
    [issue#36184](http://tracker.ceph.com/issues/36184),
    [issue#36165](http://tracker.ceph.com/issues/36165),
    [issue#36153](http://tracker.ceph.com/issues/36153),
    [pr#24408](https://github.com/ceph/ceph/pull/24408), Patrick
    Donnelly)
-   qa: increase rm timeout for workunit cleanup
    ([issue#36501](http://tracker.ceph.com/issues/36501),
    [issue#36365](http://tracker.ceph.com/issues/36365),
    [pr#24684](https://github.com/ceph/ceph/pull/24684), Patrick
    Donnelly)
-   qa: install dependencies for rbd_workunit_kernel_untar_build
    ([issue#35074](http://tracker.ceph.com/issues/35074),
    [issue#35077](http://tracker.ceph.com/issues/35077),
    [pr#24240](https://github.com/ceph/ceph/pull/24240), Ilya Dryomov)
-   qa: remove knfs site from future releases
    ([issue#36075](http://tracker.ceph.com/issues/36075),
    [issue#36102](http://tracker.ceph.com/issues/36102),
    [pr#24269](https://github.com/ceph/ceph/pull/24269), Yuri Weinstein)
-   qa/suites/rados/thrash-old-clients: exclude packages for hammer,
    jewel ([pr#25193](https://github.com/ceph/ceph/pull/25193), Neha
    Ojha)
-   qa/suites/rgw/verify/tasks/cls_rgw: test cls_rgw
    ([issue#25024](http://tracker.ceph.com/issues/25024),
    [pr#23197](https://github.com/ceph/ceph/pull/23197), Casey Bodley,
    Sage Weil)
-   qa/tasks/qemu: use unique clone directory to avoid race with
    workunit ([issue#36542](http://tracker.ceph.com/issues/36542),
    [issue#36569](http://tracker.ceph.com/issues/36569),
    [pr#24811](https://github.com/ceph/ceph/pull/24811), Jason Dillaman)
-   qa: test_recovery_pool tries asok on wrong node
    ([issue#24928](http://tracker.ceph.com/issues/24928),
    [issue#24858](http://tracker.ceph.com/issues/24858),
    [pr#23087](https://github.com/ceph/ceph/pull/23087), Patrick
    Donnelly)
-   qa: tolerate failed rank while waiting for state
    ([issue#36280](http://tracker.ceph.com/issues/36280),
    [issue#35828](http://tracker.ceph.com/issues/35828),
    [pr#24572](https://github.com/ceph/ceph/pull/24572), Patrick
    Donnelly)
-   qa/workunits: replace \'realpath\' with \'readlink -f\' in
    fsstress.sh ([issue#36409](http://tracker.ceph.com/issues/36409),
    [issue#36430](http://tracker.ceph.com/issues/36430),
    [issue#35538](http://tracker.ceph.com/issues/35538),
    [pr#24622](https://github.com/ceph/ceph/pull/24622), Ilya Dryomov,
    Jason Dillaman)
-   RADOS: probably missing clone location for async_recovery_targets
    ([issue#35964](http://tracker.ceph.com/issues/35964),
    [issue#35546](http://tracker.ceph.com/issues/35546),
    [pr#24345](https://github.com/ceph/ceph/pull/24345), xie xingguo)
-   mimic:rbd: fix error import when the input is a pipe
    ([issue#35705](http://tracker.ceph.com/issues/35705),
    [issue#34536](http://tracker.ceph.com/issues/34536),
    [pr#24002](https://github.com/ceph/ceph/pull/24002), songweibin)
-   \[rbd-mirror\] failed assertion when updating mirror status
    ([issue#36084](http://tracker.ceph.com/issues/36084),
    [issue#36120](http://tracker.ceph.com/issues/36120),
    [pr#24321](https://github.com/ceph/ceph/pull/24321), Jason Dillaman)
-   rbd: \[rbd-mirror\] forced promotion after killing remote cluster
    results in stuck state
    ([issue#36659](http://tracker.ceph.com/issues/36659),
    [issue#36693](http://tracker.ceph.com/issues/36693),
    [pr#24952](https://github.com/ceph/ceph/pull/24952), Jonathan
    Brielmaier, Jason Dillaman)
-   rbd: \[rbd-mirror\] periodic mirror status timer might fail to be
    scheduled ([issue#36500](http://tracker.ceph.com/issues/36500),
    [issue#36555](http://tracker.ceph.com/issues/36555),
    [pr#24916](https://github.com/ceph/ceph/pull/24916), Jason Dillaman)
-   rbd: rbd-nbd: do not ceph_abort() after print the usages
    ([issue#36660](http://tracker.ceph.com/issues/36660),
    [issue#36713](http://tracker.ceph.com/issues/36713),
    [pr#24988](https://github.com/ceph/ceph/pull/24988), Shiyang Ruan)
-   rbd: TokenBucketThrottle: use reference to m_blockers.front() and
    then update it ([issue#36529](http://tracker.ceph.com/issues/36529),
    [issue#36475](http://tracker.ceph.com/issues/36475),
    [pr#24915](https://github.com/ceph/ceph/pull/24915), Dongsheng Yang)
-   Revert \"mimic: cephfs-journal-tool: enable purge_queue journal\'s
    event commands\"
    ([issue#36346](http://tracker.ceph.com/issues/36346),
    [issue#24604](http://tracker.ceph.com/issues/24604),
    [pr#24485](https://github.com/ceph/ceph/pull/24485), Xuehan Xu,
    \"Yan, Zheng\")
-   rgw: abort_bucket_multiparts() ignores individual NoSuchUpload
    errors ([issue#36129](http://tracker.ceph.com/issues/36129),
    [issue#35986](http://tracker.ceph.com/issues/35986),
    [pr#24388](https://github.com/ceph/ceph/pull/24388), Casey Bodley)
-   rgw-admin: reshard add can add a non existant bucket
    ([issue#36449](http://tracker.ceph.com/issues/36449),
    [issue#36756](http://tracker.ceph.com/issues/36756),
    [pr#25087](https://github.com/ceph/ceph/pull/25087), Jonathan
    Brielmaier, Abhishek Lekshmanan)
-   rgw: async sync_object and remove_object does not access coroutine
    me... ([issue#36138](http://tracker.ceph.com/issues/36138),
    [issue#35905](http://tracker.ceph.com/issues/35905),
    [pr#24417](https://github.com/ceph/ceph/pull/24417), Tianshan Qu)
-   rgw/beast: drop privileges after binding ports
    ([issue#36041](http://tracker.ceph.com/issues/36041),
    [pr#24436](https://github.com/ceph/ceph/pull/24436), Paul Emmerich)
-   rgw: beast frontend fails to parse ipv6 endpoints
    ([issue#36662](http://tracker.ceph.com/issues/36662),
    [issue#36734](http://tracker.ceph.com/issues/36734),
    [pr#25079](https://github.com/ceph/ceph/pull/25079), Jonathan
    Brielmaier, Casey Bodley)
-   rgw: cls_user_remove_bucket does not write the modified
    cls_user_stats ([issue#36496](http://tracker.ceph.com/issues/36496),
    [issue#36533](http://tracker.ceph.com/issues/36533),
    [pr#24910](https://github.com/ceph/ceph/pull/24910), Casey Bodley)
-   rgw: default quota not set in radosgw for Openstack users
    ([issue#24595](http://tracker.ceph.com/issues/24595),
    [issue#36223](http://tracker.ceph.com/issues/36223),
    [pr#24907](https://github.com/ceph/ceph/pull/24907), Casey Bodley)
-   mimic:rgw: fix chunked-encoding for chunks \>1MiB
    ([issue#36125](http://tracker.ceph.com/issues/36125),
    [issue#35990](http://tracker.ceph.com/issues/35990),
    [pr#24363](https://github.com/ceph/ceph/pull/24363), Robin H.
    Johnson)
-   rgw: fix deadlock on RGWIndexCompletionManager::stop
    ([issue#26949](http://tracker.ceph.com/issues/26949),
    [issue#35710](http://tracker.ceph.com/issues/35710),
    [pr#24101](https://github.com/ceph/ceph/pull/24101), Yao Zongyou)
-   mimic:rgw: fix leak of curl handle on shutdown
    ([issue#35715](http://tracker.ceph.com/issues/35715),
    [issue#36213](http://tracker.ceph.com/issues/36213),
    [pr#24518](https://github.com/ceph/ceph/pull/24518), Casey Bodley)
-   mimic:rgw: list bucket can not show the object uploaded by
    RGWPostObj when enable bucket versioning
    ([pr#24571](https://github.com/ceph/ceph/pull/24571), yuliyang)
-   rgw: radosgw-admin user stats are incorrect when dynamic re-sharding
    is enabled ([issue#36535](http://tracker.ceph.com/issues/36535),
    [pr#24911](https://github.com/ceph/ceph/pull/24911), Casey Bodley)
-   rgw: raise debug level on redundant data sync error messages
    ([issue#35830](http://tracker.ceph.com/issues/35830),
    [issue#36140](http://tracker.ceph.com/issues/36140),
    [pr#24418](https://github.com/ceph/ceph/pull/24418), Casey Bodley)
-   rgw: raise default rgw_curl_low_speed_time to 300 seconds
    ([issue#35708](http://tracker.ceph.com/issues/35708),
    [issue#27989](http://tracker.ceph.com/issues/27989),
    [pr#24071](https://github.com/ceph/ceph/pull/24071), Casey Bodley)
-   rgw: renew resharding locks to prevent expiration
    ([issue#36687](http://tracker.ceph.com/issues/36687),
    [issue#27219](http://tracker.ceph.com/issues/27219),
    [issue#34307](http://tracker.ceph.com/issues/34307),
    [pr#24899](https://github.com/ceph/ceph/pull/24899), Orit
    Wasserman, J. Eric Ivancich)
-   rgw: resharding produces invalid values of bucket stats
    ([issue#36290](http://tracker.ceph.com/issues/36290),
    [issue#36381](http://tracker.ceph.com/issues/36381),
    [pr#24526](https://github.com/ceph/ceph/pull/24526), Abhishek
    Lekshmanan)
-   mimic:rgw: return x-amz-version-id: null when delete obj in
    versioning ([issue#35814](http://tracker.ceph.com/issues/35814),
    [pr#24189](https://github.com/ceph/ceph/pull/24189), yuliyang)
-   rgw: RGWAsyncGetBucketInstanceInfo does not access coroutine memory
    ([issue#36211](http://tracker.ceph.com/issues/36211),
    [issue#35812](http://tracker.ceph.com/issues/35812),
    [pr#24516](https://github.com/ceph/ceph/pull/24516), Casey Bodley)
-   rgw: set default objecter_inflight_ops = 24576
    ([issue#36571](http://tracker.ceph.com/issues/36571),
    [issue#25109](http://tracker.ceph.com/issues/25109),
    [pr#24860](https://github.com/ceph/ceph/pull/24860), Jonathan
    Brielmaier, Matt Benjamin)
-   rgw: support server-side encryption when SSL is terminated in a
    proxy ([issue#36645](http://tracker.ceph.com/issues/36645),
    [issue#27221](http://tracker.ceph.com/issues/27221),
    [pr#24931](https://github.com/ceph/ceph/pull/24931), Jonathan
    Brielmaier, Casey Bodley)
-   rgw: use-after-free from
    RGWRadosGetOmapKeysCR::\~RGWRadosGetOmapKeysCR
    ([issue#21154](http://tracker.ceph.com/issues/21154),
    [issue#36537](http://tracker.ceph.com/issues/36537),
    [issue#36539](http://tracker.ceph.com/issues/36539),
    [pr#24912](https://github.com/ceph/ceph/pull/24912), Casey Bodley,
    Sage Weil)
-   rpm: use updated gperftools
    ([issue#36508](http://tracker.ceph.com/issues/36508),
    [issue#35969](http://tracker.ceph.com/issues/35969),
    [pr#24260](https://github.com/ceph/ceph/pull/24260), Brad Hubbard,
    Kefu Chai)
-   segv in BlueStore::OldExtent::create
    ([issue#36592](http://tracker.ceph.com/issues/36592),
    [issue#36526](http://tracker.ceph.com/issues/36526),
    [pr#24745](https://github.com/ceph/ceph/pull/24745), Sage Weil)
-   test/librbd: not valid to have different parents between image
    snapshots ([issue#36117](http://tracker.ceph.com/issues/36117),
    [pr#24244](https://github.com/ceph/ceph/pull/24244), Jason Dillaman)
-   \[test\] periodic seg faults within unittest_librbd
    ([issue#36220](http://tracker.ceph.com/issues/36220),
    [issue#36238](http://tracker.ceph.com/issues/36238),
    [pr#24711](https://github.com/ceph/ceph/pull/24711), Jason Dillaman)
-   test/rbd_mirror: race in WaitingOnLeaderReleaseLeader
    ([issue#36236](http://tracker.ceph.com/issues/36236),
    [issue#36276](http://tracker.ceph.com/issues/36276),
    [pr#24551](https://github.com/ceph/ceph/pull/24551), Mykola Golub)
-   tests: ceph-admin-commands.sh workunit does not log what it\'s doing
    ([issue#37153](http://tracker.ceph.com/issues/37153),
    [issue#37089](http://tracker.ceph.com/issues/37089),
    [pr#25085](https://github.com/ceph/ceph/pull/25085), Nathan Cutler)
-   tests: librados api aio tests race condition
    ([issue#24587](http://tracker.ceph.com/issues/24587),
    [issue#36647](http://tracker.ceph.com/issues/36647),
    [pr#25027](https://github.com/ceph/ceph/pull/25027), Josh Durgin)
-   tests: make readable.sh fail if it doesn\'t run anything
    ([pr#25050](https://github.com/ceph/ceph/pull/25050), Greg Farnum)
-   tests: rbd: move OpenStack devstack test to rocky release
    ([issue#36410](http://tracker.ceph.com/issues/36410),
    [issue#36428](http://tracker.ceph.com/issues/36428),
    [pr#24913](https://github.com/ceph/ceph/pull/24913), Jason Dillaman)
-   tests: unittest_rbd_mirror:
    TestMockImageMap.AddInstancePingPongImageTest: Value of: it !=
    peer_ack_ctxs-\>end()
    ([issue#36683](http://tracker.ceph.com/issues/36683),
    [issue#36689](http://tracker.ceph.com/issues/36689),
    [pr#24946](https://github.com/ceph/ceph/pull/24946), Mykola Golub,
    Jonathan Brielmaier)
-   tests: use timeout for fs asok operations
    ([issue#36335](http://tracker.ceph.com/issues/36335),
    [issue#36503](http://tracker.ceph.com/issues/36503),
    [pr#25332](https://github.com/ceph/ceph/pull/25332), Patrick
    Donnelly)
-   tests: /usr/bin/ld: cannot find -lradospp in rados mimic
    ([issue#37396](http://tracker.ceph.com/issues/37396),
    [pr#25285](https://github.com/ceph/ceph/pull/25285), Nathan Cutler)
-   test: Use a grep pattern that works across releases
    ([issue#35845](http://tracker.ceph.com/issues/35845),
    [issue#35909](http://tracker.ceph.com/issues/35909),
    [pr#24017](https://github.com/ceph/ceph/pull/24017), David Zafman)
-   tools: ceph-objectstore-tool: Allow target level as first positional
    ... ([issue#35846](http://tracker.ceph.com/issues/35846),
    [issue#35992](http://tracker.ceph.com/issues/35992),
    [pr#24116](https://github.com/ceph/ceph/pull/24116), David Zafman)

## v13.2.2 Mimic

This is the second bugfix release of the Mimic v13.2.x long term stable
release series. This release contains many fixes across all components
of Ceph. We recommend that all users upgrade.

-   This version contains an upgrade bug,
    <http://tracker.ceph.com/issues/36686>, due to which upgrading
    during recovery/backfill can cause OSDs to fail. This bug can be
    worked around, either by restarting all the OSDs after the upgrade,
    or by upgrading when all PGs are in \"active+clean\" state.

    If you have successfully upgraded to 13.2.2, this issue should not
    impact you. Going forward, we are working on a clean upgrade path
    for this feature.

### Changelog

-   build/ops: Boost system library is no longer required to compile and
    link example librados program
    ([issue#25073](http://tracker.ceph.com/issues/25073),
    [issue#25054](http://tracker.ceph.com/issues/25054),
    [pr#23201](https://github.com/ceph/ceph/pull/23201), Nathan Cutler)
-   build/ops: debian/rules: fix ceph-mgr .pyc files left behind
    ([issue#27059](http://tracker.ceph.com/issues/27059),
    [issue#26883](http://tracker.ceph.com/issues/26883),
    [pr#23831](https://github.com/ceph/ceph/pull/23831), Dan Mick)
-   build/ops: mimic 13.2.0 doesn\'t build in Fedora rawhide
    ([issue#24449](http://tracker.ceph.com/issues/24449),
    [issue#24905](http://tracker.ceph.com/issues/24905),
    [pr#23885](https://github.com/ceph/ceph/pull/23885), Kefu Chai)
-   ceph-disk: compatibility fix for python 3
    ([pr#24008](https://github.com/ceph/ceph/pull/24008), Tim Serong)
-   ceph-disk: return a list instead of an iterator
    ([pr#23392](https://github.com/ceph/ceph/pull/23392), Alexander
    Graul)
-   cephfs-journal-tool: enable purge_queue journal\'s event commands
    ([issue#24604](http://tracker.ceph.com/issues/24604),
    [issue#26989](http://tracker.ceph.com/issues/26989),
    [pr#23818](https://github.com/ceph/ceph/pull/23818), Xuehan Xu)
-   ceph tell osd.x bench writes resulting JSON to stderr instead of
    stdout ([issue#35942](http://tracker.ceph.com/issues/35942),
    [issue#24022](http://tracker.ceph.com/issues/24022),
    [pr#24041](https://github.com/ceph/ceph/pull/24041), Коренберг
    Маркr, John Spray, Kefu Chai)
-   ceph-volume add a \_\_release\_\_ string, to help
    version-conditional calls
    ([issue#25169](http://tracker.ceph.com/issues/25169),
    [pr#23333](https://github.com/ceph/ceph/pull/23333), Alfredo Deza)
-   ceph-volume: adds test for [ceph-volume lvm list
    /dev/sda]{.title-ref}
    ([issue#24784](http://tracker.ceph.com/issues/24784),
    [issue#24957](http://tracker.ceph.com/issues/24957),
    [pr#23349](https://github.com/ceph/ceph/pull/23349), Andrew Schoen)
-   ceph-volume: an OSD ID must exist and be destroyed before reuse
    ([pr#23101](https://github.com/ceph/ceph/pull/23101), Andrew Schoen,
    Ron Allred)
-   ceph-volume: batch: allow journal+block.db sizing on the CLI
    ([issue#36088](http://tracker.ceph.com/issues/36088),
    [pr#24208](https://github.com/ceph/ceph/pull/24208), Alfredo Deza)
-   ceph-volume batch: allow \--osds-per-device, default it to 1
    ([issue#35913](http://tracker.ceph.com/issues/35913),
    [pr#24079](https://github.com/ceph/ceph/pull/24079), Alfredo Deza)
-   ceph-volume batch carve out lvs for bluestore
    ([issue#34535](http://tracker.ceph.com/issues/34535),
    [pr#24074](https://github.com/ceph/ceph/pull/24074), Alfredo Deza)
-   ceph-volume batch command
    ([pr#23777](https://github.com/ceph/ceph/pull/23777), Alfredo Deza)
-   ceph-volume: batch tests for mixed-type of devices
    ([issue#35535](http://tracker.ceph.com/issues/35535),
    [issue#27210](http://tracker.ceph.com/issues/27210),
    [pr#23966](https://github.com/ceph/ceph/pull/23966), Alfredo Deza)
-   ceph_volume_client: allow atomic update of RADOS objects
    ([issue#24173](http://tracker.ceph.com/issues/24173),
    [issue#24863](http://tracker.ceph.com/issues/24863),
    [pr#23878](https://github.com/ceph/ceph/pull/23878), Rishabh Dave)
-   CephVolumeClient: delay required after adding data pool to MDSMap
    ([issue#25206](http://tracker.ceph.com/issues/25206),
    [pr#23725](https://github.com/ceph/ceph/pull/23725), Patrick
    Donnelly)
-   ceph-volume: do not use stdin in luminous
    ([issue#25173](http://tracker.ceph.com/issues/25173),
    [pr#23368](https://github.com/ceph/ceph/pull/23368), Alfredo Deza)
-   ceph-volume: earlier detection for \--journal and \--filestore flag
    requirements ([issue#24794](http://tracker.ceph.com/issues/24794),
    [pr#24205](https://github.com/ceph/ceph/pull/24205), Alfredo Deza)
-   ceph-volume enable the ceph-osd during lvm activation
    ([issue#24152](http://tracker.ceph.com/issues/24152),
    [pr#23393](https://github.com/ceph/ceph/pull/23393), Dan van der
    Ster, Alfredo Deza)
-   ceph-volume expand auto engine for multiple devices on filestore
    ([pr#23807](https://github.com/ceph/ceph/pull/23807), Andrew Schoen,
    Alfredo Deza)
-   ceph-volume: expand auto engine for single type devices on filestore
    ([pr#23786](https://github.com/ceph/ceph/pull/23786), Alfredo Deza)
-   ceph-volume fix zap not working with LVs
    ([issue#35970](http://tracker.ceph.com/issues/35970),
    [pr#24081](https://github.com/ceph/ceph/pull/24081), Alfredo Deza)
-   ceph-volume lvm.activate conditional mon-config on prime-osd-dir
    ([issue#25216](http://tracker.ceph.com/issues/25216),
    [pr#23400](https://github.com/ceph/ceph/pull/23400), Alfredo Deza)
-   ceph-volume: [lvm batch]{.title-ref} allow extra flags (like
    dmcrypt) for bluestore
    ([pr#23780](https://github.com/ceph/ceph/pull/23780), Alfredo Deza)
-   ceph-volume: [lvm batch]{.title-ref} documentation and man page
    updates ([pr#23756](https://github.com/ceph/ceph/pull/23756),
    Alfredo Deza)
-   ceph-volume lvm.batch remove non-existent sys_api property
    ([issue#34310](http://tracker.ceph.com/issues/34310),
    [pr#23810](https://github.com/ceph/ceph/pull/23810), Alfredo Deza)
-   ceph-volume lvm.listing only include devices if they exist
    ([issue#24952](http://tracker.ceph.com/issues/24952),
    [pr#23149](https://github.com/ceph/ceph/pull/23149), Alfredo Deza)
-   ceph-volume: process.call with stdin in Python 3 fix
    ([issue#24993](http://tracker.ceph.com/issues/24993),
    [pr#23239](https://github.com/ceph/ceph/pull/23239), Alfredo Deza)
-   ceph-volume: PVolumes.get() should return one PV when using name or
    uuid ([issue#24784](http://tracker.ceph.com/issues/24784),
    [pr#23327](https://github.com/ceph/ceph/pull/23327), Andrew Schoen)
-   ceph-volume: refuse to zap mapper devices
    ([issue#24504](http://tracker.ceph.com/issues/24504),
    [pr#22965](https://github.com/ceph/ceph/pull/22965), Andrew Schoen)
-   ceph-volume: Restore SELinux context
    ([pr#23295](https://github.com/ceph/ceph/pull/23295), Boris Ranto)
-   ceph-volume: run tests without waiting on ceph repos
    ([pr#23806](https://github.com/ceph/ceph/pull/23806), Andrew Schoen)
-   ceph-volume tests/functional add mgrs daemons to lvm tests
    ([pr#23784](https://github.com/ceph/ceph/pull/23784), Alfredo Deza)
-   ceph-volume: tests.functional inherit SSH_ARGS from ansible
    ([pr#23812](https://github.com/ceph/ceph/pull/23812), Alfredo Deza)
-   ceph-volume: update batch documentation to explain filestore
    strategies ([issue#34309](http://tracker.ceph.com/issues/34309),
    [pr#23826](https://github.com/ceph/ceph/pull/23826), Alfredo Deza)
-   ceph-volume: update version of ansible to 2.6.x for simple tests
    ([pr#23269](https://github.com/ceph/ceph/pull/23269), Andrew Schoen)
-   client: add inst to asok status output
    ([issue#24724](http://tracker.ceph.com/issues/24724),
    [issue#24931](http://tracker.ceph.com/issues/24931),
    [pr#23109](https://github.com/ceph/ceph/pull/23109), Patrick
    Donnelly)
-   client: check for unmounted condition before printing debug output
    ([issue#25213](http://tracker.ceph.com/issues/25213),
    [issue#26914](http://tracker.ceph.com/issues/26914),
    [pr#23603](https://github.com/ceph/ceph/pull/23603), Jeff Layton)
-   client: requests that do name lookup may be sent to wrong mds
    ([issue#26984](http://tracker.ceph.com/issues/26984),
    [issue#26860](http://tracker.ceph.com/issues/26860),
    [pr#23700](https://github.com/ceph/ceph/pull/23700), \"Yan, Zheng\")
-   cls/rgw: add rgw_usage_log_entry type to ceph-dencoder
    ([issue#35070](http://tracker.ceph.com/issues/35070),
    [pr#23857](https://github.com/ceph/ceph/pull/23857), Vaibhav
    Bhembre)
-   common: check completion condition before waiting
    ([issue#25007](http://tracker.ceph.com/issues/25007),
    [issue#25222](http://tracker.ceph.com/issues/25222),
    [pr#23435](https://github.com/ceph/ceph/pull/23435), Patrick
    Donnelly)
-   core: deep scrub cannot find the bitrot if the object is cached
    ([issue#35068](http://tracker.ceph.com/issues/35068),
    [pr#23873](https://github.com/ceph/ceph/pull/23873), Adam C.
    Emerson, Xiaoguang Wang)
-   core: Fix 25085 and 24949
    ([pr#23272](https://github.com/ceph/ceph/pull/23272), David Zafman)
-   core: force-create-pg broken
    ([issue#34532](http://tracker.ceph.com/issues/34532),
    [issue#26940](http://tracker.ceph.com/issues/26940),
    [pr#23872](https://github.com/ceph/ceph/pull/23872), Sage Weil)
-   core: Limit pg log length during recovery/backfill so that we don\'t
    run out of memory
    ([issue#21416](http://tracker.ceph.com/issues/21416),
    [pr#23403](https://github.com/ceph/ceph/pull/23403), Neha Ojha)
-   doc: broken bash example in bluestore migration
    ([issue#35078](http://tracker.ceph.com/issues/35078),
    [pr#23854](https://github.com/ceph/ceph/pull/23854), Alfredo Deza)
-   doc: Fix broken urls
    ([issue#25185](http://tracker.ceph.com/issues/25185),
    [issue#26916](http://tracker.ceph.com/issues/26916),
    [pr#23607](https://github.com/ceph/ceph/pull/23607), Jos Collin)
-   doc: <http://docs.ceph.com/docs/mimic/rados/operations/pg-states/>
    ([issue#25055](http://tracker.ceph.com/issues/25055),
    [pr#23163](https://github.com/ceph/ceph/pull/23163), Jan Fajerski,
    Nathan Cutler)
-   docs: radosgw: ldap-auth: fixed option name
    \'rgw_ldap_searchfilter\'
    ([issue#32129](http://tracker.ceph.com/issues/32129),
    [pr#23956](https://github.com/ceph/ceph/pull/23956), Konstantin
    Shalygin)
-   filestore: add pgid in filestore pg dir split log message
    ([issue#25225](http://tracker.ceph.com/issues/25225),
    [pr#23453](https://github.com/ceph/ceph/pull/23453), Vikhyat Umrao)
-   kv: MergeOperator name() returns string, and caller calls c_str() on
    the temporary ([issue#26907](http://tracker.ceph.com/issues/26907),
    [issue#26875](http://tracker.ceph.com/issues/26875),
    [pr#23865](https://github.com/ceph/ceph/pull/23865), Sage Weil)
-   libradosstriper conditional compile
    ([issue#27213](http://tracker.ceph.com/issues/27213),
    [pr#23869](https://github.com/ceph/ceph/pull/23869), Kefu Chai,
    Jesse Williamson)
-   librbd: deep-copy should not write to objects that cannot exist
    ([issue#25000](http://tracker.ceph.com/issues/25000),
    [issue#25083](http://tracker.ceph.com/issues/25083),
    [pr#23358](https://github.com/ceph/ceph/pull/23358), Jason Dillaman)
-   librbd: validate data pool for self-managed snapshot support
    ([issue#24945](http://tracker.ceph.com/issues/24945),
    [pr#23560](https://github.com/ceph/ceph/pull/23560), Mykola Golub)
-   link against libstdc++ statically
    ([issue#26880](http://tracker.ceph.com/issues/26880),
    [issue#25209](http://tracker.ceph.com/issues/25209),
    [pr#23490](https://github.com/ceph/ceph/pull/23490), Kefu Chai)
-   mds: avoid using g_conf-\>get_val\<\...\>(\...) in hot path
    ([issue#24820](http://tracker.ceph.com/issues/24820),
    [pr#23407](https://github.com/ceph/ceph/pull/23407), \"Yan, Zheng\")
-   mds: calculate load by checking self CPU usage
    ([issue#26834](http://tracker.ceph.com/issues/26834),
    [issue#26888](http://tracker.ceph.com/issues/26888),
    [pr#23503](https://github.com/ceph/ceph/pull/23503), \"Yan, Zheng\")
-   mds: crash when dumping ops in flight
    ([issue#26894](http://tracker.ceph.com/issues/26894),
    [issue#26982](http://tracker.ceph.com/issues/26982),
    [pr#23672](https://github.com/ceph/ceph/pull/23672), \"Yan, Zheng\")
-   mds: dump recent events on respawn
    ([issue#25040](http://tracker.ceph.com/issues/25040),
    [pr#23275](https://github.com/ceph/ceph/pull/23275), Patrick
    Donnelly)
-   mds: explain delayed client_request due to subtree migration
    ([issue#26988](http://tracker.ceph.com/issues/26988),
    [issue#24840](http://tracker.ceph.com/issues/24840),
    [pr#23792](https://github.com/ceph/ceph/pull/23792), Yan, Zheng,
    \"Yan, Zheng\")
-   mds: handle discontinuous mdsmap
    ([issue#24856](http://tracker.ceph.com/issues/24856),
    [pr#23180](https://github.com/ceph/ceph/pull/23180), \"Yan, Zheng\")
-   mds: health warning for slow metadata IO
    ([issue#24879](http://tracker.ceph.com/issues/24879),
    [issue#25045](http://tracker.ceph.com/issues/25045),
    [pr#23343](https://github.com/ceph/ceph/pull/23343), \"Yan, Zheng\")
-   mds: increase debug level for dropped client cap msg
    ([issue#25042](http://tracker.ceph.com/issues/25042),
    [pr#23309](https://github.com/ceph/ceph/pull/23309), Patrick
    Donnelly)
-   mds: introduce cephfs\' own feature bits
    ([issue#14456](http://tracker.ceph.com/issues/14456),
    [issue#24914](http://tracker.ceph.com/issues/24914),
    [pr#23105](https://github.com/ceph/ceph/pull/23105), Yan, Zheng,
    \"Yan, Zheng\", Patrick Donnelly)
-   mds: mark beacons as high priority
    ([issue#26905](http://tracker.ceph.com/issues/26905),
    [issue#26899](http://tracker.ceph.com/issues/26899),
    [pr#23565](https://github.com/ceph/ceph/pull/23565), Patrick
    Donnelly)
-   mds: MDBalancer::try_rebalance() may stop prematurely
    ([issue#32086](http://tracker.ceph.com/issues/32086),
    [issue#26973](http://tracker.ceph.com/issues/26973),
    [pr#23883](https://github.com/ceph/ceph/pull/23883), \"Yan, Zheng\")
-   MDSMonitor: note ignored beacons/map changes at higher debug level
    ([issue#26898](http://tracker.ceph.com/issues/26898),
    [issue#26929](http://tracker.ceph.com/issues/26929),
    [pr#23704](https://github.com/ceph/ceph/pull/23704), Patrick
    Donnelly)
-   mds,osd,mon,msg: use intrusive_ptr for holding Connection::priv
    ([issue#20924](http://tracker.ceph.com/issues/20924),
    [pr#22339](https://github.com/ceph/ceph/pull/22339), \"Yan, Zheng\",
    Kefu Chai)
-   mds: print mdsmap processed at low debug level
    ([issue#25035](http://tracker.ceph.com/issues/25035),
    [pr#23196](https://github.com/ceph/ceph/pull/23196), Patrick
    Donnelly)
-   mds: scrub doesn\'t always return JSON results
    ([issue#23958](http://tracker.ceph.com/issues/23958),
    [issue#25037](http://tracker.ceph.com/issues/25037),
    [pr#23225](https://github.com/ceph/ceph/pull/23225), Venky Shankar)
-   mds: use fast dispatch to handle MDSBeacon
    ([issue#23519](http://tracker.ceph.com/issues/23519),
    [issue#26923](http://tracker.ceph.com/issues/26923),
    [pr#23703](https://github.com/ceph/ceph/pull/23703), \"Yan, Zheng\")
-   mgr balancer does not save optimized plan but latest
    ([issue#32082](http://tracker.ceph.com/issues/32082),
    [issue#27000](http://tracker.ceph.com/issues/27000),
    [pr#23782](https://github.com/ceph/ceph/pull/23782), Stefan Priebe)
-   mgr: \"balancer execute\" only requires read permissions
    ([issue#26912](http://tracker.ceph.com/issues/26912),
    [issue#25345](http://tracker.ceph.com/issues/25345),
    [pr#23583](https://github.com/ceph/ceph/pull/23583), John Spray)
-   mgrc: enable disabling stats via mgr_stats_threshold
    ([issue#25197](http://tracker.ceph.com/issues/25197),
    [issue#26837](http://tracker.ceph.com/issues/26837),
    [pr#23463](https://github.com/ceph/ceph/pull/23463), John Spray)
-   mgr/dashboard: Display RGW user/bucket quota max size in human
    readable form ([issue#35706](http://tracker.ceph.com/issues/35706),
    [pr#24047](https://github.com/ceph/ceph/pull/24047), Volker Theile)
-   mgr/dashboard: Escape regex pattern in DeletionModalComponent
    ([issue#24902](http://tracker.ceph.com/issues/24902),
    [issue#26920](http://tracker.ceph.com/issues/26920),
    [pr#23669](https://github.com/ceph/ceph/pull/23669), Tiago Melo)
-   mgr/dashboard: Prevent RGW API user deletion
    ([pr#22670](https://github.com/ceph/ceph/pull/22670), Volker Theile)
-   mgr/dashboard: RestClient can\'t handle ProtocolError exceptions
    ([pr#23875](https://github.com/ceph/ceph/pull/23875), Volker Theile)
-   mgr/dashboard: RGW is not working if an URL prefix is defined
    ([pr#23203](https://github.com/ceph/ceph/pull/23203), Volker Theile)
-   mgr/dashboard: URL prefix is not working
    ([issue#25120](http://tracker.ceph.com/issues/25120),
    [pr#23874](https://github.com/ceph/ceph/pull/23874), Ricardo
    Marques)
-   mgr: Ignore daemon if no metadata was returned
    ([pr#23356](https://github.com/ceph/ceph/pull/23356), Wido den
    Hollander)
-   mgr/MgrClient: Protect daemon_health_metrics
    ([issue#23352](http://tracker.ceph.com/issues/23352),
    [pr#23458](https://github.com/ceph/ceph/pull/23458), Kjetil
    Joergensen, Brad Hubbard)
-   mgr: Sync the prometheus module
    ([pr#23215](https://github.com/ceph/ceph/pull/23215), Boris Ranto)
-   mon: add purge-new
    ([pr#23259](https://github.com/ceph/ceph/pull/23259), Sage Weil)
-   mon: Automatically set expected_num_objects for new pools with
    \>=100 PGs per OSD
    ([issue#24687](http://tracker.ceph.com/issues/24687),
    [issue#25144](http://tracker.ceph.com/issues/25144),
    [pr#23860](https://github.com/ceph/ceph/pull/23860), Douglas Fuller)
-   multisite: intermittent failures in test_bucket_sync_disable_enable
    ([issue#26895](http://tracker.ceph.com/issues/26895),
    [issue#26980](http://tracker.ceph.com/issues/26980),
    [pr#23856](https://github.com/ceph/ceph/pull/23856), Casey Bodley)
-   multisite: object metadata operations are skipped by sync
    ([issue#24367](http://tracker.ceph.com/issues/24367),
    [issue#24986](http://tracker.ceph.com/issues/24986),
    [pr#23172](https://github.com/ceph/ceph/pull/23172), Casey Bodley)
-   object errors found in be_select_auth_object() aren\'t logged the
    same ([issue#32108](http://tracker.ceph.com/issues/32108),
    [issue#25108](http://tracker.ceph.com/issues/25108),
    [pr#23870](https://github.com/ceph/ceph/pull/23870), David Zafman)
-   os/bluestore: bluestore_buffer_hit_bytes perf counter doesn\'t reset
    ([pr#23772](https://github.com/ceph/ceph/pull/23772), Igor Fedotov)
-   os/bluestore/BlueStore.cc: 1025: FAILED assert(buffer_bytes \>=
    b-\>length) from ObjectStore/StoreTest.ColSplitTest2/2
    ([issue#24439](http://tracker.ceph.com/issues/24439),
    [issue#26944](http://tracker.ceph.com/issues/26944),
    [pr#23748](https://github.com/ceph/ceph/pull/23748), Sage Weil)
-   os/bluestore: fix assertion in StupidAllocator::get_fragmentation
    ([pr#23676](https://github.com/ceph/ceph/pull/23676), Igor Fedotov)
-   osd: do_sparse_read(): Verify checksum earlier so we will try to
    repair ([issue#24875](http://tracker.ceph.com/issues/24875),
    [pr#23378](https://github.com/ceph/ceph/pull/23378), David Zafman)
-   osd,mon: increase mon_max_pg_per_osd to 300
    ([issue#25176](http://tracker.ceph.com/issues/25176),
    [pr#23861](https://github.com/ceph/ceph/pull/23861), Neha Ojha)
-   osd/OSDMap: CRUSH_TUNABLES5 added in jewel, not kraken
    ([issue#25057](http://tracker.ceph.com/issues/25057),
    [issue#25101](http://tracker.ceph.com/issues/25101),
    [pr#23226](https://github.com/ceph/ceph/pull/23226), Sage Weil)
-   osd/PrimaryLogPG: avoid dereferencing invalid complete_to
    ([pr#23951](https://github.com/ceph/ceph/pull/23951), xie xingguo)
-   osd: segv in OSDMap::calc_pg_upmaps from balancer
    ([issue#22056](http://tracker.ceph.com/issues/22056),
    [issue#26933](http://tracker.ceph.com/issues/26933),
    [pr#23888](https://github.com/ceph/ceph/pull/23888), Brad Hubbard)
-   qa: cfuse_workunit_kernel_untar_build fails on Ubuntu 18.04
    ([issue#26956](http://tracker.ceph.com/issues/26956),
    [issue#26967](http://tracker.ceph.com/issues/26967),
    [issue#24679](http://tracker.ceph.com/issues/24679),
    [pr#23769](https://github.com/ceph/ceph/pull/23769), Patrick
    Donnelly)
-   qa: fix ceph-disk suite and add coverage for ceph-detect-init
    ([pr#23337](https://github.com/ceph/ceph/pull/23337), Nathan Cutler)
-   qa/rgw: patch keystone requirements.txt
    ([issue#26946](http://tracker.ceph.com/issues/26946),
    [issue#23659](http://tracker.ceph.com/issues/23659),
    [pr#23771](https://github.com/ceph/ceph/pull/23771), Casey Bodley)
-   qa/suites/rados: move valgrind test to singleton-flat
    ([issue#24992](http://tracker.ceph.com/issues/24992),
    [pr#23744](https://github.com/ceph/ceph/pull/23744), Sage Weil)
-   qa/tasks: s3a fix mirror
    ([pr#24038](https://github.com/ceph/ceph/pull/24038), Vasu Kulkarni)
-   qa/tests: added OBJECT_MISPLACED to the whitelist
    ([pr#23301](https://github.com/ceph/ceph/pull/23301), Yuri
    Weinstein)
-   qa/tests: added v13.2.1 to the mix
    ([pr#23218](https://github.com/ceph/ceph/pull/23218), Yuri
    Weinstein)
-   qa/tests: update ansible version to 2.5
    ([pr#24091](https://github.com/ceph/ceph/pull/24091), Yuri
    Weinstein)
-   rados: not all exceptions accept keyargs
    ([issue#25178](http://tracker.ceph.com/issues/25178),
    [issue#24033](http://tracker.ceph.com/issues/24033),
    [pr#23335](https://github.com/ceph/ceph/pull/23335), Rishabh Dave)
-   rados python bindings use prval from stack
    ([issue#25204](http://tracker.ceph.com/issues/25204),
    [issue#25175](http://tracker.ceph.com/issues/25175),
    [pr#23863](https://github.com/ceph/ceph/pull/23863), Sage Weil)
-   rbd: improved trash snapshot namespace handling
    ([issue#25121](http://tracker.ceph.com/issues/25121),
    [issue#23398](http://tracker.ceph.com/issues/23398),
    [issue#25114](http://tracker.ceph.com/issues/25114),
    [pr#23559](https://github.com/ceph/ceph/pull/23559), Mykola Golub,
    Jason Dillaman)
-   rgw: add curl_low_speed_limit and curl_low_speed_time config to
    avoid ([issue#25021](http://tracker.ceph.com/issues/25021),
    [pr#23173](https://github.com/ceph/ceph/pull/23173), Mark Kogan,
    Zhang Shaowen)
-   rgw: change default rgw_thread_pool_size to 512
    ([issue#25214](http://tracker.ceph.com/issues/25214),
    [issue#25088](http://tracker.ceph.com/issues/25088),
    [issue#25218](http://tracker.ceph.com/issues/25218),
    [issue#24544](http://tracker.ceph.com/issues/24544),
    [pr#23383](https://github.com/ceph/ceph/pull/23383), Douglas Fuller,
    Casey Bodley)
-   rgw: civetweb fails on urls with control characters
    ([issue#26849](http://tracker.ceph.com/issues/26849),
    [issue#24158](http://tracker.ceph.com/issues/24158),
    [pr#23855](https://github.com/ceph/ceph/pull/23855), Abhishek
    Lekshmanan)
-   rgw: civetweb: use poll instead of select while waiting on sockets
    ([issue#35954](http://tracker.ceph.com/issues/35954),
    [pr#24058](https://github.com/ceph/ceph/pull/24058), Abhishek
    Lekshmanan)
-   rgw: do not ignore EEXIST in RGWPutObj::execute
    ([issue#25078](http://tracker.ceph.com/issues/25078),
    [issue#22790](http://tracker.ceph.com/issues/22790),
    [pr#23206](https://github.com/ceph/ceph/pull/23206), Matt Benjamin)
-   rgw: fail to recover index from crash mimic backport
    ([issue#24640](http://tracker.ceph.com/issues/24640),
    [issue#24629](http://tracker.ceph.com/issues/24629),
    [issue#24280](http://tracker.ceph.com/issues/24280),
    [pr#23118](https://github.com/ceph/ceph/pull/23118), Tianshan Qu)
-   rgw_file: deep stat handling
    ([issue#26842](http://tracker.ceph.com/issues/26842),
    [issue#24915](http://tracker.ceph.com/issues/24915),
    [pr#23498](https://github.com/ceph/ceph/pull/23498), Matt Benjamin)
-   rgw: Fix log level of gc_iterate_entries
    ([issue#23801](http://tracker.ceph.com/issues/23801),
    [issue#26921](http://tracker.ceph.com/issues/26921),
    [pr#23686](https://github.com/ceph/ceph/pull/23686), iliul)
-   rgw: Limit the number of lifecycle rules on one bucket
    ([issue#26845](http://tracker.ceph.com/issues/26845),
    [issue#24572](http://tracker.ceph.com/issues/24572),
    [pr#23521](https://github.com/ceph/ceph/pull/23521), Zhang Shaowen)
-   rgw: radosgw-admin: \'sync error trim\' loops until complete
    ([issue#24873](http://tracker.ceph.com/issues/24873),
    [issue#24984](http://tracker.ceph.com/issues/24984),
    [pr#23140](https://github.com/ceph/ceph/pull/23140), Casey Bodley)
-   rgw: The delete markers generated by object expiration should have
    owner ([issue#24568](http://tracker.ceph.com/issues/24568),
    [issue#26847](http://tracker.ceph.com/issues/26847),
    [pr#23541](https://github.com/ceph/ceph/pull/23541), Zhang Shaowen)
-   rpm: should change ceph-mgr package depency from py-bcrypt to
    python2-bcrypt ([issue#27212](http://tracker.ceph.com/issues/27212),
    [pr#23868](https://github.com/ceph/ceph/pull/23868), Konstantin
    Sakhinov)
-   rpm: silence osd block chown
    ([issue#25152](http://tracker.ceph.com/issues/25152),
    [pr#23324](https://github.com/ceph/ceph/pull/23324), Dan van der
    Ster)
-   run-rbd-unit-tests.sh test fails to finish in jenkin\'s make check
    run ([issue#27060](http://tracker.ceph.com/issues/27060),
    [issue#24910](http://tracker.ceph.com/issues/24910),
    [pr#23858](https://github.com/ceph/ceph/pull/23858), Mykola Golub)
-   scrub livelock ([issue#26931](http://tracker.ceph.com/issues/26931),
    [issue#26890](http://tracker.ceph.com/issues/26890),
    [pr#23722](https://github.com/ceph/ceph/pull/23722), Sage Weil)
-   spdk: compile with -march=core2 instead of -march=native
    ([issue#25032](http://tracker.ceph.com/issues/25032),
    [pr#23175](https://github.com/ceph/ceph/pull/23175), Nathan Cutler)
-   tests: cluster \[WRN\] 25 slow requests in powercycle
    ([issue#25119](http://tracker.ceph.com/issues/25119),
    [pr#23886](https://github.com/ceph/ceph/pull/23886), Neha Ojha)
-   test: Use pids instead of jobspecs which were wrong
    ([issue#32079](http://tracker.ceph.com/issues/32079),
    [issue#27056](http://tracker.ceph.com/issues/27056),
    [pr#23893](https://github.com/ceph/ceph/pull/23893), David Zafman)
-   tools/ceph-detect-init: support RHEL as a platform
    ([issue#18163](http://tracker.ceph.com/issues/18163),
    [pr#23303](https://github.com/ceph/ceph/pull/23303), Nathan Cutler)
-   tools: ceph-detect-init: support SLED
    ([issue#18163](http://tracker.ceph.com/issues/18163),
    [pr#23111](https://github.com/ceph/ceph/pull/23111), Nathan Cutler)
-   tools: cephfs-data-scan: print the max used ino
    ([issue#26978](http://tracker.ceph.com/issues/26978),
    [issue#26925](http://tracker.ceph.com/issues/26925),
    [pr#23880](https://github.com/ceph/ceph/pull/23880), \"Yan, Zheng\")

## v13.2.1 Mimic

This is the first bugfix release of the Mimic v13.2.x long term stable
release series. This release contains many fixes across all components
of Ceph, including a few security fixes. We recommend that all users
upgrade.

### Notable Changes

-   CVE 2018-1128: auth: cephx authorizer subject to replay attack
    ([issue#24836](http://tracker.ceph.com/issues/24836), Sage Weil)
-   CVE 2018-1129: auth: cephx signature check is weak
    ([issue#24837](http://tracker.ceph.com/issues/24837), Sage Weil)
-   CVE 2018-10861: mon: auth checks not correct for pool ops
    ([issue#24838](http://tracker.ceph.com/issues/24838), Jason
    Dillaman)

### Changelog

-   bluestore: common/hobject: improved hash calculation for hobject_t
    etc ([pr#22777](https://github.com/ceph/ceph/pull/22777), Adam
    Kupczyk, Sage Weil)
-   bluestore,core: mimic: os/bluestore: don\'t store/use
    path_block.{db,wal} from meta
    ([pr#22477](https://github.com/ceph/ceph/pull/22477), Sage Weil,
    Alfredo Deza)
-   bluestore: os/bluestore: backport 24319 and 24550
    ([issue#24550](http://tracker.ceph.com/issues/24550),
    [issue#24502](http://tracker.ceph.com/issues/24502),
    [issue#24319](http://tracker.ceph.com/issues/24319),
    [issue#24581](http://tracker.ceph.com/issues/24581),
    [pr#22649](https://github.com/ceph/ceph/pull/22649), Sage Weil)
-   bluestore: os/bluestore: fix incomplete faulty range marking when
    doing compression
    ([pr#22910](https://github.com/ceph/ceph/pull/22910), Igor Fedotov)
-   bluestore: spdk: fix ceph-osd crash when activate SPDK
    ([issue#24472](http://tracker.ceph.com/issues/24472),
    [issue#24371](http://tracker.ceph.com/issues/24371),
    [pr#22684](https://github.com/ceph/ceph/pull/22684), tone-zhang)
-   build/ops: build/ops: ceph.git has two different versions of dpdk in
    the source tree
    ([issue#24942](http://tracker.ceph.com/issues/24942),
    [issue#24032](http://tracker.ceph.com/issues/24032),
    [pr#23070](https://github.com/ceph/ceph/pull/23070), Kefu Chai)
-   build/ops: build/ops: install-deps.sh fails on newest openSUSE Leap
    ([issue#25065](http://tracker.ceph.com/issues/25065),
    [pr#23178](https://github.com/ceph/ceph/pull/23178), Kyr Shatskyy)
-   build/ops: build/ops: Mimic build fails with -DWITH_RADOSGW=0
    ([issue#24766](http://tracker.ceph.com/issues/24766),
    [pr#22851](https://github.com/ceph/ceph/pull/22851), Dan Mick)
-   build/ops: cmake: enable RTTI for both debug and release RocksDB
    builds ([pr#22299](https://github.com/ceph/ceph/pull/22299), Igor
    Fedotov)
-   build/ops: deb/rpm: add python-six as build-time and run-time
    dependency ([issue#24885](http://tracker.ceph.com/issues/24885),
    [pr#22948](https://github.com/ceph/ceph/pull/22948), Nathan Cutler,
    Kefu Chai)
-   build/ops: deb,rpm: fix block.db symlink ownership
    ([pr#23246](https://github.com/ceph/ceph/pull/23246), Sage Weil)
-   build/ops: include: fix build with older clang (OSX target)
    ([pr#23049](https://github.com/ceph/ceph/pull/23049), Christopher
    Blum)
-   build/ops: include: fix build with older clang
    ([pr#23034](https://github.com/ceph/ceph/pull/23034), Kefu Chai)
-   build/ops,rbd: build/ops: order rbdmap.service before
    remote-fs-pre.target
    ([issue#24713](http://tracker.ceph.com/issues/24713),
    [issue#24734](http://tracker.ceph.com/issues/24734),
    [pr#22843](https://github.com/ceph/ceph/pull/22843), Ilya Dryomov)
-   cephfs: cephfs: allow prohibiting user snapshots in CephFS
    ([issue#24705](http://tracker.ceph.com/issues/24705),
    [issue#24284](http://tracker.ceph.com/issues/24284),
    [pr#22812](https://github.com/ceph/ceph/pull/22812), \"Yan, Zheng\")
-   cephfs: cephfs-journal-tool: Fix purging when importing an
    zero-length journal
    ([issue#24861](http://tracker.ceph.com/issues/24861),
    [pr#22981](https://github.com/ceph/ceph/pull/22981), yupeng chen,
    zhongyan gu)
-   cephfs: client: fix bug #24491 \_ll_drop_pins may access invalid
    iterator ([issue#24534](http://tracker.ceph.com/issues/24534),
    [pr#22791](https://github.com/ceph/ceph/pull/22791), Liu Yangkuan)
-   cephfs: client: update inode fields according to issued caps
    ([issue#24539](http://tracker.ceph.com/issues/24539),
    [issue#24269](http://tracker.ceph.com/issues/24269),
    [pr#22819](https://github.com/ceph/ceph/pull/22819), \"Yan, Zheng\")
-   cephfs: common/DecayCounter: set last_decay to current time when
    decoding dec...
    ([issue#24440](http://tracker.ceph.com/issues/24440),
    [issue#24537](http://tracker.ceph.com/issues/24537),
    [pr#22816](https://github.com/ceph/ceph/pull/22816), Zhi Zhang)
-   cephfs,core: mon/MDSMonitor: do not send redundant MDS health
    messages to cluster log
    ([issue#24308](http://tracker.ceph.com/issues/24308),
    [issue#24330](http://tracker.ceph.com/issues/24330),
    [pr#22265](https://github.com/ceph/ceph/pull/22265), Sage Weil)
-   cephfs: mds: add magic to header of open file table
    ([issue#24541](http://tracker.ceph.com/issues/24541),
    [issue#24240](http://tracker.ceph.com/issues/24240),
    [pr#22841](https://github.com/ceph/ceph/pull/22841), \"Yan, Zheng\")
-   cephfs: mds: low wrlock efficiency due to dirfrags traversal
    ([issue#24704](http://tracker.ceph.com/issues/24704),
    [issue#24467](http://tracker.ceph.com/issues/24467),
    [pr#22884](https://github.com/ceph/ceph/pull/22884), Xuehan Xu)
-   cephfs: PurgeQueue sometimes ignores Journaler errors
    ([issue#24533](http://tracker.ceph.com/issues/24533),
    [issue#24703](http://tracker.ceph.com/issues/24703),
    [pr#22810](https://github.com/ceph/ceph/pull/22810), John Spray)
-   cephfs,rbd: osdc: Fix the wrong BufferHead offset
    ([issue#24583](http://tracker.ceph.com/issues/24583),
    [pr#22869](https://github.com/ceph/ceph/pull/22869), dongdong tao)
-   cephfs: repeated eviction of idle client until some IO happens
    ([issue#24052](http://tracker.ceph.com/issues/24052),
    [issue#24296](http://tracker.ceph.com/issues/24296),
    [pr#22550](https://github.com/ceph/ceph/pull/22550), \"Yan, Zheng\")
-   cephfs: test gets ENOSPC from bluestore block device
    ([issue#24238](http://tracker.ceph.com/issues/24238),
    [issue#24913](http://tracker.ceph.com/issues/24913),
    [issue#24899](http://tracker.ceph.com/issues/24899),
    [issue#24758](http://tracker.ceph.com/issues/24758),
    [pr#22835](https://github.com/ceph/ceph/pull/22835), Patrick
    Donnelly, Sage Weil)
-   cephfs,tests: pjd: cd: too many arguments
    ([issue#24310](http://tracker.ceph.com/issues/24310),
    [pr#22882](https://github.com/ceph/ceph/pull/22882), Neha Ojha)
-   cephfs,tests: qa: client socket inaccessible without sudo
    ([issue#24872](http://tracker.ceph.com/issues/24872),
    [issue#24904](http://tracker.ceph.com/issues/24904),
    [pr#23030](https://github.com/ceph/ceph/pull/23030), Patrick
    Donnelly)
-   cephfs,tests: qa: fix ffsb cd argument
    ([issue#24719](http://tracker.ceph.com/issues/24719),
    [issue#24829](http://tracker.ceph.com/issues/24829),
    [issue#24680](http://tracker.ceph.com/issues/24680),
    [issue#24579](http://tracker.ceph.com/issues/24579),
    [pr#22956](https://github.com/ceph/ceph/pull/22956), Yan, Zheng,
    Patrick Donnelly)
-   cephfs,tests: qa/suites: Add supported-random-distro\$ links
    ([issue#24706](http://tracker.ceph.com/issues/24706),
    [issue#24138](http://tracker.ceph.com/issues/24138),
    [pr#22700](https://github.com/ceph/ceph/pull/22700), Warren Usui)
-   ceph-volume describe better the options for migrating away from
    ceph-disk ([pr#22514](https://github.com/ceph/ceph/pull/22514),
    Alfredo Deza)
-   ceph-volume dmcrypt and activate \--all documentation updates
    ([pr#22529](https://github.com/ceph/ceph/pull/22529), Alfredo Deza)
-   ceph-volume: error on commands that need ceph.conf to operate
    ([issue#23941](http://tracker.ceph.com/issues/23941),
    [pr#22747](https://github.com/ceph/ceph/pull/22747), Andrew Schoen)
-   ceph-volume expand on the LVM API to create multiple LVs at
    different sizes
    ([pr#22508](https://github.com/ceph/ceph/pull/22508), Alfredo Deza)
-   ceph-volume initial take on auto sub-command
    ([pr#22515](https://github.com/ceph/ceph/pull/22515), Alfredo Deza)
-   ceph-volume lvm.activate Do not search for a MON configuration
    ([pr#22398](https://github.com/ceph/ceph/pull/22398), Wido den
    Hollander)
-   ceph-volume lvm.common use destroy-new, doesn\'t need admin keyring
    ([issue#24585](http://tracker.ceph.com/issues/24585),
    [pr#22900](https://github.com/ceph/ceph/pull/22900), Alfredo Deza)
-   ceph-volume: provide a nice errror message when missing ceph.conf
    ([pr#22832](https://github.com/ceph/ceph/pull/22832), Andrew Schoen)
-   ceph-volume tests destroy osds on monitor hosts
    ([pr#22507](https://github.com/ceph/ceph/pull/22507), Alfredo Deza)
-   ceph-volume tests do not include admin keyring in OSD nodes
    ([pr#22425](https://github.com/ceph/ceph/pull/22425), Alfredo Deza)
-   ceph-volume tests.functional install new ceph-ansible dependencies
    ([pr#22535](https://github.com/ceph/ceph/pull/22535), Alfredo Deza)
-   ceph-volume: tests/functional run lvm list after OSD provisioning
    ([issue#24961](http://tracker.ceph.com/issues/24961),
    [pr#23148](https://github.com/ceph/ceph/pull/23148), Alfredo Deza)
-   ceph-volume tests/functional use Ansible 2.6
    ([pr#23244](https://github.com/ceph/ceph/pull/23244), Alfredo Deza)
-   ceph-volume: unmount lvs correctly before zapping
    ([issue#24796](http://tracker.ceph.com/issues/24796),
    [pr#23127](https://github.com/ceph/ceph/pull/23127), Andrew Schoen)
-   cmake: bump up the required boost version to 1.67
    ([pr#22412](https://github.com/ceph/ceph/pull/22412), Kefu Chai)
-   common: common: Abort in OSDMap::decode() during
    qa/standalone/erasure-code/test-erasure-eio.sh
    ([issue#24865](http://tracker.ceph.com/issues/24865),
    [issue#23492](http://tracker.ceph.com/issues/23492),
    [pr#23024](https://github.com/ceph/ceph/pull/23024), Sage Weil)
-   common: common: fix typo in rados bench write JSON output
    ([issue#24292](http://tracker.ceph.com/issues/24292),
    [issue#24199](http://tracker.ceph.com/issues/24199),
    [pr#22406](https://github.com/ceph/ceph/pull/22406), Sandor
    Zeestraten)
-   common,core: common: partially revert 95fc248 to make
    get_process_name work
    ([issue#24123](http://tracker.ceph.com/issues/24123),
    [issue#24215](http://tracker.ceph.com/issues/24215),
    [pr#22311](https://github.com/ceph/ceph/pull/22311), Mykola Golub)
-   common: osd: Change osd_skip_data_digest default to false and make
    it LEVEL_DEV ([pr#23084](https://github.com/ceph/ceph/pull/23084),
    Sage Weil, David Zafman)
-   common: tell \... config rm \<foo\> not idempotent
    ([issue#24468](http://tracker.ceph.com/issues/24468),
    [issue#24408](http://tracker.ceph.com/issues/24408),
    [pr#22552](https://github.com/ceph/ceph/pull/22552), Sage Weil)
-   core: bluestore: flush_commit is racy
    ([issue#24261](http://tracker.ceph.com/issues/24261),
    [issue#21480](http://tracker.ceph.com/issues/21480),
    [pr#22382](https://github.com/ceph/ceph/pull/22382), Sage Weil)
-   core: ceph osd safe-to-destroy crashes the mgr
    ([issue#24708](http://tracker.ceph.com/issues/24708),
    [issue#23249](http://tracker.ceph.com/issues/23249),
    [pr#22805](https://github.com/ceph/ceph/pull/22805), Sage Weil)
-   core: change default filestore_merge_threshold to -10
    ([issue#24686](http://tracker.ceph.com/issues/24686),
    [issue#24747](http://tracker.ceph.com/issues/24747),
    [pr#22813](https://github.com/ceph/ceph/pull/22813), Douglas Fuller)
-   core: common/hobject: improved hash calculation
    ([pr#22722](https://github.com/ceph/ceph/pull/22722), Adam Kupczyk)
-   core: cosbench stuck at booting cosbench driver
    ([issue#24473](http://tracker.ceph.com/issues/24473),
    [pr#22887](https://github.com/ceph/ceph/pull/22887), Neha Ojha)
-   core: librados: fix buffer overflow for aio_exec python binding
    ([issue#24475](http://tracker.ceph.com/issues/24475),
    [pr#22707](https://github.com/ceph/ceph/pull/22707), Aleksei
    Gutikov)
-   core: mon: enable level_compaction_dynamic_level_bytes for rocksdb
    ([issue#24375](http://tracker.ceph.com/issues/24375),
    [issue#24361](http://tracker.ceph.com/issues/24361),
    [pr#22361](https://github.com/ceph/ceph/pull/22361), Kefu Chai)
-   core: mon/MgrMonitor: change \'unresponsive\' message to info level
    ([issue#24246](http://tracker.ceph.com/issues/24246),
    [issue#24222](http://tracker.ceph.com/issues/24222),
    [pr#22333](https://github.com/ceph/ceph/pull/22333), Sage Weil)
-   core: mon/OSDMonitor: no_reply on MOSDFailure messages
    ([issue#24322](http://tracker.ceph.com/issues/24322),
    [issue#24350](http://tracker.ceph.com/issues/24350),
    [pr#22297](https://github.com/ceph/ceph/pull/22297), Sage Weil)
-   core: os/bluestore: firstly delete db then delete bluefs if open db
    met error ([pr#22525](https://github.com/ceph/ceph/pull/22525),
    Jianpeng Ma)
-   core: os/bluestore: fix races on SharedBlob::coll in \~SharedBlob
    ([issue#24859](http://tracker.ceph.com/issues/24859),
    [issue#24887](http://tracker.ceph.com/issues/24887),
    [pr#23065](https://github.com/ceph/ceph/pull/23065), Radoslaw
    Zarzynski)
-   core: osd: choose_acting loop
    ([issue#24383](http://tracker.ceph.com/issues/24383),
    [issue#24618](http://tracker.ceph.com/issues/24618),
    [pr#22889](https://github.com/ceph/ceph/pull/22889), Neha Ojha)
-   core: osd: do not blindly roll forward to log.head
    ([issue#24597](http://tracker.ceph.com/issues/24597),
    [pr#22997](https://github.com/ceph/ceph/pull/22997), Sage Weil)
-   core: osd: eternal stuck PG in \'unfound_recovery\'
    ([issue#24500](http://tracker.ceph.com/issues/24500),
    [issue#24373](http://tracker.ceph.com/issues/24373),
    [pr#22545](https://github.com/ceph/ceph/pull/22545), Sage Weil)
-   core: osd: fix deep scrub with osd_skip_data_digest=true (default)
    and blue... ([issue#24922](http://tracker.ceph.com/issues/24922),
    [issue#24958](http://tracker.ceph.com/issues/24958),
    [pr#23094](https://github.com/ceph/ceph/pull/23094), Sage Weil)
-   core: osd: fix getting osd maps on initial osd startup
    ([pr#22651](https://github.com/ceph/ceph/pull/22651), Paul Emmerich)
-   core: osd: increase default hard pg limit
    ([issue#24355](http://tracker.ceph.com/issues/24355),
    [pr#22621](https://github.com/ceph/ceph/pull/22621), Josh Durgin)
-   core: osd: may get empty info at recovery
    ([issue#24771](http://tracker.ceph.com/issues/24771),
    [issue#24588](http://tracker.ceph.com/issues/24588),
    [pr#22861](https://github.com/ceph/ceph/pull/22861), Sage Weil)
-   core: osd/PrimaryLogPG: rebuild attrs from clients
    ([issue#24768](http://tracker.ceph.com/issues/24768),
    [issue#24805](http://tracker.ceph.com/issues/24805),
    [pr#22960](https://github.com/ceph/ceph/pull/22960), Sage Weil)
-   core: osd: retry to read object attrs at EC recovery
    ([issue#24406](http://tracker.ceph.com/issues/24406),
    [pr#22394](https://github.com/ceph/ceph/pull/22394), xiaofei cui)
-   core: osd/Session: fix invalid iterator dereference in
    Sessoin::have_backoff()
    ([issue#24486](http://tracker.ceph.com/issues/24486),
    [issue#24494](http://tracker.ceph.com/issues/24494),
    [pr#22730](https://github.com/ceph/ceph/pull/22730), Sage Weil)
-   core: PG: add custom_reaction Backfilled and release reservations
    after bac... ([issue#24332](http://tracker.ceph.com/issues/24332),
    [pr#22559](https://github.com/ceph/ceph/pull/22559), Neha Ojha)
-   core: set correctly shard for existed Collection
    ([issue#24769](http://tracker.ceph.com/issues/24769),
    [issue#24761](http://tracker.ceph.com/issues/24761),
    [pr#22859](https://github.com/ceph/ceph/pull/22859), Jianpeng Ma)
-   core,tests: Bring back diff -y for non-FreeBSD
    ([issue#24738](http://tracker.ceph.com/issues/24738),
    [issue#24470](http://tracker.ceph.com/issues/24470),
    [pr#22826](https://github.com/ceph/ceph/pull/22826), Sage Weil,
    David Zafman)
-   core,tests: ceph_test_rados_api_misc: fix
    LibRadosMiscPool.PoolCreationRace
    ([issue#24204](http://tracker.ceph.com/issues/24204),
    [issue#24150](http://tracker.ceph.com/issues/24150),
    [pr#22291](https://github.com/ceph/ceph/pull/22291), Sage Weil)
-   core,tests: qa/workunits/suites/blogbench.sh: use correct dir name
    ([pr#22775](https://github.com/ceph/ceph/pull/22775), Neha Ojha)
-   core,tests: Wip scrub omap
    ([issue#24366](http://tracker.ceph.com/issues/24366),
    [issue#24381](http://tracker.ceph.com/issues/24381),
    [pr#22374](https://github.com/ceph/ceph/pull/22374), David Zafman)
-   core,tools: ceph-detect-init: stop using platform.linux_distribution
    ([issue#18163](http://tracker.ceph.com/issues/18163),
    [pr#21523](https://github.com/ceph/ceph/pull/21523), Nathan Cutler)
-   core: ValueError: too many values to unpack due to lack of subdir
    ([issue#24617](http://tracker.ceph.com/issues/24617),
    [pr#22888](https://github.com/ceph/ceph/pull/22888), Neha Ojha)
-   doc: ceph-bluestore-tool manpage not getting rendered correctly
    ([issue#25062](http://tracker.ceph.com/issues/25062),
    [issue#24800](http://tracker.ceph.com/issues/24800),
    [pr#23176](https://github.com/ceph/ceph/pull/23176), Nathan Cutler)
-   doc: doc: update experimental features - snapshots
    ([pr#22803](https://github.com/ceph/ceph/pull/22803), Jos Collin)
-   doc: fix the links in releases/schedule.rst
    ([pr#22372](https://github.com/ceph/ceph/pull/22372), Kefu Chai)
-   doc: \[mimic\] doc/cephfs: remove lingering \"experimental\" note
    about multimds ([pr#22854](https://github.com/ceph/ceph/pull/22854),
    John Spray)
-   lvm: when osd creation fails log the exception
    ([issue#24456](http://tracker.ceph.com/issues/24456),
    [pr#22640](https://github.com/ceph/ceph/pull/22640), Andrew Schoen)
-   mgr/dashboard: Fix bug when creating S3 keys
    ([pr#22468](https://github.com/ceph/ceph/pull/22468), Volker Theile)
-   mgr/dashboard: fix lint error caused by codelyzer update
    ([pr#22713](https://github.com/ceph/ceph/pull/22713), Tiago Melo)
-   mgr/dashboard: Fix some datatable CSS issues
    ([pr#22274](https://github.com/ceph/ceph/pull/22274), Volker Theile)
-   mgr/dashboard: Float numbers incorrectly formatted
    ([issue#24081](http://tracker.ceph.com/issues/24081),
    [issue#24707](http://tracker.ceph.com/issues/24707),
    [pr#22886](https://github.com/ceph/ceph/pull/22886), Stephan Müller,
    Tiago Melo)
-   mgr/dashboard: Missing breadcrumb on monitor performance counters
    page ([issue#24764](http://tracker.ceph.com/issues/24764),
    [pr#22849](https://github.com/ceph/ceph/pull/22849), Ricardo
    Marques, Tiago Melo)
-   mgr/dashboard: Replace Pool with Pools
    ([issue#24699](http://tracker.ceph.com/issues/24699),
    [pr#22807](https://github.com/ceph/ceph/pull/22807), Lenz Grimmer)
-   mgr: mgr/dashboard: Listen on port 8443 by default and not 8080
    ([pr#22449](https://github.com/ceph/ceph/pull/22449), Wido den
    Hollander)
-   mgr,mon: exception for dashboard in config-key warning
    ([pr#22770](https://github.com/ceph/ceph/pull/22770), John Spray)
-   mgr,pybind: Python bindings use iteritems method which is not Python
    3 compatible ([issue#24803](http://tracker.ceph.com/issues/24803),
    [issue#24779](http://tracker.ceph.com/issues/24779),
    [pr#22917](https://github.com/ceph/ceph/pull/22917), Nathan Cutler)
-   mgr: Sync up ceph-mgr prometheus related changes
    ([pr#22341](https://github.com/ceph/ceph/pull/22341), Boris Ranto)
-   mon: don\'t require CEPHX_V2 from mons until nautilus
    ([pr#23233](https://github.com/ceph/ceph/pull/23233), Sage Weil)
-   mon/OSDMonitor: Respect paxos_propose_interval
    ([pr#22268](https://github.com/ceph/ceph/pull/22268), Xiaoxi CHEN)
-   osd: forward-port osd_distrust_data_digest from luminous
    ([pr#23184](https://github.com/ceph/ceph/pull/23184), Sage Weil)
-   osd/OSDMap: fix CEPHX_V2 osd requirement to nautilus, not mimic
    ([pr#23250](https://github.com/ceph/ceph/pull/23250), Sage Weil)
-   qa/rgw: disable testing on ec-cache pools
    ([issue#23965](http://tracker.ceph.com/issues/23965),
    [pr#23096](https://github.com/ceph/ceph/pull/23096), Casey Bodley)
-   qa/suites/upgrade/mimic-p2p: allow target version to apply
    ([pr#23262](https://github.com/ceph/ceph/pull/23262), Sage Weil)
-   qa/tests: added supported distro for powercycle suite
    ([pr#22224](https://github.com/ceph/ceph/pull/22224), Yuri
    Weinstein)
-   qa/tests: changed distro symlink to point to new way using supported
    OSes ([pr#22653](https://github.com/ceph/ceph/pull/22653), Yuri
    Weinstein)
-   rbd: librbd: deep_copy: resize head object map if needed
    ([issue#24499](http://tracker.ceph.com/issues/24499),
    [issue#24399](http://tracker.ceph.com/issues/24399),
    [pr#22768](https://github.com/ceph/ceph/pull/22768), Mykola Golub)
-   rbd: librbd: fix crash when opening nonexistent snapshot
    ([issue#24637](http://tracker.ceph.com/issues/24637),
    [issue#24698](http://tracker.ceph.com/issues/24698),
    [pr#22943](https://github.com/ceph/ceph/pull/22943), Mykola Golub)
-   rbd: librbd: force \'invalid object map\' flag on-disk update
    ([issue#24496](http://tracker.ceph.com/issues/24496),
    [issue#24434](http://tracker.ceph.com/issues/24434),
    [pr#22754](https://github.com/ceph/ceph/pull/22754), Mykola Golub)
-   rbd: librbd: utilize the journal disabled policy when removing
    images ([issue#24388](http://tracker.ceph.com/issues/24388),
    [issue#23512](http://tracker.ceph.com/issues/23512),
    [pr#22662](https://github.com/ceph/ceph/pull/22662), Jason Dillaman)
-   rbd: Prevent the use of internal feature bits from outside cls/rbd
    ([issue#24165](http://tracker.ceph.com/issues/24165),
    [issue#24203](http://tracker.ceph.com/issues/24203),
    [pr#22222](https://github.com/ceph/ceph/pull/22222), Jason Dillaman)
-   rbd: rbd-mirror daemon failed to stop on active/passive test case
    ([issue#24390](http://tracker.ceph.com/issues/24390),
    [pr#22667](https://github.com/ceph/ceph/pull/22667), Jason Dillaman)
-   rbd: \[rbd-mirror\] entries_behind_master will not be zero after
    mirror over ([issue#24391](http://tracker.ceph.com/issues/24391),
    [issue#23516](http://tracker.ceph.com/issues/23516),
    [pr#22549](https://github.com/ceph/ceph/pull/22549), Jason Dillaman)
-   rbd: rbd-mirror simple image map policy doesn\'t always level-load
    instances ([issue#24519](http://tracker.ceph.com/issues/24519),
    [issue#24161](http://tracker.ceph.com/issues/24161),
    [pr#22892](https://github.com/ceph/ceph/pull/22892), Venky Shankar)
-   rbd: rbd trash purge \--threshold should support data pool
    ([issue#24476](http://tracker.ceph.com/issues/24476),
    [issue#22872](http://tracker.ceph.com/issues/22872),
    [pr#22891](https://github.com/ceph/ceph/pull/22891), Mahati
    Chamarthy)
-   rbd,tests: qa: krbd_exclusive_option.sh: bump lock_timeout to 60
    seconds ([issue#25081](http://tracker.ceph.com/issues/25081),
    [pr#23209](https://github.com/ceph/ceph/pull/23209), Ilya Dryomov)
-   rbd: yet another case when deep copying a clone may result in
    invalid object map
    ([issue#24596](http://tracker.ceph.com/issues/24596),
    [issue#24545](http://tracker.ceph.com/issues/24545),
    [pr#22894](https://github.com/ceph/ceph/pull/22894), Mykola Golub)
-   rgw: cls_bucket_list fails causes cascading osd crashes
    ([issue#24631](http://tracker.ceph.com/issues/24631),
    [issue#24117](http://tracker.ceph.com/issues/24117),
    [pr#22927](https://github.com/ceph/ceph/pull/22927), Yehuda Sadeh)
-   rgw: multisite: RGWSyncTraceNode released twice and crashed in
    reload ([issue#24432](http://tracker.ceph.com/issues/24432),
    [issue#24619](http://tracker.ceph.com/issues/24619),
    [pr#22926](https://github.com/ceph/ceph/pull/22926), Tianshan Qu)
-   rgw: objects in cache never refresh after rgw_cache_expiry_interval
    ([issue#24346](http://tracker.ceph.com/issues/24346),
    [issue#24385](http://tracker.ceph.com/issues/24385),
    [pr#22643](https://github.com/ceph/ceph/pull/22643), Casey Bodley)
-   rgw: add configurable AWS-compat invalid range get behavior
    ([issue#24317](http://tracker.ceph.com/issues/24317),
    [issue#24352](http://tracker.ceph.com/issues/24352),
    [pr#22590](https://github.com/ceph/ceph/pull/22590), Matt Benjamin)
-   rgw: Admin OPS Api overwrites email when user is modified
    ([issue#24253](http://tracker.ceph.com/issues/24253),
    [pr#22523](https://github.com/ceph/ceph/pull/22523), Volker Theile)
-   rgw: fix gc may cause a large number of read traffic
    ([issue#24807](http://tracker.ceph.com/issues/24807),
    [issue#24767](http://tracker.ceph.com/issues/24767),
    [pr#22941](https://github.com/ceph/ceph/pull/22941), Xin Liao)
-   rgw: have a configurable authentication order
    ([issue#23089](http://tracker.ceph.com/issues/23089),
    [issue#24547](http://tracker.ceph.com/issues/24547),
    [pr#22842](https://github.com/ceph/ceph/pull/22842), Abhishek
    Lekshmanan)
-   rgw: index complete miss zones_trace set
    ([issue#24701](http://tracker.ceph.com/issues/24701),
    [issue#24590](http://tracker.ceph.com/issues/24590),
    [pr#22818](https://github.com/ceph/ceph/pull/22818), Tianshan Qu)
-   rgw: Invalid Access-Control-Request-Request may bypass
    validate_cors_rule_method
    ([issue#24809](http://tracker.ceph.com/issues/24809),
    [issue#24223](http://tracker.ceph.com/issues/24223),
    [pr#22935](https://github.com/ceph/ceph/pull/22935), Jeegn Chen)
-   rgw: meta and data notify thread miss stop cr manager
    ([issue#24702](http://tracker.ceph.com/issues/24702),
    [issue#24589](http://tracker.ceph.com/issues/24589),
    [pr#22821](https://github.com/ceph/ceph/pull/22821), Tianshan Qu)
-   rgw:-multisite: endless loop in RGWBucketShardIncrementalSyncCR
    ([issue#24700](http://tracker.ceph.com/issues/24700),
    [issue#24603](http://tracker.ceph.com/issues/24603),
    [pr#22815](https://github.com/ceph/ceph/pull/22815), cfanz)
-   rgw: performance regression for luminous 12.2.4
    ([issue#23379](http://tracker.ceph.com/issues/23379),
    [issue#24633](http://tracker.ceph.com/issues/24633),
    [pr#22929](https://github.com/ceph/ceph/pull/22929), Mark Kogan)
-   rgw: radogw-admin reshard status command should print text for
    reshar... ([issue#24834](http://tracker.ceph.com/issues/24834),
    [issue#23257](http://tracker.ceph.com/issues/23257),
    [pr#23021](https://github.com/ceph/ceph/pull/23021), Orit Wasserman)
-   rgw: \"radosgw-admin objects expire\" always returns ok even if the
    pro... ([issue#24831](http://tracker.ceph.com/issues/24831),
    [issue#24592](http://tracker.ceph.com/issues/24592),
    [pr#23001](https://github.com/ceph/ceph/pull/23001), Zhang Shaowen)
-   rgw: require \--yes-i-really-mean-it to run radosgw-admin orphans
    find ([issue#24146](http://tracker.ceph.com/issues/24146),
    [issue#24843](http://tracker.ceph.com/issues/24843),
    [pr#22986](https://github.com/ceph/ceph/pull/22986), Matt Benjamin)
-   rgw: REST admin metadata API paging failure bucket &
    bucket.instance: InvalidArgument
    ([issue#23099](http://tracker.ceph.com/issues/23099),
    [issue#24813](http://tracker.ceph.com/issues/24813),
    [pr#22933](https://github.com/ceph/ceph/pull/22933), Matt Benjamin)
-   rgw: set cr state if aio_read err return in
    RGWCloneMetaLogCoroutine:state_send_rest_request
    ([issue#24566](http://tracker.ceph.com/issues/24566),
    [issue#24783](http://tracker.ceph.com/issues/24783),
    [pr#22880](https://github.com/ceph/ceph/pull/22880), Tianshan Qu)
-   rgw: test/rgw: fix for bucket checkpoints
    ([issue#24212](http://tracker.ceph.com/issues/24212),
    [issue#24313](http://tracker.ceph.com/issues/24313),
    [pr#22466](https://github.com/ceph/ceph/pull/22466), Casey Bodley)
-   rgw,tests: add unit test for cls bi list command
    ([issue#24736](http://tracker.ceph.com/issues/24736),
    [issue#24483](http://tracker.ceph.com/issues/24483),
    [pr#22845](https://github.com/ceph/ceph/pull/22845), Orit Wasserman)
-   tests: mimic - qa/tests: Set ansible-version: 2.4
    ([issue#24926](http://tracker.ceph.com/issues/24926),
    [pr#23122](https://github.com/ceph/ceph/pull/23122), Yuri Weinstein)
-   tests: osd sends op_reply out of order
    ([issue#25010](http://tracker.ceph.com/issues/25010),
    [pr#23136](https://github.com/ceph/ceph/pull/23136), Neha Ojha)
-   tests: qa/tests - added overrides stanza to allow runs on ovh on
    rhel OS ([pr#23156](https://github.com/ceph/ceph/pull/23156), Yuri
    Weinstein)
-   tests: qa/tests - added skeleton for mimic point to point upgrades
    testing ([pr#22697](https://github.com/ceph/ceph/pull/22697), Yuri
    Weinstein)
-   tests: qa/tests: fix supported distro lists for ceph-deploy
    ([pr#23017](https://github.com/ceph/ceph/pull/23017), Vasu Kulkarni)
-   tests: qa: wait longer for osd to flush pg stats
    ([issue#24321](http://tracker.ceph.com/issues/24321),
    [pr#22492](https://github.com/ceph/ceph/pull/22492), Kefu Chai)
-   tests: tests: Health check failed: 1 MDSs report slow requests
    (MDS_SLOW_REQUEST) in powercycle
    ([issue#25034](http://tracker.ceph.com/issues/25034),
    [pr#23154](https://github.com/ceph/ceph/pull/23154), Neha Ojha)
-   tests: tests: make test_ceph_argparse.py pass on py3-only systems
    ([issue#24825](http://tracker.ceph.com/issues/24825),
    [issue#24816](http://tracker.ceph.com/issues/24816),
    [pr#22988](https://github.com/ceph/ceph/pull/22988), Nathan Cutler)
-   tests: upgrade/luminous-x: whitelist REQUEST_SLOW for
    rados_mon_thrash
    ([issue#25056](http://tracker.ceph.com/issues/25056),
    [issue#25051](http://tracker.ceph.com/issues/25051),
    [pr#23164](https://github.com/ceph/ceph/pull/23164), Nathan Cutler)

## v13.2.0 Mimic

This is the first stable release of Mimic, the next long term release
series.

### Major Changes from Luminous

-   *Dashboard*:
    -   The (read-only) Ceph manager dashboard introduced in Ceph
        Luminous has been replaced with a new implementation inspired by
        and derived from the [openATTIC](https://openattic.org) Ceph
        management tool, providing a drop-in replacement offering a
        `number of additional management
        features <mgr-dashboard>`{.interpreted-text role="ref"}.
-   *RADOS*:
    -   Config options can now be centrally stored and managed by the
        monitor.
    -   The monitor daemon uses significantly less disk space when
        undergoing recovery or rebalancing operations.
    -   An *async recovery* feature reduces the tail latency of requests
        when the OSDs are recovering from a recent failure.
    -   OSD preemption of scrub by conflicting requests reduces tail
        latency.
-   *RGW*:
    -   RGW can now replicate a zone (or a subset of buckets) to an
        external cloud storage service like S3.
    -   RGW now supports the S3 multi-factor authentication API on
        versioned buckets.
    -   The Beast frontend is no longer experimental, and is considered
        stable and ready for use.
-   *CephFS*:
    -   Snapshots are now stable when combined with multiple MDS
        daemons.
-   *RBD*:
    -   Image clones no longer require explicit *protect* and
        *unprotect* steps.
    -   Images can be deep-copied (including any clone linkage to a
        parent image and associated snapshots) to new pools or with
        altered data layouts.
-   *Misc*:
    -   We have dropped the Debian builds for the Mimic release due to
        the lack of GCC 8 in Stretch. We expect Debian builds to return
        with the release of Buster in early 2019, and hope to build a
        final Luminous release (and possibly later Mimic point releases)
        once Buster is available.

### Upgrading from Luminous

#### Notes

-   We recommend you avoid creating any RADOS pools while the upgrade is
    in process.
-   You can monitor the progress of your upgrade at each stage with the
    `ceph versions` command, which will tell you what ceph version(s)
    are running for each type of daemon.

#### Instructions

1.  If your cluster was originally installed with a version prior to
    Luminous, ensure that it has completed at least one full scrub of
    all PGs while running Luminous. Failure to do so will cause your
    monitor daemons to refuse to join the quorum on start, leaving them
    non-functional.

    If you are unsure whether or not your Luminous cluster has completed
    a full scrub of all PGs, you can check your cluster\'s state by
    running:

        # ceph osd dump | grep ^flags

    In order to be able to proceed to Mimic, your OSD map must include
    the `recovery_deletes` and `purged_snapdirs` flags.

    If your OSD map does not contain both these flags, you can simply
    wait for approximately 24-48 hours, which in a standard cluster
    configuration should be ample time for all your placement groups to
    be scrubbed at least once, and then repeat the above process to
    recheck.

    However, if you have just completed an upgrade to Luminous and want
    to proceed to Mimic in short order, you can force a scrub on all
    placement groups with a one-line shell command, like:

        # ceph pg dump pgs_brief | cut -d " " -f 1 | xargs -n1 ceph pg scrub

    You should take into consideration that this forced scrub may
    possibly have a negative impact on your Ceph clients\' performance.

2.  Make sure your cluster is stable and healthy (no down or recovering
    OSDs). (Optional, but recommended.)

3.  Set the `noout` flag for the duration of the upgrade. (Optional, but
    recommended.):

        # ceph osd set noout

4.  Upgrade monitors by installing the new packages and restarting the
    monitor daemons.:

        # systemctl restart ceph-mon.target

    Once all monitors are up, verify that the monitor upgrade is
    complete by looking for the `mimic` feature string in the mon map.
    For example:

        # ceph mon feature ls

    should include [mimic]{.title-ref} under persistent features:

        on current monmap (epoch NNN)
           persistent: [kraken,luminous,mimic]
           required: [kraken,luminous,mimic]

5.  Upgrade `ceph-mgr` daemons by installing the new packages and
    restarting with:

        # systemctl restart ceph-mgr.target

    Verify the `ceph-mgr` daemons are running by checking `ceph -s`:

        # ceph -s

        ...
          services:
           mon: 3 daemons, quorum foo,bar,baz
           mgr: foo(active), standbys: bar, baz
        ...

6.  Upgrade all OSDs by installing the new packages and restarting the
    ceph-osd daemons on all hosts:

        # systemctl restart ceph-osd.target

    You can monitor the progress of the OSD upgrades with the new
    `ceph versions` or `ceph osd versions` command:

        # ceph osd versions
        {
           "ceph version 12.2.5 (...) luminous (stable)": 12,
           "ceph version 13.2.0 (...) mimic (stable)": 22,
        }

7.  Upgrade all CephFS MDS daemons. For each CephFS file system,

    1.  Reduce the number of ranks to 1. (Make note of the original
        number of MDS daemons first if you plan to restore it later.):

    > \# ceph status \# ceph fs set \<fs_name\> max_mds 1

    1.  Wait for the cluster to deactivate any non-zero ranks by
        periodically checking the status:

    > \# ceph status

    1.  Take all standby MDS daemons offline on the appropriate hosts
        with:

    > \# systemctl stop ceph-mds@\<daemon_name\>

    1.  Confirm that only one MDS is online and is rank 0 for your FS:

    > \# ceph status

    1.  Upgrade the last remaining MDS daemon by installing the new
        packages and restarting the daemon:

            # systemctl restart ceph-mds.target

    2.  Restart all standby MDS daemons that were taken offline:

    > \# systemctl start ceph-mds.target

    1.  Restore the original value of `max_mds` for the volume:

    > \# ceph fs set \<fs_name\> max_mds \<original_max_mds\>

8.  Upgrade all radosgw daemons by upgrading packages and restarting
    daemons on all hosts:

        # systemctl restart radosgw.target

9.  Complete the upgrade by disallowing pre-Mimic OSDs and enabling all
    new Mimic-only functionality:

        # ceph osd require-osd-release mimic

10. If you set `noout` at the beginning, be sure to clear it with:

        # ceph osd unset noout

11. Verify the cluster is healthy with `ceph health`.

### Upgrading from pre-Luminous releases (like Jewel)

You *must* first upgrade to Luminous (12.2.z) before attempting an
upgrade to Mimic. In addition, your cluster must have completed at least
one scrub of all PGs while running Luminous, setting the
`recovery_deletes` and `purged_snapdirs` flags in the OSD map.

### Upgrade compatibility notes

These changes occurred between the Luminous and Mimic releases.

-   *core*:

    -   The `pg force-recovery` command will not work for erasure-coded
        PGs when a Luminous monitor is running along with a Mimic OSD.
        Please use the recommended upgrade order of monitors before OSDs
        to avoid this issue.
    -   The sample `crush-location-hook` script has been removed. Its
        output is equivalent to the built-in default behavior, so it has
        been replaced with an example in the CRUSH documentation.
    -   The `-f` option of the rados tool now means `--format` instead
        of `--force`, for consistency with the ceph tool.
    -   The format of the `config diff` output via the admin socket has
        changed. It now reflects the source of each config option (e.g.,
        default, config file, command line) as well as the final
        (active) value.
    -   Commands variously marked as [del]{.title-ref},
        [delete]{.title-ref}, [remove]{.title-ref} etc. should now all
        be normalized as [rm]{.title-ref}. Commands already supporting
        alternatives to [rm]{.title-ref} remain backward-compatible.
        This changeset applies to the `radosgw-admin` tool as well.
    -   Monitors will now prune on-disk full maps if the number of maps
        grows above a certain number (mon_osdmap_full_prune_min,
        default: 10000), thus preventing unbounded growth of the monitor
        data store. This feature is enabled by default, and can be
        disabled by setting [mon_osdmap_full_prune_enabled]{.title-ref}
        to false.
    -   *rados list-inconsistent-obj format changes:*
        -   Various error strings have been improved. For example, the
            \"oi\" or \"oi_attr\" in errors which stands for object info
            is now \"info\" (e.g. oi_attr_missing is now info_missing).
        -   The object\'s \"selected_object_info\" is now in json format
            instead of string.
        -   The attribute errors (attr_value_mismatch,
            attr_name_mismatch) only apply to user attributes. Only user
            attributes are output and have the internal leading
            underscore stripped.
        -   If there are hash information errors (hinfo_missing,
            hinfo_corrupted, hinfo_inconsistency) then \"hashinfo\" is
            added with the json format of the information. If the
            information is corrupt then \"hashinfo\" is a string
            containing the value.
        -   If there are snapset errors (snapset_missing,
            snapset_corrupted, snapset_inconsistency) then \"snapset\"
            is added with the json format of the information. If the
            information is corrupt then \"snapset\" is a string
            containing the value.
        -   If there are object information errors (info_missing,
            info_corrupted, obj_size_info_mismatch,
            object_info_inconsistency) then \"object_info\" is added
            with the json format of the information instead of a string.
            If the information is corrupt then \"object_info\" is a
            string containing the value.
    -   *rados list-inconsistent-snapset format changes:*
        -   Various error strings have been improved. For example, the
            \"ss_attr\" in errors which stands for snapset info is now
            \"snapset\" (e.g. ss_attr_missing is now snapset_missing).
            The error snapset_mismatch has been renamed to snapset_error
            to better reflect what it means.
        -   The head snapset information is output in json format as
            \"snapset.\" This means that even when there are no head
            errors, the head object will be output when any shard has an
            error. This head object is there to show the snapset that
            was used in determining errors.
    -   The [osd_mon_report_interval_min]{.title-ref} option has been
        renamed to [osd_mon_report_interval]{.title-ref}, and the
        [osd_mon_report_interval_max]{.title-ref} (unused) has been
        eliminated. If this value has been customized on your cluster
        then your configuration should be adjusted in order to avoid
        reverting to the default value.
    -   The config-key interface can store arbitrary binary blobs but
        JSON can only express printable strings. If binary blobs are
        present, the \'ceph config-key dump\' command will show them as
        something like [\<\<\< binary blob of length N
        \>\>\>]{.title-ref}.
    -   Bootstrap auth keys will now be generated automatically on a
        fresh deployment; these keys will also be generated, if missing,
        during upgrade.
    -   The `osd force-create-pg` command now requires a force option to
        proceed because the command is dangerous: it declares that data
        loss is permanent and instructs the cluster to proceed with an
        empty PG in its place, without making any further efforts to
        find the missing data.

    *CephFS*:

    -   Upgrading an MDS cluster to 12.2.3+ will result in all active
        MDS exiting due to feature incompatibilities once an upgraded
        MDS comes online (even as standby). Operators may ignore the
        error messages and continue upgrading/restarting or follow this
        upgrade sequence:

        After upgrading the monitors to Mimic, reduce the number of
        ranks to 1 ([ceph fs set \<fs_name\> max_mds 1]{.title-ref}),
        wait for all other MDS to deactivate, leaving the one active
        MDS, stop all standbys, upgrade the single active MDS, then
        upgrade/start standbys. Finally, restore the previous max_mds.

        !! NOTE: see release notes on snapshots in CephFS if you have
        ever enabled snapshots on your file system.

        See also: <https://tracker.ceph.com/issues/23172>

    -   Several `ceph mds ...` commands have been obsoleted and replaced
        by equivalent `ceph fs ...` commands:

        -   `mds dump` -\> `fs dump`
        -   `mds getmap` -\> `fs dump`
        -   `mds stop` -\> `mds deactivate`
        -   `mds set_max_mds` -\> `fs set max_mds`
        -   `mds set` -\> `fs set`
        -   `mds cluster_down` -\> `fs set cluster_down true`
        -   `mds cluster_up` -\> `fs set cluster_down false`
        -   `mds add_data_pool` -\> `fs add_data_pool`
        -   `mds remove_data_pool` -\> `fs rm_data_pool`
        -   `mds rm_data_pool` -\> `fs rm_data_pool`

    -   New CephFS file system attributes session_timeout and
        session_autoclose are configurable via `ceph fs set`. The MDS
        config options [mds_session_timeout]{.title-ref},
        [mds_session_autoclose]{.title-ref}, and
        [mds_max_file_size]{.title-ref} are now obsolete.

    -   As the multiple MDS feature is now standard, it is now enabled
        by default. `ceph fs set allow_multimds` is now deprecated and
        will be removed in a future release.

    -   As the directory fragmentation feature is now standard, it is
        now enabled by default. `ceph fs set allow_dirfrags` is now
        deprecated and will be removed in a future release.

    -   MDS daemons now activate and deactivate based on the value of
        [max_mds]{.title-ref}. Accordingly, `ceph mds deactivate` has
        been deprecated as it is now redundant.

    -   Taking a CephFS cluster down is now done by setting the down
        flag which deactivates all MDS. For example: [ceph fs set cephfs
        down true]{.title-ref}.

    -   Preventing standbys from joining as new actives (formerly the
        now deprecated cluster_down flag) on a file system is now
        accomplished by setting the joinable flag. This is useful mostly
        for testing so that a file system may be quickly brought down
        and deleted.

    -   New CephFS file system attributes session_timeout and
        session_autoclose are configurable via [ceph fs
        set]{.title-ref}. The MDS config options mds_session_timeout,
        mds_session_autoclose, and mds_max_file_size are now obsolete.

    -   Each mds rank now maintains a table that tracks open files and
        their ancestor directories. Recovering MDS can quickly get open
        files\' paths, significantly reducing the time of loading inodes
        for open files. MDS creates the table automatically if it does
        not exist.

    -   CephFS snapshot is now stable and enabled by default on new
        filesystems. To enable snapshot on existing filesystems, use the
        command:

            ceph fs set <fs_name> allow_new_snaps

        The on-disk format of snapshot metadata has changed. The old
        format metadata can not be properly handled in multiple active
        MDS configuration. To guarantee all snapshot metadata on
        existing filesystems get updated, perform the sequence of
        upgrading the MDS cluster strictly.

        See <http://docs.ceph.com/docs/mimic/cephfs/upgrading/>

        For filesystems that have ever enabled snapshots, the
        multiple-active MDS feature is disabled by the mimic monitor
        daemon. This will cause the \"restore previous max_mds\" step in
        above URL to fail. To re-enable the feature, either delete all
        old snapshots or scrub the whole filesystem:

        > -   `ceph daemon <mds of rank 0> scrub_path / force recursive repair`
        > -   `ceph daemon <mds of rank 0> scrub_path '~mdsdir' force recursive repair`

    -   Support has been added in Mimic for quotas in the Linux kernel
        client as of v4.17.

        See <http://docs.ceph.com/docs/mimic/cephfs/quota/>

    -   Many fixes have been made to the MDS metadata balancer which
        distributes load across MDS. It is expected that the automatic
        balancing should work well for most use-cases. In Luminous,
        subtree pinning was advised as a manual workaround for poor
        balancer behavior. This may no longer be necessary so it is
        recommended to try experimentally disabling pinning as a form of
        load balancing to see if the built-in balancer adequately works
        for you. Please report any poor behavior post-upgrade.

    -   NFS-Ganesha is an NFS userspace server that can export shares
        from multiple file systems, including CephFS. Support for this
        CephFS client has improved significantly in Mimic. In
        particular, delegations are now supported through the libcephfs
        library so that Ganesha may issue delegations to its NFS clients
        allowing for safe write buffering and coherent read caching.
        Documentation is also now available:
        <http://docs.ceph.com/docs/mimic/cephfs/nfs/>

    -   MDS uptime is now available in the output of the MDS admin
        socket `status` command.

    -   MDS performance counters for client requests now include average
        latency as well as the count.

-   *RBD*

    -   The RBD C API\'s [rbd_discard]{.title-ref} method now enforces a
        maximum length of 2GB to match the C++ API\'s
        [Image::discard]{.title-ref} method. This restriction prevents
        overflow of the result code.
    -   The rbd CLI\'s `lock list` JSON and XML output has changed.
    -   The rbd CLI\'s `showmapped` JSON and XML output has changed.
    -   RBD now optionally supports simplified image clone semantics
        where non-protected snapshots can be cloned; and snapshots with
        linked clones can be removed and the space automatically
        reclaimed once all remaining linked clones are detached. This
        feature is enabled by default if the OSD
        \"require-min-compat-client\" flag is set to mimic or later; or
        can be overridden via the \"rbd_default_clone_format\"
        configuration option.
    -   RBD now supports deep copy of images that preserves snapshot
        history.

-   *RGW*

    -   The RGW Beast frontend is now declared stable and ready for
        production use. `rgw_frontends`{.interpreted-text role="ref"}
        for details.
    -   Civetweb frontend has been updated to the latest 1.10 release.
    -   The S3 API now has support for multi-factor authentication.
        Refer to `rgw_mfa`{.interpreted-text role="ref"} for details.
    -   RGW now has a sync plugin to sync to AWS and clouds with S3-like
        APIs.

-   *MGR*

    -   The (read-only) Ceph manager dashboard introduced in Ceph
        Luminous has been replaced with a new implementation, providing
        a drop-in replacement offering a number of additional management
        features. To access the new dashboard, you first need to define
        a username and password and create an SSL certificate. See the
        `mgr-dashboard`{.interpreted-text role="ref"} for a feature
        overview and installation instructions.

    -   The `ceph-rest-api` command-line tool (obsoleted by the MGR
        [restful]{.title-ref} module and deprecated since v12.2.5) has
        been dropped.

        There is a MGR module called [restful]{.title-ref} which
        provides similar functionality via a \"pass through\" method.
        See <http://docs.ceph.com/docs/master/mgr/restful> for details.

    -   New command to track throughput and IOPS statistics, also
        available in `ceph -s` and previously in `ceph -w`. To use this
        command, enable the `iostat` Manager module and invoke it using
        `ceph iostat`. See the
        `iostat documentation <mgr-iostat-overview>`{.interpreted-text
        role="ref"} for details.

-   *build/packaging*

    -   The `rcceph` script (`systemd/ceph` in the source code tree,
        shipped as `/usr/sbin/rcceph` in the ceph-base package for
        CentOS and SUSE) has been dropped. This script was used to
        perform admin operations (start, stop, restart, etc.) on all OSD
        and/or MON daemons running on a given machine. This
        functionality is provided by the systemd target units
        (`ceph-osd.target`, `ceph-mon.target`, etc.).
    -   The python-ceph-compat package is declared deprecated, and will
        be dropped when all supported distros have completed the move to
        Python 3. It has already been dropped from those supported
        distros where Python 3 is standard and Python 2 is optional
        (currently only SUSE).
    -   Ceph codebase has now moved to the C++-17 standard.
    -   The Ceph LZ4 compression plugin is now enabled by default, and
        introduces a new build dependency.

### Detailed Changelog

-   arch/arm: set ceph_arch_aarch64_crc32 only if the build host
    supports crc32cx
    ([issue#19705](http://tracker.ceph.com/issues/19705),
    [pr#17420](https://github.com/ceph/ceph/pull/17420), Kefu Chai)

-   assert(false)-\>ceph_abort()
    ([pr#18072](https://github.com/ceph/ceph/pull/18072), Li Wang)

-   auth: keep /dev/urandom open for get_random_bytes
    ([issue#21401](http://tracker.ceph.com/issues/21401),
    [pr#17972](https://github.com/ceph/ceph/pull/17972), Casey Bodley)

-   bluestore: BlueStore::ExtentMap::dup impl
    ([pr#19719](https://github.com/ceph/ceph/pull/19719), Shinobu Kinjo)

-   bluestore: bluestore/NVMEDevice: accurate the latency perf counter
    of queue latency
    ([pr#17435](https://github.com/ceph/ceph/pull/17435), Ziye Yang, Pan
    Liu)

-   bluestore: bluestore/NVMEDevice: convert the legacy config opt
    related with SPDK
    ([pr#18502](https://github.com/ceph/ceph/pull/18502), Ziye Yang)

-   bluestore: bluestore/NVMEDevice: do not deference a dangling pointer
    ([pr#19067](https://github.com/ceph/ceph/pull/19067), Kefu Chai)

-   bluestore: bluestore/NVMEDevice: fix the bug in write function
    ([pr#17086](https://github.com/ceph/ceph/pull/17086), Ziye Yang, Pan
    Liu)

-   bluestore: bluestore/NVMeDevice: update NVMeDevice code due to SPDK
    upgrade ([pr#16927](https://github.com/ceph/ceph/pull/16927), Ziye
    Yang)

-   bluestore,build/ops: bluestore,cmake: enable building bluestore
    without aio ([pr#19017](https://github.com/ceph/ceph/pull/19017),
    Kefu Chai)

-   bluestore,build/ops: Build: create a proper WITH_BLUESTORE option
    ([pr#18357](https://github.com/ceph/ceph/pull/18357), Alan Somers)

-   bluestore,build/ops: ceph.spec.in,debian/rules: change aio-max-nr to
    1048576 ([pr#17894](https://github.com/ceph/ceph/pull/17894),
    chenliuzhong)

-   bluestore,build/ops,tests: os: add compile option to build
    libbluefs.so ([pr#16733](https://github.com/ceph/ceph/pull/16733),
    Pan Liu)

-   bluestore,build/ops,tests: test/fio: fix build failure caused by
    sequencer replacement
    ([pr#20387](https://github.com/ceph/ceph/pull/20387), Igor Fedotov)

-   bluestore: ceph-bluestore-tool: better fsck/repair,
    bluefs-bdev-{expand,sizes}
    ([pr#17709](https://github.com/ceph/ceph/pull/17709), Sage Weil)

-   bluestore: ceph-bluestore-tool: check if bdev is empty on
    \'bluefs-bdev-expand\'
    ([pr#17874](https://github.com/ceph/ceph/pull/17874), WANG Guoqin)

-   bluestore: ceph-bluestore-tool: link target shouldn\'t ending with
    \"n\" ([pr#18585](https://github.com/ceph/ceph/pull/18585), Yao
    Zongyou)

-   bluestore,common: intarith: get rid of P2\* and ROUND_UP\* macros
    ([pr#21085](https://github.com/ceph/ceph/pull/21085), xie xingguo)

-   bluestore: comp_min_blob_size init error
    ([pr#18318](https://github.com/ceph/ceph/pull/18318), linbing)

-   bluestore: config: Change bluestore_cache_kv_max to type INT64
    ([pr#20255](https://github.com/ceph/ceph/pull/20255), Zhi Zhang)

-   bluestore,core: ceph-bluestore-tool: prime-osd-dir: update symlinks
    instead of bailing
    ([pr#18565](https://github.com/ceph/ceph/pull/18565), Sage Weil)

-   bluestore,core: common/options: bluefs_buffered_io=true by default
    ([pr#20542](https://github.com/ceph/ceph/pull/20542), Sage Weil)

-   bluestore,core: os/bluestore: compensate for bad freelistmanager
    size/blocks metadata
    ([issue#21089](http://tracker.ceph.com/issues/21089),
    [pr#17268](https://github.com/ceph/ceph/pull/17268), Sage Weil)

-   bluestore,core: os/bluestore: fix data read error injection in
    bluestore ([pr#19866](https://github.com/ceph/ceph/pull/19866), Sage
    Weil)

-   bluestore,core: os/bluestore: kv_max -\> kv_min
    ([pr#20544](https://github.com/ceph/ceph/pull/20544), Sage Weil)

-   bluestore,core: os/bluestore: switch default allocator to stupid;
    test both bitmap and stupid in qa
    ([pr#16906](https://github.com/ceph/ceph/pull/16906), Sage Weil)

-   bluestore,core: src/bluestore/NVMEDevice: make all read use
    aio_submit ([pr#17655](https://github.com/ceph/ceph/pull/17655),
    Ziye Yang, Pan Liu)

-   bluestore,core,tests: test/unittest_bluefs: check whether rmdir
    success ([pr#15363](https://github.com/ceph/ceph/pull/15363), shiqi)

-   bluestore,core: tool: ceph-kvstore-tool doesn\'t umount BlueStore
    properly ([issue#21625](http://tracker.ceph.com/issues/21625),
    [pr#18083](https://github.com/ceph/ceph/pull/18083), Chang Liu)

-   bluestore: define default value of LoglevelV only once (3 templates)
    ([pr#20727](https://github.com/ceph/ceph/pull/20727), Matt Benjamin)

-   bluestore: drop unused friend class in SharedDriverQueueData
    ([pr#16894](https://github.com/ceph/ceph/pull/16894), Pan Liu)

-   bluestore: fix aio_t::rval type
    ([issue#23527](http://tracker.ceph.com/issues/23527),
    [pr#21136](https://github.com/ceph/ceph/pull/21136), kungf)

-   bluestore: fix build on armhf
    ([pr#20951](https://github.com/ceph/ceph/pull/20951), Kefu Chai)

-   bluestore: fixed compilation error when enable spdk with gcc 4.8.5
    ([pr#16945](https://github.com/ceph/ceph/pull/16945), Ziye Yang, Pan
    Liu)

-   bluestore: kv/RocksDBStore: extract common code to a new function
    ([pr#16532](https://github.com/ceph/ceph/pull/16532), Pan Liu)

-   bluestore/NVMEDevice: code cleanup
    ([pr#17284](https://github.com/ceph/ceph/pull/17284), Ziye Yang, Pan
    Liu)

-   bluestore: os/bluestore: add bluestore_prefer_deferred_size_hdd/ssd
    to tracked keys
    ([pr#17459](https://github.com/ceph/ceph/pull/17459), xie xingguo)

-   bluestore: os/bluestore: add discard method for ssd\'s performance
    ([pr#14727](https://github.com/ceph/ceph/pull/14727), Taeksang Kim)

-   bluestore: os/bluestore: Add lat record of deferred_queued and
    deferred_aio_wait
    ([pr#17015](https://github.com/ceph/ceph/pull/17015), lisali)

-   bluestore: os/bluestore: Add missing \_\_func\_\_ in dout
    ([pr#17903](https://github.com/ceph/ceph/pull/17903), lisali)

-   bluestore: os/bluestore: add perf counter for allocator
    fragmentation ([pr#21377](https://github.com/ceph/ceph/pull/21377),
    Igor Fedotov)

-   bluestore: os/bluestore: allocate entire write in one go
    ([pr#17698](https://github.com/ceph/ceph/pull/17698), Sage Weil)

-   bluestore: os/bluestore: allow reconstruction of osd data dir from
    bluestore bdev label
    ([pr#18256](https://github.com/ceph/ceph/pull/18256), Sage Weil)

-   bluestore: os/bluestore: alter the allow_eio policy regarding
    kernel\'s error list
    ([issue#23333](http://tracker.ceph.com/issues/23333),
    [pr#21306](https://github.com/ceph/ceph/pull/21306), Radoslaw
    Zarzynski)

-   bluestore: os/bluestore: avoid excessive ops in \_txc_release_alloc
    ([pr#18854](https://github.com/ceph/ceph/pull/18854), Igor Fedotov)

-   bluestore: os/bluestore: avoid omit cache for remove-collection
    ([pr#18785](https://github.com/ceph/ceph/pull/18785), Jianpeng Ma)

-   bluestore: os/bluestore: avoid overhead of std::function in blob_t
    ([pr#20294](https://github.com/ceph/ceph/pull/20294), Radoslaw
    Zarzynski)

-   bluestore: os/bluestore: avoid unneeded BlobRefing in \_do_read()
    ([pr#19864](https://github.com/ceph/ceph/pull/19864), Radoslaw
    Zarzynski)

-   bluestore: os/bluestore: be more verbose when hitting unloaded shard
    in extent map ([pr#21245](https://github.com/ceph/ceph/pull/21245),
    Igor Fedotov)

-   bluestore: os/bluestore/BlueFS: compact log even when sync_metadata
    sees no work ([pr#17354](https://github.com/ceph/ceph/pull/17354),
    Sage Weil)

-   bluestore: os/bluestore/BlueFS: Don\'t call debug related code under
    any condition ([pr#17627](https://github.com/ceph/ceph/pull/17627),
    Jianpeng Ma)

-   bluestore: os/bluestore/BlueFS: don\'t need wait for aio when using
    \_sync_write ([pr#16066](https://github.com/ceph/ceph/pull/16066),
    Haodong Tang)

-   bluestore: os/bluestore/BlueFS: fix race with log flush during async
    log compaction ([issue#21878](http://tracker.ceph.com/issues/21878),
    [pr#18428](https://github.com/ceph/ceph/pull/18428), Sage Weil)

-   bluestore: os/bluestore/BlueFS: move release unused extents work in
    \_flush_and_syn_log
    ([pr#17684](https://github.com/ceph/ceph/pull/17684), Jianpeng Ma)

-   bluestore: os/bluestore/BlueFS: prevent \_compact_log_async reentry
    ([issue#21250](http://tracker.ceph.com/issues/21250),
    [pr#17503](https://github.com/ceph/ceph/pull/17503), Sage Weil)

-   bluestore: os/bluestore/BlueFS: Reduce unnecessary operations in
    collect_metadata
    ([pr#17995](https://github.com/ceph/ceph/pull/17995), Luo Kexue)

-   bluestore: os/bluestore/BlueFS: sanity check that alloc-\>allocate()
    won\'t return 0
    ([pr#18259](https://github.com/ceph/ceph/pull/18259), xie xingguo)

-   bluestore: os/bluestore/BlueFS: several cleanups
    ([pr#17966](https://github.com/ceph/ceph/pull/17966), xie xingguo)

-   bluestore: os/bluestore/bluefs_types: make block_mask 64-bit
    ([pr#21629](https://github.com/ceph/ceph/pull/21629), Sage Weil)

-   bluestore: os/bluestore/BlueStore: ASAP wake up \_kv_finalize_thread
    ([pr#18203](https://github.com/ceph/ceph/pull/18203), Jianpeng Ma)

-   bluestore: os/bluestore/BlueStore: narrow deferred_lock in
    \_deferred_submit_unlock
    ([pr#17628](https://github.com/ceph/ceph/pull/17628), Jianpeng Ma)

-   bluestore: os/bluestore: bluestore repair should use
    interval_set::union_insert
    ([pr#20900](https://github.com/ceph/ceph/pull/20900), Igor Fedotov)

-   bluestore: os/bluestore: cleanup around ExtentList, AllocExtent and
    bluestore_extent_t classes
    ([pr#20360](https://github.com/ceph/ceph/pull/20360), Igor Fedotov)

-   bluestore: os/bluestore: clearer comments, not slower code
    ([pr#16872](https://github.com/ceph/ceph/pull/16872), Mark Nelson)

-   bluestore: os/bluestore: correctly check all block devices to decide
    if journal is_rotational
    ([issue#23141](http://tracker.ceph.com/issues/23141),
    [pr#20602](https://github.com/ceph/ceph/pull/20602), Greg Farnum)

-   bluestore: os/bluestore: delete redundant header file in
    KernelDevice.cc
    ([pr#18631](https://github.com/ceph/ceph/pull/18631), Jing Li)

-   bluestore: os/bluestore: do not assert if BlueFS rebalance is unable
    to allocate sufficient space
    ([pr#18494](https://github.com/ceph/ceph/pull/18494), Igor Fedotov)

-   bluestore: os/bluestore: do not core dump when BlueRocksEnv gets
    EEXIST error ([issue#20871](http://tracker.ceph.com/issues/20871),
    [pr#17357](https://github.com/ceph/ceph/pull/17357), liuchang0812)

-   bluestore: os/bluestore: do not core dump when we try to open
    kvstore twice ([pr#18161](https://github.com/ceph/ceph/pull/18161),
    Chang Liu)

-   bluestore: os/bluestore: do not release empty
    bluefs_extents_reclaiming
    ([pr#18671](https://github.com/ceph/ceph/pull/18671), Igor Fedotov)

-   bluestore: os/bluestore: do not segv on kraken upgrade debug print
    ([issue#20977](http://tracker.ceph.com/issues/20977),
    [pr#16992](https://github.com/ceph/ceph/pull/16992), Sage Weil)

-   bluestore: os/bluestore: don\'t re-initialize csum-setting for
    existing blobs ([issue#21175](http://tracker.ceph.com/issues/21175),
    [pr#17398](https://github.com/ceph/ceph/pull/17398), xie xingguo)

-   bluestore: os/bluestore: do SSD discard on mkfs
    ([pr#20897](https://github.com/ceph/ceph/pull/20897), Igor Fedotov)

-   bluestore: os/bluestore: drop deferred_submit_lock, fix aio leak
    ([issue#21171](http://tracker.ceph.com/issues/21171),
    [pr#17352](https://github.com/ceph/ceph/pull/17352), Sage Weil)

-   bluestore: os/bluestore: drop unused function declaration
    ([pr#18075](https://github.com/ceph/ceph/pull/18075), Li Wang)

-   bluestore: os/bluestore: drop unused param \"what\" in apply()
    ([pr#17251](https://github.com/ceph/ceph/pull/17251), songweibin)

-   bluestore: os/bluestore: \_dump_onode() don\'t prolongate Onode
    anymore ([pr#19841](https://github.com/ceph/ceph/pull/19841),
    Radoslaw Zarzynski)

-   bluestore: os/bluestore: dynamic CF configuration; put pglog omap in
    separate CF ([pr#18224](https://github.com/ceph/ceph/pull/18224),
    Sage Weil)

-   bluestore: os/bluestore: enlarege aligned_size avoid too many
    vector(\> IOV_MAX)
    ([issue#21932](http://tracker.ceph.com/issues/21932),
    [pr#18828](https://github.com/ceph/ceph/pull/18828), Jianpeng Ma)

-   bluestore: os/bluestore: ExtentMap::reshard - fix wrong shard length
    ([pr#17334](https://github.com/ceph/ceph/pull/17334), chenliuzhong)

-   bluestore: os/bluestore: fail early on very large objects
    ([issue#20923](http://tracker.ceph.com/issues/20923),
    [pr#16924](https://github.com/ceph/ceph/pull/16924), Sage Weil)

-   bluestore: os/bluestore: fix another aio stall/deadlock
    ([issue#21470](http://tracker.ceph.com/issues/21470),
    [pr#18118](https://github.com/ceph/ceph/pull/18118), Sage Weil)

-   bluestore: os/bluestore: fix broken cap in
    \_balance_bluefs_freespace()
    ([pr#21097](https://github.com/ceph/ceph/pull/21097), Igor Fedotov)

-   bluestore: os/bluestore: fix clone dirty_range again
    ([issue#20983](http://tracker.ceph.com/issues/20983),
    [pr#16994](https://github.com/ceph/ceph/pull/16994), Sage Weil)

-   bluestore: os/bluestore: fix dirty_shard off-by-one
    ([pr#16850](https://github.com/ceph/ceph/pull/16850), Sage Weil)

-   bluestore: os/bluestore: fix exceeding the max IO queue depth in
    KernelDevice ([issue#23246](http://tracker.ceph.com/issues/23246),
    [pr#20996](https://github.com/ceph/ceph/pull/20996), Radoslaw
    Zarzynski)

-   bluestore: os/bluestore: fix potential assert when splitting
    collection ([pr#19519](https://github.com/ceph/ceph/pull/19519),
    Igor Fedotov)

-   bluestore: os/bluestore: fix SharedBlob unregistration
    ([issue#22039](http://tracker.ceph.com/issues/22039),
    [pr#18805](https://github.com/ceph/ceph/pull/18805), Sage Weil)

-   bluestore: os/bluestore: fix some code formatting
    ([pr#21037](https://github.com/ceph/ceph/pull/21037), Gu Zhongyan)

-   bluestore: os/bluestore: fix the allocate in bluefs
    ([pr#19030](https://github.com/ceph/ceph/pull/19030), tangwenjun)

-   bluestore: os/bluestore: fix the demotion in
    StupidAllocator::init_rm_free
    ([pr#20430](https://github.com/ceph/ceph/pull/20430), Kefu Chai)

-   bluestore: os/bluestore: fix the wrong usage for map_any
    ([pr#18939](https://github.com/ceph/ceph/pull/18939), Jianpeng Ma)

-   bluestore: os/bluestore: fix wrong usage for BlueFS::\_allocate
    ([pr#20708](https://github.com/ceph/ceph/pull/20708), Jianpeng Ma)

-   bluestore: os/bluestore: free the spdk qpair resource correctly in
    destructor of SharedDriverQueueData
    ([pr#20929](https://github.com/ceph/ceph/pull/20929), Jianyu Li)

-   bluestore: os/bluestore: handle small main device properly
    ([pr#17416](https://github.com/ceph/ceph/pull/17416), xie xingguo)

-   bluestore: os/bluestore: ignore 0x2000\~2000 extent oddity from
    luminous upgrade
    ([issue#21408](http://tracker.ceph.com/issues/21408),
    [pr#17845](https://github.com/ceph/ceph/pull/17845), Sage Weil)

-   bluestore: os/bluestore: implement BlueStore repair
    ([pr#19843](https://github.com/ceph/ceph/pull/19843), Igor Fedotov)

-   bluestore: os/bluestore: make bluefs behave better near enospc
    ([pr#18120](https://github.com/ceph/ceph/pull/18120), Sage Weil)

-   bluestore: os/bluestore: mark derivatives of AioContext as final
    ([pr#20227](https://github.com/ceph/ceph/pull/20227), Radoslaw
    Zarzynski)

-   bluestore: os/bluestore: move aio_callback{,\_priv} to base class
    BlockDevice ([pr#17002](https://github.com/ceph/ceph/pull/17002),
    mychoxin)

-   bluestore: os/bluestore: move assert of read/write to base class
    ([pr#17033](https://github.com/ceph/ceph/pull/17033), mychoxin)

-   bluestore: os/bluestore: move size and block_size to the base class
    BlockDevice ([pr#16886](https://github.com/ceph/ceph/pull/16886),
    Pan Liu)

-   bluestore: os/bluestore: no need to fsync when failed to write label
    ([pr#20092](https://github.com/ceph/ceph/pull/20092), tangwenjun)

-   bluestore: os/bluestore: no trim debug noise if there is no trimming
    to be done ([pr#20684](https://github.com/ceph/ceph/pull/20684),
    Sage Weil)

-   bluestore: os/bluestore/NVMEDevice: change write_bl to bl
    ([pr#17145](https://github.com/ceph/ceph/pull/17145), Ziye Yang, Pan
    Liu)

-   bluestore: os/bluestore/NVMEDevice: fix the nvme queue depth issue
    ([pr#17200](https://github.com/ceph/ceph/pull/17200), Ziye Yang, Pan
    Liu)

-   bluestore: os/bluestore/NVMEDevice: Remove using dpdk thread
    ([pr#17769](https://github.com/ceph/ceph/pull/17769), Ziye Yang, Pan
    Liu)

-   bluestore: os/bluestore: OpSequencer: reduce kv_submitted_waiters if
    \_is_all_kv_submitted() return true
    ([pr#18622](https://github.com/ceph/ceph/pull/18622), Jianpeng Ma)

-   bluestore: os/bluestore: optimize \_collection_list
    ([pr#18777](https://github.com/ceph/ceph/pull/18777), Jianpeng Ma)

-   bluestore: os/bluestore: pass strict flag to
    bluestore_blob_use_tracker_t::equal()
    ([pr#15705](https://github.com/ceph/ceph/pull/15705), xie xingguo)

-   bluestore: os/bluestore: Prealloc memory avoid realloc in
    list_collection
    ([pr#18804](https://github.com/ceph/ceph/pull/18804), Jianpeng Ma)

-   bluestore: os/bluestore: prevent mount if osd_max_object_size \>= 4G
    ([pr#19043](https://github.com/ceph/ceph/pull/19043), Sage Weil)

-   bluestore: os/bluestore: print aio in batch
    ([pr#18873](https://github.com/ceph/ceph/pull/18873), Kefu Chai)

-   bluestore: os/bluestore: print leaked extents to debug output
    ([pr#17225](https://github.com/ceph/ceph/pull/17225), Sage Weil)

-   bluestore: os/bluestore: propagate read-EIO to high level callers
    ([pr#17744](https://github.com/ceph/ceph/pull/17744), xie xingguo)

-   bluestore: os/bluestore: put cached attrs in correct mempool
    ([issue#21417](http://tracker.ceph.com/issues/21417),
    [pr#18001](https://github.com/ceph/ceph/pull/18001), Sage Weil)

-   bluestore: os/bluestore: recalc_allocated() when decoding
    bluefs_fnode_t ([issue#23212](http://tracker.ceph.com/issues/23212),
    [pr#20701](https://github.com/ceph/ceph/pull/20701), Jianpeng Ma,
    Kefu Chai)

-   bluestore: os/bluestore: reduce meaningless flush
    ([pr#19027](https://github.com/ceph/ceph/pull/19027), tangwenjun)

-   bluestore: os/bluestore: refactor FreeListManager to get clearer
    view on the number
    ([issue#22535](http://tracker.ceph.com/issues/22535),
    [pr#19718](https://github.com/ceph/ceph/pull/19718), Igor Fedotov)

-   bluestore: os/bluestore: release disk extents in bulky manner
    ([pr#17913](https://github.com/ceph/ceph/pull/17913), Radoslaw
    Zarzynski)

-   bluestore: os/bluestore: remove ineffective BlueFS fnode extent
    calculation ([pr#18905](https://github.com/ceph/ceph/pull/18905),
    Igor Fedotov)

-   bluestore: os/bluestore: remove unused parameters
    ([pr#18635](https://github.com/ceph/ceph/pull/18635), Jianpeng Ma)

-   bluestore: os/bluestore: remove unused variable
    ([pr#21063](https://github.com/ceph/ceph/pull/21063), Gu Zhongyan)

-   bluestore: os/bluestore: remove useless function submit
    ([pr#17537](https://github.com/ceph/ceph/pull/17537), mychoxin)

-   bluestore: os/bluestore: reorder members of bluefs_extent_t for
    space efficiency
    ([pr#21034](https://github.com/ceph/ceph/pull/21034), Radoslaw
    Zarzynski)

-   bluestore: os/bluestore: replace dout with ldout in StupidAllocator
    ([pr#17404](https://github.com/ceph/ceph/pull/17404), Radoslaw
    Zarzynski)

-   bluestore: os/bluestore: report error and quit correctly when disk
    error happens ([issue#21263](http://tracker.ceph.com/issues/21263),
    [pr#17522](https://github.com/ceph/ceph/pull/17522), Pan Liu)

-   bluestore: os/bluestore: Revert \"os/bluestore: allow multiple
    DeferredBatches in flight at once\"
    ([issue#20925](http://tracker.ceph.com/issues/20925),
    [issue#20295](http://tracker.ceph.com/issues/20295),
    [pr#16900](https://github.com/ceph/ceph/pull/16900), Sage Weil)

-   bluestore: os/bluestore: s/bluefs_total/bluefs_free/
    ([pr#21036](https://github.com/ceph/ceph/pull/21036), xie xingguo)

-   bluestore: os/bluestore: separate finisher for deferred_try_submit
    ([issue#21207](http://tracker.ceph.com/issues/21207),
    [pr#17409](https://github.com/ceph/ceph/pull/17409), Sage Weil)

-   bluestore: os/bluestore: set bitmap freelist resolution to
    min_alloc_size ([pr#17610](https://github.com/ceph/ceph/pull/17610),
    Sage Weil)

-   bluestore: os/bluestore: shrink aio submit size to pending value
    ([pr#17588](https://github.com/ceph/ceph/pull/17588), kungf)

-   bluestore: os/bluestore: silence -Wreturn-type warning
    ([pr#18286](https://github.com/ceph/ceph/pull/18286), Kefu Chai)

-   bluestore: os/bluestore: support calculate cost when using spdk
    ([pr#17091](https://github.com/ceph/ceph/pull/17091), Ziye Yang, Pan
    Liu)

-   bluestore: os/bluestore: synchronous on_applied completions
    ([pr#18196](https://github.com/ceph/ceph/pull/18196), Sage Weil)

-   bluestore: os/bluestore: trim cache every 50ms (instead of 200ms)
    ([pr#20498](https://github.com/ceph/ceph/pull/20498), Sage Weil)

-   bluestore: os/bluestore: update description for
    bluestore_compression\_\[min_blob_size options
    ([pr#21244](https://github.com/ceph/ceph/pull/21244), Igor Fedotov)

-   bluestore: os/bluestore: using macro OBJECT_MAX_SIZE to check
    osd_max_object_size
    ([pr#19622](https://github.com/ceph/ceph/pull/19622), Jianpeng Ma)

-   bluestore: osd/bluestore: delete unused variable in KernelDevice
    ([pr#20857](https://github.com/ceph/ceph/pull/20857), Leo Zhang)

-   bluestore: osd,os/bluestore: Display current size of
    osd_max_object_size
    ([pr#19725](https://github.com/ceph/ceph/pull/19725), Shinobu Kinjo)

-   bluestore: Revert \"os/bluestore: pass strict flag to
    bluestore_blob_use_tracker_t::equal()\"
    ([issue#21293](http://tracker.ceph.com/issues/21293),
    [pr#17569](https://github.com/ceph/ceph/pull/17569), Sage Weil)

-   bluestore,rgw: rgw,unittest_bit_alloc: silence clang analyzer
    warning ([pr#17294](https://github.com/ceph/ceph/pull/17294), Kefu
    Chai)

-   bluestore,tests: objectstore/store_test: fix lack of flush prior to
    collection_empty()...
    ([issue#22409](http://tracker.ceph.com/issues/22409),
    [pr#19764](https://github.com/ceph/ceph/pull/19764), Igor Fedotov)

-   bluestore,tests: Revert \"bluestore/fio: Fixed problem with all
    objects having the same hash
    ([pr#18352](https://github.com/ceph/ceph/pull/18352), Radoslaw
    Zarzynski)

-   bluestore,tools: ceph-bluestore-tool: create out_dir before create
    full path of kvdb
    ([pr#18367](https://github.com/ceph/ceph/pull/18367), Leo Zhang)

-   bluestore,tools: os/bluestore/bluestore_tool: add log-dump command
    to dump bluefs\'s log
    ([pr#18535](https://github.com/ceph/ceph/pull/18535), Yang Honggang)

-   build: fix dpdk build error
    ([pr#18087](https://github.com/ceph/ceph/pull/18087), chunmei)

-   build mimic-dev1 with gcc 7
    ([issue#22438](http://tracker.ceph.com/issues/22438),
    [pr#19548](https://github.com/ceph/ceph/pull/19548), Kefu Chai)

-   build/ops: automake: remove files required by automake
    ([pr#17937](https://github.com/ceph/ceph/pull/17937), Kefu Chai)

-   build/ops: blkin: link against lttng-ust-fork
    ([pr#17673](https://github.com/ceph/ceph/pull/17673), Mohamad Gebai)

-   build/ops: boost: remove boost submodule
    ([pr#17405](https://github.com/ceph/ceph/pull/17405), Kefu Chai)

-   build/ops: build: do_cmake: allow ARGS to be overridden
    ([pr#19876](https://github.com/ceph/ceph/pull/19876), Abhishek
    Lekshmanan)

-   build/ops: build: remove PGMap.cc from libcommon
    ([pr#18496](https://github.com/ceph/ceph/pull/18496), Sage Weil)

-   build/ops: ceph-disk activate unlocks bluestore data partition
    ([issue#20488](http://tracker.ceph.com/issues/20488),
    [pr#16357](https://github.com/ceph/ceph/pull/16357), Felix
    Winterhalter)

-   build/ops: ceph_disk: allow \"no fsid\" on activate
    ([pr#18991](https://github.com/ceph/ceph/pull/18991), Dan Mick)

-   build/ops,cephfs: ceph-object-corpus: update to fix make check
    ([pr#21261](https://github.com/ceph/ceph/pull/21261), Patrick
    Donnelly)

-   build/ops,cephfs: cmake, test/fs, client: fix build with clang
    ([pr#20392](https://github.com/ceph/ceph/pull/20392), Adam C.
    Emerson)

-   build/ops: ceph.spec: use devtoolset-6-gcc-c++ on aarch64
    ([issue#22301](http://tracker.ceph.com/issues/22301),
    [pr#19341](https://github.com/ceph/ceph/pull/19341), Kefu Chai)

-   build/ops: ceph-volume: Require lvm2, move to osd package
    ([issue#22443](http://tracker.ceph.com/issues/22443),
    [pr#19529](https://github.com/ceph/ceph/pull/19529), Theofilos
    Mouratidis)

-   build/ops: ceph-volume: tests add tests for the is_mounted utility
    ([pr#16962](https://github.com/ceph/ceph/pull/16962), Alfredo Deza)

-   build/ops: change WITH_SYSTEMD default to ON
    ([pr#20404](https://github.com/ceph/ceph/pull/20404), Nathan Cutler)

-   build/ops: cmake/BuildBoost: fixes to ready seastar
    ([pr#20616](https://github.com/ceph/ceph/pull/20616), Kefu Chai,
    Casey Bodley)

-   build/ops: cmake,deb: install system units using cmake
    ([pr#20618](https://github.com/ceph/ceph/pull/20618), Kefu Chai)

-   build/ops: cmake: link libcommon with libstdc++ statically if
    WITH_STATIC_LIBSTDCXX
    ([issue#22438](http://tracker.ceph.com/issues/22438),
    [pr#19515](https://github.com/ceph/ceph/pull/19515), Kefu Chai)

-   build/ops: cmake,make-dist: bump up boost version to 1.67
    ([pr#21572](https://github.com/ceph/ceph/pull/21572), Kefu Chai)

-   build/ops: cmake,mds: detect std::map::merge() before using it
    ([pr#21211](https://github.com/ceph/ceph/pull/21211), Willem Jan
    Withagen, Kefu Chai)

-   build/ops: cmake/mgr: use Python 3 virtualenv if mgr subinterpreter
    is Python 3 ([pr#21446](https://github.com/ceph/ceph/pull/21446),
    Nathan Cutler)

-   build/ops,common: cmake, common: silence cmake and gcc warnings
    ([issue#23774](http://tracker.ceph.com/issues/23774),
    [pr#21484](https://github.com/ceph/ceph/pull/21484), Kefu Chai)

-   build/ops: common/time: add time.h for Alpine build
    ([pr#19863](https://github.com/ceph/ceph/pull/19863), huanwen ren)

-   build/ops,common: Update C++ standard to 14 and clean up
    ([pr#19490](https://github.com/ceph/ceph/pull/19490), Adam C.
    Emerson)

-   build/ops,core: ceph-crush-location: remove
    ([pr#19881](https://github.com/ceph/ceph/pull/19881), Sage Weil)

-   build/ops,core: ceph-volume: do not use \--key during mkfs
    ([issue#22283](http://tracker.ceph.com/issues/22283),
    [pr#19276](https://github.com/ceph/ceph/pull/19276), Kefu Chai, Sage
    Weil)

-   build/ops,core: /etc/sysconfig/ceph: remove jemalloc option
    ([issue#20557](http://tracker.ceph.com/issues/20557),
    [pr#18487](https://github.com/ceph/ceph/pull/18487), Sage Weil)

-   build/ops,core: mimic: cmake,common,filestore: silence gcc-8
    warnings/errors
    ([pr#21862](https://github.com/ceph/ceph/pull/21862), Kefu Chai)

-   build/ops,core: mimic: cmake: do not check for aligned_alloc()
    anymore ([issue#23653](http://tracker.ceph.com/issues/23653),
    [pr#22048](https://github.com/ceph/ceph/pull/22048), Kefu Chai)

-   build/ops,core: msg/async: update to work with dpdk shipped with
    spdk v17.10 ([pr#19470](https://github.com/ceph/ceph/pull/19470),
    Kefu Chai)

-   build/ops,core: zstd: Upgrade to v1.3.2
    ([pr#18407](https://github.com/ceph/ceph/pull/18407), Adam C.
    Emerson)

-   build/ops: debian/control: adjust
    ceph-{osdomap,kvstore,monstore}-tool feature move
    ([issue#22319](http://tracker.ceph.com/issues/22319),
    [pr#19328](https://github.com/ceph/ceph/pull/19328), Sage Weil)

-   build/ops: debian/control: adjust
    ceph-{osdomap,kvstore,monstore}-tool feature move
    ([issue#22319](http://tracker.ceph.com/issues/22319),
    [pr#19395](https://github.com/ceph/ceph/pull/19395), Kefu Chai, Sage
    Weil)

-   build/ops: debian/control: adjust
    ceph-{osdomap,kvstore,monstore}-tool feature move
    ([pr#19356](https://github.com/ceph/ceph/pull/19356), Kefu Chai)

-   build/ops: debian: fix package relationships after 40caf6a6
    ([issue#21762](http://tracker.ceph.com/issues/21762),
    [pr#18474](https://github.com/ceph/ceph/pull/18474), Kefu Chai)

-   build/ops: debian: lock ceph user during purge
    ([pr#15118](https://github.com/ceph/ceph/pull/15118), Caleb Boylan)

-   build/ops: debian/rules: no more ChangeLog
    ([pr#18023](https://github.com/ceph/ceph/pull/18023), Sage Weil)

-   build/ops: debian/rules: strip ceph-base libraries
    ([issue#22640](http://tracker.ceph.com/issues/22640),
    [pr#19870](https://github.com/ceph/ceph/pull/19870), Sage Weil)

-   build/ops: do\_{cmake,freebsd}: Don\'t invoke nproc(1) on FreeBSD
    ([pr#17949](https://github.com/ceph/ceph/pull/17949), Alan Somers)

-   build/ops: dpdk: remove redundant dpdk submodule
    ([pr#18712](https://github.com/ceph/ceph/pull/18712), chunmei)

-   build/ops: EventKqueue: Clang want realloc return to be typed
    ([pr#21550](https://github.com/ceph/ceph/pull/21550), Willem Jan
    Withagen)

-   build/ops: filestore,rgw: fix types/casts making clang on 32-Bit
    working ([pr#21055](https://github.com/ceph/ceph/pull/21055), Daniel
    Glaser)

-   build/ops: Fix ppc64 support for ceph
    ([pr#16753](https://github.com/ceph/ceph/pull/16753), Boris Ranto)

-   build/ops: Fix two dpdk assert happened in dpdk library
    ([pr#18409](https://github.com/ceph/ceph/pull/18409), chunmei)

-   build/ops: FreeBSD: add new required packages to be installed
    ([pr#21349](https://github.com/ceph/ceph/pull/21349), Willem Jan
    Withagen)

-   build/ops: githubmap: add some known Ceph reviewers
    ([pr#17507](https://github.com/ceph/ceph/pull/17507), Patrick
    Donnelly)

-   build/ops: .githubmap: Add wjwithagen as a known Ceph reviewer
    ([pr#17518](https://github.com/ceph/ceph/pull/17518), Willem Jan
    Withagen)

-   build/ops: .githubmap: Update
    ([pr#18230](https://github.com/ceph/ceph/pull/18230), Sage Weil)

-   build/ops: .gitignore: allow debian .patch files
    ([pr#17577](https://github.com/ceph/ceph/pull/17577), Ken Dreyer)

-   build/ops: include: compat.h, fix the return result of
    pthread_set_name()
    ([pr#20474](https://github.com/ceph/ceph/pull/20474), Willem Jan
    Withagen)

-   build/ops: install-deps: Add support for \'opensuse-tumbleweed\'
    ([pr#21650](https://github.com/ceph/ceph/pull/21650), Ricardo
    Marques)

-   build/ops: install-deps.sh: avoid re-installing g++-7
    ([pr#19468](https://github.com/ceph/ceph/pull/19468), Kefu Chai)

-   build/ops: install-deps.sh, cmake: use GCC-7 on xenial also
    ([pr#19418](https://github.com/ceph/ceph/pull/19418), Kefu Chai)

-   build/ops: install-deps.sh: install new gcc as the default the right
    way ([pr#19417](https://github.com/ceph/ceph/pull/19417), Kefu Chai)

-   build/ops: install-deps.sh: pass \--no-recommends to zypper
    ([issue#22998](http://tracker.ceph.com/issues/22998),
    [pr#20434](https://github.com/ceph/ceph/pull/20434), Nathan Cutler)

-   build/ops: install-deps.sh: set python2 %bcond by environment
    ([issue#22999](http://tracker.ceph.com/issues/22999),
    [pr#20436](https://github.com/ceph/ceph/pull/20436), Nathan Cutler)

-   build/ops: install-deps.sh: use DTS on centos if GCC is too old
    ([pr#19398](https://github.com/ceph/ceph/pull/19398), Kefu Chai)

-   build/ops: install-deps.sh: use tee for writing a file
    ([pr#19516](https://github.com/ceph/ceph/pull/19516), Kefu Chai)

-   build/ops: install-deps: use DTS-7 on aarch64 and only download
    mirrored package indexes
    ([pr#19645](https://github.com/ceph/ceph/pull/19645), Kefu Chai,
    Songbo Wang)

-   build/ops: libmpem: Revert \"submodule: make libmpem as a
    submodule.\" ([pr#18414](https://github.com/ceph/ceph/pull/18414),
    Jianpeng Ma)

-   build/ops: logrotate: add systemd reload in logrotate in case of
    centos minimal without killall
    ([pr#16586](https://github.com/ceph/ceph/pull/16586), Tianshan Qu)

-   build/ops: make-dist,cmake: avoid re-downloading boost
    ([pr#19124](https://github.com/ceph/ceph/pull/19124), Kefu Chai)

-   build/ops: make-dist,cmake: move boost tarball location to
    download.ceph.com
    ([pr#17980](https://github.com/ceph/ceph/pull/17980), Sage Weil)

-   build/ops: make-dist,cmake: Try multiple URLs to download boost
    before failing ([pr#18048](https://github.com/ceph/ceph/pull/18048),
    Brad Hubbard)

-   build/ops: make-dist: fall back to python3
    ([pr#21127](https://github.com/ceph/ceph/pull/21127), Nathan Cutler)

-   build/ops,mgr: mgr/dashboard: build tweaks
    ([pr#20752](https://github.com/ceph/ceph/pull/20752), John Spray)

-   build/ops,mgr: mgr/dashboard: remove node/npm system installation
    ([pr#20898](https://github.com/ceph/ceph/pull/20898), Tiago Melo)

-   build/ops,mgr: packaging: explicit jinja2 dependency for dashboard
    ([issue#22457](http://tracker.ceph.com/issues/22457),
    [pr#19598](https://github.com/ceph/ceph/pull/19598), John Spray)

-   build/ops,mgr,tests: mgr/dashboard: replace dashboard with
    dashboard_v2 ([pr#20912](https://github.com/ceph/ceph/pull/20912),
    Ricardo Dias)

-   build/ops: mimic: cmake: use javac -h for creating JNI native
    headers ([issue#24012](http://tracker.ceph.com/issues/24012),
    [pr#21824](https://github.com/ceph/ceph/pull/21824), Kefu Chai)

-   build/ops: mimic: silence various warnings to enable GCC-8 build
    ([pr#22081](https://github.com/ceph/ceph/pull/22081), Adam C.
    Emerson, Kefu Chai)

-   build/ops: mon,osd: do not use crush_device_class file to initalize
    class for new osds
    ([pr#19939](https://github.com/ceph/ceph/pull/19939), Sage Weil)

-   build/ops: mstart.sh: support read CLUSTERS_LIST from env var
    ([pr#16988](https://github.com/ceph/ceph/pull/16988), Jiaying Ren)

-   build/ops: os/CMakeLists: fix link errro when enable WITH_PMEM=ON
    ([pr#20658](https://github.com/ceph/ceph/pull/20658), Jianpeng Ma)

-   build/ops: osdc,os,osd: fix build on osx
    ([pr#20029](https://github.com/ceph/ceph/pull/20029), Kefu Chai)

-   build/ops: python-numpy-devel build dependency for SUSE
    ([issue#21176](http://tracker.ceph.com/issues/21176),
    [pr#17366](https://github.com/ceph/ceph/pull/17366), Nathan Cutler)

-   build/ops: qa/tests - added for the suites with subset be able to
    use \'testing\' ...
    ([pr#21454](https://github.com/ceph/ceph/pull/21454), Yuri
    Weinstein)

-   build/ops,rbd: ceph-dencoder: moved RBD types outside of RGW
    preprocessor guard
    ([issue#22321](http://tracker.ceph.com/issues/22321),
    [pr#19343](https://github.com/ceph/ceph/pull/19343), Jason Dillaman)

-   build/ops: rbdmap: fix umount when multiple mounts use the same RBD
    ([pr#17978](https://github.com/ceph/ceph/pull/17978), Alexandre
    Marangone)

-   build/ops: Revert \"make-dist: add OBS-specific release suffix on
    SUSE\" ([pr#20813](https://github.com/ceph/ceph/pull/20813), Nathan
    Cutler)

-   build/ops,rgw: radosgw: Make compilation with CryptoPP possible
    ([pr#14955](https://github.com/ceph/ceph/pull/14955), Adam Kupczyk)

-   build/ops: rocksdb: do not use aligned_alloc
    ([issue#23653](http://tracker.ceph.com/issues/23653),
    [pr#21632](https://github.com/ceph/ceph/pull/21632), Kefu Chai)

-   build/ops: rpm: adjust ceph-{osdomap,kvstore,monstore}-tool feature
    move ([issue#22558](http://tracker.ceph.com/issues/22558),
    [pr#19777](https://github.com/ceph/ceph/pull/19777), Kefu Chai)

-   build/ops: rpm: build-depends on \"cunit-devel\" for suse
    ([pr#18997](https://github.com/ceph/ceph/pull/18997), Kefu Chai)

-   build/ops: rpm: conditionalize Python 2 availability to enable Ceph
    build on Python 3-only system
    ([pr#20018](https://github.com/ceph/ceph/pull/20018), Nathan Cutler)

-   build/ops: rpm,debian: Ensure all ceph-disk runtime dependencies are
    declared for ceph-base
    ([issue#23657](http://tracker.ceph.com/issues/23657),
    [pr#21356](https://github.com/ceph/ceph/pull/21356), Nathan Cutler)

-   build/ops: rpm,deb: package ceph-kvstore-tool man page
    ([pr#17387](https://github.com/ceph/ceph/pull/17387), Sage Weil)

-   build/ops: rpm: drop legacy librbd.so.1 symlink in /usr/lib64/qemu
    ([pr#17324](https://github.com/ceph/ceph/pull/17324), Nathan Cutler)

-   build/ops: rpm: fix \_defined_if_python2_absent conditional
    ([pr#20166](https://github.com/ceph/ceph/pull/20166), Nathan Cutler)

-   build/ops: rpm: fix systemd macros for ceph-volume@.service
    ([issue#22217](http://tracker.ceph.com/issues/22217),
    [pr#19081](https://github.com/ceph/ceph/pull/19081), Nathan Cutler)

-   build/ops: rpm: move ceph-\*-tool binaries out of ceph-test
    subpackage ([issue#21762](http://tracker.ceph.com/issues/21762),
    [pr#18289](https://github.com/ceph/ceph/pull/18289), Nathan Cutler)

-   build/ops: rpm: Python 3-only ceph-disk and ceph-volume
    ([pr#20140](https://github.com/ceph/ceph/pull/20140), Nathan Cutler)

-   build/ops: rpm: recommend chrony instead of ntp-daemon
    ([pr#20138](https://github.com/ceph/ceph/pull/20138), Nathan Cutler)

-   build/ops: rpm: recommend python-influxdb with ceph-mgr
    ([pr#18511](https://github.com/ceph/ceph/pull/18511), Nathan Cutler,
    Tim Serong)

-   build/ops: rpm: Revert \"ceph.spec: work around build.opensuse.org\"
    ([pr#21716](https://github.com/ceph/ceph/pull/21716), Nathan Cutler)

-   build/ops: rpm: rip out rcceph script
    ([pr#19899](https://github.com/ceph/ceph/pull/19899), Nathan Cutler)

-   build/ops: rpm: selinux-policy fixes
    ([pr#19026](https://github.com/ceph/ceph/pull/19026), Brad Hubbard)

-   build/ops: rpm: set build parallelism based on available memory
    ([pr#19122](https://github.com/ceph/ceph/pull/19122), Nathan Cutler,
    Richard Brown)

-   build/ops: rpm: set permissions 0755 on rbd resource agent
    ([issue#22362](http://tracker.ceph.com/issues/22362),
    [pr#19494](https://github.com/ceph/ceph/pull/19494), Nathan Cutler)

-   build/ops: run-make-check.sh: fix SUSE support
    ([issue#22875](http://tracker.ceph.com/issues/22875),
    [pr#20234](https://github.com/ceph/ceph/pull/20234), Nathan Cutler)

-   build/ops: run-make-check.sh: handle Python 2 absence
    ([issue#23035](http://tracker.ceph.com/issues/23035),
    [pr#20480](https://github.com/ceph/ceph/pull/20480), Nathan Cutler)

-   build/ops: run-make-check.sh: run ulimit without sudo
    ([pr#17361](https://github.com/ceph/ceph/pull/17361), yang.wang)

-   build/ops: script/build-integration-branch: print pr url list with
    titles ([pr#17426](https://github.com/ceph/ceph/pull/17426), Sage
    Weil)

-   build/ops: selinux: Allow nvme devices
    ([issue#19200](http://tracker.ceph.com/issues/19200),
    [pr#15597](https://github.com/ceph/ceph/pull/15597), Boris Ranto)

-   build/ops: setup-virtualenv.sh: do not hardcode python binary
    ([issue#23437](http://tracker.ceph.com/issues/23437),
    [pr#21002](https://github.com/ceph/ceph/pull/21002), Nathan Cutler)

-   build/ops: spdk: update SPDK to fix the build failure on aarch64
    ([pr#20134](https://github.com/ceph/ceph/pull/20134), Tone Zhang,
    Kefu Chai)

-   build/ops: spdk: update SPDK to v17.10
    ([pr#19208](https://github.com/ceph/ceph/pull/19208), Kefu Chai)

-   build/ops: spdk: update submodule to more recent upstream
    ([pr#20077](https://github.com/ceph/ceph/pull/20077), Nathan Cutler)

-   build/ops: specs: require of e2fsprogs
    ([pr#21345](https://github.com/ceph/ceph/pull/21345), Guillaume
    Abrioux)

-   build/ops: src/script/build-integration-branch
    ([pr#17382](https://github.com/ceph/ceph/pull/17382), Sage Weil)

-   build/ops: src: s/pip \--use-wheel/pip/
    ([pr#21159](https://github.com/ceph/ceph/pull/21159), Kefu Chai)

-   build/ops: submodule: make libmpem as a submodule
    ([pr#17036](https://github.com/ceph/ceph/pull/17036), Jianpeng Ma)

-   build/ops: sysctl.d: set kernel.pid_max=4194304
    ([issue#21929](http://tracker.ceph.com/issues/21929),
    [pr#18544](https://github.com/ceph/ceph/pull/18544), David
    Disseldorp)

-   build/ops: systemd: rbd-mirror does not start on reboot
    ([pr#17969](https://github.com/ceph/ceph/pull/17969), Sébastien Han)

-   build/ops: test: delete asok directories correctly
    ([pr#21023](https://github.com/ceph/ceph/pull/21023), Chang Liu)

-   build/ops: test/fio: enable objectstore FIO plugin building without
    the need to install and build FIO source code
    ([pr#20535](https://github.com/ceph/ceph/pull/20535), Igor Fedotov)

-   build/ops,tests: common,test,cmake: various changes to re-enable
    build on osx ([pr#18888](https://github.com/ceph/ceph/pull/18888),
    Kefu Chai)

-   build/ops,tests: qa/tests: Changed rhel7.4 to rhel7.5
    ([pr#21336](https://github.com/ceph/ceph/pull/21336), Yuri
    Weinstein)

-   build/ops,tests: test/fio: fix fio objectstore plugin building
    broken by ([pr#20514](https://github.com/ceph/ceph/pull/20514), Igor
    Fedotov)

-   build/ops: udev: Fix typo in udev OSD rules file
    ([pr#18976](https://github.com/ceph/ceph/pull/18976), Mitch Birti)

-   build/ops: use devtoolset-7 on centos/rhel-7
    ([pr#18863](https://github.com/ceph/ceph/pull/18863), Kefu Chai)

-   cephfs: Client:Fix readdir bug
    ([pr#18784](https://github.com/ceph/ceph/pull/18784), dongdong tao)

-   cephfs: Client: setattr should drop \"Fs\" rather than \"As\" for
    mtime and size ([pr#18786](https://github.com/ceph/ceph/pull/18786),
    dongdong tao)

-   cephfs,common,rbd: common/common_init: disable ms subsystem log
    gathering for clients
    ([issue#21860](http://tracker.ceph.com/issues/21860),
    [pr#18418](https://github.com/ceph/ceph/pull/18418), Jason Dillaman)

-   cephfs,common,rbd: Various fixes for SCA issues
    ([pr#21708](https://github.com/ceph/ceph/pull/21708), Danny Al-Gaaf)

-   cephfs,core: mon/OSDMonitor: set FLAG_SELFMANAGED_SNAPS on cephfs
    snap removal ([issue#23949](http://tracker.ceph.com/issues/23949),
    [pr#21756](https://github.com/ceph/ceph/pull/21756), Sage Weil)

-   cephfs: MDS: add null check before we push_back \"onfinish\"
    ([pr#18892](https://github.com/ceph/ceph/pull/18892), dongdong tao)

-   cephfs: MDS: correct the error msg when init mon client
    ([pr#18836](https://github.com/ceph/ceph/pull/18836), dongdong tao)

-   cephfs: MDS: make popular counter decay at proper rate
    ([pr#18776](https://github.com/ceph/ceph/pull/18776), Jianyu Li)

-   cephfs: MDS: make rebalancer evaluate the overload state of each mds
    with the same criterion
    ([pr#19255](https://github.com/ceph/ceph/pull/19255), Jianyu Li)

-   cephfs: messages: Initialization of is_primary
    ([pr#16897](https://github.com/ceph/ceph/pull/16897), amitkuma)

-   cephfs: messages: Initialization of member variables
    ([pr#16898](https://github.com/ceph/ceph/pull/16898), amitkuma)

-   cephfs: mimic: MDSMonitor: clean up use of pending fsmap in
    uncommitted ops
    ([issue#23768](http://tracker.ceph.com/issues/23768),
    [pr#22005](https://github.com/ceph/ceph/pull/22005), Patrick
    Donnelly)

-   cephfs: mon/MDSMonitor: wait for readable OSDMap before sanitizing
    ([issue#21945](http://tracker.ceph.com/issues/21945),
    [pr#18603](https://github.com/ceph/ceph/pull/18603), Patrick
    Donnelly)

-   cephfs,mon: mon/MDSMonitor: fix a bug at preprocess_beacon
    ([pr#17415](https://github.com/ceph/ceph/pull/17415), wangshuguang)

-   cephfs: osdc/Journaler: use new style options
    ([pr#17806](https://github.com/ceph/ceph/pull/17806), Kefu Chai)

-   cephfs: qa: check pool full flags
    ([issue#22475](http://tracker.ceph.com/issues/22475),
    [pr#19588](https://github.com/ceph/ceph/pull/19588), Patrick
    Donnelly)

-   cephfs: qa: fix typo in test_full
    ([issue#23643](http://tracker.ceph.com/issues/23643),
    [pr#21334](https://github.com/ceph/ceph/pull/21334), Patrick
    Donnelly)

-   cephfs: Revert \"ceph_context: re-expand admin_socket metavariables
    in child process\"
    ([pr#18545](https://github.com/ceph/ceph/pull/18545), Patrick
    Donnelly)

-   cephfs,tests: qa/suites/powercycle/osd/whitelist_health: whitelist
    slow trimming ([pr#17307](https://github.com/ceph/ceph/pull/17307),
    Sage Weil)

-   cephfs,tests: qa/workunits/cephtool/test.sh: fix test_mon_mds()
    ([pr#21579](https://github.com/ceph/ceph/pull/21579), Kefu Chai)

-   cephfs,tools: mount.fuse.ceph: Fix typo
    ([pr#19128](https://github.com/ceph/ceph/pull/19128), Jos Collin)

-   cephfs: vstart_runner: fixes for recent cephfs changes
    ([pr#19533](https://github.com/ceph/ceph/pull/19533), Patrick
    Donnelly)

-   ceph-volume: add ANSIBLE_SSH_RETRIES=5 to functional tests
    ([pr#20592](https://github.com/ceph/ceph/pull/20592), Andrew Schoen)

-   ceph-volume add functional tests for simple, rearrange lvm tests
    ([pr#18882](https://github.com/ceph/ceph/pull/18882), Alfredo Deza)

-   ceph-volume: Add linesep/newline at end of JSON file when writing
    ([pr#19458](https://github.com/ceph/ceph/pull/19458), Wido den
    Hollander)

-   ceph-volume: adds a \--destroy flag to ceph-volume lvm zap
    ([issue#22653](http://tracker.ceph.com/issues/22653),
    [pr#20010](https://github.com/ceph/ceph/pull/20010), Andrew Schoen)

-   ceph-volume: adds \--crush-device-class flag for lvm prepare and
    create ([pr#19949](https://github.com/ceph/ceph/pull/19949), Andrew
    Schoen)

-   ceph-volume: adds custom cluster name support to simple
    ([pr#20367](https://github.com/ceph/ceph/pull/20367), Andrew Schoen)

-   ceph-volume: adds functional CI testing
    ([pr#16919](https://github.com/ceph/ceph/pull/16919), Andrew Schoen,
    Alfredo Deza)

-   ceph-volume: adds functional testing for bluestore
    ([pr#18656](https://github.com/ceph/ceph/pull/18656), Andrew Schoen)

-   ceph-volume: adds raw device support to \'lvm list\'
    ([issue#23140](http://tracker.ceph.com/issues/23140),
    [pr#20620](https://github.com/ceph/ceph/pull/20620), Andrew Schoen)

-   ceph-volume: adds success messages for lvm prepare/activate/create
    ([issue#22307](http://tracker.ceph.com/issues/22307),
    [pr#19875](https://github.com/ceph/ceph/pull/19875), Andrew Schoen)

-   ceph-volume: adds support to zap encrypted devices
    ([issue#22878](http://tracker.ceph.com/issues/22878),
    [pr#20537](https://github.com/ceph/ceph/pull/20537), Andrew Schoen)

-   ceph-volume: adds the ceph-volume lvm zap subcommand
    ([pr#18513](https://github.com/ceph/ceph/pull/18513), Andrew Schoen)

-   ceph-volume allow filtering by [uuid]{.title-ref}, do not require
    osd id ([pr#17606](https://github.com/ceph/ceph/pull/17606), Andrew
    Schoen, Alfredo Deza)

-   ceph-volume: allow parallel creates
    ([issue#23757](http://tracker.ceph.com/issues/23757),
    [pr#21489](https://github.com/ceph/ceph/pull/21489), Theofilos
    Mouratidis)

-   ceph-volume: allow skipping systemd interactions on activate/create
    ([issue#23678](http://tracker.ceph.com/issues/23678),
    [pr#21496](https://github.com/ceph/ceph/pull/21496), Alfredo Deza)

-   ceph-volume: allow using a device or partition for [lvm
    \--data]{.title-ref}
    ([pr#18924](https://github.com/ceph/ceph/pull/18924), Alfredo Deza)

-   ceph-volume be resilient to \$PATH issues
    ([pr#20650](https://github.com/ceph/ceph/pull/20650), Alfredo Deza)

-   ceph-volume consume mount/format options from ceph.conf
    ([pr#20408](https://github.com/ceph/ceph/pull/20408), Alfredo Deza)

-   ceph-volume: correctly fallback to bluestore when no objectstore is
    specified ([pr#19213](https://github.com/ceph/ceph/pull/19213),
    Alfredo Deza)

-   ceph-volume correctly normalize mount flags
    ([pr#20543](https://github.com/ceph/ceph/pull/20543), Alfredo Deza)

-   ceph-volume: create the ceph-volume and ceph-volume-systemd man
    pages ([issue#21030](http://tracker.ceph.com/issues/21030),
    [pr#17152](https://github.com/ceph/ceph/pull/17152), Alfredo Deza)

-   ceph-volume: dmcrypt support for lvm
    ([issue#22619](http://tracker.ceph.com/issues/22619),
    [pr#20054](https://github.com/ceph/ceph/pull/20054), Alfredo Deza)

-   ceph-volume dmcrypt support for simple
    ([issue#22620](http://tracker.ceph.com/issues/22620),
    [pr#20264](https://github.com/ceph/ceph/pull/20264), Andrew Schoen,
    Alfredo Deza)

-   ceph-volume/doc: add missing subcommand in examples
    ([pr#19381](https://github.com/ceph/ceph/pull/19381), Guillaume
    Abrioux)

-   ceph-volume: ensure correct \--filestore/\--bluestore behavior
    ([pr#18518](https://github.com/ceph/ceph/pull/18518), Alfredo Deza)

-   ceph-volume failed ceph-osd \--mkfs command doesn\'t halt the OSD
    creation process
    ([issue#23874](http://tracker.ceph.com/issues/23874),
    [pr#21685](https://github.com/ceph/ceph/pull/21685), Alfredo Deza)

-   ceph-volume: fix action plugins path in tests
    ([pr#20910](https://github.com/ceph/ceph/pull/20910), Guillaume
    Abrioux)

-   ceph-volume fix filestore OSD creation after mon-config changes
    ([issue#23260](http://tracker.ceph.com/issues/23260),
    [pr#20787](https://github.com/ceph/ceph/pull/20787), Alfredo Deza)

-   ceph-volume: fix typo in ceph-volume lvm prepare help
    ([pr#21196](https://github.com/ceph/ceph/pull/21196), Jeffrey Zhang)

-   ceph-volume: fix usage of the \--osd-id flag
    ([issue#22642](http://tracker.ceph.com/issues/22642),
    [issue#22836](http://tracker.ceph.com/issues/22836),
    [pr#20203](https://github.com/ceph/ceph/pull/20203), Andrew Schoen)

-   ceph-volume Format correctly when vg/lv cannot be used
    ([issue#22299](http://tracker.ceph.com/issues/22299),
    [pr#19285](https://github.com/ceph/ceph/pull/19285), Alfredo Deza)

-   ceph-volume handle inline comments in the ceph.conf file
    ([issue#22297](http://tracker.ceph.com/issues/22297),
    [pr#19319](https://github.com/ceph/ceph/pull/19319), Alfredo Deza)

-   ceph-volume: handle leading whitespace/tabs in ceph.conf
    ([issue#22280](http://tracker.ceph.com/issues/22280),
    [pr#19259](https://github.com/ceph/ceph/pull/19259), Alfredo Deza)

-   ceph-volume Implement an \'activate all\' to help with dense servers
    or migrating OSDs
    ([pr#21130](https://github.com/ceph/ceph/pull/21130), Alfredo Deza)

-   ceph-volume improve robustness when reloading vms in tests
    ([pr#21070](https://github.com/ceph/ceph/pull/21070), Alfredo Deza)

-   ceph-volume: log the current running command for easier debugging
    ([issue#23004](http://tracker.ceph.com/issues/23004),
    [pr#20594](https://github.com/ceph/ceph/pull/20594), Andrew Schoen)

-   ceph-volume lvm api refactor/move
    ([pr#18110](https://github.com/ceph/ceph/pull/18110), Alfredo Deza)

-   ceph-volume lvm list
    ([pr#18095](https://github.com/ceph/ceph/pull/18095), Alfredo Deza)

-   ceph-volume lvm.prepare update to use create_osd_path
    ([pr#18514](https://github.com/ceph/ceph/pull/18514), Alfredo Deza)

-   ceph-volume: lvm zap will unmount osd paths used by zapped devices
    ([issue#22876](http://tracker.ceph.com/issues/22876),
    [pr#20265](https://github.com/ceph/ceph/pull/20265), Andrew Schoen)

-   ceph-volume: Nits noticed while studying code
    ([pr#21455](https://github.com/ceph/ceph/pull/21455), Dan Mick)

-   ceph-volume Persist non-lv devices for journals
    ([pr#17403](https://github.com/ceph/ceph/pull/17403), Alfredo Deza)

-   ceph-volume process the abspath of the executable first
    ([issue#23259](http://tracker.ceph.com/issues/23259),
    [pr#20824](https://github.com/ceph/ceph/pull/20824), Alfredo Deza)

-   ceph-volume: removed the explicit use of sudo
    ([issue#22282](http://tracker.ceph.com/issues/22282),
    [pr#19363](https://github.com/ceph/ceph/pull/19363), Andrew Schoen)

-   ceph-volume: remove extra space
    ([pr#21140](https://github.com/ceph/ceph/pull/21140), Sébastien Han)

-   ceph-volume rollback on failed OSD prepare/create
    ([issue#22281](http://tracker.ceph.com/issues/22281),
    [pr#19351](https://github.com/ceph/ceph/pull/19351), Alfredo Deza)

-   ceph-volume should be able to handle multiple LVM (VG/LV) tags
    ([issue#22305](http://tracker.ceph.com/issues/22305),
    [pr#19321](https://github.com/ceph/ceph/pull/19321), Alfredo Deza)

-   ceph-volume: support GPT and other deployed OSDs
    ([pr#18823](https://github.com/ceph/ceph/pull/18823), Alfredo Deza)

-   ceph-volume tests add optional flags for vagrant
    ([pr#20849](https://github.com/ceph/ceph/pull/20849), Alfredo Deza)

-   ceph-volume tests alleviate libvirt timeouts when reloading
    ([issue#23163](http://tracker.ceph.com/issues/23163),
    [pr#20718](https://github.com/ceph/ceph/pull/20718), Alfredo Deza)

-   ceph-volume tests.devices.lvm prepare isn\'t bluestore specific
    anymore ([pr#18984](https://github.com/ceph/ceph/pull/18984),
    Alfredo Deza)

-   ceph-volume tests remove unused import
    ([pr#20459](https://github.com/ceph/ceph/pull/20459), Alfredo Deza)

-   ceph-volume tests use granular env vars for vagrant
    ([pr#20864](https://github.com/ceph/ceph/pull/20864), Alfredo Deza)

-   ceph-volume: Try to cast OSD metadata to int while scanning
    directory ([pr#19477](https://github.com/ceph/ceph/pull/19477), Wido
    den Hollander)

-   ceph-volume update man page for prepare/activate flags
    ([pr#21570](https://github.com/ceph/ceph/pull/21570), Alfredo Deza)

-   ceph-volume use realpath when checking mounts
    ([issue#22988](http://tracker.ceph.com/issues/22988),
    [pr#20427](https://github.com/ceph/ceph/pull/20427), Alfredo Deza)

-   ceph-volume: use unique logical volumes
    ([pr#17207](https://github.com/ceph/ceph/pull/17207), Alfredo Deza)

-   ceph-volume: Using \--readonly for {vglv}s commands
    ([pr#21409](https://github.com/ceph/ceph/pull/21409), Erwan Velu)

-   ceph-volume: warn on missing ceph.conf file
    ([issue#22326](http://tracker.ceph.com/issues/22326),
    [pr#19347](https://github.com/ceph/ceph/pull/19347), Alfredo Deza)

-   ceph-volume warn on mix of filestore and bluestore flags
    ([issue#23003](http://tracker.ceph.com/issues/23003),
    [pr#20513](https://github.com/ceph/ceph/pull/20513), Alfredo Deza)

-   cleanup: Replacing MIN,MAX with std::min,std::max
    ([pr#18124](https://github.com/ceph/ceph/pull/18124), Amit Kumar)

-   cli: rados: support for high precision time using stat2
    ([issue#21199](http://tracker.ceph.com/issues/21199),
    [pr#17395](https://github.com/ceph/ceph/pull/17395), Abhishek
    Lekshmanan)

-   cls_acl/\_crypto: Add modeline
    ([pr#19010](https://github.com/ceph/ceph/pull/19010), Shinobu Kinjo)

-   cmake: add chrono to BOOST_COMPONENTS
    ([issue#23424](http://tracker.ceph.com/issues/23424),
    [pr#20977](https://github.com/ceph/ceph/pull/20977), Nathan Cutler)

-   cmake: add cython_rbd as a dependency to vstart target
    ([pr#18382](https://github.com/ceph/ceph/pull/18382), Ali Maredia)

-   cmake: bail out if GCC version is less than 5.1
    ([pr#19344](https://github.com/ceph/ceph/pull/19344), Kefu Chai)

-   cmake: BuildBoost.cmake: use specified compiler for building boost
    ([pr#19898](https://github.com/ceph/ceph/pull/19898), Kefu Chai)

-   cmake: bump target jdk to 1.7
    ([issue#23458](http://tracker.ceph.com/issues/23458),
    [pr#21082](https://github.com/ceph/ceph/pull/21082), Shengjing Zhu)

-   cmake: bump up required cmake version to 2.8.12
    ([pr#18285](https://github.com/ceph/ceph/pull/18285), Kefu Chai)

-   cmake: changes of BuildBoost.cmake to ready seastar
    ([pr#21404](https://github.com/ceph/ceph/pull/21404), Kefu Chai)

-   cmake: check for aligned_alloc() instead of checking tcmalloc
    version ([pr#18557](https://github.com/ceph/ceph/pull/18557), Kefu
    Chai)

-   cmake: check gcc version not release date for libstdc++ saneness
    ([pr#18938](https://github.com/ceph/ceph/pull/18938), Kefu Chai)

-   cmake: check version of boost in src/boost
    ([pr#19914](https://github.com/ceph/ceph/pull/19914), Kefu Chai)

-   cmake: cleanups
    ([pr#18597](https://github.com/ceph/ceph/pull/18597), Kefu Chai)

-   cmake,common: changes to port part of ceph to osx
    ([pr#17615](https://github.com/ceph/ceph/pull/17615), Kefu Chai)

-   cmake: compile nvml as an external project
    ([pr#17462](https://github.com/ceph/ceph/pull/17462), Jianpeng Ma)

-   cmake: define HAVE_STDLIB_MAP_SPLICING for both libstdc++ and libc++
    ([pr#21284](https://github.com/ceph/ceph/pull/21284), Kefu Chai)

-   cmake: disable DOWNLOAD_NO_PROGRESS if cmake ver is lower than 3.1
    ([pr#20492](https://github.com/ceph/ceph/pull/20492), Kefu Chai)

-   cmake: disable FAIL_ON_WARNINGS for rocksdb
    ([pr#19426](https://github.com/ceph/ceph/pull/19426), Kefu Chai)

-   cmake: disable VTA on options.cc
    ([pr#17393](https://github.com/ceph/ceph/pull/17393), Kefu Chai)

-   cmake: do not find bzip2/lz4 for rocksdb
    ([pr#19963](https://github.com/ceph/ceph/pull/19963), runsisi)

-   cmake: do not link against librados.a
    ([pr#18576](https://github.com/ceph/ceph/pull/18576), Kefu Chai)

-   cmake: do not link against unused or duplicated libraries
    ([pr#18092](https://github.com/ceph/ceph/pull/18092), Kefu Chai)

-   cmake: enabled py3 only build
    ([pr#20064](https://github.com/ceph/ceph/pull/20064), Kefu Chai)

-   cmake: enable LZ4 by default
    ([pr#21332](https://github.com/ceph/ceph/pull/21332), Grant Slater,
    Casey Bodley)

-   cmake: enable new policies to silence cmake warnings
    ([pr#21662](https://github.com/ceph/ceph/pull/21662), Kefu Chai)

-   cmake: fix building without mgr module
    ([pr#21591](https://github.com/ceph/ceph/pull/21591), Yuan Zhou)

-   cmake: fix frontend cmake build
    ([pr#21449](https://github.com/ceph/ceph/pull/21449), Ricardo Dias)

-   cmake: fix libcephfs-test.jar build failure
    ([issue#22828](http://tracker.ceph.com/issues/22828),
    [pr#20175](https://github.com/ceph/ceph/pull/20175), Tone Zhang)

-   cmake: fix the include dir for building boost::python
    ([pr#20324](https://github.com/ceph/ceph/pull/20324), Kefu Chai)

-   cmake: fix typo in status message
    ([pr#21464](https://github.com/ceph/ceph/pull/21464), Lenz Grimmer)

-   cmake: hide symbols import from other libraries in libcls\_\*
    ([issue#23517](http://tracker.ceph.com/issues/23517),
    [pr#21571](https://github.com/ceph/ceph/pull/21571), Kefu Chai)

-   cmake: identify the possible incompatibility of rocksdb and tcmalloc
    ([issue#21422](http://tracker.ceph.com/issues/21422),
    [pr#17788](https://github.com/ceph/ceph/pull/17788), Kefu Chai)

-   cmake: in case of bad \"ALLOCATOR\" selected issue warning
    ([pr#17422](https://github.com/ceph/ceph/pull/17422), Adam Kupczyk)

-   cmake: include frontend build in \'all\' target
    ([pr#21466](https://github.com/ceph/ceph/pull/21466), John Spray)

-   cmake: let \"tests\" depend on \"mgr-dashboard-frontend-build\"
    ([pr#21468](https://github.com/ceph/ceph/pull/21468), Kefu Chai)

-   cmake: \'make check\' builds radosgw and its cls dependencies
    ([pr#20422](https://github.com/ceph/ceph/pull/20422), Casey Bodley)

-   cmake: mgr: exclude .gitignore
    ([pr#19174](https://github.com/ceph/ceph/pull/19174), Nathan Cutler)

-   cmake/modules/BuildRocksDB.cmake: enable compressions for rocksdb
    ([issue#24025](http://tracker.ceph.com/issues/24025),
    [pr#22183](https://github.com/ceph/ceph/pull/22183), Kefu Chai)

-   cmake: only create sysctl file on linux
    ([pr#19029](https://github.com/ceph/ceph/pull/19029), Kefu Chai)

-   cmake: pass static linkflags to the linker who links libcommon
    ([pr#19763](https://github.com/ceph/ceph/pull/19763), Kefu Chai)

-   cmake: s/boost_256/boost_sha256/
    ([pr#21573](https://github.com/ceph/ceph/pull/21573), Kefu Chai)

-   cmake: set supported language the right way
    ([pr#18216](https://github.com/ceph/ceph/pull/18216), Kefu Chai)

-   cmake: should use the value of GPERFTOOLS_LIBRARIES as REQUIRED_VARS
    ([pr#18645](https://github.com/ceph/ceph/pull/18645), Kefu Chai)

-   cmake: s/sysconf/sysconfig/
    ([pr#20631](https://github.com/ceph/ceph/pull/20631), Kefu Chai)

-   cmake: sync nvml submodule to latest code
    ([pr#20411](https://github.com/ceph/ceph/pull/20411), Jianpeng Ma)

-   cmake: System Includes to silence warnings from submodules and
    libraries! ([pr#18711](https://github.com/ceph/ceph/pull/18711),
    Adam C. Emerson)

-   cmake: typo fix when npm is not found
    ([pr#20801](https://github.com/ceph/ceph/pull/20801), Abhishek
    Lekshmanan)

-   cmake: update minimum boost version to 1.66
    ([issue#20048](http://tracker.ceph.com/issues/20048),
    [issue#22600](http://tracker.ceph.com/issues/22600),
    [pr#19808](https://github.com/ceph/ceph/pull/19808), Casey Bodley)

-   cmake: update the error message for gperftools bug
    ([pr#17901](https://github.com/ceph/ceph/pull/17901), Kefu Chai)

-   cmake: warn if libstdc++ older than 5.1.0 is used
    ([pr#18837](https://github.com/ceph/ceph/pull/18837), Kefu Chai)

-   cmake: WITH_SPDK=ON by default
    ([pr#18944](https://github.com/ceph/ceph/pull/18944), Liu-Chunmei,
    Kefu Chai, wanjun.lp, Ziye Yang)

-   common: adding line break at end of some cli results
    ([issue#21019](http://tracker.ceph.com/issues/21019),
    [pr#16687](https://github.com/ceph/ceph/pull/16687), songweibin)

-   common: add line break for \"ceph daemon TYPE.ID version\"
    ([pr#17146](https://github.com/ceph/ceph/pull/17146), Zhu
    Shangzhong)

-   common: Add metadata with only Ceph version number and release
    ([pr#21095](https://github.com/ceph/ceph/pull/21095), Wido den
    Hollander)

-   common: Add min/max of ms_async_op_threads
    ([pr#19942](https://github.com/ceph/ceph/pull/19942), Shinobu Kinjo)

-   common: Add noreturn attribute to silence uninitialized warning
    ([pr#19348](https://github.com/ceph/ceph/pull/19348), Adam C.
    Emerson)

-   common: auth: add err reason for log info in load function
    ([pr#17256](https://github.com/ceph/ceph/pull/17256), Luo Kexue)

-   common: bench test fall into dead loop when \<seconds\>=0
    ([pr#16382](https://github.com/ceph/ceph/pull/16382), PC)

-   common: buffer: avoid changing bufferlist ABI by removing new
    \_mempool field
    ([issue#21573](http://tracker.ceph.com/issues/21573),
    [pr#18408](https://github.com/ceph/ceph/pull/18408), Sage Weil)

-   common: by default, do not assert on leaks in the shared_cache code
    ([issue#21737](http://tracker.ceph.com/issues/21737),
    [pr#18201](https://github.com/ceph/ceph/pull/18201), Greg Farnum)

-   common: ceph: add the right bracket to watch-channel argument in the
    help message ([pr#19698](https://github.com/ceph/ceph/pull/19698),
    Chang Liu)

-   common: ceph.in: execv using the same python
    ([pr#17713](https://github.com/ceph/ceph/pull/17713), Kefu Chai)

-   common: ceph_release: s/rc/stable/
    ([pr#22264](https://github.com/ceph/ceph/pull/22264), Sage Weil)

-   common: change routines to public access
    ([pr#20003](https://github.com/ceph/ceph/pull/20003), Willem Jan
    Withagen)

-   common: Check this-\>data.op_size before use
    ([pr#18816](https://github.com/ceph/ceph/pull/18816), Amit Kumar)

-   common: cleanup address_helper
    ([pr#19643](https://github.com/ceph/ceph/pull/19643), Shinobu Kinjo)

-   common: cmake,common/RWLock: check for libpthread extensions
    ([pr#19202](https://github.com/ceph/ceph/pull/19202), Kefu Chai)

-   common: common: add for_each_substr() for cheap string split
    ([pr#18798](https://github.com/ceph/ceph/pull/18798), Casey Bodley)

-   common: common: add streaming interfaces for json/xml escaping
    ([pr#19806](https://github.com/ceph/ceph/pull/19806), Casey Bodley)

-   common: common/admin_socket: validate command json before feeding it
    to hook ([pr#20437](https://github.com/ceph/ceph/pull/20437), Kefu
    Chai)

-   common: common/blkdev: fix build in FreeBSD environment
    ([pr#19316](https://github.com/ceph/ceph/pull/19316), Mykola Golub)

-   common: common/buffer: cleanups
    ([pr#18312](https://github.com/ceph/ceph/pull/18312), Shinobu Kinjo)

-   common: common/buffer: switch crc cache to single pair instead of
    map ([pr#18906](https://github.com/ceph/ceph/pull/18906), Piotr
    Dałek)

-   common: common/config: add units to options
    ([issue#22747](http://tracker.ceph.com/issues/22747),
    [pr#20419](https://github.com/ceph/ceph/pull/20419), Kefu Chai)

-   common: common/config: limit calls to normalize_key_name
    ([pr#20318](https://github.com/ceph/ceph/pull/20318), Piotr Dałek)

-   common: common/config: make internal_safe_to_start_threads internal
    ([pr#18884](https://github.com/ceph/ceph/pull/18884), Sage Weil)

-   common: common/ConfUtils: check key before actually normalizing
    ([pr#20370](https://github.com/ceph/ceph/pull/20370), Piotr Dałek)

-   common: common/dns_resolv.cc: Query for AAAA-record if ms_bind_ipv6
    is True ([issue#23078](http://tracker.ceph.com/issues/23078),
    [pr#20530](https://github.com/ceph/ceph/pull/20530), Wido den
    Hollander)

-   common: common/dns_resolve: fix memory leak
    ([pr#19649](https://github.com/ceph/ceph/pull/19649), Yao Zongyou)

-   common: common/event_socket.h: include \<errno.h\> to use errno
    ([pr#18351](https://github.com/ceph/ceph/pull/18351), Kefu Chai)

-   common: common/Formatter: fix string_view usage for
    {json,xml}\_stream_escaper
    ([issue#23622](http://tracker.ceph.com/issues/23622),
    [pr#21317](https://github.com/ceph/ceph/pull/21317), Sage Weil)

-   common: common/hobject: compare two objects\' key directly
    ([pr#21062](https://github.com/ceph/ceph/pull/21062), xie xingguo)

-   common: common/hobject: preserve the order of hobject
    ([pr#21217](https://github.com/ceph/ceph/pull/21217), Kefu Chai)

-   common: common/ipaddr: Do not select link-local IPv6 addresses
    ([issue#21813](http://tracker.ceph.com/issues/21813),
    [pr#20862](https://github.com/ceph/ceph/pull/20862), Wido den
    Hollander)

-   common: common/lockdep: drop hash\<pthread_t\> specialization
    ([pr#20574](https://github.com/ceph/ceph/pull/20574), Kefu Chai)

-   common: common/LogClient: assign seq and queue atomically
    ([issue#18209](http://tracker.ceph.com/issues/18209),
    [pr#16828](https://github.com/ceph/ceph/pull/16828), Sage Weil)

-   common: common/log: Speed improvement for log
    ([pr#19100](https://github.com/ceph/ceph/pull/19100), Adam Kupczyk,
    Kefu Chai)

-   common: common/OpHistory: move insert/cleanup into separate thread
    ([pr#20540](https://github.com/ceph/ceph/pull/20540), Piotr Dałek)

-   common: common/options: drop unused options
    ([pr#20895](https://github.com/ceph/ceph/pull/20895), Kefu Chai)

-   common: common/options: long description for log_stderr_prefix
    ([pr#19869](https://github.com/ceph/ceph/pull/19869), Sage Weil)

-   common: common/options: pass by reference and use user-literals for
    size ([pr#18034](https://github.com/ceph/ceph/pull/18034), Kefu
    Chai)

-   common: common/options: use user-defined literals for default values
    ([pr#17180](https://github.com/ceph/ceph/pull/17180), Kefu Chai)

-   common: common/perf_counters: remove unused parameter
    ([pr#19805](https://github.com/ceph/ceph/pull/19805), Kefu Chai)

-   common: common/pick_address.cc: Cleanup
    ([pr#19707](https://github.com/ceph/ceph/pull/19707), Shinobu Kinjo)

-   common: common/pick_address: wrong prefix_len in pick_iface()
    ([pr#20128](https://github.com/ceph/ceph/pull/20128), Gu Zhongyan)

-   common: common/str_list: s/boost::string_view/std::string_view
    ([pr#20475](https://github.com/ceph/ceph/pull/20475), Kefu Chai)

-   common: common/strtol: fix strict_strtoll() so it accepts hex
    starting with 0x
    ([pr#21521](https://github.com/ceph/ceph/pull/21521), Kefu Chai)

-   common: common/strtoll: remove superfluous const modifier
    ([pr#21560](https://github.com/ceph/ceph/pull/21560), Jan Fajerski)

-   common: common/throttle: start using 64-bit values
    ([issue#22539](http://tracker.ceph.com/issues/22539),
    [pr#19759](https://github.com/ceph/ceph/pull/19759), Igor Fedotov)

-   common: common/types: make numbers a bit nicer when displaying space
    usage ([pr#17126](https://github.com/ceph/ceph/pull/17126), xie
    xingguo)

-   common: common/util: do not print error if VERSION_ID is missing
    ([pr#17787](https://github.com/ceph/ceph/pull/17787), Kefu Chai)

-   common: compressor: use generate_random_number() for type=\"random\"
    ([pr#18272](https://github.com/ceph/ceph/pull/18272), Casey Bodley)

-   common: compressor/zstd: improvements
    ([pr#18879](https://github.com/ceph/ceph/pull/18879), Sage Weil)

-   common: compute SimpleLRU\'s size with contents.size() instead of
    lru.size() ([issue#22613](http://tracker.ceph.com/issues/22613),
    [pr#19813](https://github.com/ceph/ceph/pull/19813), Xuehan Xu)

-   common: config: expand tilde for \~/.ceph/\$cluster.conf
    ([issue#23215](http://tracker.ceph.com/issues/23215),
    [pr#20774](https://github.com/ceph/ceph/pull/20774), Rishabh Dave)

-   common: config: notify config observers on set_mon_vals()
    ([pr#21161](https://github.com/ceph/ceph/pull/21161), Casey Bodley)

-   common: config: Remove \_get_val
    ([pr#18222](https://github.com/ceph/ceph/pull/18222), Adam C.
    Emerson)

-   common/config: use with_val() for better performance
    ([pr#19056](https://github.com/ceph/ceph/pull/19056), Adam C.
    Emerson)

-   common: consolidate spinlocks
    ([pr#15816](https://github.com/ceph/ceph/pull/15816), Jesse
    Williamson)

-   common,core: common, osd: various cleanups
    ([pr#18149](https://github.com/ceph/ceph/pull/18149), Kefu Chai)

-   common,core: common/pick_address: add
    {public,cluster}\_network_interface option
    ([pr#18028](https://github.com/ceph/ceph/pull/18028), Sage Weil)

-   common,core: common/Throttle: Clean up
    ([pr#16618](https://github.com/ceph/ceph/pull/16618), Adam C.
    Emerson)

-   common,core: fix broken use of streamstream::rdbuf()
    ([issue#22715](http://tracker.ceph.com/issues/22715),
    [pr#19998](https://github.com/ceph/ceph/pull/19998), Sage Weil)

-   common,core: include/ceph_features: deprecate a bunch of features
    ([pr#18546](https://github.com/ceph/ceph/pull/18546), Sage Weil)

-   common,core: include,messages,rbd: Initialize counter,group_pool
    ([pr#17774](https://github.com/ceph/ceph/pull/17774), Amit Kumar)

-   common,core: options: Do not use linked lists of pointers!
    ([pr#17984](https://github.com/ceph/ceph/pull/17984), Adam C.
    Emerson)

-   common,core: osdc/Objecter: take budgets across a LingerOp instead
    of on child Ops
    ([issue#22882](http://tracker.ceph.com/issues/22882),
    [pr#20519](https://github.com/ceph/ceph/pull/20519), Greg Farnum)

-   common,core: osd/OpRequest: reduce overhead when disabling tracking
    ([pr#18470](https://github.com/ceph/ceph/pull/18470), Haomai Wang)

-   common,core: rados: Prefer templates to macros
    ([pr#19913](https://github.com/ceph/ceph/pull/19913), Adam C.
    Emerson)

-   common,core,rbd,rgw: common,osd,rgw: Fixes for issues found during
    SCA ([pr#21419](https://github.com/ceph/ceph/pull/21419), Danny
    Al-Gaaf)

-   common,core,rbd,tests,tools: common,mds,mgr,mon,osd: store event
    only if it\'s added
    ([pr#16312](https://github.com/ceph/ceph/pull/16312), Kefu Chai)

-   common,core: Revert \"msg/async/AsyncConnection: unregister
    connection when racing happened\"
    ([issue#22231](http://tracker.ceph.com/issues/22231),
    [pr#19586](https://github.com/ceph/ceph/pull/19586), Sage Weil)

-   common,core: Revert \"osd/OSDMap: allow bidirectional swap of
    pg-upmap-items\"
    ([issue#21410](http://tracker.ceph.com/issues/21410),
    [pr#17760](https://github.com/ceph/ceph/pull/17760), Sage Weil)

-   common: Coverity and SCA fixes
    ([pr#17431](https://github.com/ceph/ceph/pull/17431), Danny Al-Gaaf)

-   common/crc/aarch64: Added cpu feature pmull and make aarch64
    specific... ([pr#22184](https://github.com/ceph/ceph/pull/22184),
    Adam Kupczyk)

-   common: crush/CrushWrapper: fix out of bounds access
    ([issue#20926](http://tracker.ceph.com/issues/20926),
    [pr#16869](https://github.com/ceph/ceph/pull/16869), Sage Weil)

-   common: crypto: remove cryptopp library
    ([pr#20015](https://github.com/ceph/ceph/pull/20015), Casey Bodley)

-   common: denc cleanups and other fixes
    ([pr#19877](https://github.com/ceph/ceph/pull/19877), Adam C.
    Emerson)

-   common: denc: support enum with underlying type
    ([pr#18701](https://github.com/ceph/ceph/pull/18701), Kefu Chai)

-   common: Destroy attr of RWLock after initialized
    ([pr#17103](https://github.com/ceph/ceph/pull/17103), Wen Zhang)

-   common: dmclock: update mClockPriorityQueue with changes in subtree
    ([pr#20992](https://github.com/ceph/ceph/pull/20992), Casey Bodley)

-   common: dout: DoutPrefixProvider operates directly on stream
    ([pr#21608](https://github.com/ceph/ceph/pull/21608), Casey Bodley)

-   common: drop namespace using directives for std
    ([pr#19159](https://github.com/ceph/ceph/pull/19159), Shinobu Kinjo)

-   common: drop unused variables \"bluestore_csum\_\*\_block\" in opts
    ([pr#17394](https://github.com/ceph/ceph/pull/17394), songweibin)

-   common: encoding: reset optional\<\> if it is uninitialized
    ([pr#17599](https://github.com/ceph/ceph/pull/17599), Kefu Chai)

-   common: Extends random.h: numeric types relaxed to compatible types
    (with ([pr#20670](https://github.com/ceph/ceph/pull/20670), Jesse
    Williamson)

-   common: fix BoundedKeyCounter const_pointer_iterator
    ([issue#22139](http://tracker.ceph.com/issues/22139),
    [pr#18953](https://github.com/ceph/ceph/pull/18953), Casey Bodley)

-   common: fix daemon abnormal exit at parsing invalid arguments
    ([issue#21365](http://tracker.ceph.com/issues/21365),
    [issue#21338](http://tracker.ceph.com/issues/21338),
    [pr#17664](https://github.com/ceph/ceph/pull/17664), Yan Jun)

-   common: fix potential memory leak in HTMLFormatter
    ([pr#20699](https://github.com/ceph/ceph/pull/20699), Yao Zongyou)

-   common: fix typo deamon in comments
    ([pr#17687](https://github.com/ceph/ceph/pull/17687),
    yonghengdexin735)

-   common: fix typo in options.cc
    ([pr#20549](https://github.com/ceph/ceph/pull/20549), songweibin)

-   common: FreeBSD wants the correct struct selection for ipv6
    ([issue#21813](http://tracker.ceph.com/issues/21813),
    [pr#21143](https://github.com/ceph/ceph/pull/21143), Willem Jan
    Withagen)

-   common: global: output usage on -h, \--help, or no args before
    contacting mons
    ([pr#20812](https://github.com/ceph/ceph/pull/20812), Sage Weil)

-   common: hint the main branch of dout() accordingly to default
    verbosity ([pr#21259](https://github.com/ceph/ceph/pull/21259),
    Radoslaw Zarzynski)

-   common: implement random number generator (following N3551)
    ([issue#18873](http://tracker.ceph.com/issues/18873),
    [pr#15341](https://github.com/ceph/ceph/pull/15341), Jesse
    Williamson)

-   common: Improving message sent to user when getting signals
    ([issue#23320](http://tracker.ceph.com/issues/23320),
    [pr#21000](https://github.com/ceph/ceph/pull/21000), Erwan Velu)

-   common: include/encoding: fix compat version error message
    ([pr#19660](https://github.com/ceph/ceph/pull/19660), Xinying Song)

-   common: include/interval_set: parameterize by map type and kill
    btree_interval_set.h
    ([pr#18611](https://github.com/ceph/ceph/pull/18611), Sage Weil)

-   common: include/rados: fix typo in librados.h
    ([pr#17988](https://github.com/ceph/ceph/pull/17988), wumingqiao)

-   common: include: Remove unused header, ciso646
    ([pr#18320](https://github.com/ceph/ceph/pull/18320), Shinobu Kinjo)

-   common: include/types: format decimal numbers with decimal factor
    ([issue#22095](http://tracker.ceph.com/issues/22095),
    [pr#19117](https://github.com/ceph/ceph/pull/19117), Jan Fajerski)

-   common: include: xlist: Fix Clang error for missing string
    ([pr#19367](https://github.com/ceph/ceph/pull/19367), Willem Jan
    Withagen)

-   common: interval_set: kill subset_of()
    ([pr#21108](https://github.com/ceph/ceph/pull/21108), xie xingguo)

-   common: interval_set: optimize intersect_of insert operations
    ([issue#21229](http://tracker.ceph.com/issues/21229),
    [pr#17265](https://github.com/ceph/ceph/pull/17265), Zac Medico)

-   common: introduce md_config_cacher_t
    ([pr#20320](https://github.com/ceph/ceph/pull/20320), Radoslaw
    Zarzynski)

-   common: kick off mimic
    ([pr#16993](https://github.com/ceph/ceph/pull/16993), Sage Weil)

-   common: lockdep fixes
    ([issue#20988](http://tracker.ceph.com/issues/20988),
    [pr#17738](https://github.com/ceph/ceph/pull/17738), Jeff Layton)

-   common: log: clear thread-local stream\'s ios flags on reuse
    ([pr#20174](https://github.com/ceph/ceph/pull/20174), Casey Bodley)

-   common: logically dead code inside shunique_lock.h
    ([pr#17341](https://github.com/ceph/ceph/pull/17341), Amit Kumar)

-   common: make ceph_clock_now() inlineable
    ([pr#20443](https://github.com/ceph/ceph/pull/20443), Radoslaw
    Zarzynski)

-   common: Make code to invoke assert() smaller
    ([pr#20445](https://github.com/ceph/ceph/pull/20445), Adam Kupczyk)

-   common: make some message informative, instead of error
    ([pr#16594](https://github.com/ceph/ceph/pull/16594), Willem Jan
    Withagen)

-   common: mark events of TrackedOp outside its constructor
    ([issue#22608](http://tracker.ceph.com/issues/22608),
    [pr#19828](https://github.com/ceph/ceph/pull/19828), Xuehan Xu)

-   common: mgr/dashboard_v2: Fix test_cluster_configuration test
    ([issue#23265](http://tracker.ceph.com/issues/23265),
    [pr#20782](https://github.com/ceph/ceph/pull/20782), Sebastian
    Wagner)

-   common: mimic: include/types: space between number and units
    ([pr#22107](https://github.com/ceph/ceph/pull/22107), Sage Weil)

-   common,mon: crush,mon: fix weight-set vs crush device classes
    ([issue#20939](http://tracker.ceph.com/issues/20939),
    [pr#16883](https://github.com/ceph/ceph/pull/16883), Sage Weil)

-   common,mon,osd,pybind: silence warning and remove executable mode
    bit ([pr#17512](https://github.com/ceph/ceph/pull/17512), Kefu Chai)

-   common: msg/async/AsyncConnection: less noisy debug
    ([pr#20600](https://github.com/ceph/ceph/pull/20600), Sage Weil)

-   common: msg/async: execute on core specified by core_id not its
    index ([pr#20659](https://github.com/ceph/ceph/pull/20659), Kefu
    Chai)

-   common: msg/msg_types: fix the entity_addr_t\'s decoder
    ([pr#17699](https://github.com/ceph/ceph/pull/17699), Kefu Chai)

-   common: msg/simple: s/ceph::size/std::size/
    ([pr#19896](https://github.com/ceph/ceph/pull/19896), Kefu Chai)

-   common/options.cc: cleanup readable literals for default sizes
    ([pr#18425](https://github.com/ceph/ceph/pull/18425), Enming Zhang)

-   common/options.cc: Set Filestore rocksdb compaction readahead option
    ([issue#21505](http://tracker.ceph.com/issues/21505),
    [pr#17900](https://github.com/ceph/ceph/pull/17900), Mark Nelson)

-   common: OpTracker doesn\'t visit TrackedOp when nref == 0
    ([issue#24037](http://tracker.ceph.com/issues/24037),
    [pr#22160](https://github.com/ceph/ceph/pull/22160), Radoslaw
    Zarzynski)

-   common: osdc/Objecter: fix warning
    ([pr#21757](https://github.com/ceph/ceph/pull/21757), Sage Weil)

-   common: osdc/Objecter: record correctly value for
    l_osdc_op_send_bytes
    ([issue#21982](http://tracker.ceph.com/issues/21982),
    [pr#18810](https://github.com/ceph/ceph/pull/18810), Jianpeng Ma)

-   common: osd/PrimaryLogPG: send requests to primary on cache miss
    ([issue#20919](http://tracker.ceph.com/issues/20919),
    [pr#16884](https://github.com/ceph/ceph/pull/16884), Sage Weil)

-   common: osd_types: define max in eversion_t::max() to static
    ([pr#17453](https://github.com/ceph/ceph/pull/17453), yang.wang)

-   common,os: initialize commit_data,cmount,iocb
    ([pr#17766](https://github.com/ceph/ceph/pull/17766), Amit Kumar)

-   common: posix_fallocate on ZFS returns EINVAL
    ([pr#20398](https://github.com/ceph/ceph/pull/20398), Willem Jan
    Withagen)

-   common: rados: clean up rados_getxattrs() and
    rados_striper_getxattrs()
    ([pr#20259](https://github.com/ceph/ceph/pull/20259), Gu Zhongyan)

-   common: RAII-styled mechanism for updating PerfCounters
    ([pr#19149](https://github.com/ceph/ceph/pull/19149), Radoslaw
    Zarzynski)

-   common: random: revert change from boost::optional to std::optional
    ([issue#23778](http://tracker.ceph.com/issues/23778),
    [pr#21567](https://github.com/ceph/ceph/pull/21567), Casey Bodley)

-   common: Remove ceph_clock_gettime, extern keyword
    ([pr#19353](https://github.com/ceph/ceph/pull/19353), Shinobu Kinjo)

-   common: retry_sys_call no need take address of a function pointer
    ([pr#21281](https://github.com/ceph/ceph/pull/21281), Leo Zhang)

-   common: Revert \"common/config: return const reference instead of a
    copy\" ([pr#18934](https://github.com/ceph/ceph/pull/18934), Kefu
    Chai)

-   common: Revert \"core: hint the dout()\'s message crafting as a cold
    code.\" ([issue#23169](http://tracker.ceph.com/issues/23169),
    [pr#20636](https://github.com/ceph/ceph/pull/20636), Kefu Chai)

-   common,rgw: rgw,common,rbd: s/boost::regex/std::regex/
    ([pr#19393](https://github.com/ceph/ceph/pull/19393), Kefu Chai)

-   common,rgw: rgw,common: remove already included header files
    ([pr#19390](https://github.com/ceph/ceph/pull/19390), Yao Zongyou)

-   common: silence jenkins\'s buiding warning in obj_bencher.cc
    ([pr#17272](https://github.com/ceph/ceph/pull/17272), Luo Kexue)

-   common: src/common: update some ms\_\* options to be more consistent
    ([pr#20652](https://github.com/ceph/ceph/pull/20652), shangfufei)

-   common: src/msg/async/rdma: decrease cpu usage by rdtsc instruction
    ([pr#16965](https://github.com/ceph/ceph/pull/16965), Jin Cai)

-   common: Static Pointer
    ([pr#19079](https://github.com/ceph/ceph/pull/19079), Adam C.
    Emerson)

-   common: strict_strtol INT_MAX and INT_MIN is valid
    ([pr#18574](https://github.com/ceph/ceph/pull/18574), Shasha Lu)

-   common: s/unique_lock/lock_guard/, if manual lock/unlock are not
    necessary ([pr#19770](https://github.com/ceph/ceph/pull/19770),
    Shinobu Kinjo)

-   common: Switch singletons to use immobile_any and cleanups
    ([pr#20273](https://github.com/ceph/ceph/pull/20273), Adam C.
    Emerson)

-   common: test: fix unittest memory leak to silence valgrind
    ([pr#19654](https://github.com/ceph/ceph/pull/19654), Yao Zongyou)

-   common,tests: test/common: unittest_mclock_priority_queue builds
    with \"make\" command
    ([pr#17582](https://github.com/ceph/ceph/pull/17582), J. Eric
    Ivancich)

-   common,tests: test/librados: create unique lock names
    ([issue#20798](http://tracker.ceph.com/issues/20798),
    [pr#16953](https://github.com/ceph/ceph/pull/16953), Neha Ojha)

-   common: tools/crushtool: skip device id if no name exists
    ([issue#22117](http://tracker.ceph.com/issues/22117),
    [pr#18901](https://github.com/ceph/ceph/pull/18901), Jan Fajerski)

-   common: use mono clock for HeartbeatMap
    ([pr#17827](https://github.com/ceph/ceph/pull/17827), Xinze Chi,
    Kefu Chai)

-   common: use move instead of copy in build_options()
    ([pr#18003](https://github.com/ceph/ceph/pull/18003), Casey Bodley)

-   common: utime： fix \_\_32u sec time overflow
    ([pr#21113](https://github.com/ceph/ceph/pull/21113), kungf)

-   compressor: add zstd back
    ([pr#21106](https://github.com/ceph/ceph/pull/21106), Kefu Chai)

-   compressor: conditionalize on HAVE_LZ4
    ([pr#17059](https://github.com/ceph/ceph/pull/17059), Kefu Chai)

-   compressor: kill AsyncCompressor which is broken
    ([pr#18472](https://github.com/ceph/ceph/pull/18472), Haomai Wang)

-   core: blkin: Fix unconditional tracing in OSD
    ([pr#19156](https://github.com/ceph/ceph/pull/19156), Yingxin)

-   core: ceph-debug-docker.sh: add ceph-osd-dbg package
    ([pr#17947](https://github.com/ceph/ceph/pull/17947), Patrick
    Donnelly)

-   core: ceph.in: Add blocking mode for scrub and deep-scrub
    ([pr#19793](https://github.com/ceph/ceph/pull/19793), Brad Hubbard)

-   core: ceph.in: do not panic at control+d in interactive mode
    ([pr#18374](https://github.com/ceph/ceph/pull/18374), Kefu Chai)

-   core: ceph.in: print all matched commands if arg missing
    ([issue#22344](http://tracker.ceph.com/issues/22344),
    [pr#19547](https://github.com/ceph/ceph/pull/19547), Kefu Chai)

-   core: ceph.in: use a different variable for holding thrown exception
    ([pr#20663](https://github.com/ceph/ceph/pull/20663), Kefu Chai)

-   core: ceph-kvstore-tool: copy to different store type and cleanup
    properly ([pr#18029](https://github.com/ceph/ceph/pull/18029), Josh
    Durgin)

-   core: ceph-mgr: exit after usage
    ([issue#23482](http://tracker.ceph.com/issues/23482),
    [pr#21401](https://github.com/ceph/ceph/pull/21401), Sage Weil)

-   core: ceph_osd.cc: Drop legacy or redundant code
    ([pr#18718](https://github.com/ceph/ceph/pull/18718), Shinobu Kinjo)

-   core: ceph-osd: some flags are not documented in the help output
    ([issue#20057](http://tracker.ceph.com/issues/20057),
    [pr#15565](https://github.com/ceph/ceph/pull/15565), Yanhu Cao)

-   core: ceph: print output of \"status\" as string not as bytes
    ([pr#21297](https://github.com/ceph/ceph/pull/21297), Kefu Chai)

-   core: ceph-rest-api: when port=0 use the DEFAULT_PORT instead
    ([pr#17443](https://github.com/ceph/ceph/pull/17443), You Ji)

-   core: ceph_test_objectstore: disable filestore_fiemap for tests
    ([issue#21880](http://tracker.ceph.com/issues/21880),
    [pr#18452](https://github.com/ceph/ceph/pull/18452), Sage Weil)

-   core: ceph_test_objectstore: do not change model for 0-length zero
    ([issue#21712](http://tracker.ceph.com/issues/21712),
    [pr#18519](https://github.com/ceph/ceph/pull/18519), Sage Weil)

-   core: ceph_test_rados_api_aio: fix race with full pool and osdmap
    ([issue#23916](http://tracker.ceph.com/issues/23916),
    [issue#23917](http://tracker.ceph.com/issues/23917),
    [pr#21709](https://github.com/ceph/ceph/pull/21709), Sage Weil)

-   core: ceph_test_rados_api_tier: add ListSnap test
    ([pr#17706](https://github.com/ceph/ceph/pull/17706), Xuehan Xu)

-   core: client,osd,test: Initialize fuse_req_key,snap,who,seq
    ([pr#17772](https://github.com/ceph/ceph/pull/17772), Amit Kumar)

-   core: common/admin_socket: various cleanups
    ([pr#20274](https://github.com/ceph/ceph/pull/20274), Adam C.
    Emerson)

-   core: common/config: cleanup remove some unused macros
    ([pr#19599](https://github.com/ceph/ceph/pull/19599), Yao Zongyou)

-   core: common,mds,osd: Explicitly delete copy ctor if noncopyable
    ([pr#19465](https://github.com/ceph/ceph/pull/19465), Shinobu Kinjo)

-   core: common/options: enable multiple rocksdb compaction threads for
    filestore ([pr#18232](https://github.com/ceph/ceph/pull/18232), Josh
    Durgin)

-   core: common, osd: duplicated \"start\" event in OpTracker, improve
    OpTracker::dump_ops
    ([pr#21119](https://github.com/ceph/ceph/pull/21119), Chang Liu)

-   core: compressor: Add Brotli Compressor
    ([pr#19549](https://github.com/ceph/ceph/pull/19549), BI SHUN KE)

-   core: config: lower default omap entries recovered at once
    ([issue#21897](http://tracker.ceph.com/issues/21897),
    [pr#19910](https://github.com/ceph/ceph/pull/19910), Josh Durgin)

-   core: crush/CrushWrapper: fix potential invalid use of iterator
    ([pr#21325](https://github.com/ceph/ceph/pull/21325), xie xingguo)

-   core: dmclock: Delivery of the dmclock delta, rho and phase
    parameter + Enabling the client service tracker
    ([pr#16369](https://github.com/ceph/ceph/pull/16369), Byungsu Park,
    Taewoong Kim)

-   core: erasure-code: refactor the interfaces to hide internals from
    public ([pr#18683](https://github.com/ceph/ceph/pull/18683), Kefu
    Chai)

-   core: erasure-code: use jerasure_free_schedule to properly free a
    schedule ([pr#19650](https://github.com/ceph/ceph/pull/19650), Yao
    Zongyou)

-   core: erasure-code: use std::count() instead
    ([pr#19428](https://github.com/ceph/ceph/pull/19428), Kefu Chai)

-   core: etc/default/ceph: remove jemalloc option
    ([issue#20557](http://tracker.ceph.com/issues/20557),
    [pr#18486](https://github.com/ceph/ceph/pull/18486), Sage Weil)

-   core: filestore: include \<linux/falloc.h\>
    ([pr#20415](https://github.com/ceph/ceph/pull/20415), wumingqiao)

-   core: Fix a dead lock when doing rdma performance test by fio
    ([pr#17016](https://github.com/ceph/ceph/pull/17016), Wang
    Chuanhong)

-   core: Fix asserts caused by DNE pgs left behind after lots of OSD
    restarts ([issue#21833](http://tracker.ceph.com/issues/21833),
    [pr#20571](https://github.com/ceph/ceph/pull/20571), David Zafman)

-   core: include: kill MIN and MAX macros
    ([pr#20886](https://github.com/ceph/ceph/pull/20886), Sage Weil)

-   core: interval_set: optimize intersection_of
    ([pr#17088](https://github.com/ceph/ceph/pull/17088), Zac Medico)

-   core: kv/KeyValueDB: add column family
    ([pr#18049](https://github.com/ceph/ceph/pull/18049), Jianjian Huo,
    Adam C. Emerson, Sage Weil)

-   core: kv/RocksDB: get index and filter blocks memory usage
    ([pr#19934](https://github.com/ceph/ceph/pull/19934), Zhi Zhang)

-   core: kv/RocksDBStore: fix rocksdb error when block cache is
    disabled ([issue#23816](http://tracker.ceph.com/issues/23816),
    [pr#21583](https://github.com/ceph/ceph/pull/21583), Yang Honggang)

-   core: librados: add OPERATION_ORDERSNAP flag and yet another
    aio_operate method
    ([pr#20343](https://github.com/ceph/ceph/pull/20343), Mykola Golub)

-   core: librados.h: add LIBRADOS_SUPPORTS_APP_METADATA
    ([pr#16542](https://github.com/ceph/ceph/pull/16542), Matt Benjamin)

-   core: libradosstriper: fix the function declaration of
    rados_striper_trunc
    ([pr#20301](https://github.com/ceph/ceph/pull/20301), yuelongguang)

-   core: libradosstriper: silence warning from -Wreorder
    ([pr#16890](https://github.com/ceph/ceph/pull/16890), songweibin)

-   core: make the main dout() paths faster and more maintanable
    ([pr#20290](https://github.com/ceph/ceph/pull/20290), Radoslaw
    Zarzynski)

-   core: messages: Initialization of variable beat
    ([pr#17641](https://github.com/ceph/ceph/pull/17641), Amit Kumar)

-   core: messages: Initialize member variables
    ([pr#16846](https://github.com/ceph/ceph/pull/16846), amitkuma)

-   core: messages: initialize variable tid in MMDSFindIno
    ([pr#16793](https://github.com/ceph/ceph/pull/16793), amitkuma)

-   core: messages: Initializing members in MOSDPGUpdateLogMissing
    ([pr#16928](https://github.com/ceph/ceph/pull/16928), amitkuma)

-   core: messages: Initializing variable ceph_mds_reply_head
    ([pr#17090](https://github.com/ceph/ceph/pull/17090), amitkuma)

-   core: messages,journal: Initialization of stats_period,m_active_set
    ([pr#17792](https://github.com/ceph/ceph/pull/17792), Amit Kumar)

-   core: messages/MOSDMap: do compat reencode of crush map, too
    ([issue#21882](http://tracker.ceph.com/issues/21882),
    [pr#18454](https://github.com/ceph/ceph/pull/18454), Sage Weil)

-   core: messages/MOSDOp: a fixes of encode_payload
    ([pr#16836](https://github.com/ceph/ceph/pull/16836), Ying He)

-   core: messages: Silence uninitialized member warnings
    ([pr#17596](https://github.com/ceph/ceph/pull/17596), Amit Kumar)

-   core: mgr/DaemonServer.cc: add \'is_valid=false\' when decode caps
    error ([issue#20990](http://tracker.ceph.com/issues/20990),
    [pr#16978](https://github.com/ceph/ceph/pull/16978), Yanhu Cao)

-   core,mgr: mgr/balancer: improve error message
    ([issue#22814](http://tracker.ceph.com/issues/22814),
    [pr#21427](https://github.com/ceph/ceph/pull/21427), Sage Weil)

-   core,mgr: osd,mgrclient: pass daemon_status by rvalue ref and other
    cleanups ([pr#18509](https://github.com/ceph/ceph/pull/18509), Kefu
    Chai)

-   core,mgr: osd,mgr: report slow requests and pending creating pgs to
    mgr ([pr#18614](https://github.com/ceph/ceph/pull/18614), Kefu Chai)

-   core: mimic: crush: update choose_args on bucket removal
    ([issue#24167](http://tracker.ceph.com/issues/24167),
    [pr#22120](https://github.com/ceph/ceph/pull/22120), Sage Weil)

-   core: mimic: osdc: guard op-\>on_notify_finish with lock
    ([issue#23966](http://tracker.ceph.com/issues/23966),
    [pr#21834](https://github.com/ceph/ceph/pull/21834), Kefu Chai)

-   core: mimic: osd: clean up smart probe
    ([issue#23899](http://tracker.ceph.com/issues/23899),
    [issue#24104](http://tracker.ceph.com/issues/24104),
    [pr#21959](https://github.com/ceph/ceph/pull/21959), Sage Weil, Gu
    Zhongyan)

-   core: mimic: osd: Don\'t evict even when preemption has restarted
    with smaller chunk
    ([pr#22041](https://github.com/ceph/ceph/pull/22041), David Zafman)

-   core: mimic: osd/PrimaryLogPG: fix try_flush_mark_clean write
    contention case
    ([issue#24200](http://tracker.ceph.com/issues/24200),
    [issue#24174](http://tracker.ceph.com/issues/24174),
    [pr#22113](https://github.com/ceph/ceph/pull/22113), Sage Weil)

-   core: mon/ConfigKeyService: dump: print placeholder value for binary
    blobs ([issue#23622](http://tracker.ceph.com/issues/23622),
    [pr#21329](https://github.com/ceph/ceph/pull/21329), Sage Weil)

-   core,mon: crush, mon: bump up map version only if we truly created a
    weight-set ([pr#20178](https://github.com/ceph/ceph/pull/20178), xie
    xingguo)

-   core: mon/LogMonitor: separate out summary by channel
    ([pr#21395](https://github.com/ceph/ceph/pull/21395), Sage Weil)

-   core,mon: mon/AuthMonitor: create bootstrap keys on create_initial()
    ([pr#21236](https://github.com/ceph/ceph/pull/21236), Joao Eduardo
    Luis)

-   core,mon: mon/LogMonitor: do not crash on log sub w/ no messages
    ([pr#21469](https://github.com/ceph/ceph/pull/21469), Sage Weil)

-   core,mon: mon,osd,crush: misc cleanup
    ([pr#20687](https://github.com/ceph/ceph/pull/20687), songweibin)

-   core,mon: mon/OSDMonitor: Comment out unused function
    ([pr#20275](https://github.com/ceph/ceph/pull/20275), Brad Hubbard)

-   core,mon: mon/OSDMonitor: don\'t create pgs if pool was deleted
    ([issue#21309](http://tracker.ceph.com/issues/21309),
    [pr#17600](https://github.com/ceph/ceph/pull/17600), Joao Eduardo
    Luis)

-   core,mon: mon/OSDMonitor: implement cluster pg limit
    ([pr#17427](https://github.com/ceph/ceph/pull/17427), Sage Weil)

-   core,mon: mon/OSDMonitor: list osd tree in named bucket
    ([pr#19564](https://github.com/ceph/ceph/pull/19564), kungf)

-   core: mon, osd: add create-time for pool
    ([pr#21690](https://github.com/ceph/ceph/pull/21690), xie xingguo)

-   core: mon, osd: fix potential collided \*Up Set\* after PG remapping
    ([issue#23118](http://tracker.ceph.com/issues/23118),
    [pr#20653](https://github.com/ceph/ceph/pull/20653), xie xingguo)

-   core,mon: osd,mon: add max-pg-per-osd limit
    ([pr#18358](https://github.com/ceph/ceph/pull/18358), Kefu Chai)

-   core: mon/OSDMonitor: filter out pgs that shouldn\'t exist from
    force-create-pg
    ([pr#20267](https://github.com/ceph/ceph/pull/20267), Sage Weil)

-   core: mon/OSDMonitor: fix min_size default for replicated pools
    ([pr#20555](https://github.com/ceph/ceph/pull/20555), Josh Durgin)

-   core: mon/OSDMonitor: Fix OSDMonitor error message outputs
    ([issue#22351](http://tracker.ceph.com/issues/22351),
    [pr#20022](https://github.com/ceph/ceph/pull/20022), Brad Hubbard)

-   core: mon/OSDMonitor: make \'osd crush class rename\' idempotent
    ([pr#17330](https://github.com/ceph/ceph/pull/17330), xie xingguo)

-   core: mon/OSDMonitor: rename outer name declaration to avoid
    shadowing ([pr#20032](https://github.com/ceph/ceph/pull/20032), Sage
    Weil)

-   core: mon/OSDMonitor: require \--yes-i-really-mean-it for
    force-create-pg
    ([pr#21619](https://github.com/ceph/ceph/pull/21619), Sage Weil)

-   core: mon,osd,osdc: refactor snap trimming (phase 1)
    ([pr#18276](https://github.com/ceph/ceph/pull/18276), Sage Weil)

-   core: mon, osd: per pool space-full flag support
    ([pr#17371](https://github.com/ceph/ceph/pull/17371), xie xingguo)

-   core: mon, osd: turn down non-error scrub message severity
    ([issue#20947](http://tracker.ceph.com/issues/20947),
    [pr#16916](https://github.com/ceph/ceph/pull/16916), John Spray)

-   core: mon/PGMap: fix PGMapDigest decode
    ([pr#22099](https://github.com/ceph/ceph/pull/22099), Sage Weil)

-   core: mon/PGMap: Fix %USED calculation bug
    ([issue#22247](http://tracker.ceph.com/issues/22247),
    [pr#19165](https://github.com/ceph/ceph/pull/19165), Xiaoxi Chen)

-   core: mon/PGMap: remove or narrow columns \'pg ls\' output
    ([pr#20945](https://github.com/ceph/ceph/pull/20945), Sage Weil)

-   core: mon/PGMap: \'unclean\' does not imply damaged
    ([pr#18493](https://github.com/ceph/ceph/pull/18493), Sage Weil)

-   core: MOSDPGRecoveryDelete\[Reply\]: bump header version
    ([pr#17585](https://github.com/ceph/ceph/pull/17585), Josh Durgin)

-   core: msg/asyc/rmda: fix the bug of assert when Infiniband::recv_msg
    receives disconnect message
    ([pr#17688](https://github.com/ceph/ceph/pull/17688), Jin Cai)

-   core: msg/async/AsyncConnection: combine multi alloc into one
    ([pr#18833](https://github.com/ceph/ceph/pull/18833), Haomai Wang)

-   core: msg/async/AsyncConnection: Fix FPE in process_connection
    ([issue#23618](http://tracker.ceph.com/issues/23618),
    [pr#21314](https://github.com/ceph/ceph/pull/21314), Brad Hubbard)

-   core: msg/async/AsyncConnection: state will be NONE if replacing by
    another one ([issue#21883](http://tracker.ceph.com/issues/21883),
    [pr#18467](https://github.com/ceph/ceph/pull/18467), Haomai Wang)

-   core: msg/async/AsyncConnection: unregister connection when racing
    happened ([pr#19013](https://github.com/ceph/ceph/pull/19013),
    Haomai Wang)

-   core: msg/async: batch handle numevents
    ([pr#18321](https://github.com/ceph/ceph/pull/18321), Jianpeng Ma)

-   core: msg/async: don\'t kill connection if replacing
    ([issue#21143](http://tracker.ceph.com/issues/21143),
    [pr#17288](https://github.com/ceph/ceph/pull/17288), Haomai Wang)

-   core: msg/async: don\'t stuck into resetsession/retrysession loop
    ([pr#17276](https://github.com/ceph/ceph/pull/17276), Haomai Wang)

-   core: msg/async: fix bug of data type conversion when uint64_t -\>
    int -\> uint64_t
    ([pr#18210](https://github.com/ceph/ceph/pull/18210), shangfufei)

-   core: msg/async: print error log if add_event fail
    ([pr#17102](https://github.com/ceph/ceph/pull/17102), mychoxin)

-   core: msg/async/rdma: fix multi cephcontext confllicting
    ([pr#16893](https://github.com/ceph/ceph/pull/16893), Haomai Wang)

-   core: msg/async/rdma: fix the bug that rdma polling thread uses the
    same thread name with msg worker
    ([pr#16936](https://github.com/ceph/ceph/pull/16936), Jin Cai)

-   core: msg/async/rdma: improves RX buffer management
    ([pr#16693](https://github.com/ceph/ceph/pull/16693), Alex Mikheev)

-   core: msg/async/rdma: uninitialized variable fix
    ([pr#18091](https://github.com/ceph/ceph/pull/18091), Vasily
    Philipov)

-   core: msg/DispatchQueue: clear queue after wait()
    ([issue#18351](http://tracker.ceph.com/issues/18351),
    [pr#20374](https://github.com/ceph/ceph/pull/20374), Sage Weil)

-   core: msgr/simple: set Pipe::out_seq to in_seq of the connecting
    side ([issue#23807](http://tracker.ceph.com/issues/23807),
    [pr#21585](https://github.com/ceph/ceph/pull/21585), Xuehan Xu)

-   core: os/bluestore: debug bluestore cache shutdown
    ([issue#21259](http://tracker.ceph.com/issues/21259),
    [pr#17844](https://github.com/ceph/ceph/pull/17844), Sage Weil)

-   core: os/bluestore: disable on_applied sync_complete
    ([issue#22668](http://tracker.ceph.com/issues/22668),
    [pr#20169](https://github.com/ceph/ceph/pull/20169), Sage Weil)

-   core: os/bluestore: make bdev label parsing error more meaningful
    and less noisy ([pr#20090](https://github.com/ceph/ceph/pull/20090),
    Sage Weil)

-   core: os/bluestore: make BlueStore opened by start_kv_only
    umountable ([issue#21624](http://tracker.ceph.com/issues/21624),
    [pr#18082](https://github.com/ceph/ceph/pull/18082), Chang Liu)

-   core: os/bluestore: use db-\>rm_range_keys to delete range of keys
    ([pr#18279](https://github.com/ceph/ceph/pull/18279), Xiaoyan Li)

-   core: OSD/admin_socket: add get_mapped_pools command
    ([pr#19112](https://github.com/ceph/ceph/pull/19112), Xiaoxi Chen)

-   core: osdc, class_api: kill implicit string conversions
    ([pr#16648](https://github.com/ceph/ceph/pull/16648), Piotr Dałek)

-   core: osdc: dec num_in_flight for pool_dne case
    ([pr#21110](https://github.com/ceph/ceph/pull/21110), Jianpeng Ma)

-   core: osdc: Do not use lock_guard as unique_lock
    ([pr#19756](https://github.com/ceph/ceph/pull/19756), Shinobu Kinjo)

-   core: osdc: invoke notify finish context on linger commit failure
    ([issue#23966](http://tracker.ceph.com/issues/23966),
    [pr#21786](https://github.com/ceph/ceph/pull/21786), Jason Dillaman)

-   core: osdc/Objecter: add ignore overlay flag if got redirect reply
    ([pr#21275](https://github.com/ceph/ceph/pull/21275), Ting Yi Lin)

-   core: osdc/Objecter: delay initialization of hobject_t in \_send_op
    ([issue#21845](http://tracker.ceph.com/issues/21845),
    [pr#18427](https://github.com/ceph/ceph/pull/18427), Jason Dillaman)

-   core: osdc/Objecter: fix recursive locking in \_finish_command
    ([issue#23940](http://tracker.ceph.com/issues/23940),
    [pr#21742](https://github.com/ceph/ceph/pull/21742), Sage Weil)

-   core: osdc/Objecter: misc cleanups
    ([pr#18476](https://github.com/ceph/ceph/pull/18476), Jianpeng Ma)

-   core: osdc/Objecter: prevent double-invocation of linger op callback
    ([issue#23872](http://tracker.ceph.com/issues/23872),
    [pr#21649](https://github.com/ceph/ceph/pull/21649), Jason Dillaman)

-   core: osdc/Objecter: skip sparse-read result decode if bufferlist is
    empty ([issue#21844](http://tracker.ceph.com/issues/21844),
    [pr#18400](https://github.com/ceph/ceph/pull/18400), Jason Dillaman)

-   core: osd,compressor: Expose compression algorithms via MOSDBoot
    ([issue#22420](http://tracker.ceph.com/issues/22420),
    [pr#20558](https://github.com/ceph/ceph/pull/20558), Jesse
    Williamson)

-   core: osdc: remove unused function
    ([pr#21081](https://github.com/ceph/ceph/pull/21081), Jianpeng Ma)

-   core: osd,dmclock: use pointer to ClientInfo instead of a copy of it
    ([pr#18387](https://github.com/ceph/ceph/pull/18387), Kefu Chai)

-   core: osd: do not forget pg_stat acks which failed to send
    ([pr#16702](https://github.com/ceph/ceph/pull/16702), huangjun)

-   core: OSD: drop unsed parameter passed to check_osdmap_features
    ([pr#18466](https://github.com/ceph/ceph/pull/18466), Leo Zhang)

-   core: osd/ECBackend: inject sleep during deep scrub
    ([pr#20531](https://github.com/ceph/ceph/pull/20531), xie xingguo)

-   core: osd/ECBackend: only check required shards when finishing
    recovery reads ([issue#23195](http://tracker.ceph.com/issues/23195),
    [pr#21273](https://github.com/ceph/ceph/pull/21273), Josh Durgin)

-   core: osd/ECBackend: update misleading comment about EIO handling
    ([pr#21686](https://github.com/ceph/ceph/pull/21686), Josh Durgin)

-   core: osd/ECBackend: wait for apply for luminous peers
    ([pr#21604](https://github.com/ceph/ceph/pull/21604), Sage Weil)

-   core: osd/ECMsgTypes: fix ECSubRead compat decode
    ([pr#20948](https://github.com/ceph/ceph/pull/20948), Sage Weil)

-   core: osd, librados: add a rados op (TIER_PROMOTE)
    ([pr#19362](https://github.com/ceph/ceph/pull/19362), Myoungwon Oh)

-   core: osd,librados: add manifest, operations for chunked object
    ([pr#15482](https://github.com/ceph/ceph/pull/15482), Myoungwon Oh)

-   core: osd,messages: Initialize read_length,options,send_reply
    ([pr#17799](https://github.com/ceph/ceph/pull/17799), Amit Kumar)

-   core: osd/OSD: batch-list objects to reduce memory consumption
    ([pr#20767](https://github.com/ceph/ceph/pull/20767), xie xingguo)

-   core: osd/OSD.cc: add \'isvalid=false\' when failed to parse caps
    ([pr#16888](https://github.com/ceph/ceph/pull/16888), Yanhu Cao)

-   core: osd/OSD.cc: use option \'osd_scrub_cost\' instead
    ([pr#18479](https://github.com/ceph/ceph/pull/18479), Liao Weizhong)

-   core: osd/OSDMap: add osdmap epoch info when printing info summary
    ([pr#20184](https://github.com/ceph/ceph/pull/20184), shun-s)

-   core: osd/OSDMap: fix HAVE_FEATURE logic in encode()
    ([pr#20922](https://github.com/ceph/ceph/pull/20922), Ilya Dryomov)

-   core: osd/OSDMap: ignore PGs from pools of failure-domain OSD
    ([pr#20703](https://github.com/ceph/ceph/pull/20703), xie xingguo)

-   core: osd/OSDMap: misleading message in print_oneline_summary()
    ([issue#22350](http://tracker.ceph.com/issues/22350),
    [pr#20313](https://github.com/ceph/ceph/pull/20313), Gu Zhongyan)

-   core: osd/OSDMap: more pg upmap fixes
    ([issue#23878](http://tracker.ceph.com/issues/23878),
    [pr#21670](https://github.com/ceph/ceph/pull/21670), xiexingguo)

-   core: osd/OSDMap: remove the unnecessary checks for null
    ([pr#18636](https://github.com/ceph/ceph/pull/18636), Kefu Chai)

-   core: osd/OSDMap: skip out/crush-out osds
    ([pr#20655](https://github.com/ceph/ceph/pull/20655), xie xingguo)

-   core: osd/OSDMap: upmap should respect the osd reweights
    ([issue#21538](http://tracker.ceph.com/issues/21538),
    [pr#17944](https://github.com/ceph/ceph/pull/17944), Theofilos
    Mouratidis)

-   core: osd/osd_type: get_clone_bytes - inline size() for overlapping
    size ([pr#17823](https://github.com/ceph/ceph/pull/17823), xie
    xingguo)

-   core: osd/osd_types.cc: copy extents map too while making clone
    ([pr#18396](https://github.com/ceph/ceph/pull/18396), xie xingguo)

-   core: osd/osd_types: fix ideal lower bound object-id of pg
    ([pr#21235](https://github.com/ceph/ceph/pull/21235), xie xingguo)

-   core: osd/osd_types: fix object_stat_sum_t decode
    ([pr#18551](https://github.com/ceph/ceph/pull/18551), Sage Weil)

-   core: osd/osd_types: fix pg_pool_t encoding for hammer
    ([pr#21282](https://github.com/ceph/ceph/pull/21282), Sage Weil)

-   core: osd/osd_types: kill preferred field in pg_t
    ([pr#20567](https://github.com/ceph/ceph/pull/20567), Sage Weil)

-   core: osd/osd_types: object_info_t: remove unused function
    ([pr#17905](https://github.com/ceph/ceph/pull/17905), Kefu Chai)

-   core: osd/osd_types: pg_pool_t: remove crash_replay_interval member
    ([pr#18379](https://github.com/ceph/ceph/pull/18379), Sage Weil)

-   core: osd/osd_types: remove backlog type for pg_log_entry_t
    ([pr#20887](https://github.com/ceph/ceph/pull/20887), Sage Weil)

-   core: osd/OSD: Using Wait rather than WaitInterval to wait
    queue.is_empty()
    ([pr#17659](https://github.com/ceph/ceph/pull/17659), Jianpeng Ma)

-   core: osd/PG: allow scrub preemption
    ([pr#18971](https://github.com/ceph/ceph/pull/18971), Sage Weil)

-   core: osd/PGBackend: delete reply if fails to complete delete
    request ([issue#20913](http://tracker.ceph.com/issues/20913),
    [pr#17183](https://github.com/ceph/ceph/pull/17183), Kefu Chai)

-   core: osd/PGBackend: drop input \"snapid_t\" from
    objects_list_range()
    ([pr#21151](https://github.com/ceph/ceph/pull/21151), xie xingguo)

-   core: osd/PGBackend: fix large_omap_objects checking
    ([pr#21150](https://github.com/ceph/ceph/pull/21150), xie xingguo)

-   core: osd/PGBackend: release a msg using msg-\>put() not delete
    ([issue#20913](http://tracker.ceph.com/issues/20913),
    [pr#17246](https://github.com/ceph/ceph/pull/17246), Kefu Chai)

-   core: osd/PG: const cleanup for recoverable/readable predicates
    ([pr#18982](https://github.com/ceph/ceph/pull/18982), Neha Ojha)

-   core: osd/PG: decay scrub_chunk_max too if scrub is preempted
    ([pr#20552](https://github.com/ceph/ceph/pull/20552), xie xingguo)

-   core: osd/PG: discard msgs from down peers
    ([issue#19605](http://tracker.ceph.com/issues/19605),
    [pr#17217](https://github.com/ceph/ceph/pull/17217), Kefu Chai)

-   core: osd/PG: drop unused variable \"oldest_update\" in PG.h
    ([pr#17142](https://github.com/ceph/ceph/pull/17142), songweibin)

-   core: osd/PG: extend pg state bits to fix pg ls commands error
    ([issue#21609](http://tracker.ceph.com/issues/21609),
    [pr#18058](https://github.com/ceph/ceph/pull/18058), Yan Jun)

-   core: osd/PG: fix calc of misplaced objects
    ([pr#18528](https://github.com/ceph/ceph/pull/18528), Kefu Chai)

-   core: osd/PG: fix DeferRecovery vs AllReplicasRecovered race
    ([issue#23860](http://tracker.ceph.com/issues/23860),
    [pr#21706](https://github.com/ceph/ceph/pull/21706), Sage Weil)

-   core: osd/PG: fix objects degraded higher than 100%
    ([issue#21803](http://tracker.ceph.com/issues/21803),
    [issue#21898](http://tracker.ceph.com/issues/21898),
    [pr#18297](https://github.com/ceph/ceph/pull/18297), Sage Weil,
    David Zafman)

-   core: osd/PG: fix out of order priority for PG deletion
    ([pr#21613](https://github.com/ceph/ceph/pull/21613), xie xingguo)

-   core: osd/PG: fix recovery op leak
    ([pr#18524](https://github.com/ceph/ceph/pull/18524), Sage Weil)

-   core: osd/PG: fix uninit read in Incomplete::react(AdvMap&)
    ([issue#23980](http://tracker.ceph.com/issues/23980),
    [pr#21798](https://github.com/ceph/ceph/pull/21798), Sage Weil)

-   core: osd/PG: force rebuild of missing set on jewel upgrade
    ([issue#20958](http://tracker.ceph.com/issues/20958),
    [pr#16950](https://github.com/ceph/ceph/pull/16950), Sage Weil)

-   core: osd/PG: include primary in PG operator\<\< for ec pools
    ([pr#19453](https://github.com/ceph/ceph/pull/19453), Sage Weil)

-   core: osd/PGLog: assert out on performing overflowed log trimming
    ([pr#21580](https://github.com/ceph/ceph/pull/21580), xie xingguo)

-   core: osd/PGLog: cleanup unused function revise_have
    ([pr#19329](https://github.com/ceph/ceph/pull/19329), Enming Zhang)

-   core: osd/PGLog: fix sanity check against \*\*complete-to\*\* iter
    ([pr#21612](https://github.com/ceph/ceph/pull/21612), songweibin)

-   core: osd/PGLog: get rid of ineffective container operations
    ([pr#19161](https://github.com/ceph/ceph/pull/19161), xie xingguo)

-   core: osd/PGLog: write only changed dup entries
    ([issue#21026](http://tracker.ceph.com/issues/21026),
    [pr#17245](https://github.com/ceph/ceph/pull/17245), Josh Durgin)

-   core: osd, pg, mgr: make snap trim queue problems visible
    ([issue#22448](http://tracker.ceph.com/issues/22448),
    [pr#19520](https://github.com/ceph/ceph/pull/19520), Piotr Dałek)

-   core: osd/PG: misc cleanups
    ([pr#18340](https://github.com/ceph/ceph/pull/18340), Yan Jun)

-   core: osd/PG: miscellaneous choose acting changes and cleanups
    ([pr#18481](https://github.com/ceph/ceph/pull/18481), xie xingguo)

-   core: osd/PG: pass scrub priority to replica
    ([pr#20317](https://github.com/ceph/ceph/pull/20317), Sage Weil)

-   core: osd/PG: perfer async_recovery_targets in reverse order of cost
    ([pr#21578](https://github.com/ceph/ceph/pull/21578), xie xingguo)

-   core: osd/PG: perfer EC async_recovery_targets in reverse order of
    cost ([pr#21588](https://github.com/ceph/ceph/pull/21588), xie
    xingguo)

-   core: osd/PG: PGPool::update: avoid expensive union_of
    ([pr#17239](https://github.com/ceph/ceph/pull/17239), Zac Medico)

-   core: osd/PGPool::update: optimize with subset_of
    ([pr#17820](https://github.com/ceph/ceph/pull/17820), Zac Medico)

-   core: osd/PG: reduce some overhead on operating MissingLoc
    ([pr#18186](https://github.com/ceph/ceph/pull/18186), xie xingguo)

-   core: osd/PG: remote recovery preemption, and new feature bit to
    condition it on
    ([pr#18553](https://github.com/ceph/ceph/pull/18553), Sage Weil)

-   core: osd/PG: remove unused parameter in calc_ec_acting
    ([pr#17304](https://github.com/ceph/ceph/pull/17304), yang.wang)

-   core: osd/PG: restart recovery if NotRecovering and unfound found
    ([issue#22145](http://tracker.ceph.com/issues/22145),
    [pr#18974](https://github.com/ceph/ceph/pull/18974), Sage Weil)

-   core: osd/PG: revert approx size
    ([issue#22654](http://tracker.ceph.com/issues/22654),
    [pr#18755](https://github.com/ceph/ceph/pull/18755), Adam Kupczyk)

-   core: osd/PG: re-write of \_update_calc_stats and improve pg
    degraded state ([issue#20059](http://tracker.ceph.com/issues/20059),
    [pr#19850](https://github.com/ceph/ceph/pull/19850), David Zafman)

-   core: osd/PG: some cleanups && add should_gather filter for loop
    logging ([pr#19546](https://github.com/ceph/ceph/pull/19546), Enming
    Zhang)

-   core: osd/PG: two cleanups
    ([pr#17171](https://github.com/ceph/ceph/pull/17171), xie xingguo)

-   core: osd/PG: use osd_backfill_retry_interval for
    schedule_backfill_retry()
    ([pr#18686](https://github.com/ceph/ceph/pull/18686), xie xingguo)

-   core: osd/PrimaryLogPG: add condition \"is_chunky_scrub_active\" to
    check object in chunky_scrub
    ([pr#18506](https://github.com/ceph/ceph/pull/18506), Jianpeng Ma)

-   core: osd/PrimaryLogPG: arrange recovery order by number of missing
    objects ([pr#18292](https://github.com/ceph/ceph/pull/18292), xie
    xingguo)

-   core: osd/PrimaryLogPG: avoid infinite loop when flush collides with
    write lock ([pr#21653](https://github.com/ceph/ceph/pull/21653),
    Sage Weil)

-   core: osd/PrimaryLogPG: calc clone_overlap size in a more efficient
    and concise way
    ([pr#17928](https://github.com/ceph/ceph/pull/17928), xie xingguo)

-   core: osd/PrimaryLogPG: cleanup do_sub_op && do_sub_op_reply and
    define soid in prepare_transaction more appropriate
    ([pr#19495](https://github.com/ceph/ceph/pull/19495), Enming Zhang)

-   core: osd/PrimaryLogPG: clear data digest on WRITEFULL if
    skip_data_digest
    ([pr#21676](https://github.com/ceph/ceph/pull/21676), Sage Weil)

-   core: osd/PrimaryLogPG: clear pin_stats_invalid bit properly on
    scrub-repair completion
    ([pr#18052](https://github.com/ceph/ceph/pull/18052), xie xingguo)

-   core: osd/PrimaryLogPG: defer evict if head \*or\* object intersect
    scrub interval ([issue#23646](http://tracker.ceph.com/issues/23646),
    [pr#21628](https://github.com/ceph/ceph/pull/21628), Sage Weil)

-   core: osd/PrimaryLogPG: do not pull-up snapc to snapset
    ([pr#18713](https://github.com/ceph/ceph/pull/18713), Sage Weil)

-   core: osd/PrimaryLogPG: do not set data digest for bluestore
    ([pr#17515](https://github.com/ceph/ceph/pull/17515), xie xingguo)

-   core: osd/PrimaryLogPG: do not set data/omap digest blindly
    ([pr#18061](https://github.com/ceph/ceph/pull/18061), xie xingguo)

-   core: osd/PrimaryLogPG: do not use approx_size() for log trimming
    ([pr#18338](https://github.com/ceph/ceph/pull/18338), xie xingguo)

-   core: osd/PrimaryLogPG: do_osd_ops - propagate EAGAIN/EINPROGRESS on
    failok ([pr#17222](https://github.com/ceph/ceph/pull/17222), xie
    xingguo)

-   core: osd/PrimaryLogPG: drop unused parameters
    ([pr#18581](https://github.com/ceph/ceph/pull/18581), Liao Weizhong)

-   core: osd/PrimaryLogPG: fix dup stat for async read
    ([pr#18693](https://github.com/ceph/ceph/pull/18693), Xinze Chi)

-   core: osd/PrimaryLogPG: Fix log messages
    ([pr#21639](https://github.com/ceph/ceph/pull/21639), Gu Zhongyan)

-   core: osd/PrimaryLogPG: fix sparse read won\'t trigger repair
    correctly ([pr#17221](https://github.com/ceph/ceph/pull/17221), xie
    xingguo)

-   core: osd/PrimaryLogPG: fix the oi size mismatch with real object
    size ([issue#23701](http://tracker.ceph.com/issues/23701),
    [pr#21408](https://github.com/ceph/ceph/pull/21408), Peng Xie)

-   core: osd/PrimaryLogPG: kick off recovery on backoffing a degraded
    object ([pr#17987](https://github.com/ceph/ceph/pull/17987), xie
    xingguo)

-   core: osd/PrimaryLogPG: kill add_interval_usage
    ([pr#17807](https://github.com/ceph/ceph/pull/17807), xie xingguo)

-   core: osd/PrimaryLogPG: maybe_handle_manifest_detail - sanity check
    obc existence ([pr#17298](https://github.com/ceph/ceph/pull/17298),
    xie xingguo)

-   core: osd/PrimaryLogPG: misc cleanups
    ([pr#17830](https://github.com/ceph/ceph/pull/17830), Yan Jun)

-   core: osd/PrimaryLogPG: more oi.extents fixes
    ([pr#18616](https://github.com/ceph/ceph/pull/18616), xie xingguo)

-   core: osd/PrimaryLogPG: prepare_transaction - fix EDQUOT vs ENOSPC
    ([pr#17808](https://github.com/ceph/ceph/pull/17808), xie xingguo)

-   core: osd/PrimaryLogPG: request osdmap update in the right block
    ([issue#21428](http://tracker.ceph.com/issues/21428),
    [pr#17828](https://github.com/ceph/ceph/pull/17828), Josh Durgin)

-   core: osd/PrimaryLogPG: several oi.extents fixes
    ([pr#18527](https://github.com/ceph/ceph/pull/18527), xie xingguo)

-   core: osd/PrimaryLogPG: trigger auto-repair on full-object-size CRC
    error ([pr#18353](https://github.com/ceph/ceph/pull/18353), xie
    xingguo)

-   core: osd/ReplicatedBackend: clean up code
    ([pr#20127](https://github.com/ceph/ceph/pull/20127), Jianpeng Ma)

-   core: osd/ReplicatedBackend: \'osd_deep_scrub_keys\' doesn\'t work
    ([pr#20221](https://github.com/ceph/ceph/pull/20221), fang yuxiang)

-   core: osd/ReplicatedPG: add omap write bytes to delta_stats
    ([pr#18471](https://github.com/ceph/ceph/pull/18471), Haomai Wang)

-   core: osd_types.cc: reorder fields in serialized pg_stat_t
    ([pr#19965](https://github.com/ceph/ceph/pull/19965), Piotr Dałek)

-   core: os/filestore: disable rocksdb compression
    ([pr#18707](https://github.com/ceph/ceph/pull/18707), Sage Weil)

-   core: os/filestore/FileStore: Initialized by nullptr, NULL or 0
    instead ([pr#18980](https://github.com/ceph/ceph/pull/18980),
    Shinobu Kinjo)

-   core: os/filestore: fix device/partition metadata detection
    ([issue#20944](http://tracker.ceph.com/issues/20944),
    [pr#16913](https://github.com/ceph/ceph/pull/16913), Sage Weil)

-   core: os/filestore: fix do_copy_range replay bug
    ([issue#23298](http://tracker.ceph.com/issues/23298),
    [pr#20832](https://github.com/ceph/ceph/pull/20832), Sage Weil)

-   core: os/Filestore: fix wbthrottle assert
    ([pr#14213](https://github.com/ceph/ceph/pull/14213), Xiaoxi Chen)

-   core: os/filestore: print out the error if do_read_entry() fails
    ([pr#18346](https://github.com/ceph/ceph/pull/18346), Kefu Chai)

-   core: os: FileStore, Using stl min \| max, MIN \| MAX macros instead
    ([pr#19832](https://github.com/ceph/ceph/pull/19832), Shinobu Kinjo)

-   core: os: fix 0-length zero semantics, add tests
    ([issue#21712](http://tracker.ceph.com/issues/21712),
    [pr#18159](https://github.com/ceph/ceph/pull/18159), Sage Weil)

-   core: os/FuseStore: fix incorrect used space statistics for fuse\'s
    statfs interface
    ([pr#19033](https://github.com/ceph/ceph/pull/19033), Zhi Zhang)

-   core: os/kstore: Drop unused function declaration
    ([pr#18077](https://github.com/ceph/ceph/pull/18077), Jos Collin)

-   core: os/kstore: fix statfs problem and add vstart.sh support
    ([issue#23590](http://tracker.ceph.com/issues/23590),
    [pr#21287](https://github.com/ceph/ceph/pull/21287), Yang Honggang)

-   core: os/memstore: Fix wrong use of lock_guard
    ([pr#20914](https://github.com/ceph/ceph/pull/20914), Shen-Ta Hsieh)

-   core: os/ObjectStore: fix get_data_alignment return -1 causing
    problem in msg header
    ([pr#18475](https://github.com/ceph/ceph/pull/18475), Haomai Wang)

-   core: os/ObjectStore.h: fix mistake in comment TRANSACTION ISOLATION
    ([pr#16840](https://github.com/ceph/ceph/pull/16840), mychoxin)

-   core: os,osd: initial work to drop onreadable/onapplied callbacks
    ([issue#23029](http://tracker.ceph.com/issues/23029),
    [pr#20177](https://github.com/ceph/ceph/pull/20177), Sage Weil)

-   core: os: unify Sequencer and CollectionHandle
    ([pr#20173](https://github.com/ceph/ceph/pull/20173), Sage Weil)

-   core: PG: fix name of WaitActingChange
    ([pr#18768](https://github.com/ceph/ceph/pull/18768), wumingqiao)

-   core: pg: handle MNotifyRec event in down state
    ([pr#20959](https://github.com/ceph/ceph/pull/20959), Mingxin Liu)

-   core: PGPool::update: optimize removed_snaps comparison when
    possible ([pr#17410](https://github.com/ceph/ceph/pull/17410), Zac
    Medico)

-   core: PGPool::update: optimize with interval_set.swap
    ([pr#17121](https://github.com/ceph/ceph/pull/17121), Zac Medico)

-   core: PG: primary should not be in the peer_info, skip if it is
    ([pr#20189](https://github.com/ceph/ceph/pull/20189), Neha Ojha)

-   core: ptl-tool: checkout branch after creation
    ([pr#18157](https://github.com/ceph/ceph/pull/18157), Patrick
    Donnelly)

-   core: ptl-tool: load labeled PRs
    ([pr#18231](https://github.com/ceph/ceph/pull/18231), Patrick
    Donnelly)

-   core: ptl-tool: make branch name configurable
    ([pr#18499](https://github.com/ceph/ceph/pull/18499), Patrick
    Donnelly)

-   core: ptl-tool: print bzs/tickets cited in commit msgs/comments
    ([pr#18547](https://github.com/ceph/ceph/pull/18547), Patrick
    Donnelly)

-   core: pybind/ceph_argparse: fix cli output info
    ([pr#17667](https://github.com/ceph/ceph/pull/17667), Luo Kexue)

-   core: pybind/ceph_argparse: Fix UnboundLocalError if command
    doesn\'t validate
    ([pr#21342](https://github.com/ceph/ceph/pull/21342), Tim Serong)

-   core: pybind/ceph_argparse.py:\'timeout\' must in kwargs when call
    run_in_thread ([pr#21659](https://github.com/ceph/ceph/pull/21659),
    yangdeliu)

-   core,pybind: pybind/ceph_argparse: accept flexible req
    ([pr#20791](https://github.com/ceph/ceph/pull/20791), Gu Zhongyan)

-   core,pybind: pybind/rados: add alignment getter to IoCtx
    ([pr#21222](https://github.com/ceph/ceph/pull/21222), Bruce Flynn)

-   core,pybind: pybind/rados: add rados_service\_\*()
    ([pr#18812](https://github.com/ceph/ceph/pull/18812), Kefu Chai)

-   core,pybind: pybind/rados: add support open_ioctx2 API
    ([pr#17710](https://github.com/ceph/ceph/pull/17710), songweibin)

-   core,pybind: rados: support python API of \"set_osdmap_full_try\"
    ([pr#17418](https://github.com/ceph/ceph/pull/17418), songweibin)

-   core: qa: fix the potential delay of pg state change
    ([pr#17253](https://github.com/ceph/ceph/pull/17253), huangjun)

-   core: qa/standalone/osd/repro_long_log: no-mon-config for cot
    ([pr#20919](https://github.com/ceph/ceph/pull/20919), Sage Weil)

-   core: qa/standalone/scrub/osd-scrub-repair: no -y to diff
    ([issue#21618](http://tracker.ceph.com/issues/21618),
    [pr#18079](https://github.com/ceph/ceph/pull/18079), Sage Weil)

-   core: qa/suite/rados: fix balancer vs firefly tunables failures
    ([pr#18826](https://github.com/ceph/ceph/pull/18826), Sage Weil)

-   core: qa/suites/rados: fewer msgr failures
    ([pr#20918](https://github.com/ceph/ceph/pull/20918), Sage Weil)

-   core: qa/suites/rados/perf: whitelist health warnings
    ([pr#18878](https://github.com/ceph/ceph/pull/18878), Sage Weil)

-   core: qa/suites/rados/rest/mgr: provision openstack volumes
    ([pr#20573](https://github.com/ceph/ceph/pull/20573), Sage Weil)

-   core: qa/suites/rados/singleton/all/mon-seesaw: whitelist MON_DOWN
    ([pr#18246](https://github.com/ceph/ceph/pull/18246), Sage Weil)

-   core: qa/suites/rados/singleton/all/recover-preemption: handle slow
    starting osd ([pr#18078](https://github.com/ceph/ceph/pull/18078),
    Sage Weil)

-   core: qa/suites/rados/singleton/all/recovery_preemption: whitelist
    SLOW_OPS ([pr#21250](https://github.com/ceph/ceph/pull/21250), Sage
    Weil)

-   core: qa/suites/rados/singleton/diverget_priors\*: broaden whitelist
    ([pr#17379](https://github.com/ceph/ceph/pull/17379), Sage Weil)

-   core: qa/suites/rados/thrash: extend mgr beacon grace when many msgr
    failures injected
    ([issue#21147](http://tracker.ceph.com/issues/21147),
    [pr#19242](https://github.com/ceph/ceph/pull/19242), Sage Weil)

-   core: qa/suites/rados/verify/tasks/rados_api_tests: whitelist
    OBJECT_MISPLACED
    ([pr#21646](https://github.com/ceph/ceph/pull/21646), Sage Weil)

-   core: qa/workunits/rest/test.py: stop trying to test obsolte
    cluster_up/down
    ([pr#18552](https://github.com/ceph/ceph/pull/18552), Sage Weil)

-   core: rados/objclass.h: fix build define CEPH_CLS_API in all cases
    ([pr#21606](https://github.com/ceph/ceph/pull/21606), Danny Al-Gaaf)

-   core: rados: use WaitInterval()\'s return value instead of manual
    timing ([pr#20028](https://github.com/ceph/ceph/pull/20028), Mohamad
    Gebai)

-   core,rbd: common,rbd-nbd: fix up prefork behavior vs AsyncMessenger
    singletons ([issue#23143](http://tracker.ceph.com/issues/23143),
    [pr#20681](https://github.com/ceph/ceph/pull/20681), Sage Weil)

-   core,rbd: librbd,os: address coverity false positives
    ([pr#17793](https://github.com/ceph/ceph/pull/17793), Amit Kumar)

-   core,rbd: mgr,osd,kv: Fix various warnings for Clang and GCC7
    ([pr#17976](https://github.com/ceph/ceph/pull/17976), Adam C.
    Emerson)

-   core,rbd: vstart.sh: fix mstart variables
    ([pr#20826](https://github.com/ceph/ceph/pull/20826), Sage Weil)

-   core: rdma: Assign instead of compare
    ([pr#16664](https://github.com/ceph/ceph/pull/16664), amitkuma)

-   core: remove startsync
    ([issue#20604](http://tracker.ceph.com/issues/20604),
    [pr#16396](https://github.com/ceph/ceph/pull/16396), Amit Kumar)

-   core: rocksdb: sync with upstream
    ([issue#20529](http://tracker.ceph.com/issues/20529),
    [pr#17388](https://github.com/ceph/ceph/pull/17388), Kefu Chai)

-   core: rocksdb: sync with upstream
    ([pr#21320](https://github.com/ceph/ceph/pull/21320), Kefu Chai)

-   core: scrub errors not cleared on replicas can cause inconsistent pg
    state when replica takes over primary
    ([issue#23267](http://tracker.ceph.com/issues/23267),
    [pr#21101](https://github.com/ceph/ceph/pull/21101), David Zafman)

-   core: Snapset inconsistency is detected with its own error
    ([issue#22996](http://tracker.ceph.com/issues/22996),
    [pr#20450](https://github.com/ceph/ceph/pull/20450), David Zafman)

-   core: src/messages/MOSDMap: reencode OSDMap for older clients
    ([issue#21660](http://tracker.ceph.com/issues/21660),
    [pr#18134](https://github.com/ceph/ceph/pull/18134), Sage Weil)

-   core: src/osd/PG.cc: 6455: FAILED assert(0 == \"we got a bad state
    machine event\")
    ([pr#20933](https://github.com/ceph/ceph/pull/20933), David Zafman)

-   core: src/test/osd: add two pool test for manifest objects
    ([pr#20096](https://github.com/ceph/ceph/pull/20096), Myoungwon Oh)

-   core: test/cli/osdmaptool/test-map-pgs.t: remove nondetermimistic
    test ([pr#20872](https://github.com/ceph/ceph/pull/20872), Sage
    Weil)

-   core: test/objectstore_bench: Don\'t forget judging whether call
    usage ([pr#21369](https://github.com/ceph/ceph/pull/21369), Jianpeng
    Ma)

-   core,tests: ceph_test_filestore_idempotent_sequence: many fixes
    ([issue#22920](http://tracker.ceph.com/issues/22920),
    [pr#20279](https://github.com/ceph/ceph/pull/20279), Sage Weil)

-   core,tests: ceph_test_objectstore: drop expect regex
    ([pr#16968](https://github.com/ceph/ceph/pull/16968), Sage Weil)

-   core,tests: Erasure code read test and code cleanup
    ([issue#14513](http://tracker.ceph.com/issues/14513),
    [pr#17703](https://github.com/ceph/ceph/pull/17703), David Zafman)

-   core,tests: Erasure code recovery should send additional reads if
    necessary ([issue#21382](http://tracker.ceph.com/issues/21382),
    [pr#17920](https://github.com/ceph/ceph/pull/17920), David Zafman)

-   core,tests: osd,dmclock: fix dmclock test simulator change
    ([pr#20270](https://github.com/ceph/ceph/pull/20270), J. Eric
    Ivancich)

-   core,tests: os: kstore fix unittest for FiemapHole
    ([pr#17313](https://github.com/ceph/ceph/pull/17313), Ning Yao)

-   core,tests: os/memstore: memstore_page_set=false
    ([issue#20738](http://tracker.ceph.com/issues/20738),
    [pr#16995](https://github.com/ceph/ceph/pull/16995), Sage Weil)

-   core,tests: qa/ceph_manager: check pg state again before timedout
    ([issue#21294](http://tracker.ceph.com/issues/21294),
    [pr#17810](https://github.com/ceph/ceph/pull/17810), huangjun)

-   core,tests: qa/clusters/fixed-\[23\]: 4 osds per node, not 3
    ([pr#16799](https://github.com/ceph/ceph/pull/16799), Sage Weil)

-   core,tests: qa: modify rgw default pool names
    ([pr#21630](https://github.com/ceph/ceph/pull/21630), Neha Ojha)

-   core,tests: qa/objectstore/bluestore\*: less debug output
    ([issue#20910](http://tracker.ceph.com/issues/20910),
    [pr#17505](https://github.com/ceph/ceph/pull/17505), Sage Weil)

-   core,tests: qa/overrides/2-size-2-min-size: whitelist REQUEST_STUCK
    ([pr#17243](https://github.com/ceph/ceph/pull/17243), Sage Weil)

-   core,tests: qa/standalone/ceph-helpers: pass \--verbose to ceph-disk
    ([pr#19456](https://github.com/ceph/ceph/pull/19456), Sage Weil)

-   core,tests: qa/standalone/scrub/osd-scrub-repair: fix grep pattern
    ([issue#21127](http://tracker.ceph.com/issues/21127),
    [pr#17258](https://github.com/ceph/ceph/pull/17258), Sage Weil)

-   core,tests: qa/standalone/scrub/osd-scrub-snaps: adjust test for
    lack of snapdir objects
    ([pr#17927](https://github.com/ceph/ceph/pull/17927), Sage Weil)

-   core,tests: qa/suites/rados/monthrash: tolerate PG_AVAILABILITY
    during mon thrashing
    ([pr#18122](https://github.com/ceph/ceph/pull/18122), Sage Weil)

-   core,tests: qa/suites/rados/monthrash: whitelist SLOW_OPS
    ([pr#21331](https://github.com/ceph/ceph/pull/21331), Sage Weil)

-   core,tests: qa/suites/rados/objectstore: logs
    ([issue#20738](http://tracker.ceph.com/issues/20738),
    [pr#16923](https://github.com/ceph/ceph/pull/16923), Sage Weil)

-   core,tests: qa/suites/rados/perf: create pool with lower pg_num
    ([pr#17819](https://github.com/ceph/ceph/pull/17819), Neha Ojha)

-   core,tests: qa/suites/rados/rest/mgr-restful: whitelist more health
    ([pr#18457](https://github.com/ceph/ceph/pull/18457), Sage Weil)

-   core,tests: qa/suites/rados/rest: move rest_test from
    qa/suites/rest/
    ([pr#19175](https://github.com/ceph/ceph/pull/19175), Sage Weil)

-   core,tests: qa/suites/rados/thrash: fix thrashing with ec vs map
    discon ([pr#16842](https://github.com/ceph/ceph/pull/16842), Sage
    Weil)

-   core,tests: qa/suites/rados/thrash-old-clients: add hammer clients
    ([pr#21703](https://github.com/ceph/ceph/pull/21703), Sage Weil)

-   core,tests: qa/suites/rados/thrash-old-clients: add rbd tests
    ([pr#21704](https://github.com/ceph/ceph/pull/21704), Sage Weil)

-   core,tests: qa/suites/rados/thrash-old-clients: do some thrashing
    with jewel and luminous clients
    ([pr#21679](https://github.com/ceph/ceph/pull/21679), Sage Weil)

-   core,tests: qa/suites/rados/thrash-old-clients: only centos and
    16.04 ([pr#22125](https://github.com/ceph/ceph/pull/22125), Sage
    Weil)

-   core,tests: qa/suites/upgrade/jewel-x/stress-split: tolerate sloppy
    past_intervals ([pr#17226](https://github.com/ceph/ceph/pull/17226),
    Sage Weil)

-   core,tests: qa/suites/upgrade/luminous-x/stress-split: avoid enospc
    ([pr#21753](https://github.com/ceph/ceph/pull/21753), Sage Weil)

-   core,tests: qa/tasks/ceph_manager: revive osds before doing final
    rerr reset ([issue#21206](http://tracker.ceph.com/issues/21206),
    [pr#17406](https://github.com/ceph/ceph/pull/17406), Sage Weil)

-   core,tests: qa/tasks/ceph_manager: tolerate tell osd.\* error
    ([pr#19365](https://github.com/ceph/ceph/pull/19365), Sage Weil)

-   core,tests: qa/tasks/ceph.py: tolerate flush pg stats exception
    ([pr#16905](https://github.com/ceph/ceph/pull/16905), Sage Weil)

-   core,tests: qa/tasks/filestore_idempotent: shorter test
    ([pr#20509](https://github.com/ceph/ceph/pull/20509), Sage Weil)

-   core,tests: qa/tasks/thrashosds: set min_in default to 4
    ([issue#21997](http://tracker.ceph.com/issues/21997),
    [pr#18670](https://github.com/ceph/ceph/pull/18670), Sage Weil)

-   core,tests: qa/tests: run ceph-ansible task on installer.0 role/node
    ([pr#19605](https://github.com/ceph/ceph/pull/19605), Yuri
    Weinstein)

-   core,tests: qa: tolerate failure to force backfill
    ([issue#22614](http://tracker.ceph.com/issues/22614),
    [pr#19765](https://github.com/ceph/ceph/pull/19765), Sage Weil)

-   core,tests: qa/workunits/rados/test_rados_tool: fix stray `|`, race
    ([issue#22676](http://tracker.ceph.com/issues/22676),
    [pr#19946](https://github.com/ceph/ceph/pull/19946), Sage Weil)

-   core,tests: qa/workunits/rados/test.sh: ensure tee output is valid
    filename ([pr#21507](https://github.com/ceph/ceph/pull/21507), Sage
    Weil)

-   core,tests: rados: Initialization of alignment
    ([pr#17723](https://github.com/ceph/ceph/pull/17723), Amit Kumar)

-   core,tests: rados: Initializing members of librados/TestCase.h
    ([pr#16896](https://github.com/ceph/ceph/pull/16896), amitkuma)

-   core,tests: test: Checking fd for negative before closing
    ([pr#17190](https://github.com/ceph/ceph/pull/17190), amitkuma)

-   core,tests: test: Check to avoid divide by zero
    ([pr#17220](https://github.com/ceph/ceph/pull/17220), amitkuma)

-   core: tool: change default objectstore from filestore to bluestore
    ([pr#18066](https://github.com/ceph/ceph/pull/18066), Song Shun)

-   core: tool: misc cleanup of ceph-kvstore-tool
    ([issue#22092](http://tracker.ceph.com/issues/22092),
    [pr#18815](https://github.com/ceph/ceph/pull/18815), Chang Liu)

-   core,tools: Add export and remove ceph-objectstore-tool command
    option ([issue#21272](http://tracker.ceph.com/issues/21272),
    [pr#17538](https://github.com/ceph/ceph/pull/17538), David Zafman)

-   core,tools: ceph-objectstore-tool: fix import of post-split pg from
    pre-split ancestor
    ([issue#21753](http://tracker.ceph.com/issues/21753),
    [pr#18229](https://github.com/ceph/ceph/pull/18229), Sage Weil)

-   core: tools/ceph-objectstore-tool: split filestore directories
    offline to target hash level
    ([issue#21366](http://tracker.ceph.com/issues/21366),
    [pr#17666](https://github.com/ceph/ceph/pull/17666), Zhi Zhang)

-   core,tools: common, tool: update kvstore-tool to repair key/value
    database ([issue#17730](http://tracker.ceph.com/issues/17730),
    [issue#21744](http://tracker.ceph.com/issues/21744),
    [pr#16745](https://github.com/ceph/ceph/pull/16745), liuchang0812,
    Chang Liu)

-   core,tools: osd,os/bluestore: kill clang analyzer warnings
    ([pr#18015](https://github.com/ceph/ceph/pull/18015), Kefu Chai)

-   core: tools/rados: add touch command to change object modification
    time ([pr#18913](https://github.com/ceph/ceph/pull/18913), Yao
    Zongyou)

-   core,tools: scripts: add ptl-tool for scripting merges
    ([pr#17926](https://github.com/ceph/ceph/pull/17926), Patrick
    Donnelly)

-   core: vstart.sh: drop .ceph_port and use randomly selected available
    port ([pr#19268](https://github.com/ceph/ceph/pull/19268), Shinobu
    Kinjo)

-   core: vstart.sh: drop \--{mon,osd,mds,rgw,mgr}\_num options
    ([pr#18648](https://github.com/ceph/ceph/pull/18648), Kefu Chai)

-   core: vstart.sh: Remove duplicate global section
    ([pr#17543](https://github.com/ceph/ceph/pull/17543), iliul)

-   crush: cleanup update_device_class() log messages
    ([pr#21174](https://github.com/ceph/ceph/pull/21174), Gu Zhongyan)

-   crush: fix CrushCompiler won\'t compile maps with empty shadow tree
    ([pr#17058](https://github.com/ceph/ceph/pull/17058), xie xingguo)

-   crush: fix device_class_clone for unpopulated/empty weight-sets
    ([issue#23386](http://tracker.ceph.com/issues/23386),
    [pr#22169](https://github.com/ceph/ceph/pull/22169), Sage Weil)

-   crush: fix fast rule lookup when uniform
    ([pr#17510](https://github.com/ceph/ceph/pull/17510), Sage Weil)

-   crush: force rebuilding shadow hierarchy after swapping buckets
    ([pr#17083](https://github.com/ceph/ceph/pull/17083), xie xingguo)

-   crush: improve straw2 algorithm\'s readability
    ([pr#20196](https://github.com/ceph/ceph/pull/20196), Yao Zongyou)

-   crush: \"osd crush class rename\" support
    ([pr#16961](https://github.com/ceph/ceph/pull/16961), xie xingguo)

-   crush, osd: handle multiple parents properly when applying pg upmaps
    ([issue#23921](http://tracker.ceph.com/issues/23921),
    [pr#21835](https://github.com/ceph/ceph/pull/21835), xiexingguo)

-   crush: safe check for \'ceph osd crush swap-bucket\'
    ([pr#17335](https://github.com/ceph/ceph/pull/17335), Carudy)

-   crush: various CrushWrapper cleanups
    ([pr#17360](https://github.com/ceph/ceph/pull/17360), Kefu Chai)

-   crush: various weight-set fixes
    ([pr#17014](https://github.com/ceph/ceph/pull/17014), xie xingguo)

-   denc: should check element\'s type not \'size_t\'
    ([pr#19986](https://github.com/ceph/ceph/pull/19986), Kefu Chai)

-   denc: use constexpr-if to replace some SFINAE impls
    ([pr#19662](https://github.com/ceph/ceph/pull/19662), Kefu Chai)

-   doc: 12.1.3 release notes
    ([pr#16975](https://github.com/ceph/ceph/pull/16975), Abhishek
    Lekshmanan)

-   doc: 12.2.0 major release announcements
    ([pr#16915](https://github.com/ceph/ceph/pull/16915), Abhishek
    Lekshmanan)

-   doc: 12.2.1 release notes
    ([pr#18014](https://github.com/ceph/ceph/pull/18014), Abhishek
    Lekshmanan)

-   doc: 12.2.4 release notes
    ([pr#20619](https://github.com/ceph/ceph/pull/20619), Abhishek
    Lekshmanan)

-   doc: add 12.2.2 release notes
    ([pr#19264](https://github.com/ceph/ceph/pull/19264), Abhishek
    Lekshmanan)

-   doc: add allow_multimds and fs_name parameter
    ([pr#15847](https://github.com/ceph/ceph/pull/15847), Jan Fajerski)

-   doc: add ceph-kvstore-tool\'s man
    ([pr#17092](https://github.com/ceph/ceph/pull/17092), liuchang0812)

-   doc: add changelog for 12.2.1
    ([pr#18020](https://github.com/ceph/ceph/pull/18020), Abhishek
    Lekshmanan)

-   doc: add changelog for v11.2.1
    ([pr#16956](https://github.com/ceph/ceph/pull/16956), Abhishek
    Lekshmanan)

-   doc: add changelog for v12.2.2
    ([pr#19284](https://github.com/ceph/ceph/pull/19284), Abhishek
    Lekshmanan)

-   doc: Added CHAP configuration instructions for iSCSI
    ([pr#18423](https://github.com/ceph/ceph/pull/18423), Ashish Singh)

-   doc: add example of setting pool in cephfs layout
    ([pr#17372](https://github.com/ceph/ceph/pull/17372), John Spray)

-   doc: Adding changelog for 10.2.10
    ([pr#18151](https://github.com/ceph/ceph/pull/18151), Abhishek
    Lekshmanan)

-   doc: Add introduction about different way to run rbd-mirror
    ([pr#19692](https://github.com/ceph/ceph/pull/19692), Yu Shengzuo)

-   doc: add \--max-buckets to radosgw-admin(8)
    ([pr#17439](https://github.com/ceph/ceph/pull/17439), Clément
    Pellegrini)

-   doc: add missing blank line
    ([pr#18724](https://github.com/ceph/ceph/pull/18724), iliul)

-   doc: Add missing pg states from doc
    ([pr#20504](https://github.com/ceph/ceph/pull/20504), David Zafman)

-   doc: add mount.fuse.ceph to index
    ([issue#22595](http://tracker.ceph.com/issues/22595),
    [pr#19792](https://github.com/ceph/ceph/pull/19792), Jos Collin)

-   doc: Add newbie-friendly updates to Helm start doc
    ([pr#18886](https://github.com/ceph/ceph/pull/18886), Blaine
    Gardner)

-   doc: add osd_max_object_size in osd configuration
    ([pr#18115](https://github.com/ceph/ceph/pull/18115), Mohamad Gebai)

-   doc: build-doc: Upgrade ceph python libraries
    ([pr#20726](https://github.com/ceph/ceph/pull/20726), Boris Ranto)

-   doc: ceph-disk: create deprecation warnings
    ([issue#22154](http://tracker.ceph.com/issues/22154),
    [pr#18988](https://github.com/ceph/ceph/pull/18988), Alfredo Deza)

-   doc: ceph-volume: automatic VDO detection
    ([issue#23581](http://tracker.ceph.com/issues/23581),
    [pr#21451](https://github.com/ceph/ceph/pull/21451), Alfredo Deza)

-   doc: ceph-volume docs
    ([pr#17068](https://github.com/ceph/ceph/pull/17068), Alfredo Deza)

-   doc: ceph-volume document multipath support
    ([pr#20878](https://github.com/ceph/ceph/pull/20878), Alfredo Deza)

-   doc: ceph-volume doc updates
    ([pr#20758](https://github.com/ceph/ceph/pull/20758), Alfredo Deza)

-   doc: ceph-volume include physical devices associated with an LV when
    listing ([pr#21645](https://github.com/ceph/ceph/pull/21645),
    Alfredo Deza)

-   doc: ceph-volume lvm bluestore support
    ([pr#18448](https://github.com/ceph/ceph/pull/18448), Alfredo Deza)

-   doc/ceph-volume OSD use the fsid file, not the osd_fsid
    ([issue#22427](http://tracker.ceph.com/issues/22427),
    [pr#20059](https://github.com/ceph/ceph/pull/20059), Alfredo Deza)

-   doc: change boolean option default value from zero to false
    ([pr#17733](https://github.com/ceph/ceph/pull/17733), Yao Zongyou)

-   doc: change cn mirror to ustc domain
    ([pr#18081](https://github.com/ceph/ceph/pull/18081), Shengjing Zhu)

-   doc: changelog for v12.2.3
    ([pr#20503](https://github.com/ceph/ceph/pull/20503), Abhishek
    Lekshmanan)

-   doc: cleanup erasure coded pool doc on cephfs use
    ([pr#20572](https://github.com/ceph/ceph/pull/20572), Patrick
    Donnelly)

-   doc: CodingStyle: add python and javascript/typescript
    ([pr#20186](https://github.com/ceph/ceph/pull/20186), Joao Eduardo
    Luis)

-   doc: common/options: document filestore and filejournal options
    ([pr#17739](https://github.com/ceph/ceph/pull/17739), Sage Weil)

-   doc: common/options: document objecter, filer, and journal options
    ([pr#17740](https://github.com/ceph/ceph/pull/17740), Sage Weil)

-   doc: complete and update the subsystem logging level info table
    ([pr#18500](https://github.com/ceph/ceph/pull/18500), Luo Kexue)

-   doc: correcting typos in bluestore-config-ref and
    bluestore-migration
    ([pr#19154](https://github.com/ceph/ceph/pull/19154), Katie Holly)

-   doc: correct wrong bluestore config types
    ([pr#18205](https://github.com/ceph/ceph/pull/18205), Yao Zongyou)

-   doc: delete duplicate words
    ([pr#17104](https://github.com/ceph/ceph/pull/17104), iliul)

-   doc: dev description of async recovery
    ([pr#21051](https://github.com/ceph/ceph/pull/21051), Neha Ojha,
    Josh Durgin)

-   doc: doc/bluestore: add SPDK usage for bluestore
    ([pr#17654](https://github.com/ceph/ceph/pull/17654), Haomai Wang)

-   doc: doc/cephfs/experimental-features: kernel client snapshots limit
    ([pr#18579](https://github.com/ceph/ceph/pull/18579), Ilya Dryomov)

-   doc: doc/cephfs/posix: remove stale information for seekdir
    ([pr#17658](https://github.com/ceph/ceph/pull/17658), \"Yan,
    Zheng\")

-   doc: doc/conf.py: do not set html_use_smartypants explicitly
    ([pr#17127](https://github.com/ceph/ceph/pull/17127), Kefu Chai)

-   doc: doc/dev: add a brief guide to serialization
    ([pr#20131](https://github.com/ceph/ceph/pull/20131), John Spray)

-   doc: doc/dev/cxx: add C++11 ABI related doc
    ([pr#20030](https://github.com/ceph/ceph/pull/20030), Kefu Chai)

-   doc: doc/dev/iana: document our official IANA numbers
    ([pr#16910](https://github.com/ceph/ceph/pull/16910), Sage Weil)

-   doc: doc/dev/index: update rados lead
    ([pr#16911](https://github.com/ceph/ceph/pull/16911), Sage Weil)

-   doc: doc/dev/macos: add doc for building on MacOS
    ([pr#20031](https://github.com/ceph/ceph/pull/20031), Kefu Chai)

-   doc: doc/dev/msgr2.rst: a few notes on protocol goals
    ([pr#20083](https://github.com/ceph/ceph/pull/20083), Sage Weil)

-   doc: doc/dev/perf: add doc on disabling -fomit-frame-pointer
    ([pr#17358](https://github.com/ceph/ceph/pull/17358), Kefu Chai)

-   doc: doc for mount.fuse.ceph
    ([issue#21539](http://tracker.ceph.com/issues/21539),
    [pr#19172](https://github.com/ceph/ceph/pull/19172), Jos Collin)

-   doc: doc/man remove deprecation of ceph-disk man page title
    ([pr#19325](https://github.com/ceph/ceph/pull/19325), Alfredo Deza)

-   doc: doc/mgr: Add limitations section to plugin guide
    ([pr#21347](https://github.com/ceph/ceph/pull/21347), Tim Serong)

-   doc: doc/mgr: add \"local pool\" plugin to toc
    ([pr#17961](https://github.com/ceph/ceph/pull/17961), Kefu Chai)

-   doc: doc/mgr/balancer: document
    ([issue#22789](http://tracker.ceph.com/issues/22789),
    [pr#21421](https://github.com/ceph/ceph/pull/21421), Sage Weil)

-   doc: doc/mgr: document facilities methods using
    [automethod]{.title-ref} directive
    ([pr#18680](https://github.com/ceph/ceph/pull/18680), Kefu Chai)

-   doc: doc/mgr/plugins: add note about distinction between config and
    kv store ([pr#21671](https://github.com/ceph/ceph/pull/21671), Jan
    Fajerski)

-   doc: doc/mgr: remove non user-facing code from doc
    ([pr#20372](https://github.com/ceph/ceph/pull/20372), Kefu Chai)

-   doc: doc,os,osdc: drop and modify comments
    ([pr#17732](https://github.com/ceph/ceph/pull/17732), songweibin)

-   doc: doc/rados: Add explanation of straw2
    ([pr#19247](https://github.com/ceph/ceph/pull/19247), Shinobu Kinjo)

-   doc: doc/rados/operations/bluestore-migration: document bluestore
    migration process
    ([pr#16918](https://github.com/ceph/ceph/pull/16918), Sage Weil)

-   doc: doc/rados/operations/bluestore-migration: update docs a bit
    ([pr#17011](https://github.com/ceph/ceph/pull/17011), Sage Weil)

-   doc: doc raise exceptions with a base class
    ([pr#18152](https://github.com/ceph/ceph/pull/18152), Alfredo Deza)

-   doc: doc/rbd: add info for rbd group
    ([pr#17633](https://github.com/ceph/ceph/pull/17633),
    yonghengdexin735)

-   doc: doc/rbd: add missing several commands in rbd CLI man page
    ([issue#14539](http://tracker.ceph.com/issues/14539),
    [issue#16999](http://tracker.ceph.com/issues/16999),
    [pr#19659](https://github.com/ceph/ceph/pull/19659), songweibin)

-   doc: doc/rbd: correct the path of librbd python APIs
    ([pr#19690](https://github.com/ceph/ceph/pull/19690), songweibin)

-   doc: doc/rbd: fix typo s/morror/mirror
    ([pr#19997](https://github.com/ceph/ceph/pull/19997), songweibin)

-   doc: doc/rbd: iSCSI Gateway Documentation
    ([issue#20437](http://tracker.ceph.com/issues/20437),
    [pr#17376](https://github.com/ceph/ceph/pull/17376), Aron Gunn,
    Jason Dillaman)

-   doc: doc/rbd: specify additional ESX prerequisites
    ([pr#18517](https://github.com/ceph/ceph/pull/18517), Jason
    Dillaman)

-   doc: doc/rbd: tweaks for the LIO iSCSI gateway
    ([issue#21763](http://tracker.ceph.com/issues/21763),
    [pr#18250](https://github.com/ceph/ceph/pull/18250), Jason Dillaman)

-   doc: doc/rbd: tweaks to the Windows iSCSI initiator directions
    ([pr#18704](https://github.com/ceph/ceph/pull/18704), Jason
    Dillaman)

-   doc: doc/release-notes: add jewel-\>kraken notes
    ([pr#18482](https://github.com/ceph/ceph/pull/18482), Sage Weil)

-   doc: doc/release-notes: clarify purpose of require-osd-release
    ([pr#17270](https://github.com/ceph/ceph/pull/17270), Sage Weil)

-   doc: doc/release-notes: clarify that you need to keep your existing
    OSD caps ([pr#18825](https://github.com/ceph/ceph/pull/18825), Jason
    Dillaman)

-   doc: doc/release-notes: ensure RBD users can blacklist prior to
    upgrade ([issue#21353](http://tracker.ceph.com/issues/21353),
    [pr#17755](https://github.com/ceph/ceph/pull/17755), Jason Dillaman)

-   doc: doc/release-notes: fix typo \'psd\' to \'osd\'
    ([pr#18695](https://github.com/ceph/ceph/pull/18695), wangsongbo)

-   doc: doc/releases: the Kraken sleepeth, faintest sunlights flee
    ([pr#17424](https://github.com/ceph/ceph/pull/17424), Abhishek
    Lekshmanan)

-   doc: doc/releases: update release cycle docs
    ([pr#18117](https://github.com/ceph/ceph/pull/18117), Sage Weil)

-   doc: doc/rgw: add page for http frontend configuration
    ([issue#13523](http://tracker.ceph.com/issues/13523),
    [pr#20058](https://github.com/ceph/ceph/pull/20058), Casey Bodley)

-   doc: doc/scripts: py3 compatible
    ([pr#17640](https://github.com/ceph/ceph/pull/17640), Kefu Chai)

-   doc: docs: Do not use \"min size = 1\" as an example
    ([pr#17912](https://github.com/ceph/ceph/pull/17912), Alfredo Deza)

-   doc: docs fix ceph-volume missing sub-commands
    ([issue#23148](http://tracker.ceph.com/issues/23148),
    [pr#20673](https://github.com/ceph/ceph/pull/20673), Alfredo Deza)

-   doc: doc/start/os-recommendations.rst: bump krbd kernels
    ([pr#21478](https://github.com/ceph/ceph/pull/21478), Ilya Dryomov)

-   doc: docs update ceph-deploy reference to reflect ceph-volume API
    ([pr#20510](https://github.com/ceph/ceph/pull/20510), Alfredo Deza)

-   doc: document ceph-disk prepare class hierarchy
    ([pr#17019](https://github.com/ceph/ceph/pull/17019), Loic Dachary)

-   doc: document include/ipaddr.h
    ([issue#12056](http://tracker.ceph.com/issues/12056),
    [pr#17613](https://github.com/ceph/ceph/pull/17613), Nathan Cutler)

-   doc: drop duplicate line in ceph-bluestore-tool man page
    ([pr#19169](https://github.com/ceph/ceph/pull/19169), Xiaojun Liao)

-   doc: eliminate useless cat statement
    ([pr#17154](https://github.com/ceph/ceph/pull/17154), Ken Dreyer)

-   doc: examples: add new librbd example
    ([pr#18314](https://github.com/ceph/ceph/pull/18314), Mahati
    Chamarthy)

-   doc: expand developer documentation of unit tests
    ([pr#19594](https://github.com/ceph/ceph/pull/19594), Nathan Cutler)

-   doc: Fix a grammar error in rbd-snapshot.rst
    ([pr#21470](https://github.com/ceph/ceph/pull/21470), Zeqing Tyler
    Qi)

-   doc: fix CFLAGS in doc/dev/cpu-profiler.rst
    ([pr#19752](https://github.com/ceph/ceph/pull/19752), Chang Liu)

-   doc: fix desc of option \"mon cluster log file\"
    ([pr#18770](https://github.com/ceph/ceph/pull/18770), Kefu Chai)

-   doc: fix doc/radosgw/admin.rst typos
    ([pr#17397](https://github.com/ceph/ceph/pull/17397), Enming Zhang)

-   doc: Fix dynamic resharding doc formatting
    ([pr#20970](https://github.com/ceph/ceph/pull/20970), Ashish Singh)

-   doc: fix error in osd scrub load threshold
    ([pr#21678](https://github.com/ceph/ceph/pull/21678), Dirk Sarpe)

-   doc: Fixes a spelling error and a broken hyperlink
    ([pr#20442](https://github.com/ceph/ceph/pull/20442), Jordan Hus)

-   doc: Fixes rbd snapshot flatten example
    ([issue#17723](http://tracker.ceph.com/issues/17723),
    [pr#17436](https://github.com/ceph/ceph/pull/17436), Ashish Singh)

-   doc: fixes syntax in osd-config-ref
    ([issue#21733](http://tracker.ceph.com/issues/21733),
    [pr#18188](https://github.com/ceph/ceph/pull/18188), Joshua Schmid)

-   doc: Fixes the name of the CephFS snapshot directory
    ([pr#18710](https://github.com/ceph/ceph/pull/18710), Jordan
    Rodgers)

-   doc: fix hyper link to radosgw/config-ref
    ([pr#17986](https://github.com/ceph/ceph/pull/17986), Kefu Chai)

-   doc: fix librbdpy example
    ([pr#20019](https://github.com/ceph/ceph/pull/20019), Yuan Zhou)

-   doc: fix order of options in osd new
    ([issue#21023](http://tracker.ceph.com/issues/21023),
    [pr#17326](https://github.com/ceph/ceph/pull/17326), Neha Ojha)

-   doc: fix sphinx build warnings and errors
    ([pr#17025](https://github.com/ceph/ceph/pull/17025), Alfredo Deza)

-   doc: fix the desc of \"osd max pg per osd hard ratio\"
    ([pr#18373](https://github.com/ceph/ceph/pull/18373), Kefu Chai)

-   doc: Fix typo and URL
    ([pr#18040](https://github.com/ceph/ceph/pull/18040), Jos Collin)

-   doc: fix typo e.g,. =\> e.g
    ([pr#18607](https://github.com/ceph/ceph/pull/18607), Yao Zongyou)

-   doc: fix typo in bluestore-migration.rst
    ([pr#18389](https://github.com/ceph/ceph/pull/18389), Yao Zongyou)

-   doc: Fix typo in mount.fuse.ceph
    ([pr#19215](https://github.com/ceph/ceph/pull/19215), Jos Collin)

-   doc: fix typo in php.rst
    ([pr#17762](https://github.com/ceph/ceph/pull/17762), Yao Zongyou)

-   doc: fix typo in radosgw/dynamicresharding.rst
    ([pr#18651](https://github.com/ceph/ceph/pull/18651), Alexander
    Ermolaev)

-   doc: fix typo on specify db block device
    ([pr#17590](https://github.com/ceph/ceph/pull/17590), Xiaoxi Chen)

-   doc: Fix typo s/applicatoin/application/
    ([pr#20720](https://github.com/ceph/ceph/pull/20720), Francois
    Deppierraz)

-   doc: Fix typos in placement-groups.rst
    ([pr#17973](https://github.com/ceph/ceph/pull/17973), Matt Boyle)

-   doc: Fix typos in release notes
    ([pr#18950](https://github.com/ceph/ceph/pull/18950), Stefan Knorr)

-   doc: .githubmap: Add cbodley
    ([pr#18946](https://github.com/ceph/ceph/pull/18946), Jos Collin)

-   doc: githubmap: add map for GitHub contributor lookup
    ([pr#17457](https://github.com/ceph/ceph/pull/17457), Patrick
    Donnelly)

-   doc: .githubmap, .mailmap, .organizationmap, .peoplemap: update Igor
    ([pr#19314](https://github.com/ceph/ceph/pull/19314), Igor Fedotov)

-   doc: globally change CRUSH ruleset to CRUSH rule
    ([issue#20559](http://tracker.ceph.com/issues/20559),
    [pr#19435](https://github.com/ceph/ceph/pull/19435), Nathan Cutler)

-   doc: Improved dashboard documentation
    ([pr#21443](https://github.com/ceph/ceph/pull/21443), Lenz Grimmer)

-   doc: Improved hitset parameters description
    ([pr#19691](https://github.com/ceph/ceph/pull/19691), Alexey
    Stupnikov)

-   doc: improve links in doc/releases.rst
    ([pr#18155](https://github.com/ceph/ceph/pull/18155), Nathan Cutler)

-   doc: Improve mgr/restful module documentation
    ([pr#20717](https://github.com/ceph/ceph/pull/20717), Boris Ranto)

-   doc: Improve the ceph fs set max_mds command
    ([issue#21007](http://tracker.ceph.com/issues/21007),
    [pr#17044](https://github.com/ceph/ceph/pull/17044), Bara Ancincova)

-   doc: include ceph-disk and ceph-disk-volume man pages in index
    ([pr#17168](https://github.com/ceph/ceph/pull/17168), Alfredo Deza)

-   doc: init flags to 0 in rados example
    ([pr#20671](https://github.com/ceph/ceph/pull/20671), Patrick
    Donnelly)

-   doc: Kube + Helm installation
    ([pr#18520](https://github.com/ceph/ceph/pull/18520), Alexandre
    Marangone)

-   doc: legal: remove doc license ambiguity
    ([issue#23336](http://tracker.ceph.com/issues/23336),
    [pr#20876](https://github.com/ceph/ceph/pull/20876), Nathan Cutler)

-   doc: lock_timeout is a per mapping option
    ([pr#21563](https://github.com/ceph/ceph/pull/21563), Ilya Dryomov)

-   doc: log-and-debug: fix default value of \"log max recent\"
    ([pr#20316](https://github.com/ceph/ceph/pull/20316), Nathan Cutler)

-   doc: mailmap: Add Sibei, XueYu Affiliation
    ([pr#18395](https://github.com/ceph/ceph/pull/18395), Sibei Gao)

-   doc: mailmap: Fixed maintenance guide URL
    ([pr#18076](https://github.com/ceph/ceph/pull/18076), Jos Collin)

-   doc: mailmap, organizationmap: add Dongsheng, Liuzhong, Pengcheng,
    Yang Affiliation
    ([pr#17548](https://github.com/ceph/ceph/pull/17548), Dongsheng
    Yang)

-   doc: .mailmap, .organizationmap: add Fufei, Mingqiao and Ying
    Affiliation ([pr#17540](https://github.com/ceph/ceph/pull/17540),
    Ying He)

-   doc: .mailmap, .organizationmap: Add Liu Lei\'s mailmap and
    affiliation ([pr#17105](https://github.com/ceph/ceph/pull/17105),
    iliul)

-   doc: .mailmap, .organizationmap: update JingChen, ZongyouYao,
    ShanchunLv\'s...
    ([pr#18960](https://github.com/ceph/ceph/pull/18960), Chang Liu)

-   doc: mailmap: update affiliation for Mykola Golub
    ([pr#18069](https://github.com/ceph/ceph/pull/18069), Mykola Golub)

-   doc: mailmap: update affiliation for Mykola Golub
    ([pr#19667](https://github.com/ceph/ceph/pull/19667), Mykola Golub)

-   doc: mailmap: Update umcloud affiliation
    ([pr#17441](https://github.com/ceph/ceph/pull/17441), Yixing Yan)

-   doc: make the commands in README.md properly aligned
    ([pr#18639](https://github.com/ceph/ceph/pull/18639), Yao Zongyou)

-   doc/man: add \"ls\" to \"ceph osd\" command\'s subcommands list
    ([pr#19382](https://github.com/ceph/ceph/pull/19382), Rishabh Dave)

-   doc: \"mds blacklist interval\" vs manually blacklisting
    ([pr#18195](https://github.com/ceph/ceph/pull/18195), Ken Dreyer)

-   doc: mgr/dashboard.rst: mention ceph.conf and ceph mgr services
    ([pr#20961](https://github.com/ceph/ceph/pull/20961), Nathan Cutler)

-   doc/mgr/plugins: mgr accessor during init causes exception
    ([pr#16973](https://github.com/ceph/ceph/pull/16973), Jan Fajerski)

-   doc: mimic: doc: Updated dashboard documentation (features, SSL
    config) ([pr#22079](https://github.com/ceph/ceph/pull/22079), Lenz
    Grimmer)

-   doc: misc fix spell errors in osd/OSD and doc
    ([pr#17107](https://github.com/ceph/ceph/pull/17107), songweibin)

-   doc: misc: fix various spelling errors
    ([pr#20831](https://github.com/ceph/ceph/pull/20831), Shengjing Zhu)

-   doc: Misc iSCSI doc updates
    ([pr#19931](https://github.com/ceph/ceph/pull/19931), Mike Christie)

-   doc: move glance_api_version option to the right place
    ([pr#17337](https://github.com/ceph/ceph/pull/17337), Luo Kexue)

-   doc: options.cc: document rgw config options
    ([pr#18007](https://github.com/ceph/ceph/pull/18007), Yehuda Sadeh)

-   doc: organizationmap: Add Adam Wolfe Gordon\'s affiliation
    ([pr#18295](https://github.com/ceph/ceph/pull/18295), Adam Wolfe
    Gordon)

-   doc: organizationmap: Add Ashish Singh affiliation
    ([pr#17109](https://github.com/ceph/ceph/pull/17109), Ashish Singh)

-   doc: .organizationmap: add Xin Yuan and Yichao Li\'s affiliation
    ([pr#21170](https://github.com/ceph/ceph/pull/21170), Li Wang)

-   doc: PendingReleaseNotes: Added note about Dashboard v2, fixed typo
    ([pr#21597](https://github.com/ceph/ceph/pull/21597), Lenz Grimmer)

-   doc: PendingReleaseNotes:Announce FreeBSD availability
    ([pr#16782](https://github.com/ceph/ceph/pull/16782), Willem Jan
    Withagen)

-   doc: PendingReleaseNotes: mention some monitor changes
    ([pr#21474](https://github.com/ceph/ceph/pull/21474), Joao Eduardo
    Luis)

-   doc: PendingReleaseNotes: note about upmap mapping change in
    luminous release notes
    ([pr#17813](https://github.com/ceph/ceph/pull/17813), Sage Weil)

-   doc: qa,doc: drop support of ubuntu trusty
    ([pr#19307](https://github.com/ceph/ceph/pull/19307), Kefu Chai)

-   doc/rados/operations/bluestore-migration: typos and whitespace
    ([pr#16991](https://github.com/ceph/ceph/pull/16991), Sage Weil)

-   doc/rados/operations/bluestore-migration: typos
    ([pr#17581](https://github.com/ceph/ceph/pull/17581), Sage Weil)

-   doc: README: Improve vstart.sh usage
    ([pr#17644](https://github.com/ceph/ceph/pull/17644), Fabian Vogt)

-   doc: README.md: bump up cmake to 2.8.12
    ([pr#18348](https://github.com/ceph/ceph/pull/18348), Yan Jun)

-   doc: redundant \"cephfs\" when set the \"allow_multimds\"
    ([pr#20045](https://github.com/ceph/ceph/pull/20045), Shangzhong
    Zhu)

-   doc: release notes: fix grammar/style nits
    ([pr#18876](https://github.com/ceph/ceph/pull/18876), Nathan Cutler)

-   doc: release notes for 12.2.3
    ([pr#20500](https://github.com/ceph/ceph/pull/20500), Abhishek
    Lekshmanan)

-   doc: release notes for v12.1.4 Luminous
    ([pr#17037](https://github.com/ceph/ceph/pull/17037), Abhishek
    Lekshmanan)

-   doc/release-notes: remove mention of crush weight optimization
    ([pr#16974](https://github.com/ceph/ceph/pull/16974), Sage Weil)

-   doc: release-notes.rst: add Kraken v11.2.1 and update releases.rst
    ([pr#16879](https://github.com/ceph/ceph/pull/16879), Nathan Cutler)

-   doc: release notes update for 10.2.10
    ([pr#18148](https://github.com/ceph/ceph/pull/18148), Abhishek
    Lekshmanan)

-   doc/releases: drop LTS/stable line from second chart
    ([pr#18153](https://github.com/ceph/ceph/pull/18153), Sage Weil)

-   doc: Remove additional arguments when replacing OSD
    ([pr#18345](https://github.com/ceph/ceph/pull/18345), Wido den
    Hollander)

-   doc: remove duplicated \--max-buckets option desc
    ([pr#19737](https://github.com/ceph/ceph/pull/19737), Kefu Chai)

-   doc: remove references to unversioned repository addresses
    ([pr#21357](https://github.com/ceph/ceph/pull/21357), Greg Farnum)

-   doc: remove unused config: \"osd op threads\"
    ([pr#21319](https://github.com/ceph/ceph/pull/21319), Jianpeng Ma)

-   doc: rename changelog with a .txt extension
    ([pr#18156](https://github.com/ceph/ceph/pull/18156), Abhishek
    Lekshmanan)

-   doc: reorganize releases
    ([pr#20784](https://github.com/ceph/ceph/pull/20784), Abhishek
    Lekshmanan)

-   doc: replace injectargs usage with \"config set\"
    ([pr#18789](https://github.com/ceph/ceph/pull/18789), John Spray)

-   doc: replace region with zonegroup in configure bucket sharding
    section ([issue#21610](http://tracker.ceph.com/issues/21610),
    [pr#18063](https://github.com/ceph/ceph/pull/18063), Orit Wasserman)

-   doc: restructure bluestore migration insructions
    ([pr#17603](https://github.com/ceph/ceph/pull/17603), Sage Weil)

-   doc: Revise the Example of Bucket Policy
    ([pr#17362](https://github.com/ceph/ceph/pull/17362), zhangwen)

-   doc: rgw: add a note for resharding in 12.2.1 docs
    ([pr#17675](https://github.com/ceph/ceph/pull/17675), Abhishek
    Lekshmanan)

-   doc: rgw add some basic documentation for sync plugins & ES
    ([pr#15849](https://github.com/ceph/ceph/pull/15849), Abhishek
    Lekshmanan)

-   doc: rgw adminops binding libraries
    ([pr#19164](https://github.com/ceph/ceph/pull/19164), hrchu)

-   doc: rgw mention about tagging & bucket policies in s3api
    ([pr#16907](https://github.com/ceph/ceph/pull/16907), Abhishek
    Lekshmanan)

-   doc: rgw: mention the civetweb support for binding to multiple ports
    ([issue#20942](http://tracker.ceph.com/issues/20942),
    [pr#17141](https://github.com/ceph/ceph/pull/17141), Abhishek
    Lekshmanan)

-   doc: rm stray \")\" character from mds config ref
    ([pr#18228](https://github.com/ceph/ceph/pull/18228), Ken Dreyer)

-   docs: ceph-volume CLI updates
    ([pr#17425](https://github.com/ceph/ceph/pull/17425), Alfredo Deza)

-   doc: s/deamon/daemon/
    ([pr#20931](https://github.com/ceph/ceph/pull/20931), ashitakasam)

-   doc: some improvements to ceph-conf.rst
    ([pr#21268](https://github.com/ceph/ceph/pull/21268), Nathan Cutler)

-   doc: Specify mount details in ceph-fuse
    ([pr#20071](https://github.com/ceph/ceph/pull/20071), Jos Collin)

-   doc: SubmittingPatches: clarify PR title section
    ([pr#17143](https://github.com/ceph/ceph/pull/17143), Nathan Cutler)

-   doc/templates update toctree call to include hidden entries
    ([pr#17076](https://github.com/ceph/ceph/pull/17076), Alfredo Deza)

-   doc: the client inputs the pool name instead of pool ID
    ([pr#17672](https://github.com/ceph/ceph/pull/17672), Frank Yu)

-   doc: typo fix ([pr#21077](https://github.com/ceph/ceph/pull/21077),
    Ashita Dashottar)

-   doc: update Blacklisting and OSD epoch barrier
    ([issue#22542](http://tracker.ceph.com/issues/22542),
    [pr#19701](https://github.com/ceph/ceph/pull/19701), Jos Collin)

-   doc: update ceph-disk with a state-transition diagram
    ([pr#17639](https://github.com/ceph/ceph/pull/17639), Kefu Chai)

-   doc: update ceph iscsi kernel and package info
    ([pr#20020](https://github.com/ceph/ceph/pull/20020), Mike Christie)

-   doc: Update commands and options in radosgw-admin
    ([pr#18267](https://github.com/ceph/ceph/pull/18267), Jos Collin)

-   doc: update Component Technical Leads and maintainers to canonical
    location ([pr#18376](https://github.com/ceph/ceph/pull/18376),
    Patrick McGarry)

-   doc: Update config file search paths to reflect reality
    ([pr#19882](https://github.com/ceph/ceph/pull/19882), Adam Wolfe
    Gordon)

-   doc: updated add primary storage documentation for latest CloudStack
    release (4.11) ([pr#21050](https://github.com/ceph/ceph/pull/21050),
    James McClune, John Wilkins)

-   doc: Update dashboard feature list (added RGW management)
    ([pr#21781](https://github.com/ceph/ceph/pull/21781), Lenz Grimmer)

-   doc: updated dashboard feature list (added new RGW details, Pools)
    ([pr#21562](https://github.com/ceph/ceph/pull/21562), Lenz Grimmer)

-   doc: Updated dashboard feature list
    ([pr#21693](https://github.com/ceph/ceph/pull/21693), Lenz Grimmer)

-   doc: Updated dashboard v2 feature list
    ([pr#20755](https://github.com/ceph/ceph/pull/20755), Lenz Grimmer)

-   doc: Updated documentation for Zabbix Mgr module
    ([pr#18356](https://github.com/ceph/ceph/pull/18356), Wido den
    Hollander)

-   doc: update default value of option mon_sync_timeout
    ([pr#17802](https://github.com/ceph/ceph/pull/17802), Yao Guotao)

-   doc: update default value of parameter mon_subscribe_interval
    ([pr#17669](https://github.com/ceph/ceph/pull/17669), yaoguotao)

-   doc: Update docs to remove gitbuilder and add shaman references
    ([pr#17022](https://github.com/ceph/ceph/pull/17022), Alfredo Deza)

-   doc: updated the dashboard feature list
    ([pr#21531](https://github.com/ceph/ceph/pull/21531), Lenz Grimmer)

-   doc: Updated the get-packages.rst to luminous
    ([pr#20815](https://github.com/ceph/ceph/pull/20815), Kai Wagner)

-   doc: update firewall doc to mention ceph-mgr
    ([pr#17974](https://github.com/ceph/ceph/pull/17974), John Spray)

-   doc: update iSCSI upstream kernel to 4.16
    ([pr#20695](https://github.com/ceph/ceph/pull/20695), Mike Christie)

-   doc: update link to placing-different-pools
    ([pr#17833](https://github.com/ceph/ceph/pull/17833), Mohamad Gebai)

-   doc: update Li Wang Affiliation
    ([pr#18060](https://github.com/ceph/ceph/pull/18060), Li Wang)

-   doc: update man page to explain ceph-volume support bluestore
    ([issue#22663](http://tracker.ceph.com/issues/22663),
    [pr#19960](https://github.com/ceph/ceph/pull/19960), lijing)

-   doc: Update manual deployment
    ([issue#20309](http://tracker.ceph.com/issues/20309),
    [pr#15811](https://github.com/ceph/ceph/pull/15811), Jens Rosenboom)

-   doc: update mgr/dashboard doc about standbys
    ([pr#19879](https://github.com/ceph/ceph/pull/19879), John Spray)

-   doc: Update mgr doc on how to enable Zabbix module
    ([pr#16861](https://github.com/ceph/ceph/pull/16861), Wido den
    Hollander)

-   doc: update mgr related auth settings
    ([pr#20126](https://github.com/ceph/ceph/pull/20126), Kefu Chai)

-   doc: Update monitoring.rst
    ([pr#20630](https://github.com/ceph/ceph/pull/20630), Jos Collin)

-   doc: update rbd-mirroring documentation
    ([issue#20701](http://tracker.ceph.com/issues/20701),
    [pr#16908](https://github.com/ceph/ceph/pull/16908), Jason Dillaman)

-   doc: update references to use ceph-volume
    ([pr#19241](https://github.com/ceph/ceph/pull/19241), Alfredo Deza)

-   doc: update releases to the current state
    ([pr#17364](https://github.com/ceph/ceph/pull/17364), Abhishek
    Lekshmanan)

-   doc: Updates to bluestore migration doc
    ([pr#17602](https://github.com/ceph/ceph/pull/17602), David
    Galloway)

-   doc: v12.2.5 luminous release notes
    ([pr#21621](https://github.com/ceph/ceph/pull/21621), Abhishek
    Lekshmanan)

-   doc: various cleanups
    ([pr#18480](https://github.com/ceph/ceph/pull/18480), Kefu Chai)

-   examples: fix link order in librados example Makefile
    ([pr#17842](https://github.com/ceph/ceph/pull/17842), Mahati
    Chamarthy)

-   Fix ceph-mgr restarts
    ([pr#22051](https://github.com/ceph/ceph/pull/22051), Boris Ranto)

-   follow-up fixups for atomic_t spinlocks
    ([pr#17611](https://github.com/ceph/ceph/pull/17611), Jesse
    Williamson)

-   githubmap: Add ktdreyer
    ([pr#19209](https://github.com/ceph/ceph/pull/19209), Jos Collin)

-   include/buffer.h: fix typo in comment
    ([pr#17489](https://github.com/ceph/ceph/pull/17489), mychoxin)

-   include/ceph_features: fix OS_PERF_STAT_NS\'s incarnation
    ([pr#21467](https://github.com/ceph/ceph/pull/21467), Kefu Chai)

-   install-deps.sh: fix an error condition expression
    ([pr#20819](https://github.com/ceph/ceph/pull/20819), Yao Guotao)

-   java/native: fix milliseconds to mtime/atime conversion
    ([pr#17460](https://github.com/ceph/ceph/pull/17460), dengquan)

-   java/native: s/jni: lstat/jni: stat in native_ceph_stat
    ([pr#20142](https://github.com/ceph/ceph/pull/20142), Shangzhong
    Zhu)

-   KStore: statfs needs extra includes on FreeBSD
    ([pr#21429](https://github.com/ceph/ceph/pull/21429), Willem Jan
    Withagen)

-   kv/leveldb: fix deadlock when close db
    ([pr#16643](https://github.com/ceph/ceph/pull/16643), Zengran)

-   kv: unify {create_and\_,}open() methods
    ([pr#18177](https://github.com/ceph/ceph/pull/18177), Kefu Chai)

-   librados: add async interfaces for use with Networking TS
    ([pr#19054](https://github.com/ceph/ceph/pull/19054), Casey Bodley)

-   librados: block MgrClient::start_command until mgrmap
    ([pr#21832](https://github.com/ceph/ceph/pull/21832), John Spray,
    Kefu Chai)

-   librados: extend C API for so it accepts keys with NUL chars
    ([pr#20314](https://github.com/ceph/ceph/pull/20314), Piotr Dałek)

-   librados: Fix a potential risk of buffer::list::claim_prepend(list&
    b... ([issue#21338](http://tracker.ceph.com/issues/21338),
    [pr#17661](https://github.com/ceph/ceph/pull/17661), Guan yunfei)

-   librados: fix potential race condition if notify immediately fails
    ([issue#23966](http://tracker.ceph.com/issues/23966),
    [pr#21859](https://github.com/ceph/ceph/pull/21859), Jason Dillaman)

-   librados: getter for min compatible client versions
    ([pr#20080](https://github.com/ceph/ceph/pull/20080), Jason
    Dillaman)

-   librados: invalid free() in rados_getxattrs_next()
    ([issue#22042](http://tracker.ceph.com/issues/22042),
    [pr#20260](https://github.com/ceph/ceph/pull/20260), Gu Zhongyan)

-   librados: make OPERATION_FULL_FORCE the default for rados_remove()
    ([issue#22413](http://tracker.ceph.com/issues/22413),
    [pr#20534](https://github.com/ceph/ceph/pull/20534), Kefu Chai)

-   librbd: abstract hard-coded journal and cache hooks on IO path
    ([pr#20682](https://github.com/ceph/ceph/pull/20682), Jason
    Dillaman)

-   librbd: Add a function to list image watchers
    ([pr#19188](https://github.com/ceph/ceph/pull/19188), Adam Wolfe
    Gordon)

-   librbd: add API function to get image name
    ([pr#20935](https://github.com/ceph/ceph/pull/20935), Mykola Golub)

-   librbd: added preprocessor macro for detecting compare-and-write
    support ([issue#22036](http://tracker.ceph.com/issues/22036),
    [pr#18708](https://github.com/ceph/ceph/pull/18708), Jason Dillaman)

-   librbd: add eventtrace support
    ([pr#19251](https://github.com/ceph/ceph/pull/19251), Mahati
    Chamarthy)

-   librbd: add preliminary support for new operation feature bit
    ([pr#19903](https://github.com/ceph/ceph/pull/19903), Jason
    Dillaman)

-   librbd: address coverity false positives
    ([pr#17696](https://github.com/ceph/ceph/pull/17696), Amit Kumar)

-   librbd: address coverity false positives
    ([pr#17721](https://github.com/ceph/ceph/pull/17721), Amit Kumar)

-   librbd: auto-remove trash snapshots when image is deleted
    ([issue#22873](http://tracker.ceph.com/issues/22873),
    [pr#20376](https://github.com/ceph/ceph/pull/20376), Jason Dillaman)

-   librbd: by default use new format for deep copy destination
    ([pr#20222](https://github.com/ceph/ceph/pull/20222), Mykola Golub)

-   librbd: cache last index position to accelerate snap create/rm
    ([issue#22716](http://tracker.ceph.com/issues/22716),
    [pr#19974](https://github.com/ceph/ceph/pull/19974), Song Shun)

-   librbd: cannot clone all image-metas if we have more than 64
    key/value pairs
    ([pr#18327](https://github.com/ceph/ceph/pull/18327), PCzhangPC)

-   librbd: cannot copy all image-metas if we have more than 64
    key/value pairs
    ([pr#18328](https://github.com/ceph/ceph/pull/18328), PCzhangPC)

-   librbd: clean up ManagedLock log prefix
    ([pr#20159](https://github.com/ceph/ceph/pull/20159), shun-s)

-   librbd: compare and write against a clone can result in failure
    ([issue#20789](http://tracker.ceph.com/issues/20789),
    [pr#18887](https://github.com/ceph/ceph/pull/18887), Jason Dillaman)

-   librbd: deep_copy: don\'t create snapshots above snap_id_end
    ([pr#19383](https://github.com/ceph/ceph/pull/19383), Mykola Golub)

-   librbd: default localize parent reads to false
    ([issue#20941](http://tracker.ceph.com/issues/20941),
    [pr#16882](https://github.com/ceph/ceph/pull/16882), Jason Dillaman)

-   librbd: default to sparse-reads for any IO operation over 64K
    ([issue#21849](http://tracker.ceph.com/issues/21849),
    [pr#18405](https://github.com/ceph/ceph/pull/18405), Jason Dillaman)

-   librbd: disable ENOENT tracking within the object cacher
    ([issue#23597](http://tracker.ceph.com/issues/23597),
    [pr#21308](https://github.com/ceph/ceph/pull/21308), Jason Dillaman)

-   librbd: disallow creation of v1 image format
    ([pr#20460](https://github.com/ceph/ceph/pull/20460), Julien COLLET,
    Julien Collet)

-   librbd: don\'t read metadata twice on image open
    ([pr#18542](https://github.com/ceph/ceph/pull/18542), Mykola Golub)

-   librbd: drop redundant check for null ImageCtx
    ([pr#18265](https://github.com/ceph/ceph/pull/18265), Jianpeng Ma)

-   librbd: filter out potential race with image rename
    ([issue#18435](http://tracker.ceph.com/issues/18435),
    [pr#19618](https://github.com/ceph/ceph/pull/19618), Jason Dillaman)

-   librbd: fix coverity warning for uninitialized member
    ([pr#18129](https://github.com/ceph/ceph/pull/18129), Li Wang)

-   librbd: fix deep copy a child-image
    ([pr#20099](https://github.com/ceph/ceph/pull/20099), songweibin)

-   librbd: fix don\'t send get_stripe_unit_count if striping is not
    enabled ([issue#21360](http://tracker.ceph.com/issues/21360),
    [pr#17660](https://github.com/ceph/ceph/pull/17660), Yanhu Cao)

-   librbd: fix issues discovered in clone v2 during upgrade tests
    ([issue#22979](http://tracker.ceph.com/issues/22979),
    [pr#20406](https://github.com/ceph/ceph/pull/20406), Jason Dillaman)

-   librbd: fix missing return in NotifyMessage::get_notify_op
    ([pr#20656](https://github.com/ceph/ceph/pull/20656), Yao Zongyou)

-   librbd: fix rbd close race with rewatch
    ([pr#21141](https://github.com/ceph/ceph/pull/21141), Song Shun)

-   librbd: fix refuse to release lock when cookie is the same at
    rewatch ([pr#20868](https://github.com/ceph/ceph/pull/20868), Song
    Shun)

-   librbd: fix structure size check in rbd_mirror_image_get_info/status
    ([pr#20478](https://github.com/ceph/ceph/pull/20478), Mykola Golub)

-   librbd: force removal of a snapshot cannot ignore dependent children
    ([issue#22791](http://tracker.ceph.com/issues/22791),
    [pr#20105](https://github.com/ceph/ceph/pull/20105), Jason Dillaman)

-   librbd: generalized deep copy function
    ([pr#16238](https://github.com/ceph/ceph/pull/16238), Mykola Golub)

-   librbd: group and snapshot cleanup
    ([pr#19990](https://github.com/ceph/ceph/pull/19990), Jason
    Dillaman)

-   librbd: group snapshots
    ([pr#11544](https://github.com/ceph/ceph/pull/11544), Victor
    Denisov, Jason Dillaman)

-   librbd: hold cache_lock while clearing cache nonexistence flags
    ([issue#21558](http://tracker.ceph.com/issues/21558),
    [pr#17992](https://github.com/ceph/ceph/pull/17992), Jason Dillaman)

-   librbd: image-meta config overrides should be dynamically refreshed
    ([issue#21529](http://tracker.ceph.com/issues/21529),
    [pr#18042](https://github.com/ceph/ceph/pull/18042), Dongsheng Yang,
    Jason Dillaman)

-   librbd: initial hooks for clone v2 support
    ([pr#20176](https://github.com/ceph/ceph/pull/20176), Jason
    Dillaman)

-   librbd: initialization of state member variables
    ([pr#16866](https://github.com/ceph/ceph/pull/16866), amitkuma)

-   librbd: Initializing members image,operation,journal
    ([pr#16934](https://github.com/ceph/ceph/pull/16934), amitkuma)

-   librbd: Initializing member variables
    ([pr#16867](https://github.com/ceph/ceph/pull/16867), amitkuma)

-   librbd: journal should ignore -EILSEQ errors from compare-and-write
    ([issue#21628](http://tracker.ceph.com/issues/21628),
    [pr#18099](https://github.com/ceph/ceph/pull/18099), Jason Dillaman)

-   librbd,librados: do not include stdbool.h in C++ headers
    ([pr#19945](https://github.com/ceph/ceph/pull/19945), Kefu Chai)

-   librbd: list_children should not attempt to refresh image
    ([issue#21670](http://tracker.ceph.com/issues/21670),
    [pr#18114](https://github.com/ceph/ceph/pull/18114), Jason Dillaman)

-   librbd: minor cleanup of the IO pathway
    ([pr#20560](https://github.com/ceph/ceph/pull/20560), Jason
    Dillaman)

-   librbd: minor code cleanup
    ([pr#21165](https://github.com/ceph/ceph/pull/21165), songweibin)

-   librbd: missing \'return\' in
    deep_copy::ObjectCopyRequest::send_read_object
    ([pr#21493](https://github.com/ceph/ceph/pull/21493), Mykola Golub)

-   librbd: new tag should use on-disk committed position
    ([issue#22945](http://tracker.ceph.com/issues/22945),
    [pr#20423](https://github.com/ceph/ceph/pull/20423), Jason Dillaman)

-   librbd: object map batch update might cause OSD suicide timeout
    ([issue#21797](http://tracker.ceph.com/issues/21797),
    [pr#18315](https://github.com/ceph/ceph/pull/18315), Jason Dillaman)

-   librbd: possible deadlock with synchronous maintenance operations
    ([issue#22120](http://tracker.ceph.com/issues/22120),
    [pr#18909](https://github.com/ceph/ceph/pull/18909), Jason Dillaman)

-   librbd: potential crash if object map check encounters error
    ([issue#22819](http://tracker.ceph.com/issues/22819),
    [pr#20214](https://github.com/ceph/ceph/pull/20214), Jason Dillaman)

-   librbd: potential race between discard and writeback
    ([pr#21248](https://github.com/ceph/ceph/pull/21248), Jason
    Dillaman)

-   librbd: potential race in RewatchRequest when resetting watch_handle
    ([pr#20420](https://github.com/ceph/ceph/pull/20420), Mykola Golub)

-   librbd: prefer templates to macros
    ([pr#19912](https://github.com/ceph/ceph/pull/19912), Adam C.
    Emerson)

-   librbd: prevent overflow of discard API result code
    ([issue#21966](http://tracker.ceph.com/issues/21966),
    [pr#18923](https://github.com/ceph/ceph/pull/18923), Jason Dillaman)

-   librbd: prevent watcher from unregistering with in-flight actions
    ([issue#23955](http://tracker.ceph.com/issues/23955),
    [pr#21763](https://github.com/ceph/ceph/pull/21763), Jason Dillaman)

-   librbd: refresh image after applying new metadata
    ([issue#21711](http://tracker.ceph.com/issues/21711),
    [pr#18158](https://github.com/ceph/ceph/pull/18158), Jason Dillaman)

-   librbd: release lock executing deep copy progress callback
    ([issue#23929](http://tracker.ceph.com/issues/23929),
    [pr#21727](https://github.com/ceph/ceph/pull/21727), Mykola Golub)

-   librbd: remove unused member in FlattenRequest
    ([pr#19416](https://github.com/ceph/ceph/pull/19416), Mykola Golub)

-   librbd: remove unused variables from ReadResult refactor
    ([pr#18277](https://github.com/ceph/ceph/pull/18277), Jason
    Dillaman)

-   librbd: rename of non-existent image results in seg fault
    ([issue#21248](http://tracker.ceph.com/issues/21248),
    [pr#17502](https://github.com/ceph/ceph/pull/17502), Jason Dillaman)

-   librbd: set deleted parent pointer to null
    ([issue#22158](http://tracker.ceph.com/issues/22158),
    [pr#19003](https://github.com/ceph/ceph/pull/19003), Jason Dillaman)

-   librbd: should not set self as remote peer
    ([pr#17300](https://github.com/ceph/ceph/pull/17300), songweibin)

-   librbd: small cleanup for recently merged code
    ([pr#20578](https://github.com/ceph/ceph/pull/20578), Mykola Golub)

-   librbd: snapshots should be created/removed against data pool
    ([issue#21567](http://tracker.ceph.com/issues/21567),
    [pr#18043](https://github.com/ceph/ceph/pull/18043), Jason Dillaman)

-   librbd: speed up object map disk usage and resize
    ([pr#20218](https://github.com/ceph/ceph/pull/20218), shun-s)

-   librbd: speed up sparse copy when object map is available
    ([pr#18967](https://github.com/ceph/ceph/pull/18967), Song Shun)

-   librbd: update mirror::EnableRequest diagram according to code
    ([pr#19130](https://github.com/ceph/ceph/pull/19130), Mykola Golub)

-   librbd: use steady clock to measure elapsed time in AioCompletion
    ([pr#20007](https://github.com/ceph/ceph/pull/20007), Mohamad Gebai)

-   librbd: validate if dst group snap name is the same with src
    ([pr#20395](https://github.com/ceph/ceph/pull/20395), songweibin)

-   log: Fix AddressSanitizer: new-delete-type-mismatch
    ([issue#23324](http://tracker.ceph.com/issues/23324),
    [pr#20930](https://github.com/ceph/ceph/pull/20930), Brad Hubbard)

-   log: fix build on osx
    ([pr#18213](https://github.com/ceph/ceph/pull/18213), Kefu Chai)

-   log: silence warning from -Wsign-compare
    ([pr#18326](https://github.com/ceph/ceph/pull/18326), Jos Collin)

-   log: Use the coarse real time clock in log timestamps
    ([pr#18141](https://github.com/ceph/ceph/pull/18141), Adam C.
    Emerson)

-   mds: check metadata pool not cluster is full
    ([issue#22483](http://tracker.ceph.com/issues/22483),
    [pr#19602](https://github.com/ceph/ceph/pull/19602), Patrick
    Donnelly)

-   mds: fix CEPH_STAT_RSTAT definition
    ([pr#21633](https://github.com/ceph/ceph/pull/21633), \"Yan,
    Zheng\")

-   mds: get rid of the \"if\" check which is unnecessary inside a loop
    ([pr#18904](https://github.com/ceph/ceph/pull/18904), dongdong tao)

-   mds: Remove redundant null pointer check
    ([pr#19750](https://github.com/ceph/ceph/pull/19750), Brad Hubbard)

-   mds: simplify the code logic in replay_alloc_ids
    ([pr#18893](https://github.com/ceph/ceph/pull/18893), dongdong tao)

-   mempool: fix lack of pool names in mempool:dump output for JSON
    format ([pr#18329](https://github.com/ceph/ceph/pull/18329), Igor
    Fedotov)

-   messages: Initialization of uninitialized members various classes
    ([pr#16848](https://github.com/ceph/ceph/pull/16848), amitkuma)

-   messages/MDentryLink: add const to member function
    ([pr#15479](https://github.com/ceph/ceph/pull/15479),
    yonghengdexin735)

-   messages,test,msg: initialize h,reply_type,owner
    ([pr#17767](https://github.com/ceph/ceph/pull/17767), Amit Kumar)

-   mgr: add mgr daemon to DaemonStateIndex with metadata (hostname)
    ([issue#23286](http://tracker.ceph.com/issues/23286),
    [pr#20875](https://github.com/ceph/ceph/pull/20875), Jan Fajerski)

-   mgr: add missing call to pick_addresses
    ([issue#20955](http://tracker.ceph.com/issues/20955),
    [pr#16940](https://github.com/ceph/ceph/pull/16940), John Spray)

-   mgr: add the ip addr of standbys
    ([pr#16476](https://github.com/ceph/ceph/pull/16476), huanwen ren)

-   mgr: add units to performance counters
    ([issue#22747](http://tracker.ceph.com/issues/22747),
    [pr#20152](https://github.com/ceph/ceph/pull/20152), Rubab Syed)

-   mgr: allow service daemons to unregister from ServiceMap
    ([pr#20761](https://github.com/ceph/ceph/pull/20761), Sage Weil)

-   mgr: apply a threshold to perf counter prios
    ([pr#16699](https://github.com/ceph/ceph/pull/16699), John Spray)

-   mgr: balancer: fixed mistype \"AttributeError: \'Logger\' object has
    no attribute \'err\'\"
    ([pr#20130](https://github.com/ceph/ceph/pull/20130), Konstantin
    Shalygin)

-   mgr: centralized setting/getting of mgr configs
    ([pr#21442](https://github.com/ceph/ceph/pull/21442), John Spray,
    Rubab Syed)

-   mgr: ceph-mgr: can not change prometheus port for mgr
    ([pr#17746](https://github.com/ceph/ceph/pull/17746), wujian)

-   mgr: common interface for TSDB modules
    ([pr#17735](https://github.com/ceph/ceph/pull/17735), Jan Fajerski,
    John Spray, My Do)

-   mgr/dashboard: Adapt help text if server_addr is not set
    ([pr#21640](https://github.com/ceph/ceph/pull/21640), Volker Theile)

-   mgr/dashboard: Adapt RBD form to new application_metadata type
    ([pr#21602](https://github.com/ceph/ceph/pull/21602), Volker Theile)

-   mgr/dashboard: Add Api module
    ([pr#21126](https://github.com/ceph/ceph/pull/21126), Tiago Melo)

-   mgr/dashboard: Add \'autofocus\' directive
    ([pr#21559](https://github.com/ceph/ceph/pull/21559), Volker Theile)

-   mgr/dashboard: Add CdDatePipe
    ([pr#21087](https://github.com/ceph/ceph/pull/21087), Ricardo
    Marques)

-   mgr/dashboard: Add \'cd-error-panel\' component to display error
    messages ([pr#21558](https://github.com/ceph/ceph/pull/21558),
    Volker Theile)

-   mgr/dashboard: Add \'cd-loading-panel\' component
    ([pr#21618](https://github.com/ceph/ceph/pull/21618), Volker Theile)

-   mgr/dashboard: Add custom validators
    ([pr#21041](https://github.com/ceph/ceph/pull/21041), Volker Theile)

-   mgr/dashboard: Add DimlessBinaryDirective
    ([pr#20972](https://github.com/ceph/ceph/pull/20972), Ricardo
    Marques)

-   mgr/dashboard: Add ErasureCodeProfile controller
    ([issue#23345](http://tracker.ceph.com/issues/23345),
    [pr#20920](https://github.com/ceph/ceph/pull/20920), Sebastian
    Wagner, Stephan Müller)

-   mgr/dashboard: Add \'forceIdentifier\' attribute to datatable
    ([pr#21497](https://github.com/ceph/ceph/pull/21497), Volker Theile)

-   mgr/dashboard: Add helper component
    ([pr#20971](https://github.com/ceph/ceph/pull/20971), Ricardo
    Marques)

-   mgr/dashboard: additional fixes to block pages
    ([pr#20941](https://github.com/ceph/ceph/pull/20941), Jason
    Dillaman)

-   mgr/dashboard: Add minimalistic browsable API
    ([pr#20873](https://github.com/ceph/ceph/pull/20873), Sebastian
    Wagner)

-   mgr/dashboard: Add notification service/component
    ([pr#21078](https://github.com/ceph/ceph/pull/21078), Tiago Melo)

-   mgr/dashboard: Add Pool-create to the backend
    ([issue#23345](http://tracker.ceph.com/issues/23345),
    [pr#20865](https://github.com/ceph/ceph/pull/20865), Sebastian
    Wagner)

-   mgr/dashboard: Add RGW user and bucket management features
    ([pr#21351](https://github.com/ceph/ceph/pull/21351), Volker Theile)

-   mgr/dashboard: Adds reusable deletion dialog
    ([pr#20899](https://github.com/ceph/ceph/pull/20899), Stephan
    Müller, Tiago Melo)

-   mgr/dashboard: Add submit button component
    ([pr#21011](https://github.com/ceph/ceph/pull/21011), Tiago Melo)

-   mgr/dashboard: Add usage bar component
    ([pr#21128](https://github.com/ceph/ceph/pull/21128), Ricardo
    Marques)

-   mgr/dashboard: Angular modules cleanup
    ([pr#21402](https://github.com/ceph/ceph/pull/21402), Tiago Melo)

-   mgr/dashboard: Asynchronous tasks (frontend)
    ([pr#20962](https://github.com/ceph/ceph/pull/20962), Ricardo
    Marques)

-   mgr/dashboard: awsauth: fix python3 string decode problem
    ([pr#21875](https://github.com/ceph/ceph/pull/21875), Ricardo Dias)

-   mgr/dashboard: Change font-family of checkbox
    ([pr#21787](https://github.com/ceph/ceph/pull/21787), Tiago Melo)

-   mgr/dashboard: Clean up Pylint warnings
    ([pr#21694](https://github.com/ceph/ceph/pull/21694), Sebastian
    Wagner)

-   mgr/dashboard: Convert floating values to bytes
    ([pr#21677](https://github.com/ceph/ceph/pull/21677), Stephan
    Müller)

-   mgr/dashboard: Convert the RBD feature names to a list of strings
    ([pr#21024](https://github.com/ceph/ceph/pull/21024), Tatjana
    Dehler)

-   mgr/dashboard: Deletion dialog falsely executes deletion when
    pressing \'Cancel\'
    ([pr#22032](https://github.com/ceph/ceph/pull/22032), Volker Theile)

-   mgr/dashboard: Display notification if RGW is not configured
    ([pr#21977](https://github.com/ceph/ceph/pull/21977), Volker Theile)

-   mgr/dashboard: Display RBD form errors on submission
    ([pr#21529](https://github.com/ceph/ceph/pull/21529), Ricardo
    Marques)

-   mgr/dashboard: Enable object rendering in KV-table
    ([pr#21701](https://github.com/ceph/ceph/pull/21701), Stephan
    Müller)

-   mgr/dashboard: fix 500 error on block device iSCSI status page
    ([pr#20928](https://github.com/ceph/ceph/pull/20928), Jason
    Dillaman)

-   mgr/dashboard: fix dashboard python 3 support
    ([pr#21007](https://github.com/ceph/ceph/pull/21007), Ricardo Dias)

-   mgr/dashboard: Fix data race and use-before-assignment
    ([pr#21590](https://github.com/ceph/ceph/pull/21590), Sebastian
    Wagner)

-   mgr/dashboard: fixed password generation in Auth controller
    ([issue#23404](http://tracker.ceph.com/issues/23404),
    [pr#21006](https://github.com/ceph/ceph/pull/21006), Ricardo Dias)

-   mgr/dashboard: Fixes documentation link- to open in new tab
    ([pr#22262](https://github.com/ceph/ceph/pull/22262), Kanika
    Murarka)

-   mgr/dashboard: Fixes type error in RBD form
    ([pr#21681](https://github.com/ceph/ceph/pull/21681), Stephan
    Müller)

-   mgr/dashboard: fix frontend e2e tests
    ([pr#20943](https://github.com/ceph/ceph/pull/20943), Tiago Melo)

-   mgr/dashboard: fix FS status on old MDS daemons
    ([issue#20692](http://tracker.ceph.com/issues/20692),
    [pr#16960](https://github.com/ceph/ceph/pull/16960), John Spray)

-   mgr/dashboard: fix linting problem
    ([pr#22277](https://github.com/ceph/ceph/pull/22277), Tiago Melo)

-   mgr/dashboard: Fix missing \$event on deletion modal
    ([pr#21667](https://github.com/ceph/ceph/pull/21667), Ricardo
    Marques)

-   mgr/dashboard: Fix moment.js deprecation warning
    ([pr#22052](https://github.com/ceph/ceph/pull/22052), Tiago Melo)

-   mgr/dashboard: Fix objects named [default]{.title-ref} are
    inaccessible ([pr#20976](https://github.com/ceph/ceph/pull/20976),
    Sebastian Wagner)

-   mgr/dashboard: Fix RBD task metadata
    ([pr#22152](https://github.com/ceph/ceph/pull/22152), Tiago Melo)

-   mgr/dashboard: Fix table without fetchData
    ([pr#21086](https://github.com/ceph/ceph/pull/21086), Ricardo
    Marques)

-   mgr/dashboard: Fix the data table action selector
    ([pr#21270](https://github.com/ceph/ceph/pull/21270), Stephan
    Müller)

-   mgr/dashboard: fix two type errors found by mypy
    ([pr#21774](https://github.com/ceph/ceph/pull/21774), Sebastian
    Wagner)

-   mgr/dashboard: Handle errors during deletion
    ([pr#22029](https://github.com/ceph/ceph/pull/22029), Volker Theile)

-   mgr/dashboard: Implement a RGW proxy
    ([pr#21258](https://github.com/ceph/ceph/pull/21258), Volker Theile,
    Patrick Nawracay)

-   mgr/dashboard: Improve background tasks style
    ([pr#21462](https://github.com/ceph/ceph/pull/21462), Ricardo
    Marques)

-   mgr/dashboard: improve error handling
    ([pr#18182](https://github.com/ceph/ceph/pull/18182), Nick Erdmann)

-   mgr/dashboard: Improve error panel
    ([pr#21978](https://github.com/ceph/ceph/pull/21978), Volker Theile)

-   mgr/dashboard: Improve [npm start]{.title-ref} script
    ([pr#20989](https://github.com/ceph/ceph/pull/20989), Ricardo
    Marques)

-   mgr/dashboard: Improve table search
    ([pr#20807](https://github.com/ceph/ceph/pull/20807), Stephan
    Müller)

-   mgr/dashboard: Load the datatable content on component
    initialization ([pr#21595](https://github.com/ceph/ceph/pull/21595),
    Volker Theile)

-   mgr/dashboard: Navbar dropdown button does not respond for mobile
    browsers ([pr#21979](https://github.com/ceph/ceph/pull/21979),
    Volker Theile)

-   mgr/dashboard: Notification improvements
    ([pr#21350](https://github.com/ceph/ceph/pull/21350), Tiago Melo)

-   mgr/dashboard: pool: fix python3 dict_keys error
    ([pr#21636](https://github.com/ceph/ceph/pull/21636), Ricardo Dias)

-   mgr/dashboard: Pool listing
    ([pr#21353](https://github.com/ceph/ceph/pull/21353), Stephan
    Müller)

-   mgr/dashboard: rbd: add \@AuthRequired to snapshots controller
    ([pr#21517](https://github.com/ceph/ceph/pull/21517), Ricardo Dias)

-   mgr/dashboard: RBD copy, RBD flatten and snapshot clone (frontend)
    ([pr#21526](https://github.com/ceph/ceph/pull/21526), Ricardo
    Marques, Ricardo Dias)

-   mgr/dashboard: RBD management (frontend)
    ([pr#21385](https://github.com/ceph/ceph/pull/21385), Ricardo
    Marques)

-   mgr/dashboard: Refactor multiple duplicates of
    [get_rate()]{.title-ref}
    ([pr#21022](https://github.com/ceph/ceph/pull/21022), Sebastian
    Wagner)

-   mgr/dashboard: Refactor RGW backend
    ([pr#21855](https://github.com/ceph/ceph/pull/21855), Volker Theile)

-   mgr/dashboard: Rename and refactor ApiInterceptorService class
    ([pr#21386](https://github.com/ceph/ceph/pull/21386), Volker Theile)

-   mgr/dashboard: Replace font-awesome with fork-awesome
    ([pr#21327](https://github.com/ceph/ceph/pull/21327), Lenz Grimmer)

-   mgr/dashboard: restcontroller: fix detection of id args in element
    requests ([pr#21290](https://github.com/ceph/ceph/pull/21290),
    Ricardo Dias)

-   mgr/dashboard: RESTController improvements
    ([pr#21516](https://github.com/ceph/ceph/pull/21516), Ricardo Dias)

-   mgr/dashboard: run-tox: pass CEPH_BUILD_DIR value into tox script
    ([pr#21445](https://github.com/ceph/ceph/pull/21445), Ricardo Dias)

-   mgr: dashboard: show per pool IOPS on health page (#22495)
    ([issue#22495](http://tracker.ceph.com/issues/22495),
    [pr#19981](https://github.com/ceph/ceph/pull/19981), Konstantin
    Shalygin)

-   mgr/dashboard: Support aditional info on \'cd-view-cache\'
    ([pr#21060](https://github.com/ceph/ceph/pull/21060), Ricardo
    Marques)

-   mgr/dashboard: TaskManager bug fixes
    ([pr#21240](https://github.com/ceph/ceph/pull/21240), Ricardo Dias)

-   mgr/dashboard: Update selected items on table refresh
    ([pr#21099](https://github.com/ceph/ceph/pull/21099), Ricardo
    Marques)

-   mgr/dashboard: Use Bootstrap CSS
    ([pr#21780](https://github.com/ceph/ceph/pull/21780), Volker Theile)

-   mgr/dashboard: using RoutesDispatcher as HTTP request dispatcher
    ([pr#21239](https://github.com/ceph/ceph/pull/21239), Ricardo Dias)

-   mgr/dashboard_v2: add mgr to the list of perf counters
    ([pr#20783](https://github.com/ceph/ceph/pull/20783), Tiago Melo)

-   mgr/dashboard_v2: add mocked service provider for TcmuIscsiService
    ([pr#20775](https://github.com/ceph/ceph/pull/20775), Tiago Melo)

-   mgr/dashboard_v2: Add toggle able columns
    ([pr#20806](https://github.com/ceph/ceph/pull/20806), Stephan
    Müller)

-   mgr/dashboard_v2: Configuration settings support
    ([pr#20743](https://github.com/ceph/ceph/pull/20743), Ricardo Dias)

-   mgr/dashboard_v2: fix and improve table details
    ([pr#20811](https://github.com/ceph/ceph/pull/20811), Tiago Melo)

-   mgr/dashboard_v2: Fix cephfs template table usage
    ([pr#20804](https://github.com/ceph/ceph/pull/20804), Stephan
    Müller)

-   mgr/dashboard_v2: fix cluster configuration page
    ([pr#20821](https://github.com/ceph/ceph/pull/20821), Tiago Melo)

-   mgr/dashboard_v2: Improve charts tooltips
    ([pr#20757](https://github.com/ceph/ceph/pull/20757), Tiago Melo)

-   mgr/dashboard_v2: Pool controller
    ([pr#20823](https://github.com/ceph/ceph/pull/20823), Ricardo Dias)

-   mgr/dashboard_v2: Rotate the refresh icon on load
    ([pr#20805](https://github.com/ceph/ceph/pull/20805), Stephan
    Müller)

-   mgr: die on bind() failure
    ([pr#20595](https://github.com/ceph/ceph/pull/20595), John Spray)

-   mgr: disconnect unregistered service daemon when report received
    ([issue#22286](http://tracker.ceph.com/issues/22286),
    [pr#19261](https://github.com/ceph/ceph/pull/19261), Jason Dillaman)

-   mgr: emit cluster log message on serve() exception
    ([issue#21999](http://tracker.ceph.com/issues/21999),
    [pr#18672](https://github.com/ceph/ceph/pull/18672), John Spray)

-   mgr: Expose rgw perf counters
    ([pr#21269](https://github.com/ceph/ceph/pull/21269), Boris Ranto)

-   mgr: fix \"access denied\" message
    ([pr#19518](https://github.com/ceph/ceph/pull/19518), John Spray)

-   mgr: fix crashable DaemonStateIndex::get calls
    ([issue#17737](http://tracker.ceph.com/issues/17737),
    [pr#17933](https://github.com/ceph/ceph/pull/17933), John Spray)

-   mgr: fix crash in MonCommandCompletion
    ([issue#21157](http://tracker.ceph.com/issues/21157),
    [pr#17308](https://github.com/ceph/ceph/pull/17308), John Spray)

-   mgr: fixes python error handling
    ([issue#23406](http://tracker.ceph.com/issues/23406),
    [pr#21005](https://github.com/ceph/ceph/pull/21005), Ricardo Dias)

-   mgr: fix MSG_MGR_MAP handling
    ([pr#20892](https://github.com/ceph/ceph/pull/20892), Gu Zhongyan)

-   mgr: fix \"osd status\" command exception if OSD not in pgmap stats
    ([issue#21707](http://tracker.ceph.com/issues/21707),
    [pr#18173](https://github.com/ceph/ceph/pull/18173), Yanhu Cao)

-   mgr: fix py3 support
    ([issue#22880](http://tracker.ceph.com/issues/22880),
    [pr#20362](https://github.com/ceph/ceph/pull/20362), Kefu Chai)

-   mgr: fix py calls for dne service perf counters
    ([issue#21253](http://tracker.ceph.com/issues/21253),
    [pr#17605](https://github.com/ceph/ceph/pull/17605), John Spray)

-   mgr: implement completion of osd MetadataUpdate
    ([issue#21159](http://tracker.ceph.com/issues/21159),
    [pr#16925](https://github.com/ceph/ceph/pull/16925), Yanhu Cao)

-   mgr: implement \'osd safe-to-destroy\' and \'osd ok-to-stop\'
    commands ([pr#16976](https://github.com/ceph/ceph/pull/16976), Sage
    Weil)

-   mgr: improved module loading for error reporting etc
    ([issue#21999](http://tracker.ceph.com/issues/21999),
    [issue#21683](http://tracker.ceph.com/issues/21683),
    [issue#21502](http://tracker.ceph.com/issues/21502),
    [pr#19235](https://github.com/ceph/ceph/pull/19235), John Spray)

-   mgr: improve reporting on unloadable modules
    ([issue#23358](http://tracker.ceph.com/issues/23358),
    [pr#20921](https://github.com/ceph/ceph/pull/20921), John Spray)

-   mgr: increase time resolution of Commit/Apply OSD latencies
    ([pr#19232](https://github.com/ceph/ceph/pull/19232), Коренберг
    Марк)

-   mgr: initialize PyModuleRegistry sooner
    ([issue#22918](http://tracker.ceph.com/issues/22918),
    [pr#20321](https://github.com/ceph/ceph/pull/20321), John Spray)

-   mgr: In plugins \'module\' classes need not to be called \"Module\"
    anymore ([issue#17454](http://tracker.ceph.com/issues/17454),
    [pr#18526](https://github.com/ceph/ceph/pull/18526), Kefu Chai,
    bhavishyagopesh)

-   mgr: locking fixes
    ([issue#21158](http://tracker.ceph.com/issues/21158),
    [pr#17309](https://github.com/ceph/ceph/pull/17309), John Spray)

-   mgr: mgr/balancer: cast config vals to int or float
    ([issue#22429](http://tracker.ceph.com/issues/22429),
    [pr#19493](https://github.com/ceph/ceph/pull/19493), Dan van der
    Ster)

-   mgr: mgr/balancer: don\'t use \'foo\' tags on commands
    ([issue#22361](http://tracker.ceph.com/issues/22361),
    [pr#19482](https://github.com/ceph/ceph/pull/19482), John Spray)

-   mgr: mgr/balancer: fix KeyError in balancer rm
    ([issue#22470](http://tracker.ceph.com/issues/22470),
    [pr#19578](https://github.com/ceph/ceph/pull/19578), Dan van der
    Ster)

-   mgr: mgr/balancer: fix OPTIONS definition
    ([pr#21620](https://github.com/ceph/ceph/pull/21620), John Spray)

-   mgr: mgr/balancer: fix upmap; default balancer module enabled
    ([pr#18691](https://github.com/ceph/ceph/pull/18691), Sage Weil)

-   mgr: mgr/balancer: make crush-compat mode work
    ([pr#17983](https://github.com/ceph/ceph/pull/17983), Sage Weil)

-   mgr: mgr/balancer: mgr module to automatically balance PGs across
    OSDs ([pr#16272](https://github.com/ceph/ceph/pull/16272), Spandan
    Kumar Sahu, Sage Weil)

-   mgr: mgr/balancer: more pool-specific enhancements
    ([pr#20225](https://github.com/ceph/ceph/pull/20225), xie xingguo)

-   mgr: mgr/balancer: pool-specific optimization support and bug fixes
    ([pr#20154](https://github.com/ceph/ceph/pull/20154), xie xingguo)

-   mgr: mgr/balancer: replace magic value of -1 for DEFAULT_CHOOSE_ARGS
    ([pr#20258](https://github.com/ceph/ceph/pull/20258), Kefu Chai)

-   mgr: mgr/balancer: skip CRUSH_ITEM_NONE
    ([pr#18894](https://github.com/ceph/ceph/pull/18894), Sage Weil)

-   mgr: mgr/balancer: two more fixes
    ([pr#20180](https://github.com/ceph/ceph/pull/20180), xie xingguo)

-   mgr: mgrc: free MMgrClose in handle_mgr_close
    ([issue#23846](http://tracker.ceph.com/issues/23846),
    [pr#21626](https://github.com/ceph/ceph/pull/21626), Casey Bodley)

-   mgr: mgr/DaemonServer: add overrides value to \'config show\'
    ([pr#21093](https://github.com/ceph/ceph/pull/21093), Gu Zhongyan)

-   mgr: mgr/DaemonServer.cc: \[Cleanup\] Change to using get_val
    template function
    ([pr#18717](https://github.com/ceph/ceph/pull/18717), Shinobu Kinjo)

-   mgr: mgr/DaemonServer: \[Cleanup\] Remove redundant code
    ([pr#18716](https://github.com/ceph/ceph/pull/18716), Shinobu Kinjo)

-   mgr: mgr/dashboard: add configuration setting browser
    ([issue#22522](http://tracker.ceph.com/issues/22522),
    [pr#20043](https://github.com/ceph/ceph/pull/20043), Rubab Syed)

-   mgr: mgr/dashboard: add image id to mgr rbd info instead of
    block_name_prefix
    ([pr#20884](https://github.com/ceph/ceph/pull/20884), zouaiguo)

-   mgr: mgr/dashboard: Add monitor list
    ([pr#19632](https://github.com/ceph/ceph/pull/19632), Rubab Syed)

-   mgr: mgr/dashboard: Add RGW user and bucket lists (read-only)
    ([pr#20869](https://github.com/ceph/ceph/pull/20869), Volker Theile)

-   mgr: mgr/dashboard: add TLS
    ([pr#21627](https://github.com/ceph/ceph/pull/21627), John Spray)

-   mgr: mgr/dashboard: Add toBytes() method to FormatterService
    ([pr#20978](https://github.com/ceph/ceph/pull/20978), Volker Theile)

-   mgr: mgr/dashboard: asynchronous task support
    ([pr#20870](https://github.com/ceph/ceph/pull/20870), Ricardo Dias)

-   mgr: mgr/dashboard: change raw usage chart\'s color depending on
    usage ([pr#17421](https://github.com/ceph/ceph/pull/17421), Nick
    Erdmann)

-   mgr: mgr/dashboard: fix audit log loading
    ([pr#18848](https://github.com/ceph/ceph/pull/18848), John Spray)

-   mgr: mgr/dashboard: Fix backend tests for newer CherryPy versions
    ([pr#20778](https://github.com/ceph/ceph/pull/20778), Patrick
    Nawracay)

-   mgr: mgr/dashboard: Fix PG status coloring
    ([pr#19431](https://github.com/ceph/ceph/pull/19431), Wido den
    Hollander)

-   mgr: mgr/dashboard: format tooltip\'s label as user friendly string
    ([pr#18769](https://github.com/ceph/ceph/pull/18769), Yao Zongyou)

-   mgr: mgr/dashboard: handle null in format_number
    ([issue#21570](http://tracker.ceph.com/issues/21570),
    [pr#17991](https://github.com/ceph/ceph/pull/17991), John Spray)

-   mgr: mgr/dashboard: HTTP request logging
    ([pr#20797](https://github.com/ceph/ceph/pull/20797), Ricardo Dias)

-   mgr: mgr/dashboard: Improve auth interceptor
    ([pr#20847](https://github.com/ceph/ceph/pull/20847), Volker Theile)

-   mgr: mgr/dashboard: performance counter browsers
    ([issue#22521](http://tracker.ceph.com/issues/22521),
    [pr#19922](https://github.com/ceph/ceph/pull/19922), Rubab-Syed)

-   mgr: mgr/dashboard: RBD management (backend)
    ([pr#21360](https://github.com/ceph/ceph/pull/21360), Ricardo Dias)

-   mgr: mgr/dashboard: Remove unused code
    ([pr#21045](https://github.com/ceph/ceph/pull/21045), Volker Theile)

-   mgr: mgr/dashboard: Remove useless code
    ([pr#20958](https://github.com/ceph/ceph/pull/20958), Volker Theile)

-   mgr: mgr/dashboard: show warnings if data is out of date or mons are
    down ([pr#18847](https://github.com/ceph/ceph/pull/18847), John
    Spray)

-   mgr: mgr/dashboard: sort servers and OSDs in OSD list
    ([issue#21572](http://tracker.ceph.com/issues/21572),
    [pr#17993](https://github.com/ceph/ceph/pull/17993), John Spray)

-   mgr: mgr/dashboard: use rel=\"icon\" for favicon
    ([pr#18013](https://github.com/ceph/ceph/pull/18013), Kefu Chai)

-   mgr: mgr/dashboard v2: Add CSS class for required form fields
    ([pr#20747](https://github.com/ceph/ceph/pull/20747), Volker Theile)

-   mgr: mgr/dashboard_v2: Add RBD create functionality to the Python
    backend ([pr#20751](https://github.com/ceph/ceph/pull/20751),
    Tatjana Dehler)

-   mgr: mgr/dashboard v2: Add units to performance counters
    ([pr#20742](https://github.com/ceph/ceph/pull/20742), Volker Theile)

-   mgr: mgr/dashboard v2: Display loading indicator in datatables
    during first load
    ([pr#20744](https://github.com/ceph/ceph/pull/20744), Volker Theile)

-   mgr: mgr/dashboard v2: Don\'t show details if multiple OSDs are
    selected ([pr#20772](https://github.com/ceph/ceph/pull/20772),
    Volker Theile)

-   mgr: mgr/dashboard v2: implement can_run method
    ([pr#20728](https://github.com/ceph/ceph/pull/20728), John Spray)

-   mgr: mgr/dashboard_v2: Initial submission of a web-based management
    UI (replacement for the existing dashboard)
    ([pr#20103](https://github.com/ceph/ceph/pull/20103), Stephan
    Müller, Lenz Grimmer, Tiago Melo, Ricardo Marques, Sebastian Wagner,
    Patrick Nawracay, Ricardo Dias, Volker Theile, Kai Wagner, Tatjana
    Dehler)

-   mgr: mgr/dashboard v2: Introduce CdTableSelection model
    ([pr#20746](https://github.com/ceph/ceph/pull/20746), Volker Theile)

-   mgr: mgr/dashboard_v2: Removed unused
    [tools.detail_route()]{.title-ref}
    ([pr#20765](https://github.com/ceph/ceph/pull/20765), Sebastian
    Wagner)

-   mgr: mgr/influx: Added Additional Stats
    ([pr#21424](https://github.com/ceph/ceph/pull/21424), mhdo2)

-   mgr: mgr/influx: Add InfluxDB SSL Option
    ([pr#19374](https://github.com/ceph/ceph/pull/19374), Tobias Gall)

-   mgr: mgr/influx: Only split string on first occurence of dot (.)
    ([issue#23996](http://tracker.ceph.com/issues/23996),
    [pr#21795](https://github.com/ceph/ceph/pull/21795), Wido den
    Hollander)

-   mgr: mgr/influx: PEP-8 and other fixes to Influx module
    ([pr#19229](https://github.com/ceph/ceph/pull/19229), Wido den
    Hollander)

-   mgr: mgr/influx: Various fixes and improvements
    ([pr#20187](https://github.com/ceph/ceph/pull/20187), Wido den
    Hollander)

-   mgr: mgr/influx: Various time fixes
    ([pr#20494](https://github.com/ceph/ceph/pull/20494), Wido den
    Hollander)

-   mgr: mgr/localpool: default to 3x; allow min_size adjustment
    ([pr#18089](https://github.com/ceph/ceph/pull/18089), Sage Weil)

-   mgr: mgr/MgrClient: guard send_pgstats() with lock
    ([issue#23370](http://tracker.ceph.com/issues/23370),
    [pr#20909](https://github.com/ceph/ceph/pull/20909), Kefu Chai)

-   mgr: mgr/MgrClient: service registration filtered by service name
    instead of daemon name
    ([pr#21459](https://github.com/ceph/ceph/pull/21459), runsisi)

-   mgr: mgr/PGMap: drop REQUEST\_{SLOW,STUCK} HEALTH_WARNs
    ([pr#19114](https://github.com/ceph/ceph/pull/19114), Kefu Chai)

-   mgr: mgr/prometheus: add ceph_disk_occupation series
    ([issue#21594](http://tracker.ceph.com/issues/21594),
    [pr#18021](https://github.com/ceph/ceph/pull/18021), John Spray)

-   mgr: mgr/prometheus: add missing \'deep\' state to PG_STATES in
    ceph-mgr prometheus plugin
    ([issue#22116](http://tracker.ceph.com/issues/22116),
    [pr#18890](https://github.com/ceph/ceph/pull/18890), Peter Woodman)

-   mgr: mgr/prometheus: Fix for MDS metrics
    ([issue#20899](http://tracker.ceph.com/issues/20899),
    [pr#17318](https://github.com/ceph/ceph/pull/17318), John Spray,
    Jeremy H Austin)

-   mgr: mgr/prometheus: fix PG state names
    ([pr#21288](https://github.com/ceph/ceph/pull/21288), John Spray)

-   mgr: mgr/prometheus: Skip bogus entries
    ([pr#20456](https://github.com/ceph/ceph/pull/20456), Boris Ranto)

-   mgr: mgr/prometheus: skip OSD output if missing from CRUSH devices
    ([pr#20644](https://github.com/ceph/ceph/pull/20644), John Spray)

-   mgr: mgr/restful: A couple of restful fixes
    ([pr#18649](https://github.com/ceph/ceph/pull/18649), Boris Ranto)

-   mgr: mgr/restful: cleaner message when not configured
    ([issue#21292](http://tracker.ceph.com/issues/21292),
    [pr#17573](https://github.com/ceph/ceph/pull/17573), John Spray)

-   mgr: mgr/smart: fix python3 module loading
    ([pr#21047](https://github.com/ceph/ceph/pull/21047), Ricardo Dias)

-   mgr: mgr/status: fix ceph fs status returns error
    ([issue#21752](http://tracker.ceph.com/issues/21752),
    [pr#18233](https://github.com/ceph/ceph/pull/18233), Yanhu Cao)

-   mgr: mgr/status: format byte quantities in base 2 multiples
    ([issue#21189](http://tracker.ceph.com/issues/21189),
    [pr#17380](https://github.com/ceph/ceph/pull/17380), John Spray)

-   mgr: mgr/telemetry: Add Ceph Telemetry module to send reports back
    to project ([pr#21970](https://github.com/ceph/ceph/pull/21970),
    Wido den Hollander)

-   mgr: mgr/zabbix: fix div by zero
    ([issue#21518](http://tracker.ceph.com/issues/21518),
    [pr#17931](https://github.com/ceph/ceph/pull/17931), John Spray)

-   mgr: mgr/zabbix: ignore osd with 0 kb capacity
    ([issue#21904](http://tracker.ceph.com/issues/21904),
    [pr#18809](https://github.com/ceph/ceph/pull/18809), Ilja Slepnev)

-   mgr: mgr/zabbix: Implement health checks
    ([pr#20198](https://github.com/ceph/ceph/pull/20198), Wido den
    Hollander)

-   mgr: mgr/zabbix: Send max, min and avg PGs of OSDs to Zabbix
    ([pr#21043](https://github.com/ceph/ceph/pull/21043), Wido den
    Hollander)

-   mgr: mgr/Zabbix: Various fixes to Zabbix module
    ([pr#19452](https://github.com/ceph/ceph/pull/19452), Wido den
    Hollander)

-   mgr: mimic: mgr/telegraf: Telegraf module for Ceph Mgr
    ([pr#22013](https://github.com/ceph/ceph/pull/22013), Wido den
    Hollander)

-   mgr: Modify mgr-influx module database check to not require admin
    privileges ([pr#18102](https://github.com/ceph/ceph/pull/18102),
    Benjeman Meekhof)

-   mgr: mon,mgr: improve \'mgr module disable\' cmd
    ([pr#21188](https://github.com/ceph/ceph/pull/21188), Gu Zhongyan)

-   mgr: mon, mgr: move \"osd pool stats\" command to mgr and mgr python
    module ([pr#19985](https://github.com/ceph/ceph/pull/19985), Chang
    Liu)

-   mgr: mon/MgrStatMonitor: fix formatting of pending_digest
    ([issue#22991](http://tracker.ceph.com/issues/22991),
    [pr#20426](https://github.com/ceph/ceph/pull/20426), Patrick
    Donnelly)

-   mgr,mon: mon/MgrMonitor: read cmd descs if empty on
    update_from_paxos()
    ([issue#21300](http://tracker.ceph.com/issues/21300),
    [pr#17846](https://github.com/ceph/ceph/pull/17846), Joao Eduardo
    Luis)

-   mgr,mon: mon,mgr: remove single wildcard \'\*\' from ceph comand
    line description
    ([pr#21139](https://github.com/ceph/ceph/pull/21139), Gu Zhongyan)

-   mgr,mon: mon/mgr: sync \"mgr_command_descs\",\"osd_metadata\" and
    \"mgr_metadata\" prefixes to new mons
    ([issue#21527](http://tracker.ceph.com/issues/21527),
    [pr#17929](https://github.com/ceph/ceph/pull/17929), huanwen ren)

-   mgr,mon: mon/MonCommands: mgr metadata - improve parameter naming
    consistency ([issue#23330](http://tracker.ceph.com/issues/23330),
    [pr#20866](https://github.com/ceph/ceph/pull/20866), Jan Fajerski)

-   mgr: preventing blank hostname in DaemonState
    ([issue#20887](http://tracker.ceph.com/issues/20887),
    [issue#21060](http://tracker.ceph.com/issues/21060),
    [pr#17138](https://github.com/ceph/ceph/pull/17138), liuchang0812)

-   mgr: prometheus: added osd commit/apply latency metrics (#22718)
    ([issue#22718](http://tracker.ceph.com/issues/22718),
    [pr#19980](https://github.com/ceph/ceph/pull/19980), Konstantin
    Shalygin)

-   mgr: prometheus: Don\'t crash on OSDs without metadata
    ([pr#20539](https://github.com/ceph/ceph/pull/20539), Christopher
    Blum)

-   mgr: prometheus fix metadata labels
    ([pr#21557](https://github.com/ceph/ceph/pull/21557), Jan Fajerski)

-   mgr: prometheus: set metadata metrics value to \'1\' (#22717)
    ([issue#22717](http://tracker.ceph.com/issues/22717),
    [pr#19979](https://github.com/ceph/ceph/pull/19979), Konstantin
    Shalygin)

-   mgr: pybind/mgr/balancer: add sanity check against empty
    adjusted_map ([pr#20836](https://github.com/ceph/ceph/pull/20836),
    xie xingguo)

-   mgr: pybind/mgr/balancer: fix pool-deletion vs auto-optimization
    race ([pr#20706](https://github.com/ceph/ceph/pull/20706), xie
    xingguo)

-   mgr: pybind/mgr/balancer: fix sanity check against empty weight-set
    ([pr#20278](https://github.com/ceph/ceph/pull/20278), xie xingguo)

-   mgr: pybind/mgr/balancer: increase bad_steps properly
    ([pr#20194](https://github.com/ceph/ceph/pull/20194), xie xingguo)

-   mgr: pybind/mgr/balancer: load weight-set from ms
    ([pr#20197](https://github.com/ceph/ceph/pull/20197), xie xingguo)

-   mgr: pybind/mgr/balancer: more specific command outputs
    ([pr#20305](https://github.com/ceph/ceph/pull/20305), xie xingguo)

-   mgr: pybind/mgr/balancer: remove optimization plan properly
    ([pr#20224](https://github.com/ceph/ceph/pull/20224), xie xingguo)

-   mgr: pybind/mgr/balancer: two more fixes
    ([pr#20788](https://github.com/ceph/ceph/pull/20788), xie xingguo)

-   mgr: pybind/mgr/dashboard: add url_prefix
    ([issue#20568](http://tracker.ceph.com/issues/20568),
    [pr#17119](https://github.com/ceph/ceph/pull/17119), Nick Erdmann)

-   mgr: pybind/mgr/dashboard: fix duplicated slash in html href
    ([issue#22851](http://tracker.ceph.com/issues/22851),
    [pr#20229](https://github.com/ceph/ceph/pull/20229), Shengjing Zhu)

-   mgr,pybind: mgr/dashboard: fix pool size base conversion
    ([pr#16771](https://github.com/ceph/ceph/pull/16771), Yixing Yan)

-   mgr: pybind/mgr/dashboard: fix reverse proxy support
    ([issue#22557](http://tracker.ceph.com/issues/22557),
    [pr#19758](https://github.com/ceph/ceph/pull/19758), Nick Erdmann)

-   mgr,pybind: mgr/iostat: print output as a table
    ([pr#21338](https://github.com/ceph/ceph/pull/21338), Mohamad Gebai)

-   mgr: pybind/mgr/localpool: module to automagically create localized
    pools ([pr#17528](https://github.com/ceph/ceph/pull/17528), Sage
    Weil)

-   mgr: pybind/mgr/mgr_module: add default param for
    MgrStandbyModule.get_con...
    ([pr#19948](https://github.com/ceph/ceph/pull/19948), Kefu Chai)

-   mgr: pybind/mgr/mgr_module: make rados handle available to all
    modules ([pr#19972](https://github.com/ceph/ceph/pull/19972), Sage
    Weil)

-   mgr: pybind/mgr_module: move PRIO\_\* and PERFCOUNTER\_\* to
    MgrModule class
    ([pr#18251](https://github.com/ceph/ceph/pull/18251), Jan Fajerski)

-   mgr: pybind/mgr: new \'hello world\' mgr module skeleton
    ([pr#19491](https://github.com/ceph/ceph/pull/19491), Yaarit Hatuka)

-   mgr: pybind/mgr/prometheus: add file_sd_config command
    ([pr#21061](https://github.com/ceph/ceph/pull/21061), Jan Fajerski)

-   mgr: pybind/mgr/prometheus: add osd_in/out metric; make osd_weight a
    metric ([pr#18243](https://github.com/ceph/ceph/pull/18243), Jan
    Fajerski)

-   mgr: pybind/mgr/prometheus: add StandbyModule and handle failed MON
    cluster ([pr#19744](https://github.com/ceph/ceph/pull/19744), Jan
    Fajerski)

-   mgr: pybind/mgr/prometheus: don\'t crash when encountering an
    unknown PG state
    ([pr#18903](https://github.com/ceph/ceph/pull/18903), Jan Fajerski)

-   mgr: pybind/mgr/prometheus: don\'t export metrics for dead daemon;
    new metrics ([pr#20506](https://github.com/ceph/ceph/pull/20506),
    Jan Fajerski)

-   mgr: pybind/mgr/prometheus: fix creation of osd_metadata metric
    ([pr#21530](https://github.com/ceph/ceph/pull/21530), Jan Fajerski)

-   mgr: pybind/mgr/prometheus: fix metric type undef -\> untyped
    ([issue#22313](http://tracker.ceph.com/issues/22313),
    [pr#19524](https://github.com/ceph/ceph/pull/19524), Ilya Margolin)

-   mgr: pybind/mgr/prometheus: fix metric type undef -\> untyped
    ([pr#18208](https://github.com/ceph/ceph/pull/18208), Jan Fajerski)

-   mgr,pybind: pybing/mgr/prometheus: return default port if config-key
    get returns ...
    ([pr#21696](https://github.com/ceph/ceph/pull/21696), Jan Fajerski)

-   mgr: python interface rework + enable modules to run in standby mode
    ([issue#21593](http://tracker.ceph.com/issues/21593),
    [issue#17460](http://tracker.ceph.com/issues/17460),
    [pr#16651](https://github.com/ceph/ceph/pull/16651), John Spray,
    Sage Weil)

-   mgr: quieten logging on missing OSD stats
    ([pr#20485](https://github.com/ceph/ceph/pull/20485), John Spray)

-   mgr,rbd: mgr/dashboard: added iSCSI IOPS/throughput metrics
    ([issue#21391](http://tracker.ceph.com/issues/21391),
    [pr#18653](https://github.com/ceph/ceph/pull/18653), Jason Dillaman)

-   mgr,rbd: mgr/dashboard: fix duplicate images listed on iSCSI status
    page ([issue#21017](http://tracker.ceph.com/issues/21017),
    [pr#17055](https://github.com/ceph/ceph/pull/17055), Jason Dillaman)

-   mgr: reconcile can_run checks and selftest
    ([pr#21607](https://github.com/ceph/ceph/pull/21607), John Spray,
    Kefu Chai)

-   mgr: remove a few junk lines
    ([pr#20005](https://github.com/ceph/ceph/pull/20005), John Spray)

-   mgr: remove unused static files from dashboard module
    ([pr#16762](https://github.com/ceph/ceph/pull/16762), John Spray)

-   mgr: request daemon\'s metadata when receiving a report from an
    unknown server ([issue#21687](http://tracker.ceph.com/issues/21687),
    [pr#18484](https://github.com/ceph/ceph/pull/18484), Chang Liu)

-   mgr,rgw: mgr/dashboard: RGW page
    ([pr#19512](https://github.com/ceph/ceph/pull/19512), Chang Liu)

-   mgr,rgw: prometheus: Implement rgw_metadata metric
    ([pr#21383](https://github.com/ceph/ceph/pull/21383), Boris Ranto)

-   mgr: safety checks on pyThreadState usage
    ([pr#18093](https://github.com/ceph/ceph/pull/18093), John Spray)

-   mgr: set explicit thread name
    ([issue#21404](http://tracker.ceph.com/issues/21404),
    [pr#17756](https://github.com/ceph/ceph/pull/17756), John Spray)

-   mgr: silence warning from -Wsign-compare
    ([pr#17881](https://github.com/ceph/ceph/pull/17881), Jos Collin)

-   mgr: skip first non-zero incremental in PGMap::apply_incremental()
    ([issue#21773](http://tracker.ceph.com/issues/21773),
    [pr#18347](https://github.com/ceph/ceph/pull/18347), Aleksei
    Gutikov)

-   mgr/status: output to stdout, not stderr
    ([issue#24175](http://tracker.ceph.com/issues/24175),
    [pr#22135](https://github.com/ceph/ceph/pull/22135), John Spray)

-   mgr: store declared_types in MgrSession
    ([issue#21197](http://tracker.ceph.com/issues/21197),
    [pr#17932](https://github.com/ceph/ceph/pull/17932), John Spray)

-   mgr: systemd: Wait 10 seconds before restarting ceph-mgr
    ([issue#23083](http://tracker.ceph.com/issues/23083),
    [pr#20533](https://github.com/ceph/ceph/pull/20533), Wido den
    Hollander)

-   mgr,tests: mgr/dashboard: skip data pool testcase for none-bluestore
    clusters ([pr#21004](https://github.com/ceph/ceph/pull/21004),
    Tatjana Dehler)

-   mgr,tests: mgr/dashboard_v2: fix test_perf_counters_mgr_get
    ([pr#20916](https://github.com/ceph/ceph/pull/20916), Tiago Melo)

-   mgr,tests: qa: add new prometheus test to rados/mgr suite
    ([pr#20047](https://github.com/ceph/ceph/pull/20047), John Spray)

-   mgr,tests: qa: configure zabbix properly before selftest
    ([issue#22514](http://tracker.ceph.com/issues/22514),
    [pr#19634](https://github.com/ceph/ceph/pull/19634), John Spray)

-   mgr,tests: qa: fix mgr \_load_module helper
    ([pr#18685](https://github.com/ceph/ceph/pull/18685), John Spray)

-   mgr,tools: mgr/iostat: implement \'ceph iostat\' as a mgr plugin
    ([pr#20100](https://github.com/ceph/ceph/pull/20100), Mohamad Gebai)

-   mgr: use new style config opts + add metadata
    ([pr#17374](https://github.com/ceph/ceph/pull/17374), John Spray)

-   mgr/zabbix: Fix wrong log message
    ([pr#21237](https://github.com/ceph/ceph/pull/21237), Gu Zhongyan)

-   mgr/zabbix: monitoring template improvements
    ([pr#19901](https://github.com/ceph/ceph/pull/19901), Marc
    Schoechlin)

-   mon: Add [ceph osd get-require-min-compat-client]{.title-ref}
    command ([pr#19015](https://github.com/ceph/ceph/pull/19015),
    hansbogert)

-   mon: add \'ceph osd pool get erasure allow_ec_overwrites\' command
    ([pr#21102](https://github.com/ceph/ceph/pull/21102), Mykola Golub)

-   mon: add MMonHealth back
    ([issue#22462](http://tracker.ceph.com/issues/22462),
    [pr#20528](https://github.com/ceph/ceph/pull/20528), Kefu Chai)

-   mon: add mon_health_preluminous_compat_warning
    ([pr#16902](https://github.com/ceph/ceph/pull/16902), Sage Weil)

-   mon: a few conversions to monotonic clock
    ([pr#18595](https://github.com/ceph/ceph/pull/18595), Patrick
    Donnelly)

-   mon: align lspools output
    ([pr#19597](https://github.com/ceph/ceph/pull/19597), Jos Collin)

-   mon: allow cluter and debug logs to go to stderr, with appropriate
    prefix ([pr#19385](https://github.com/ceph/ceph/pull/19385), Sage
    Weil)

-   mon: cache reencoded osdmaps
    ([issue#23713](http://tracker.ceph.com/issues/23713),
    [pr#21605](https://github.com/ceph/ceph/pull/21605), Sage Weil,
    Xiaoxi CHEN)

-   mon: centralized config
    ([pr#20172](https://github.com/ceph/ceph/pull/20172), Sage Weil)

-   mon: \"ceph osd crush rule rename\" support
    ([pr#17029](https://github.com/ceph/ceph/pull/17029), xie xingguo)

-   mon: check monitor address configuration
    ([pr#18073](https://github.com/ceph/ceph/pull/18073), Li Wang)

-   mon: clean up cluster logging on mon events
    ([issue#22082](http://tracker.ceph.com/issues/22082),
    [pr#18822](https://github.com/ceph/ceph/pull/18822), John Spray)

-   mon: cleanups to optracker code
    ([pr#21371](https://github.com/ceph/ceph/pull/21371), John Spray)

-   mon: cleanup unused option mon_health_data_update_interval
    ([pr#17728](https://github.com/ceph/ceph/pull/17728), Yao Guotao)

-   mon: common/options: set max_background_jobs instead of
    max_background_compactions
    ([pr#18397](https://github.com/ceph/ceph/pull/18397), Kefu Chai)

-   mon: Compress the warnings of pgs not scrubbed or deep-scrubbed
    ([pr#17295](https://github.com/ceph/ceph/pull/17295), Zhi Zhang)

-   mon: do not use per_pool_sum_delta to show recovery summary
    ([issue#22727](http://tracker.ceph.com/issues/22727),
    [pr#20009](https://github.com/ceph/ceph/pull/20009), Chang Liu)

-   mon: don\'t blow away bootstrap-mgr on upgrades
    ([issue#20950](http://tracker.ceph.com/issues/20950),
    [pr#18399](https://github.com/ceph/ceph/pull/18399), John Spray)

-   mon: double mon_mgr_mkfs_grace from 60s -\> 120s
    ([pr#20955](https://github.com/ceph/ceph/pull/20955), Sage Weil)

-   mon: Drop redundant access specifier, etc (cleanup)
    ([pr#19028](https://github.com/ceph/ceph/pull/19028), Shinobu Kinjo)

-   mon: dump percent_used PGMap field as float
    ([pr#20439](https://github.com/ceph/ceph/pull/20439), John Spray)

-   mon: dump servicemap along with MgrStatMonitor dump info
    ([pr#18760](https://github.com/ceph/ceph/pull/18760), Zhi Zhang)

-   mon: expand cap validity check for mgr, osd, mds
    ([issue#22525](http://tracker.ceph.com/issues/22525),
    [pr#21311](https://github.com/ceph/ceph/pull/21311), Jing Li, Sage
    Weil)

-   mon: final luminous compatset feature and osdmap flag
    ([pr#17333](https://github.com/ceph/ceph/pull/17333), Sage Weil)

-   mon: fix commands advertised during mon cluster upgrade
    ([pr#16871](https://github.com/ceph/ceph/pull/16871), Sage Weil)

-   mon: fix dropping mgr metadata for active mgr (#21260)
    ([issue#21260](http://tracker.ceph.com/issues/21260),
    [pr#17571](https://github.com/ceph/ceph/pull/17571), John Spray)

-   mon: fix \"fs new\" pool metadata update, tests
    ([issue#20959](http://tracker.ceph.com/issues/20959),
    [pr#16954](https://github.com/ceph/ceph/pull/16954), Greg Farnum)

-   mon: fix legacy health checks in \'ceph status\' during upgrade; fix
    jewel-x upgrade combo
    ([pr#16967](https://github.com/ceph/ceph/pull/16967), Sage Weil)

-   mon: fix mgr using auth_client_required policy
    ([pr#20048](https://github.com/ceph/ceph/pull/20048), John Spray)

-   mon: fix [osd out]{.title-ref} clog message
    ([issue#21249](http://tracker.ceph.com/issues/21249),
    [pr#17525](https://github.com/ceph/ceph/pull/17525), John Spray)

-   mon: fix slow op warning on mon, improve slow op warnings
    ([issue#23769](http://tracker.ceph.com/issues/23769),
    [pr#21684](https://github.com/ceph/ceph/pull/21684), Sage Weil)

-   mon: fix structure of \'features\' command
    ([pr#20115](https://github.com/ceph/ceph/pull/20115), Sage Weil)

-   mon: fix two stray legacy get_health() callers
    ([pr#17269](https://github.com/ceph/ceph/pull/17269), Sage Weil)

-   mon: fix wrong mon-num counting logic of \'ceph features\' command
    ([pr#16887](https://github.com/ceph/ceph/pull/16887), xie xingguo)

-   mon: handle bad snapshot removal reqs gracefully
    ([issue#18746](http://tracker.ceph.com/issues/18746),
    [pr#20835](https://github.com/ceph/ceph/pull/20835), Paul Emmerich)

-   mon: handle monitor lag when killing mgrs
    ([issue#20629](http://tracker.ceph.com/issues/20629),
    [pr#18268](https://github.com/ceph/ceph/pull/18268), John Spray)

-   mon: incorrect MAX AVAIL in \"ceph df\"
    ([issue#21243](http://tracker.ceph.com/issues/21243),
    [pr#17513](https://github.com/ceph/ceph/pull/17513), liuchang0812)

-   mon: invalid JSON returned when querying pool parameters
    ([issue#23200](http://tracker.ceph.com/issues/23200),
    [pr#20745](https://github.com/ceph/ceph/pull/20745), Chang Liu)

-   mon/LogMonitor: call no_reply() on ignored log message
    ([pr#22104](https://github.com/ceph/ceph/pull/22104), Sage Weil)

-   mon: mark mgr reports as no_reply
    ([issue#22114](http://tracker.ceph.com/issues/22114),
    [pr#21057](https://github.com/ceph/ceph/pull/21057), Kefu Chai)

-   mon: mark mon_allow_pool_delete as observed
    ([pr#18125](https://github.com/ceph/ceph/pull/18125), Dan van der
    Ster)

-   mon: mark OSD beacons and pg_create messages as no_reply
    ([issue#22114](http://tracker.ceph.com/issues/22114),
    [pr#20517](https://github.com/ceph/ceph/pull/20517), Greg Farnum)

-   mon: mon/AuthMonitor: don\'t validate [fs authorize]{.title-ref}
    caps with [valid_caps()]{.title-ref}
    ([pr#21418](https://github.com/ceph/ceph/pull/21418), Joao Eduardo
    Luis)

-   mon: mon/ConfigMonitor: clean up prepare_command()
    ([pr#20911](https://github.com/ceph/ceph/pull/20911), Gu Zhongyan)

-   mon: mon/Elector: force election epoch bump on start
    ([issue#20949](http://tracker.ceph.com/issues/20949),
    [pr#16944](https://github.com/ceph/ceph/pull/16944), Sage Weil)

-   mon: mon/Elector: remove unused member fields start_stamp and
    ack_stamp ([pr#21091](https://github.com/ceph/ceph/pull/21091),
    runsisi)

-   mon: mon/LogMonitor: \"log last\" should return up to n entries
    ([pr#18759](https://github.com/ceph/ceph/pull/18759), Kefu Chai)

-   mon: mon/MDSMonitor: fix clang build failure
    ([pr#20637](https://github.com/ceph/ceph/pull/20637), Willem Jan
    Withagen)

-   mon: mon,mgr: make osd_metric more popular and report slow ops to
    mgr ([issue#23045](http://tracker.ceph.com/issues/23045),
    [pr#20660](https://github.com/ceph/ceph/pull/20660), lvshanchun)

-   mon: mon/MgrMonitor: limit mgrmap history
    ([issue#22257](http://tracker.ceph.com/issues/22257),
    [pr#19185](https://github.com/ceph/ceph/pull/19185), Sage Weil)

-   mon: mon/MonCommands: fix copy-and-paste error
    ([pr#17271](https://github.com/ceph/ceph/pull/17271), xie xingguo)

-   mon: mon,option: set default value for mon_dns_srv_name
    ([issue#21204](http://tracker.ceph.com/issues/21204),
    [pr#17539](https://github.com/ceph/ceph/pull/17539), Kefu Chai)

-   mon: mon/OSDMonitor: add location option for \"crush add-bucket\"
    command ([pr#17125](https://github.com/ceph/ceph/pull/17125), xie
    xingguo)

-   mon: mon/OSDMonitor: add \'osd crush
    set-all-straw-buckets-to-straw2\'
    ([pr#18460](https://github.com/ceph/ceph/pull/18460), Sage Weil)

-   mon: mon/OSDMonitor: add plain output for \"crush class ls-osd\"
    command ([pr#17034](https://github.com/ceph/ceph/pull/17034), xie
    xingguo)

-   mon: mon/OSDMonitor: add space after \_\_func\_\_ in log msg
    ([pr#19127](https://github.com/ceph/ceph/pull/19127), Kefu Chai)

-   mon: mon/OSDMonitor: Better prepare_command_pool_set E2BIG error
    message ([pr#19944](https://github.com/ceph/ceph/pull/19944), Brad
    Hubbard)

-   mon: mon/OSDMonitor.cc: fix expected_num_objects interpret error
    ([issue#22530](http://tracker.ceph.com/issues/22530),
    [pr#19651](https://github.com/ceph/ceph/pull/19651), Yang Honggang)

-   mon: mon/OSDMonitor.cc : set erasure-code-profile to \"\" when
    create replicated pools
    ([pr#19673](https://github.com/ceph/ceph/pull/19673), zouaiguo)

-   mon: mon/OSDMonitor: check last_scan_epoch instead when sending
    creates ([issue#20785](http://tracker.ceph.com/issues/20785),
    [pr#17248](https://github.com/ceph/ceph/pull/17248), Kefu Chai)

-   mon: mon/OSDMonitor: clean up cmd \'osd tree-from\'
    ([pr#20839](https://github.com/ceph/ceph/pull/20839), Gu Zhongyan)

-   mon: mon/OSDMonitor: do not send_pg_creates with stale info
    ([issue#20785](http://tracker.ceph.com/issues/20785),
    [pr#17065](https://github.com/ceph/ceph/pull/17065), Kefu Chai)

-   mon: mon/OSDMonitor: error out if setting ruleset-\* ec profile
    property ([pr#17848](https://github.com/ceph/ceph/pull/17848), Sage
    Weil)

-   mon: mon/OSDMonitor: fix improper input/testing range of crush somke
    testing ([pr#17179](https://github.com/ceph/ceph/pull/17179), xie
    xingguo)

-   mon: mon/OSDMonitor: fix \'osd pg temp\' unable to cleanup pg-temp
    ([pr#16892](https://github.com/ceph/ceph/pull/16892), xie xingguo)

-   mon: mon/OSDMonitor: implement \'osd crush ls \<node\>\'
    ([pr#16920](https://github.com/ceph/ceph/pull/16920), Sage Weil)

-   mon: mon/OSDMonitor: kill pending upmap changes too if pool is gone
    ([pr#20704](https://github.com/ceph/ceph/pull/20704), xie xingguo)

-   mon: mon/OSDMonitor: logging non-active osd id when handling osd
    beacon ([pr#21092](https://github.com/ceph/ceph/pull/21092),
    runsisi)

-   mon: mon/OSDMonitor: make \'osd crush rule rename\' idempotent
    ([issue#21162](http://tracker.ceph.com/issues/21162),
    [pr#17329](https://github.com/ceph/ceph/pull/17329), xie xingguo)

-   mon: mon/OSDMonitor: \"osd pool application get\" support
    ([issue#20976](http://tracker.ceph.com/issues/20976),
    [pr#16955](https://github.com/ceph/ceph/pull/16955), xie xingguo)

-   mon: mon/OSDMonitor: txsize should be greater or eq to
    prune_interval - 1
    ([pr#21430](https://github.com/ceph/ceph/pull/21430), Kefu Chai)

-   mon: mon/PGMap: drop DISK LOG column
    ([pr#17617](https://github.com/ceph/ceph/pull/17617), Sage Weil)

-   mon: mon/PGMap: fix \"0 stuck requests are blocked \> 4096 sec\"
    warn ([pr#17099](https://github.com/ceph/ceph/pull/17099), xie
    xingguo)

-   mon: mon/PGMap: nice numbers for \'data\' section of \'ceph df\'
    command ([pr#17368](https://github.com/ceph/ceph/pull/17368), xie
    xingguo)

-   mon: mon/PGMap: Remove unnecessary header
    ([pr#18343](https://github.com/ceph/ceph/pull/18343), Shinobu Kinjo)

-   mon: mon/PGMap: reweight::by_utilization - skip DNE osds
    ([issue#20970](http://tracker.ceph.com/issues/20970),
    [pr#17064](https://github.com/ceph/ceph/pull/17064), xie xingguo)

-   mon: mon/pgmap: update pool nearfull display
    ([pr#17043](https://github.com/ceph/ceph/pull/17043), huanwen ren)

-   mon: more aggressively convert crush rulesets -\> distinct rules
    ([pr#17508](https://github.com/ceph/ceph/pull/17508), John Spray,
    Sage Weil)

-   mon: more constness
    ([pr#17748](https://github.com/ceph/ceph/pull/17748), Kefu Chai)

-   mon: node ls improvement
    ([pr#20820](https://github.com/ceph/ceph/pull/20820), Gu Zhongyan)

-   mon: \'node ls\' mgr support
    ([pr#20711](https://github.com/ceph/ceph/pull/20711), Gu Zhongyan)

-   mon: NULL check of logger before use
    ([pr#18788](https://github.com/ceph/ceph/pull/18788), Amit Kumar)

-   mon,osd: dump \"compression_algorithms\" in \"mon metadata\"
    ([issue#24135](http://tracker.ceph.com/issues/24135),
    [issue#22420](http://tracker.ceph.com/issues/22420),
    [pr#22004](https://github.com/ceph/ceph/pull/22004), Kefu Chai,
    Casey Bodley)

-   mon: osd feature checks with 0 up osds
    ([issue#21471](http://tracker.ceph.com/issues/21471),
    [issue#20751](http://tracker.ceph.com/issues/20751),
    [pr#17831](https://github.com/ceph/ceph/pull/17831), Brad Hubbard,
    Sage Weil)

-   mon: osdmap prune
    ([pr#19331](https://github.com/ceph/ceph/pull/19331), Joao Eduardo
    Luis)

-   mon/OSDMonitor: cleanup: move bufferlist before use
    ([pr#18258](https://github.com/ceph/ceph/pull/18258), Shinobu Kinjo)

-   mon/OSDMonitor: use new style options
    ([pr#18209](https://github.com/ceph/ceph/pull/18209), Kefu Chai)

-   mon: osd/OSDMap.h: toss osd out if it has no more pending states
    ([pr#19642](https://github.com/ceph/ceph/pull/19642), xie xingguo)

-   mon: paxos cleanup
    ([pr#20078](https://github.com/ceph/ceph/pull/20078), huanwen ren)

-   mon/PGMap: let pg_string_state() return boost::optional\<\>
    ([issue#21609](http://tracker.ceph.com/issues/21609),
    [pr#18218](https://github.com/ceph/ceph/pull/18218), Kefu Chai)

-   mon/PGMap: use new-style options and cleanup
    ([pr#18647](https://github.com/ceph/ceph/pull/18647), Kefu Chai)

-   mon: post-luminous cleanup (part 3 of ?)
    ([pr#17607](https://github.com/ceph/ceph/pull/17607), Sage Weil)

-   mon: rate limit on health check update logging
    ([issue#20888](http://tracker.ceph.com/issues/20888),
    [pr#16942](https://github.com/ceph/ceph/pull/16942), John Spray)

-   mon: reenable timer to send digest when paxos is temporarily
    inactive ([issue#22142](http://tracker.ceph.com/issues/22142),
    [pr#19404](https://github.com/ceph/ceph/pull/19404), Jan Fajerski)

-   mon: remove health service
    ([pr#20119](https://github.com/ceph/ceph/pull/20119), Chang Liu)

-   mon: remove_is_write_ready()
    ([pr#19191](https://github.com/ceph/ceph/pull/19191), Kefu Chai)

-   mon: remove pre-luminous compat cruft (2 of many)
    ([pr#17322](https://github.com/ceph/ceph/pull/17322), Sage Weil)

-   mon: remove unused waiting_for_commit
    ([pr#18617](https://github.com/ceph/ceph/pull/18617), Kefu Chai)

-   mon: return directly after health_events_cleanup
    ([pr#16964](https://github.com/ceph/ceph/pull/16964), wang yang)

-   mon: revert mds metadata argument name change
    ([issue#22527](http://tracker.ceph.com/issues/22527),
    [pr#19926](https://github.com/ceph/ceph/pull/19926), Patrick
    Donnelly)

-   mon: show feature flags when printing MonSession
    ([pr#17535](https://github.com/ceph/ceph/pull/17535), Paul Emmerich)

-   mon: some cleanup
    ([pr#17067](https://github.com/ceph/ceph/pull/17067), huanwen ren)

-   mon,tests: vstart: set osd_pool_default_erasure_code_profile in
    initial ceph.conf
    ([pr#21008](https://github.com/ceph/ceph/pull/21008), Mykola Golub)

-   mon: update get_store_prefixes implementations
    ([issue#21534](http://tracker.ceph.com/issues/21534),
    [pr#17940](https://github.com/ceph/ceph/pull/17940), John Spray,
    huanwen ren)

-   mon: update PaxosService::cached_first_committed in
    PaxosService::maybe_trim()
    ([issue#11332](http://tracker.ceph.com/issues/11332),
    [pr#19397](https://github.com/ceph/ceph/pull/19397), Xuehan Xu,
    yupeng chen)

-   mon: use ceph_clock_now if message is self-generated
    ([pr#17311](https://github.com/ceph/ceph/pull/17311), huangjun)

-   mon: warn about using osd new instead of osd create
    ([issue#21023](http://tracker.ceph.com/issues/21023),
    [pr#17242](https://github.com/ceph/ceph/pull/17242), Neha Ojha)

-   msg/async/AsyncConnection: remove legacy feature case handle
    ([pr#18469](https://github.com/ceph/ceph/pull/18469), Haomai Wang)

-   msg/async: avoid referencing the temporary string
    ([pr#20640](https://github.com/ceph/ceph/pull/20640), Kefu Chai)

-   msg/async: batch handle msg_iovlen
    ([pr#18415](https://github.com/ceph/ceph/pull/18415), Jianpeng Ma)

-   msg/async/dpdk: remove xsky copyright and LGPL copying
    ([pr#21121](https://github.com/ceph/ceph/pull/21121), Kefu Chai)

-   msg/async/EventKqueue: assert on OOM
    ([pr#21488](https://github.com/ceph/ceph/pull/21488), Kefu Chai)

-   msg/async: fix ms_dpdk_coremask and ms_dpdk_coremask conflict
    ([pr#18678](https://github.com/ceph/ceph/pull/18678), chunmei)

-   msg/async:fix the incoming parameter type of
    EventCenter::process_events()
    ([pr#20607](https://github.com/ceph/ceph/pull/20607), shangfufei)

-   msg/async misc cleanup
    ([pr#18531](https://github.com/ceph/ceph/pull/18531), Jianpeng Ma)

-   msg/async: misc cleanup
    ([pr#18575](https://github.com/ceph/ceph/pull/18575), Jianpeng Ma)

-   msg/async/rdma: a tiny typo fix
    ([pr#18660](https://github.com/ceph/ceph/pull/18660), Yan Lei)

-   msg/async/rdma: fix a coredump introduced by PR #18053
    ([pr#18204](https://github.com/ceph/ceph/pull/18204), Yan Lei)

-   msg/async/rdma: fix a potential coredump when handling tx_buffers
    under heavy RDMA
    ([pr#18036](https://github.com/ceph/ceph/pull/18036), Yan Lei)

-   msg/async/rdma: fixes crash for multi rados client within one
    process ([pr#16981](https://github.com/ceph/ceph/pull/16981), Alex
    Mikheev, Haomai Wang, Adir Lev)

-   msg/async/rdma: fix Tx buffer leakage that can introduce \"heartbeat
    no reply\" ([pr#18053](https://github.com/ceph/ceph/pull/18053), Yan
    Lei)

-   msg/async/rdma: refactor rx buffer pool allocator
    ([pr#17018](https://github.com/ceph/ceph/pull/17018), Alex Mikheev)

-   msg/async/rdma: unnecessary reinitiliazation of an iterator
    ([pr#18190](https://github.com/ceph/ceph/pull/18190), JustL)

-   msg/async: size of EventCenter::file_events should be greater than
    fd ([issue#23253](http://tracker.ceph.com/issues/23253),
    [pr#20764](https://github.com/ceph/ceph/pull/20764), Yupeng Chen)

-   msg/async: use bitset\<\> to do the popcnt
    ([pr#18681](https://github.com/ceph/ceph/pull/18681), Kefu Chai)

-   msg/async: use device before checking
    ([pr#19738](https://github.com/ceph/ceph/pull/19738), Xiaoyan Li)

-   msg: drop duplicate include
    ([pr#19623](https://github.com/ceph/ceph/pull/19623), /bin/bash)

-   msg: drop the unnecessary polling_stop()
    ([pr#17079](https://github.com/ceph/ceph/pull/17079), Jos Collin)

-   msg: Initialize lkey,bound,port_cnt,num_chunk,gid_idx
    ([pr#17797](https://github.com/ceph/ceph/pull/17797), Amit Kumar)

-   msg: Initializing class members in module msg
    ([pr#17568](https://github.com/ceph/ceph/pull/17568), Amit Kumar)

-   msg: reimplement sigpipe blocking
    ([pr#18105](https://github.com/ceph/ceph/pull/18105), Greg Farnum)

-   msg: remove the ),it\'s redundant
    ([pr#17544](https://github.com/ceph/ceph/pull/17544), linxuhua)

-   msg: resurrect support for !CEPH_FEATURE_MSG_AUTH
    ([pr#19044](https://github.com/ceph/ceph/pull/19044), Ilya Dryomov)

-   msgr: Optimization for connection establishment
    ([pr#16006](https://github.com/ceph/ceph/pull/16006), shangfufei)

-   msg/simple: pass a char for reading from shutdown_rd_fd
    ([pr#19094](https://github.com/ceph/ceph/pull/19094), Kefu Chai)

-   NVMDevice: fix issued caused by #17002
    ([pr#17112](https://github.com/ceph/ceph/pull/17112), Ziye Yang)

-   objclass-sdk: expose \_\_cls_init() to the world
    ([pr#21581](https://github.com/ceph/ceph/pull/21581), Kefu Chai)

-   objecter: minor cleanups
    ([pr#19994](https://github.com/ceph/ceph/pull/19994), runsisi)

-   os/bluestore/bluestore_tool: Move redundant code into one method
    ([pr#19160](https://github.com/ceph/ceph/pull/19160), Shinobu Kinjo)

-   os/bluestore: implement BlueRocksEnv::AreFilesSame()
    ([issue#21842](http://tracker.ceph.com/issues/21842),
    [pr#18392](https://github.com/ceph/ceph/pull/18392), Kefu Chai)

-   os/bluestore: simplify and fix SharedBlob::put()
    ([issue#24211](http://tracker.ceph.com/issues/24211),
    [pr#22170](https://github.com/ceph/ceph/pull/22170), Sage Weil)

-   osd: additional protection for out-of-bounds EC reads
    ([issue#21629](http://tracker.ceph.com/issues/21629),
    [pr#18088](https://github.com/ceph/ceph/pull/18088), Jason Dillaman)

-   osd: add multiple objecter finishers
    ([pr#16521](https://github.com/ceph/ceph/pull/16521), Myoungwon Oh)

-   osd: add num_object_manifest
    ([pr#20690](https://github.com/ceph/ceph/pull/20690), Myoungwon Oh)

-   osd: add numpg_removing metric
    ([pr#18450](https://github.com/ceph/ceph/pull/18450), Sage Weil)

-   osd: add processed_subop_count for cls_cxx_subop_version()
    ([issue#21964](http://tracker.ceph.com/issues/21964),
    [pr#18610](https://github.com/ceph/ceph/pull/18610), Casey Bodley)

-   osd: add scrub week day constraint
    ([pr#18368](https://github.com/ceph/ceph/pull/18368), kungf)

-   osd: adjust osd_min_pg_log_entries
    ([issue#21026](http://tracker.ceph.com/issues/21026),
    [pr#17075](https://github.com/ceph/ceph/pull/17075), J. Eric
    Ivancich)

-   osd: allow FULL_TRY after failsafe
    ([pr#17177](https://github.com/ceph/ceph/pull/17177), Pan Liu)

-   osd: allow PG recovery scheduling preemption
    ([pr#17839](https://github.com/ceph/ceph/pull/17839), Sage Weil)

-   osd: async recovery
    ([pr#19811](https://github.com/ceph/ceph/pull/19811), Neha Ojha)

-   osd: avoid encoding the same log entries repeatedly for different
    peers ([pr#20201](https://github.com/ceph/ceph/pull/20201), Jianpeng
    Ma)

-   osd: avoid the config\'s get_val() overhead on the read path
    ([pr#20217](https://github.com/ceph/ceph/pull/20217), Radoslaw
    Zarzynski)

-   osd: avoid unnecessary ref-counting across
    PrimaryLogPG::get_rw_locks
    ([pr#21028](https://github.com/ceph/ceph/pull/21028), Radoslaw
    Zarzynski)

-   osd: be more precise about our asserts and cases when rebuilding
    missing sets ([issue#20985](http://tracker.ceph.com/issues/20985),
    [pr#17000](https://github.com/ceph/ceph/pull/17000), Greg Farnum)

-   osd: bring in dmclock library changes
    ([pr#16755](https://github.com/ceph/ceph/pull/16755), J. Eric
    Ivancich)

-   osd: bring in latest dmclock library updates
    ([pr#17997](https://github.com/ceph/ceph/pull/17997), J. Eric
    Ivancich)

-   osd: cap snaptrimq_len at 2\^32
    ([pr#21107](https://github.com/ceph/ceph/pull/21107), Kefu Chai)

-   osd: change log level when withholding pg creation
    ([issue#22440](http://tracker.ceph.com/issues/22440),
    [pr#20167](https://github.com/ceph/ceph/pull/20167), Dan van der
    Ster)

-   osd: change op delayed state to \'waiting for scrub\'
    ([pr#19295](https://github.com/ceph/ceph/pull/19295), kungf)

-   osd: Change shard digests to hex like object info digests
    ([pr#21362](https://github.com/ceph/ceph/pull/21362), David Zafman)

-   osd: change the conditional in \_update_calc_stats
    ([pr#13383](https://github.com/ceph/ceph/pull/13383), Zhiqiang Wang)

-   osd: check feature bits when encoding objectstore_perf_stat_t
    ([pr#20378](https://github.com/ceph/ceph/pull/20378), Kefu Chai)

-   osd: clean up dup index logic; maintain index flag logic in fewer
    places ([pr#16829](https://github.com/ceph/ceph/pull/16829), J. Eric
    Ivancich)

-   osd: clean up pre-luminous compat cruft (part 1 of many)
    ([pr#17247](https://github.com/ceph/ceph/pull/17247), Sage Weil)

-   osd: cleanups ([pr#17753](https://github.com/ceph/ceph/pull/17753),
    Kefu Chai)

-   osdc/Objecter: using coarse_mono instead
    ([pr#18473](https://github.com/ceph/ceph/pull/18473), Haomai Wang)

-   osdc/Objector: use std::shared_mutex instead of boost::shared_mutex
    ([issue#23910](http://tracker.ceph.com/issues/23910),
    [pr#21702](https://github.com/ceph/ceph/pull/21702), Abhishek
    Lekshmanan)

-   osd: correct several spell errors in comments
    ([pr#21064](https://github.com/ceph/ceph/pull/21064), songweibin)

-   osdc: Remove a bit too redundant public label
    ([pr#19466](https://github.com/ceph/ceph/pull/19466), Shinobu Kinjo)

-   osdc: self-managed snapshot helper should catch decode exception
    ([issue#24103](http://tracker.ceph.com/issues/24103),
    [issue#24000](http://tracker.ceph.com/issues/24000),
    [pr#21958](https://github.com/ceph/ceph/pull/21958), Jason Dillaman)

-   osd: debug dispatch_context cases where queries not sent
    ([pr#20917](https://github.com/ceph/ceph/pull/20917), Sage Weil)

-   osd: Deleting dead code PrimaryLogPG.cc
    ([pr#17339](https://github.com/ceph/ceph/pull/17339), Amit Kumar)

-   osd: don\'t crash on empty snapset
    ([issue#23851](http://tracker.ceph.com/issues/23851),
    [pr#21058](https://github.com/ceph/ceph/pull/21058), Mykola Golub,
    Igor Fedotov)

-   osd: Don\'t include same header twice
    ([pr#18319](https://github.com/ceph/ceph/pull/18319), Shinobu Kinjo)

-   osd: Don\'t initialze pointers by NULL or 0
    ([pr#18311](https://github.com/ceph/ceph/pull/18311), Shinobu Kinjo)

-   osd: don\'t memcpy hobject_t in PrimaryLogPG::close_op_ctx()
    ([pr#21029](https://github.com/ceph/ceph/pull/21029), Radoslaw
    Zarzynski)

-   osd: don\'t process ostream strings when not debugging
    ([pr#20298](https://github.com/ceph/ceph/pull/20298), Mark Nelson)

-   osd: drop redundant comment
    ([pr#20347](https://github.com/ceph/ceph/pull/20347), songweibin)

-   osd: Drop the unused code in OSD::\_collect_metadata
    ([pr#17131](https://github.com/ceph/ceph/pull/17131), Luo Kexue)

-   osd: drop unused osd_disk_tp related options
    ([pr#21339](https://github.com/ceph/ceph/pull/21339), Gu Zhongyan)

-   osd: eliminate ineffective container operations
    ([pr#19099](https://github.com/ceph/ceph/pull/19099), Igor Fedotov)

-   osd: enumerate device names in a simple way
    ([pr#18453](https://github.com/ceph/ceph/pull/18453), Sage Weil)

-   osd: exit(1) directly without lock if init fails
    ([pr#16647](https://github.com/ceph/ceph/pull/16647), Kefu Chai)

-   osd: fast dispatch of peering events and pg_map + osd sharded wq
    refactor ([pr#19973](https://github.com/ceph/ceph/pull/19973), Sage
    Weil)

-   osd: fine-grained statistics of logical object space usage
    ([pr#15199](https://github.com/ceph/ceph/pull/15199), xie xingguo)

-   osd: Fix assert when checking missing version
    ([issue#21218](http://tracker.ceph.com/issues/21218),
    [pr#20410](https://github.com/ceph/ceph/pull/20410), David Zafman)

-   osd: fix a valgrind issue (conditional jump depends on uninitialized
    value) ([issue#22641](http://tracker.ceph.com/issues/22641),
    [pr#19874](https://github.com/ceph/ceph/pull/19874), Myoungwon Oh)

-   osd: fix bug which cause can\'t erase OSDShardPGSlot
    ([pr#21771](https://github.com/ceph/ceph/pull/21771), Jianpeng Ma)

-   osd: fix build_initial_pg_history
    ([issue#21203](http://tracker.ceph.com/issues/21203),
    [pr#17423](https://github.com/ceph/ceph/pull/17423), w11979, Sage
    Weil)

-   osd: fix crash caused by divide by zero in heartbeat code
    ([pr#21373](https://github.com/ceph/ceph/pull/21373), Piotr Dałek)

-   osd: fix dpdk memzon mz_name setting issue
    ([pr#19809](https://github.com/ceph/ceph/pull/19809), chunmei Liu)

-   osd: fix dpdk runtime issue based on spdk/dpdk libarary
    ([pr#19559](https://github.com/ceph/ceph/pull/19559), chunmei Liu)

-   osd: fix dpdk worker references issue
    ([pr#19886](https://github.com/ceph/ceph/pull/19886), chunmei Liu)

-   osd: Fixes for osd_scrub_during_recovery handling
    ([issue#18206](http://tracker.ceph.com/issues/18206),
    [pr#17039](https://github.com/ceph/ceph/pull/17039), David Zafman)

-   osd: fix out of order caused by letting old msg from down osd be
    processed ([issue#22570](http://tracker.ceph.com/issues/22570),
    [pr#19796](https://github.com/ceph/ceph/pull/19796), Mingxin Liu)

-   osd: fix \_process handling for pg vs slot race
    ([pr#21745](https://github.com/ceph/ceph/pull/21745), Sage Weil)

-   osd: fix recovery reservation bugs, and implement remote reservation
    preemption ([pr#18485](https://github.com/ceph/ceph/pull/18485),
    Sage Weil)

-   osd: fix replica/backfill target handling of REJECT
    ([issue#21613](http://tracker.ceph.com/issues/21613),
    [pr#18070](https://github.com/ceph/ceph/pull/18070), Sage Weil)

-   osd: fix reqid assignment for reply messages in OpRequest
    ([pr#17060](https://github.com/ceph/ceph/pull/17060), Yingxin Cheng)

-   osd: fix s390x build failure
    ([issue#23238](http://tracker.ceph.com/issues/23238),
    [pr#20969](https://github.com/ceph/ceph/pull/20969), Nathan Cutler)

-   osd: fix typos and some cleanups
    ([pr#19211](https://github.com/ceph/ceph/pull/19211), Enming Zhang)

-   osd: fix unordered read bug (for chunked object)
    ([issue#22369](http://tracker.ceph.com/issues/22369),
    [pr#19464](https://github.com/ceph/ceph/pull/19464), Myoungwon Oh)

-   osd: fix waiting_for_peered vs flushing
    ([issue#21407](http://tracker.ceph.com/issues/21407),
    [pr#17759](https://github.com/ceph/ceph/pull/17759), Sage Weil)

-   osd: flush operations for chunked objects
    ([pr#19294](https://github.com/ceph/ceph/pull/19294), Myoungwon Oh)

-   osd: generalize queueing and lock interface for OpWq
    ([pr#16030](https://github.com/ceph/ceph/pull/16030), Myoungwon Oh,
    Kefu Chai, Samuel Just)

-   osd: get loadavg per cpu for scrub load threshold check
    ([pr#17718](https://github.com/ceph/ceph/pull/17718), kungf)

-   osd: get rid off extent map in object_info
    ([pr#19616](https://github.com/ceph/ceph/pull/19616), Igor Fedotov)

-   osd: hold lock while accessing recovery_needs_sleep
    ([issue#21566](http://tracker.ceph.com/issues/21566),
    [pr#18022](https://github.com/ceph/ceph/pull/18022), Neha Ojha)

-   osd: Improve recovery stat handling by using peer_missing and
    missing_loc info
    ([issue#22837](http://tracker.ceph.com/issues/22837),
    [pr#20220](https://github.com/ceph/ceph/pull/20220), Sage Weil,
    David Zafman)

-   osd: Improve size scrub error handling and ignore system attrs in
    xattr checking ([issue#20243](http://tracker.ceph.com/issues/20243),
    [issue#18836](http://tracker.ceph.com/issues/18836),
    [pr#16407](https://github.com/ceph/ceph/pull/16407), David Zafman)

-   osd: include front_iface+back_iface in metadata
    ([issue#20956](http://tracker.ceph.com/issues/20956),
    [pr#16941](https://github.com/ceph/ceph/pull/16941), John Spray)

-   osd: Initialization of data members
    ([pr#17691](https://github.com/ceph/ceph/pull/17691), Amit Kumar)

-   osd: Initialization of pointer cls
    ([pr#17115](https://github.com/ceph/ceph/pull/17115), amitkuma)

-   osd: Initializing start_offset,last_offset,offset
    ([pr#19333](https://github.com/ceph/ceph/pull/19333), Amit Kumar)

-   osd: initial minimal efforts to clean up PG interface
    ([pr#17708](https://github.com/ceph/ceph/pull/17708), Sage Weil)

-   osd: introduce sub-chunks to erasure code plugin interface
    ([issue#19278](http://tracker.ceph.com/issues/19278),
    [pr#15193](https://github.com/ceph/ceph/pull/15193), Myna Vajha)

-   osd: kill snapdirs
    ([pr#17579](https://github.com/ceph/ceph/pull/17579), Sage Weil)

-   osd: Make dmclock\'s anticipation timeout be configurable
    ([pr#18827](https://github.com/ceph/ceph/pull/18827), Taewoong Kim)

-   osd: make operations on ReplicatedBackend::in_progress_ops more
    effective ([pr#19035](https://github.com/ceph/ceph/pull/19035), Igor
    Fedotov)

-   osd: make PG::\*Force\* event structs public
    ([pr#21312](https://github.com/ceph/ceph/pull/21312), Willem Jan
    Withagen)

-   osd: make scrub no deadline when max interval is zero
    ([pr#18354](https://github.com/ceph/ceph/pull/18354), kungf)

-   osd: make scrub right now when pg stats_invalid is true
    ([pr#17884](https://github.com/ceph/ceph/pull/17884), kungf)

-   osd: make scrub wait for ec read/modify/writes to apply
    ([issue#23339](http://tracker.ceph.com/issues/23339),
    [pr#20944](https://github.com/ceph/ceph/pull/20944), Sage Weil)

-   osd: make snapmapper warn+clean up instead of assert
    ([issue#22752](http://tracker.ceph.com/issues/22752),
    [pr#20040](https://github.com/ceph/ceph/pull/20040), Sage Weil)

-   osd: make stat_bytes and stat_bytes_used counters PRIO_USEFUL
    ([issue#21981](http://tracker.ceph.com/issues/21981),
    [pr#18637](https://github.com/ceph/ceph/pull/18637), Yao Zongyou)

-   osd: make the PG\'s SORTBITWISE assert a more generous shutdown
    ([issue#20416](http://tracker.ceph.com/issues/20416),
    [pr#18047](https://github.com/ceph/ceph/pull/18047), Greg Farnum)

-   osd: Making use of find to reduce computational complexity
    ([pr#19732](https://github.com/ceph/ceph/pull/19732), Shinobu Kinjo)

-   osd: migrate PGLOG\_\* macros to constexpr
    ([issue#20811](http://tracker.ceph.com/issues/20811),
    [pr#19352](https://github.com/ceph/ceph/pull/19352), Jesse
    Williamson)

-   osd: minor optimizations for op wq
    ([pr#17704](https://github.com/ceph/ceph/pull/17704), Sage Weil, J.
    Eric Ivancich)

-   osd: min_pg_log_entries == max == pg_log_dups_tracked
    ([pr#20394](https://github.com/ceph/ceph/pull/20394), Sage Weil)

-   osd: misc cleanups
    ([pr#17430](https://github.com/ceph/ceph/pull/17430), songweibin)

-   osd: miscellaneous cleanups
    ([pr#21431](https://github.com/ceph/ceph/pull/21431), songweibin)

-   osd: more debugging for snapmapper bug
    ([issue#21557](http://tracker.ceph.com/issues/21557),
    [pr#19366](https://github.com/ceph/ceph/pull/19366), Sage Weil)

-   osd: object added to missing set for backfill, but is not in
    recovering, error!
    ([issue#18162](http://tracker.ceph.com/issues/18162),
    [pr#18145](https://github.com/ceph/ceph/pull/18145), David Zafman)

-   osd: only exit if \*latest\* map(s) say we are destroyed
    ([issue#22673](http://tracker.ceph.com/issues/22673),
    [pr#19988](https://github.com/ceph/ceph/pull/19988), Sage Weil)

-   osd: Only scan for omap corruption once
    ([issue#21328](http://tracker.ceph.com/issues/21328),
    [pr#17705](https://github.com/ceph/ceph/pull/17705), David Zafman)

-   osd,os,io: Initializing C_ProxyChunkRead members,queue,request
    ([pr#19336](https://github.com/ceph/ceph/pull/19336), amitkuma)

-   osd: pass ops_blocked_by_scrub() to requeue_scrub()
    ([pr#20319](https://github.com/ceph/ceph/pull/20319), Kefu Chai)

-   osd: pass pool options to ObjectStore on pg create
    ([issue#22419](http://tracker.ceph.com/issues/22419),
    [pr#19486](https://github.com/ceph/ceph/pull/19486), Sage Weil)

-   osd/PG: fix clang build vs private state events
    ([pr#18217](https://github.com/ceph/ceph/pull/18217), Sage Weil)

-   osd/PG: handle flushed event directly
    ([pr#19441](https://github.com/ceph/ceph/pull/19441), wumingqiao)

-   osd/PrimaryLogPG: derr when object size becomes over
    osd_max_object_size
    ([pr#19049](https://github.com/ceph/ceph/pull/19049), Shinobu Kinjo)

-   osd: process \_scan_snaps() with all snapshots with head
    ([issue#22881](http://tracker.ceph.com/issues/22881),
    [issue#23909](http://tracker.ceph.com/issues/23909),
    [pr#21546](https://github.com/ceph/ceph/pull/21546), David Zafman)

-   osd: publish osdmap to OSDService before starting wq threads
    ([issue#21977](http://tracker.ceph.com/issues/21977),
    [pr#21623](https://github.com/ceph/ceph/pull/21623), Sage Weil)

-   osd: pull latest dmclock subtree
    ([pr#19345](https://github.com/ceph/ceph/pull/19345), J. Eric
    Ivancich)

-   osd: put peering events in main sharded wq
    ([pr#18752](https://github.com/ceph/ceph/pull/18752), Sage Weil)

-   osd: put pg removal in op_wq
    ([pr#19433](https://github.com/ceph/ceph/pull/19433), Sage Weil)

-   osd: reduce all_info map find to get primary
    ([pr#19425](https://github.com/ceph/ceph/pull/19425), kungf)

-   osd: refcount for manifest object (redirect, chunked)
    ([pr#19935](https://github.com/ceph/ceph/pull/19935), Myoungwon Oh)

-   osd: remove cost from mclock op queues; cost not handled well in
    dmclock ([pr#21428](https://github.com/ceph/ceph/pull/21428), J.
    Eric Ivancich)

-   osd: Remove double space
    ([pr#19296](https://github.com/ceph/ceph/pull/19296), Shinobu Kinjo)

-   osd: remove duplicated \"commit_queued_for_journal_write\" in
    OpTracker ([issue#23440](http://tracker.ceph.com/issues/23440),
    [pr#21018](https://github.com/ceph/ceph/pull/21018), ashitakasam)

-   osd: remove duplicated function ec_pool in pg_pool_t
    ([pr#18059](https://github.com/ceph/ceph/pull/18059), Chang Liu)

-   osd: Remove redundant local variable declaration
    ([pr#19812](https://github.com/ceph/ceph/pull/19812), Shinobu Kinjo)

-   osd: Remove unnecessary headers
    ([pr#19735](https://github.com/ceph/ceph/pull/19735), Shinobu Kinjo)

-   osd: remove unused ReplicatedBackend::objects_read_async()
    ([pr#18779](https://github.com/ceph/ceph/pull/18779), Kefu Chai)

-   osd: remove unused variable in do_proxy_write
    ([pr#17391](https://github.com/ceph/ceph/pull/17391), Myoungwon Oh)

-   osd: replace mclock subop opclass w/ rep_op opclass; combine
    duplicated code
    ([pr#18194](https://github.com/ceph/ceph/pull/18194), J. Eric
    Ivancich)

-   osd: replace vectors_equal() with operator==(vector\<\>, vector\<\>)
    ([pr#18064](https://github.com/ceph/ceph/pull/18064), Kefu Chai)

-   osd: request new map from PG when needed
    ([issue#21428](http://tracker.ceph.com/issues/21428),
    [pr#17795](https://github.com/ceph/ceph/pull/17795), Josh Durgin)

-   osd: resend osd_pgtemp if it\'s not acked
    ([issue#23610](http://tracker.ceph.com/issues/23610),
    [pr#21310](https://github.com/ceph/ceph/pull/21310), Kefu Chai)

-   osd: Revert use of dmclock message feature bit since not yet
    finalized ([pr#21398](https://github.com/ceph/ceph/pull/21398), J.
    Eric Ivancich)

-   osd,rgw,librbd: SCA fixes
    ([pr#18495](https://github.com/ceph/ceph/pull/18495), Danny Al-Gaaf)

-   osd: set min_version to newest version in maybe_force_recovery
    ([pr#17752](https://github.com/ceph/ceph/pull/17752), Xinze Chi)

-   osd: Sign in early SIGHUP signal
    ([issue#22746](http://tracker.ceph.com/issues/22746),
    [pr#19958](https://github.com/ceph/ceph/pull/19958), huanwen ren)

-   osd: silence maybe-uninitialized false positives
    ([pr#19820](https://github.com/ceph/ceph/pull/19820), Yao Zongyou)

-   osd: silence warnings from -Wsign-compare
    ([pr#17872](https://github.com/ceph/ceph/pull/17872), Jos Collin)

-   osd: skip dumping logical devices
    ([pr#20740](https://github.com/ceph/ceph/pull/20740), songweibin)

-   osd: speed up get_key_name
    ([issue#21026](http://tracker.ceph.com/issues/21026),
    [pr#17071](https://github.com/ceph/ceph/pull/17071), J. Eric
    Ivancich)

-   osd: s/random_shuffle()/shuffle()/
    ([pr#19872](https://github.com/ceph/ceph/pull/19872), Willem Jan
    Withagen, Kefu Chai, Greg Farnum)

-   osd: subscribe osdmaps if any pending pgs
    ([issue#22113](http://tracker.ceph.com/issues/22113),
    [pr#18916](https://github.com/ceph/ceph/pull/18916), Kefu Chai)

-   osd: subscribe to new osdmap while waiting_for_healthy
    ([issue#21121](http://tracker.ceph.com/issues/21121),
    [pr#17244](https://github.com/ceph/ceph/pull/17244), Sage Weil)

-   osd: support class method whitelisting within caps
    ([pr#19786](https://github.com/ceph/ceph/pull/19786), Jason
    Dillaman)

-   osd: treat successful and erroroneous writes the same for log
    trimming ([issue#22050](http://tracker.ceph.com/issues/22050),
    [pr#20827](https://github.com/ceph/ceph/pull/20827), Josh Durgin)

-   osd: two cleanups
    ([pr#20830](https://github.com/ceph/ceph/pull/20830), songweibin)

-   osd: update dmclock library w git subtree pull
    ([pr#17737](https://github.com/ceph/ceph/pull/17737), J. Eric
    Ivancich)

-   osd: update info only if new_interval
    ([pr#17437](https://github.com/ceph/ceph/pull/17437), Kefu Chai)

-   osd: update store with options after pg is created
    ([issue#22419](http://tracker.ceph.com/issues/22419),
    [pr#20044](https://github.com/ceph/ceph/pull/20044), Kefu Chai)

-   osd: use dmclock library client_info_f function dynamically
    ([pr#17063](https://github.com/ceph/ceph/pull/17063), bspark)

-   osd: use existing osd_required variable for messenger policy
    ([pr#20223](https://github.com/ceph/ceph/pull/20223), Yan Jun)

-   osd: use prefix increment for non trivial iterator
    ([pr#19097](https://github.com/ceph/ceph/pull/19097), Kefu Chai)

-   osd: Use specializations, typedefs instead
    ([pr#19354](https://github.com/ceph/ceph/pull/19354), Shinobu Kinjo)

-   osd: Warn about objects with too many omap entries
    ([pr#16332](https://github.com/ceph/ceph/pull/16332), Brad Hubbard)

-   os/filestore/HashIndex.h: fixed a typo in comment
    ([pr#17685](https://github.com/ceph/ceph/pull/17685), yaoguotao)

-   os: Initializing uninitialized members aio_info
    ([pr#17066](https://github.com/ceph/ceph/pull/17066), amitkuma)

-   os: Removing dead code from LFNIndex.cc
    ([pr#17297](https://github.com/ceph/ceph/pull/17297), Amit Kumar)

-   prometheus: Handle the TIME perf counter type metrics
    ([pr#21749](https://github.com/ceph/ceph/pull/21749), Boris Ranto)

-   pybind: add return note in rbd.pyx
    ([pr#21768](https://github.com/ceph/ceph/pull/21768), Zheng Yin)

-   pybind/ceph_daemon: expand the order of magnitude of
    ([issue#23962](http://tracker.ceph.com/issues/23962),
    [pr#21836](https://github.com/ceph/ceph/pull/21836), Guan yunfei)

-   pybind: fix chart size become bigger when refresh
    ([issue#20746](http://tracker.ceph.com/issues/20746),
    [pr#16857](https://github.com/ceph/ceph/pull/16857), Yixing Yan)

-   pybind: mgr/dashboard: fix rbd\'s pool sub menu
    ([pr#16774](https://github.com/ceph/ceph/pull/16774), yanyx)

-   pybind,rbd: pybind/rbd: support open the image by image_id
    ([pr#19361](https://github.com/ceph/ceph/pull/19361), songweibin)

-   pybind: remove unused get_ceph_version()
    ([pr#17727](https://github.com/ceph/ceph/pull/17727), Kefu Chai)

-   qa: add cbt repo parameter
    ([pr#18543](https://github.com/ceph/ceph/pull/18543), Neha Ojha)

-   qa: Add cephmetrics suite
    ([pr#18451](https://github.com/ceph/ceph/pull/18451), Zack Cerza)

-   qa: add upgrade/luminous-x suite
    ([pr#17160](https://github.com/ceph/ceph/pull/17160), Yuri
    Weinstein)

-   qa/crontab: run the perf-basic suite every day
    ([pr#21252](https://github.com/ceph/ceph/pull/21252), Neha Ojha)

-   qa: Decreased amount of jobs on master, kraken, luminous runs
    ([pr#17069](https://github.com/ceph/ceph/pull/17069), Yuri
    Weinstein)

-   qa: install collectl with cbt task
    ([pr#19324](https://github.com/ceph/ceph/pull/19324), Neha Ojha)

-   qa: mimic-dev1 backports to avoid trusty nodes
    ([pr#19600](https://github.com/ceph/ceph/pull/19600), Kefu Chai)

-   qa: preserve cbt task results
    ([pr#19364](https://github.com/ceph/ceph/pull/19364), Neha Ojha)

-   qa: qa/ceph-disk: enlarge the simulated SCSI disk
    ([issue#22136](http://tracker.ceph.com/issues/22136),
    [pr#19199](https://github.com/ceph/ceph/pull/19199), Kefu Chai)

-   qa/suites/perf-basic: add desc regarding test machines
    ([pr#21183](https://github.com/ceph/ceph/pull/21183), Neha Ojha)

-   qa/suites/rados/multimon/tasks/mon_lock_with_skew: whitelist PG
    ([pr#17004](https://github.com/ceph/ceph/pull/17004), Sage Weil)

-   qa/suites/rados/perf: add optimized settings
    ([pr#17786](https://github.com/ceph/ceph/pull/17786), Neha Ojha)

-   qa/suites/rados/perf: add workloads
    ([pr#18573](https://github.com/ceph/ceph/pull/18573), Neha Ojha)

-   qa/suites/rados/verify/validater/valgrind: whitelist PG
    ([pr#17005](https://github.com/ceph/ceph/pull/17005), Sage Weil)

-   qa/suites/upgrade/jewel-x/parallel: tolerate laggy mgr
    ([pr#17227](https://github.com/ceph/ceph/pull/17227), Sage Weil)

-   qa/suites/upgrade/kraken-x: fixes
    ([pr#16881](https://github.com/ceph/ceph/pull/16881), Sage Weil)

-   qa/suites/upgrade/luminous-x fixes
    ([pr#22101](https://github.com/ceph/ceph/pull/22101), Sage Weil)

-   qa/tests - Added options to use both cases: mon.a and installer.0
    ([pr#19745](https://github.com/ceph/ceph/pull/19745), Yuri
    Weinstein)

-   qa/tests - Fixed typo in crontab entry
    ([pr#21482](https://github.com/ceph/ceph/pull/21482), Yuri
    Weinstein)

-   qa/tests: fixed typo
    ([pr#21728](https://github.com/ceph/ceph/pull/21728), Yuri
    Weinstein)

-   qa/tests - minor clean ups and made perf-suite run 3 times, so we
    can... ([pr#21309](https://github.com/ceph/ceph/pull/21309), Yuri
    Weinstein)

-   qa/tests - one more typo fixed :(
    ([pr#21483](https://github.com/ceph/ceph/pull/21483), Yuri
    Weinstein)

-   qa/tests: removed rest suite from the mix
    ([pr#21743](https://github.com/ceph/ceph/pull/21743), Yuri
    Weinstein)

-   qa: wait longer for osd to flush pg stats
    ([issue#24321](http://tracker.ceph.com/issues/24321),
    [pr#22288](https://github.com/ceph/ceph/pull/22288), Kefu Chai)

-   qa/workunits/ceph-disk: \--no-mon-config
    ([pr#21956](https://github.com/ceph/ceph/pull/21956), Kefu Chai)

-   rados: make ceph_perf_msgr_client work for multiple jobs
    ([issue#22103](http://tracker.ceph.com/issues/22103),
    [pr#18877](https://github.com/ceph/ceph/pull/18877), Jeegn Chen)

-   rbd: add deep cp CLI method
    ([pr#19996](https://github.com/ceph/ceph/pull/19996), songweibin)

-   rbd: add group rename methods
    ([issue#22981](http://tracker.ceph.com/issues/22981),
    [pr#20577](https://github.com/ceph/ceph/pull/20577), songweibin)

-   rbd: add notrim option to rbd map
    ([pr#21056](https://github.com/ceph/ceph/pull/21056), Hitoshi Kamei)

-   rbd: add parent info when moving child into trash bin
    ([pr#19280](https://github.com/ceph/ceph/pull/19280), songweibin)

-   rbd: adjusted \"lock list\" JSON and XML formatted output
    ([pr#19900](https://github.com/ceph/ceph/pull/19900), Jason
    Dillaman)

-   rbd: adjusted \"showmapped\" JSON and XML formatted output
    ([pr#19937](https://github.com/ceph/ceph/pull/19937), Mykola Golub)

-   rbd: allow remove all unprotected snapshots
    ([issue#23126](http://tracker.ceph.com/issues/23126),
    [pr#20608](https://github.com/ceph/ceph/pull/20608), songweibin)

-   rbd: allow trash rm/purge when pool quota is full used
    ([pr#20697](https://github.com/ceph/ceph/pull/20697), songweibin)

-   rbd: backport of mimic bug fixes
    ([issue#24009](http://tracker.ceph.com/issues/24009),
    [issue#24008](http://tracker.ceph.com/issues/24008),
    [pr#21930](https://github.com/ceph/ceph/pull/21930), Jason Dillaman)

-   rbd: check if an image is already mapped before rbd map
    ([issue#20580](http://tracker.ceph.com/issues/20580),
    [pr#16517](https://github.com/ceph/ceph/pull/16517), Jing Li)

-   rbd: children list should support snapshot id optional
    ([issue#23399](http://tracker.ceph.com/issues/23399),
    [pr#20966](https://github.com/ceph/ceph/pull/20966), Jason Dillaman)

-   rbd: cleanup handling of IEC byte units
    ([pr#21564](https://github.com/ceph/ceph/pull/21564), Jason
    Dillaman)

-   rbd: clean up warnings when mirror commands used on non-setup pool
    ([issue#21319](http://tracker.ceph.com/issues/21319),
    [pr#17636](https://github.com/ceph/ceph/pull/17636), Jason Dillaman)

-   rbd: cls/journal: ensure tags are properly expired
    ([issue#21960](http://tracker.ceph.com/issues/21960),
    [pr#18604](https://github.com/ceph/ceph/pull/18604), Jason Dillaman)

-   rbd: cls/journal: fixed possible infinite loop in expire_tags
    ([issue#21956](http://tracker.ceph.com/issues/21956),
    [pr#18592](https://github.com/ceph/ceph/pull/18592), Jason Dillaman)

-   rbd: cls/journal: possible infinite loop within tag_list class
    method ([issue#21771](http://tracker.ceph.com/issues/21771),
    [pr#18270](https://github.com/ceph/ceph/pull/18270), Jason Dillaman)

-   rbd: cls/rbd: group_image_list incorrectly flagged as RW
    ([issue#23388](http://tracker.ceph.com/issues/23388),
    [pr#20939](https://github.com/ceph/ceph/pull/20939), Jason Dillaman)

-   rbd: cls/rbd: metadata_list not honoring max_return parameter
    ([issue#21247](http://tracker.ceph.com/issues/21247),
    [pr#17499](https://github.com/ceph/ceph/pull/17499), Jason Dillaman)

-   rbd: cls/rbd: Silence gcc7 maybe-uninitialized warning
    ([pr#18504](https://github.com/ceph/ceph/pull/18504), Brad Hubbard)

-   rbd: common/options,librbd/Utils: refactor RBD feature validation
    ([pr#20014](https://github.com/ceph/ceph/pull/20014), Sage Weil)

-   rbd: disk usage on empty pool no longer returns an error message
    ([issue#22200](http://tracker.ceph.com/issues/22200),
    [pr#19045](https://github.com/ceph/ceph/pull/19045), Jason Dillaman)

-   rbd: do not show title if there is no group snapshot
    ([pr#20311](https://github.com/ceph/ceph/pull/20311), songweibin)

-   rbd: don\'t overwrite the error code from the remove action
    ([pr#20481](https://github.com/ceph/ceph/pull/20481), Jason
    Dillaman)

-   rbd: drop unnecessary using declaration, etc
    ([pr#19005](https://github.com/ceph/ceph/pull/19005), Shinobu Kinjo)

-   rbd: eager-thick provisioning support
    ([pr#18317](https://github.com/ceph/ceph/pull/18317), Hitoshi Kamei)

-   rbd: export/import image-meta when we export/import an image
    ([pr#17134](https://github.com/ceph/ceph/pull/17134), PCzhangPC)

-   rbd: filter out UserSnapshotNamespace in do_disk_usage
    ([pr#20532](https://github.com/ceph/ceph/pull/20532), songweibin)

-   rbd: fix crash during map when \"rw\" option is specified
    ([issue#21808](http://tracker.ceph.com/issues/21808),
    [pr#18313](https://github.com/ceph/ceph/pull/18313), Peter Keresztes
    Schmidt)

-   rbd: fix logically dead code in function list_process_image
    ([pr#16971](https://github.com/ceph/ceph/pull/16971), Luo Kexue)

-   rbd: fix rbd children listing when child is in trash
    ([issue#21893](http://tracker.ceph.com/issues/21893),
    [pr#18483](https://github.com/ceph/ceph/pull/18483), songweibin)

-   rbd: fix thread_offsets calculation of rbd bench
    ([pr#20590](https://github.com/ceph/ceph/pull/20590), Hitoshi Kamei)

-   rbd: group misc cleanup and update rbd man page
    ([pr#20199](https://github.com/ceph/ceph/pull/20199), songweibin)

-   rbd: group snapshot rename
    ([pr#12431](https://github.com/ceph/ceph/pull/12431), Victor
    Denisov)

-   rbd: implement image qos in tokenbucket algorithm
    ([pr#17032](https://github.com/ceph/ceph/pull/17032), Dongsheng
    Yang)

-   rbd: import with option \--export-format 2 fails to protect snapshot
    ([issue#23038](http://tracker.ceph.com/issues/23038),
    [pr#20613](https://github.com/ceph/ceph/pull/20613), songweibin)

-   rbd: improve \'import-diff\' corrupt input error messages
    ([issue#18844](http://tracker.ceph.com/issues/18844),
    [pr#21249](https://github.com/ceph/ceph/pull/21249), Jason Dillaman)

-   rbd: Initializing m_finalize_ctx
    ([pr#17563](https://github.com/ceph/ceph/pull/17563), Amit Kumar)

-   rbd: introduce commands of \"image-meta ls/rm\"
    ([pr#16591](https://github.com/ceph/ceph/pull/16591), PCzhangPC)

-   rbd: journal: limit number of appends sent in one librados op
    ([issue#23526](http://tracker.ceph.com/issues/23526),
    [pr#21157](https://github.com/ceph/ceph/pull/21157), Mykola Golub)

-   rbd: journal: trivial cleanup
    ([pr#19317](https://github.com/ceph/ceph/pull/19317), Shinobu Kinjo)

-   rbd: krbd: include sys/sysmacros.h for major, minor and makedev
    ([pr#20773](https://github.com/ceph/ceph/pull/20773), Ilya Dryomov)

-   rbd: krbd: rewrite \"already mapped\" code
    ([pr#17638](https://github.com/ceph/ceph/pull/17638), Ilya Dryomov)

-   rbd: librados/snap_set_diff: don\'t assert on empty snapset
    ([pr#20648](https://github.com/ceph/ceph/pull/20648), Mykola Golub)

-   rbd: librbd: create+truncate for whole-object layered discards
    ([issue#23285](http://tracker.ceph.com/issues/23285),
    [pr#20809](https://github.com/ceph/ceph/pull/20809), Ilya Dryomov)

-   rbd: librbd: make rename request complete with filtered code
    ([issue#23068](http://tracker.ceph.com/issues/23068),
    [pr#20507](https://github.com/ceph/ceph/pull/20507), Mykola Golub)

-   rbd: librbd misc cleanup
    ([pr#18419](https://github.com/ceph/ceph/pull/18419), Jianpeng Ma)

-   rbd: librbd: skip head object map update when deep copying object
    beyond image size
    ([pr#21586](https://github.com/ceph/ceph/pull/21586), Mykola Golub)

-   rbd: librbd: sync flush should re-use existing async flush logic
    ([pr#18403](https://github.com/ceph/ceph/pull/18403), Jason
    Dillaman)

-   rbd: librbd,test: address coverity false positives
    ([pr#17825](https://github.com/ceph/ceph/pull/17825), Amit Kumar)

-   rbd: mimic: librbd: deep copy optionally support flattening cloned
    image ([issue#22787](http://tracker.ceph.com/issues/22787),
    [pr#22038](https://github.com/ceph/ceph/pull/22038), Mykola Golub)

-   rbd: mimic: rbd-mirror: optionally support active/active replication
    ([pr#22105](https://github.com/ceph/ceph/pull/22105), Jason
    Dillaman)

-   rbd: mimic: rbd-mirror: potential deadlock when running asok
    \'flush\' command
    ([issue#24141](http://tracker.ceph.com/issues/24141),
    [pr#22039](https://github.com/ceph/ceph/pull/22039), Mykola Golub)

-   rbd-mirror: additional thrasher testing
    ([pr#21697](https://github.com/ceph/ceph/pull/21697), Jason
    Dillaman)

-   rbd-mirror: clean up spurious error log messages
    ([issue#21961](http://tracker.ceph.com/issues/21961),
    [pr#18601](https://github.com/ceph/ceph/pull/18601), Jason Dillaman)

-   rbd-mirror: cluster watcher should ensure it has latest OSD map
    ([issue#22461](http://tracker.ceph.com/issues/22461),
    [pr#19550](https://github.com/ceph/ceph/pull/19550), Jason Dillaman)

-   rbd-mirror: ensure unique service daemon name is utilized
    ([pr#19492](https://github.com/ceph/ceph/pull/19492), Jason
    Dillaman)

-   rbd-mirror: fix potential infinite loop when formatting status
    message ([issue#22932](http://tracker.ceph.com/issues/22932),
    [pr#20349](https://github.com/ceph/ceph/pull/20349), Mykola Golub)

-   rbd-mirror: forced promotion can result in incorrect status
    ([issue#21559](http://tracker.ceph.com/issues/21559),
    [pr#17979](https://github.com/ceph/ceph/pull/17979), Jason Dillaman)

-   rbd-mirror: ImageMap memory leak fixes
    ([pr#19163](https://github.com/ceph/ceph/pull/19163), Venky Shankar)

-   rbd-mirror: Improve data pool selection when creating images
    ([pr#18006](https://github.com/ceph/ceph/pull/18006), Adam Wolfe
    Gordon)

-   rbd-mirror: integrate image map policy as incremental step to
    active-active ([pr#21300](https://github.com/ceph/ceph/pull/21300),
    Jason Dillaman)

-   rbd-mirror: introduce basic image mapping policy
    ([issue#18786](http://tracker.ceph.com/issues/18786),
    [pr#15691](https://github.com/ceph/ceph/pull/15691), Venky Shankar)

-   rbd-mirror: missing lock when re-sending update_sync_point
    ([pr#19011](https://github.com/ceph/ceph/pull/19011), Mykola Golub)

-   rbd-mirror: persist image map timestamp
    ([pr#19338](https://github.com/ceph/ceph/pull/19338), Venky Shankar)

-   rbd-mirror: primary image should register in remote, non-primary
    image\'s journal
    ([issue#21561](http://tracker.ceph.com/issues/21561),
    [pr#18136](https://github.com/ceph/ceph/pull/18136), Jason Dillaman)

-   rbd-mirror: properly translate remote tag mirror uuid for local
    mirror ([issue#23876](http://tracker.ceph.com/issues/23876),
    [pr#21657](https://github.com/ceph/ceph/pull/21657), Jason Dillaman)

-   rbd-mirror: removed dedicated thread from image deleter
    ([issue#15322](http://tracker.ceph.com/issues/15322),
    [pr#19000](https://github.com/ceph/ceph/pull/19000), Jason Dillaman)

-   rbd-mirror: rename asok hook to match image name when not replaying
    ([issue#23888](http://tracker.ceph.com/issues/23888),
    [pr#21682](https://github.com/ceph/ceph/pull/21682), Jason Dillaman)

-   rbd-mirror: rollback state transitions in image policy
    ([pr#19577](https://github.com/ceph/ceph/pull/19577), Venky Shankar)

-   rbd-mirror: Set the data pool correctly when creating images
    ([issue#20567](http://tracker.ceph.com/issues/20567),
    [pr#17073](https://github.com/ceph/ceph/pull/17073), Adam Wolfe
    Gordon)

-   rbd-mirror: simplify notifications for image assignment
    ([issue#15764](http://tracker.ceph.com/issues/15764),
    [pr#16642](https://github.com/ceph/ceph/pull/16642), Jason Dillaman)

-   rbd-mirror: strip environment/CLI overrides for remote cluster
    ([issue#21894](http://tracker.ceph.com/issues/21894),
    [pr#18490](https://github.com/ceph/ceph/pull/18490), Jason Dillaman)

-   rbd-mirror: support deferred deletions of mirrored images
    ([pr#19536](https://github.com/ceph/ceph/pull/19536), Jason
    Dillaman)

-   rbd-mirror: sync image metadata when transfering remote image
    ([issue#21535](http://tracker.ceph.com/issues/21535),
    [pr#18026](https://github.com/ceph/ceph/pull/18026), Jason Dillaman)

-   rbd-mirror: track images in policy map in support of A/A
    ([issue#18786](http://tracker.ceph.com/issues/18786),
    [pr#15788](https://github.com/ceph/ceph/pull/15788), Venky Shankar)

-   rbd-mirror: update asok hook name on image rename
    ([issue#20860](http://tracker.ceph.com/issues/20860),
    [pr#16998](https://github.com/ceph/ceph/pull/16998), Mykola Golub)

-   rbd-mirror: use next transition state to check transition
    completeness ([pr#18969](https://github.com/ceph/ceph/pull/18969),
    Venky Shankar)

-   rbd-nbd: allow to unmap by image or snap spec
    ([pr#19666](https://github.com/ceph/ceph/pull/19666), Mykola Golub)

-   rbd-nbd: bug fix when running in container
    ([issue#22012](http://tracker.ceph.com/issues/22012),
    [issue#22011](http://tracker.ceph.com/issues/22011),
    [pr#18663](https://github.com/ceph/ceph/pull/18663), Li Wang)

-   rbd-nbd: certain kernels may not discover resized block devices
    ([issue#22131](http://tracker.ceph.com/issues/22131),
    [pr#18947](https://github.com/ceph/ceph/pull/18947), Jason Dillaman)

-   rbd-nbd: cleanup for NBDServer shut down
    ([pr#17283](https://github.com/ceph/ceph/pull/17283), Pan Liu)

-   rbd-nbd: fix ebusy when do map
    ([issue#23528](http://tracker.ceph.com/issues/23528),
    [pr#21142](https://github.com/ceph/ceph/pull/21142), Li Wang)

-   rbd-nbd: fix generic option issue
    ([issue#20426](http://tracker.ceph.com/issues/20426),
    [pr#17375](https://github.com/ceph/ceph/pull/17375), Pan Liu)

-   rbd-nbd: output format support for list-mapped command
    ([pr#19704](https://github.com/ceph/ceph/pull/19704), Mykola Golub)

-   rbd-nbd: support optionally setting device timeout
    ([issue#22333](http://tracker.ceph.com/issues/22333),
    [pr#19436](https://github.com/ceph/ceph/pull/19436), Mykola Golub)

-   rbd: null check before pool_name use
    ([pr#18790](https://github.com/ceph/ceph/pull/18790), Amit Kumar)

-   rbd: output notifyOp request name when watching
    ([pr#20551](https://github.com/ceph/ceph/pull/20551), shun-s)

-   rbd: parallelize \"rbd ls -l\"
    ([pr#15579](https://github.com/ceph/ceph/pull/15579), Piotr Dałek)

-   rbd: pool_percent_used should not divided by 100
    ([pr#20795](https://github.com/ceph/ceph/pull/20795), songweibin)

-   rbd: properly pass ceph global command line args to subprocess
    ([pr#19821](https://github.com/ceph/ceph/pull/19821), Mykola Golub)

-   rbd: pybind/rbd: add deep_copy method
    ([pr#19406](https://github.com/ceph/ceph/pull/19406), Mykola Golub)

-   rbd: pybind/rbd: fix metadata functions error handling
    ([issue#22306](http://tracker.ceph.com/issues/22306),
    [pr#19337](https://github.com/ceph/ceph/pull/19337), Mykola Golub)

-   rbd: python bindings fixes and improvements
    ([issue#23609](http://tracker.ceph.com/issues/23609),
    [pr#21304](https://github.com/ceph/ceph/pull/21304), Ricardo Dias)

-   rbd: rbd-ggate: fix parsing ceph global options
    ([pr#19822](https://github.com/ceph/ceph/pull/19822), Mykola Golub)

-   rbd: rbd-ggate: fix syntax error
    ([pr#19919](https://github.com/ceph/ceph/pull/19919), Willem Jan
    Withagen)

-   rbd: rbd-ggate: make list command produce valid xml format output
    ([pr#19823](https://github.com/ceph/ceph/pull/19823), Mykola Golub)

-   rbd: rbd-ggate: small fixes and improvements
    ([pr#19679](https://github.com/ceph/ceph/pull/19679), Mykola Golub)

-   rbd: rbd-ggate: tool to map images on FreeBSD via GEOM Gate
    ([pr#15339](https://github.com/ceph/ceph/pull/15339), Mykola Golub)

-   rbd: rbd:introduce rbd bench rw(for read and write mix) test
    ([pr#17461](https://github.com/ceph/ceph/pull/17461), PCzhangPC)

-   rbd: rbd: set a default value for options in [nbd map]{.title-ref}
    ([pr#20529](https://github.com/ceph/ceph/pull/20529), songweibin)

-   rbd: replace positional_path parameter with arg_index in get_path()
    ([pr#19722](https://github.com/ceph/ceph/pull/19722), songweibin)

-   rbd: replace trash delay option, add rbd trash purge command
    ([pr#18323](https://github.com/ceph/ceph/pull/18323), Theofilos
    Mouratidis)

-   rbd: resource agent needs to be executable
    ([issue#22980](http://tracker.ceph.com/issues/22980),
    [issue#22362](http://tracker.ceph.com/issues/22362),
    [pr#20397](https://github.com/ceph/ceph/pull/20397), Tim Bishop)

-   rbd:rm unnecessary conversion from string to char\* in image-meta
    function ([pr#17184](https://github.com/ceph/ceph/pull/17184),
    PCzhangPC)

-   rbd: show read:write proportion in the infomation of readwrite bench
    test ([pr#18249](https://github.com/ceph/ceph/pull/18249),
    PCzhangPC)

-   rbd: snap limit should\'t be set smaller than the number of existing
    snaps ([pr#16597](https://github.com/ceph/ceph/pull/16597),
    PCzhangPC)

-   rbd: support cloning an image from a non-primary snapshot
    ([issue#18480](http://tracker.ceph.com/issues/18480),
    [pr#19724](https://github.com/ceph/ceph/pull/19724), Jason Dillaman)

-   rbd: support iterating over metadata items when listing
    ([issue#21179](http://tracker.ceph.com/issues/21179),
    [pr#17532](https://github.com/ceph/ceph/pull/17532), Jason Dillaman)

-   rbd: support lock_timeout in rbd mapping
    ([pr#21344](https://github.com/ceph/ceph/pull/21344), Dongsheng
    Yang)

-   rbd: support osd_request_timeout in rbd map command
    ([issue#23073](http://tracker.ceph.com/issues/23073),
    [pr#20792](https://github.com/ceph/ceph/pull/20792), Dongsheng Yang)

-   rbd: switched from legacy to new-style configuration options
    ([issue#20737](http://tracker.ceph.com/issues/20737),
    [pr#16737](https://github.com/ceph/ceph/pull/16737), Jason Dillaman)

-   rbd,tests: qa: additional krbd discard test cases
    ([pr#20499](https://github.com/ceph/ceph/pull/20499), Ilya Dryomov)

-   rbd,tests: qa: fix POOL_APP_NOT_ENABLED warning in krbd:unmap suite
    ([pr#16966](https://github.com/ceph/ceph/pull/16966), Ilya Dryomov)

-   rbd,tests: qa: introduce rbd-mirror thrasher to existing tests
    ([issue#18753](http://tracker.ceph.com/issues/18753),
    [pr#21541](https://github.com/ceph/ceph/pull/21541), Jason Dillaman)

-   rbd,tests: qa: krbd_exclusive_option.sh: add lock_timeout test case
    ([pr#21522](https://github.com/ceph/ceph/pull/21522), Ilya Dryomov)

-   rbd,tests: qa: krbd_fallocate.sh: add notrim test case
    ([pr#21513](https://github.com/ceph/ceph/pull/21513), Ilya Dryomov)

-   rbd,tests: qa: krbd huge-image test
    ([pr#20692](https://github.com/ceph/ceph/pull/20692), Ilya Dryomov)

-   rbd,tests: qa: krbd latest-osdmap-on-map test
    ([pr#20591](https://github.com/ceph/ceph/pull/20591), Ilya Dryomov)

-   rbd,tests: qa: krbd msgr-segments test
    ([pr#20714](https://github.com/ceph/ceph/pull/20714), Ilya Dryomov)

-   rbd,tests: qa: krbd parent-overlap test
    ([pr#20721](https://github.com/ceph/ceph/pull/20721), Ilya Dryomov)

-   rbd,tests: qa: krbd whole-object-discard test
    ([pr#20750](https://github.com/ceph/ceph/pull/20750), Ilya Dryomov)

-   rbd,tests: qa/suites/krbd: add krbd BLKROSET test
    ([pr#18652](https://github.com/ceph/ceph/pull/18652), Ilya Dryomov)

-   rbd,tests: qa/suites/krbd: enable generic/050 and generic/448
    ([pr#18795](https://github.com/ceph/ceph/pull/18795), Ilya Dryomov)

-   rbd,tests: qa/suites/krbd: enable xfstests blockdev tests
    ([pr#17621](https://github.com/ceph/ceph/pull/17621), Ilya Dryomov)

-   rbd,tests: qa/suites/krbd: exclude shared/298
    ([pr#17971](https://github.com/ceph/ceph/pull/17971), Ilya Dryomov)

-   rbd,tests: qa/suites/krbd: rbd_xfstests job overhaul
    ([pr#17346](https://github.com/ceph/ceph/pull/17346), Ilya Dryomov)

-   rbd,tests: qa/suites/rbd: fewer socket failures
    ([pr#19617](https://github.com/ceph/ceph/pull/19617), Sage Weil)

-   rbd,tests: qa/suites/rbd: miscellaneous test fixes
    ([issue#21251](http://tracker.ceph.com/issues/21251),
    [pr#17504](https://github.com/ceph/ceph/pull/17504), Jason Dillaman)

-   rbd,tests: qa/suites/rbd: segregated v1 image format tests
    ([issue#22738](http://tracker.ceph.com/issues/22738),
    [pr#20729](https://github.com/ceph/ceph/pull/20729), Jason Dillaman)

-   rbd,tests: qa/suites/rbd: set qemu task time_wait param
    ([pr#21131](https://github.com/ceph/ceph/pull/21131), Mykola Golub)

-   rbd,tests: qa/tasks/cram: include /usr/sbin in the PATH for all
    commands ([pr#18793](https://github.com/ceph/ceph/pull/18793), Ilya
    Dryomov)

-   rbd,tests: qa/tasks/rbd: run all xfstests runs to completion
    ([pr#18583](https://github.com/ceph/ceph/pull/18583), Ilya Dryomov)

-   rbd,tests: qa/workunits/rbd: fix cli_generic test_purge for rbd
    default format 1
    ([pr#20389](https://github.com/ceph/ceph/pull/20389), Mykola Golub)

-   rbd,tests: qa/workunits/rbd: fixed variable name for resync image id
    ([issue#21663](http://tracker.ceph.com/issues/21663),
    [pr#18097](https://github.com/ceph/ceph/pull/18097), Jason Dillaman)

-   rbd,tests: qa/workunits/rbd: fix issues within permissions test
    ([issue#23043](http://tracker.ceph.com/issues/23043),
    [pr#20491](https://github.com/ceph/ceph/pull/20491), Jason Dillaman)

-   rbd,tests: qa/workunits/rbd: pool create may fail for small cluster
    ([pr#18067](https://github.com/ceph/ceph/pull/18067), Mykola Golub)

-   rbd,tests: qa/workunits/rbd: potential race in mirror disconnect
    test ([issue#23938](http://tracker.ceph.com/issues/23938),
    [pr#21733](https://github.com/ceph/ceph/pull/21733), Mykola Golub)

-   rbd,tests: qa/workunits/rbd: relax greps to support upgrade
    formatting change
    ([issue#21181](http://tracker.ceph.com/issues/21181),
    [pr#17559](https://github.com/ceph/ceph/pull/17559), Jason Dillaman)

-   rbd,tests: qa/workunits/rbd: remove sanity check in journal.sh test
    ([pr#20490](https://github.com/ceph/ceph/pull/20490), Jason
    Dillaman)

-   rbd,tests: qa/workunits/rbd: remove sanity check in
    test_admin_socket.sh
    ([pr#21116](https://github.com/ceph/ceph/pull/21116), Mykola Golub)

-   rbd,tests: qa/workunits/rbd: remove \"trash purge \--threshold\"
    test ([issue#22803](http://tracker.ceph.com/issues/22803),
    [pr#20170](https://github.com/ceph/ceph/pull/20170), Mykola Golub)

-   rbd,tests: qa/workunits/rbd: simplify split-brain test to avoid
    potential race ([issue#22485](http://tracker.ceph.com/issues/22485),
    [pr#19604](https://github.com/ceph/ceph/pull/19604), Jason Dillaman)

-   rbd,tests: qa/workunits/rbd: switch devstack tempest to 17.2.0 tag
    ([issue#22961](http://tracker.ceph.com/issues/22961),
    [pr#20599](https://github.com/ceph/ceph/pull/20599), Jason Dillaman)

-   rbd,tests: qa/workunits/rbd: switch devstack to pike release
    ([pr#20124](https://github.com/ceph/ceph/pull/20124), Jason
    Dillaman)

-   rbd,tests: qa/workunits/rbd: test data pool is mirrored correctly
    ([pr#17062](https://github.com/ceph/ceph/pull/17062), Mykola Golub)

-   rbd,tests: qa/workunits/rbd: unnecessary sleep after failed remove
    ([pr#18619](https://github.com/ceph/ceph/pull/18619), Mykola Golub)

-   rbd,tests: qa/workunits/rbd: use command line option to specify
    watcher asok ([issue#20954](http://tracker.ceph.com/issues/20954),
    [pr#16917](https://github.com/ceph/ceph/pull/16917), Mykola Golub)

-   rbd,tests: qa/workunits/rbd: wait for demote status is propagated
    ([pr#19073](https://github.com/ceph/ceph/pull/19073), Mykola Golub)

-   rbd,tests: qa/workunits/rbd: wait for status propagated only if
    daemon started ([pr#19082](https://github.com/ceph/ceph/pull/19082),
    Mykola Golub)

-   rbd,tests: rbd/test: add snap protection test for ex/import
    ([pr#20689](https://github.com/ceph/ceph/pull/20689), songweibin)

-   rbd,tests: stop.sh: use \--no-mon-config when trying to unmap rbd
    devices ([pr#21020](https://github.com/ceph/ceph/pull/21020), Mykola
    Golub)

-   rbd,tests: test: address coverity false positives
    ([pr#17803](https://github.com/ceph/ceph/pull/17803), Amit Kumar)

-   rbd,tests: test/cls_rbd: mask newer feature bits to support upgrade
    tests ([issue#21217](http://tracker.ceph.com/issues/21217),
    [pr#17509](https://github.com/ceph/ceph/pull/17509), Jason Dillaman)

-   rbd,tests: test/librados_test_stub: always create copy of buffers
    passed to operation
    ([pr#21074](https://github.com/ceph/ceph/pull/21074), Mykola Golub)

-   rbd,tests: test/librbd: added update_features RPC message to
    test_notify ([issue#21936](http://tracker.ceph.com/issues/21936),
    [pr#18561](https://github.com/ceph/ceph/pull/18561), Jason Dillaman)

-   rbd,tests: test/librbd: clean up for several mock function tests
    ([pr#18952](https://github.com/ceph/ceph/pull/18952), Jason
    Dillaman)

-   rbd,tests: test/librbd: Do not instantiate TrimRequest template
    class ([pr#19402](https://github.com/ceph/ceph/pull/19402), Boris
    Ranto)

-   rbd,tests: test/librbd: ensure OutOfOrder test has enough concurrent
    management ops ([pr#21436](https://github.com/ceph/ceph/pull/21436),
    Mykola Golub)

-   rbd,tests: test/librbd: fix mock method macro of set_journal_policy
    ([pr#17216](https://github.com/ceph/ceph/pull/17216), Yan Jun)

-   rbd,tests: test/librbd: fix race condition with OSD map refresh
    ([issue#20918](http://tracker.ceph.com/issues/20918),
    [pr#16877](https://github.com/ceph/ceph/pull/16877), Jason Dillaman)

-   rbd,tests: test/librbd: fix valgrind memory leak warning
    ([pr#17187](https://github.com/ceph/ceph/pull/17187), Mykola Golub)

-   rbd,tests: test/librbd: initialize on_finish,locker,force,snap_id
    ([pr#17800](https://github.com/ceph/ceph/pull/17800), Amit Kumar)

-   rbd,tests: test/librbd: make fsx build on non-linux platform
    ([pr#16939](https://github.com/ceph/ceph/pull/16939), Mykola Golub)

-   rbd,tests: test/librbd: memory leak in recently added test
    ([pr#18478](https://github.com/ceph/ceph/pull/18478), Mykola Golub)

-   rbd,tests: test/librbd: rbd-ggate mode for fsx
    ([pr#19315](https://github.com/ceph/ceph/pull/19315), Mykola Golub)

-   rbd,tests: test/librbd: test metadata_set/remove is applied
    ([pr#18288](https://github.com/ceph/ceph/pull/18288), Mykola Golub)

-   rbd,tests: test/librbd: TestMirroringWatcher unit tests should
    ignore duplicates
    ([issue#21029](http://tracker.ceph.com/issues/21029),
    [pr#17078](https://github.com/ceph/ceph/pull/17078), Jason Dillaman)

-   rbd,tests: test/librbd: utilize unique pool for cache tier testing
    ([issue#11502](http://tracker.ceph.com/issues/11502),
    [pr#20486](https://github.com/ceph/ceph/pull/20486), Jason Dillaman)

-   rbd,tests: test/librbd: valgrind warning in
    TestMockManagedLockBreakRequest.DeadLockOwner
    ([pr#18940](https://github.com/ceph/ceph/pull/18940), Mykola Golub)

-   rbd,tests: test/pybind/rbd: skip test_deep_copy_clone if layering
    not enabled ([pr#20295](https://github.com/ceph/ceph/pull/20295),
    Mykola Golub)

-   rbd,tests: test/rbd: cli_generic fails if v1 image format or
    deep-flatten disabled
    ([issue#22950](http://tracker.ceph.com/issues/22950),
    [pr#20364](https://github.com/ceph/ceph/pull/20364), songweibin)

-   rbd,tests: test/rbd_mirror: fix valgrind warnings in unittest
    ([pr#19016](https://github.com/ceph/ceph/pull/19016), Mykola Golub)

-   rbd,tests: test/rbd-mirror: image map policy test
    ([pr#19320](https://github.com/ceph/ceph/pull/19320), Venky Shankar)

-   rbd,tests: test/rbd-mirror: improve coverage for dead instance
    handling ([pr#21403](https://github.com/ceph/ceph/pull/21403), Jason
    Dillaman)

-   rbd,tests: test/rbd_mirror: \"use of uninitialised value\" valgrind
    warning ([pr#19437](https://github.com/ceph/ceph/pull/19437), Mykola
    Golub)

-   rbd,tools: rbd-fuse: make sure PATH_MAX is defined
    ([pr#18615](https://github.com/ceph/ceph/pull/18615), Roberto
    Oliveira)

-   rbd,tools: rbd-replay: remove boost dependency
    ([pr#21202](https://github.com/ceph/ceph/pull/21202), Kefu Chai)

-   rbd: tools/rbd: use steady clock in bencher
    ([pr#20008](https://github.com/ceph/ceph/pull/20008), Mohamad Gebai)

-   rbd: \'trash list \--long\' will return a failure on non-cloned
    images ([pr#19540](https://github.com/ceph/ceph/pull/19540), Jason
    Dillaman)

-   rbd: \'trash ls -l\' will display column titles if existed non-USER
    trash image only
    ([pr#21343](https://github.com/ceph/ceph/pull/21343), songweibin)

-   rbd: unified way to map images using different drivers
    ([pr#19711](https://github.com/ceph/ceph/pull/19711), Mykola Golub)

-   rbd: use different logic to disturb thread\'s offset in bench seq
    test ([pr#17218](https://github.com/ceph/ceph/pull/17218),
    PCzhangPC)

-   Revert \"ceph-fuse: Delete inode\'s bufferhead was in Tx state would
    le... ([pr#21976](https://github.com/ceph/ceph/pull/21976), \"Yan,
    Zheng\")

-   Revert \"msg/async/rdma: fix multi cephcontext confllicting\"
    ([pr#16980](https://github.com/ceph/ceph/pull/16980), Haomai Wang)

-   Revert \"os/bluestore: compensate for bad freelistmanager
    size/blocks metadata\"
    ([pr#17275](https://github.com/ceph/ceph/pull/17275), Xie Xingguo)

-   rgw: ability to list bucket contents in unsorted order for
    efficiency ([pr#21026](https://github.com/ceph/ceph/pull/21026), J.
    Eric Ivancich)

-   rgw: abort multipart if upload meta object doesn\'t exist
    ([pr#19918](https://github.com/ceph/ceph/pull/19918), fang yuxiang)

-   rgw: Access RGWConf through RGWEnv
    ([pr#17432](https://github.com/ceph/ceph/pull/17432), Jos Collin)

-   rgw: add \"Accept-Ranges\" to response header of Swift API
    ([issue#21554](http://tracker.ceph.com/issues/21554),
    [pr#17967](https://github.com/ceph/ceph/pull/17967), Tone Zhang)

-   rgw: add a default redirect field for zones
    ([pr#9571](https://github.com/ceph/ceph/pull/9571), Yehuda Sadeh)

-   rgw: add an option to clear all usage entries
    ([pr#19322](https://github.com/ceph/ceph/pull/19322), Abhishek
    Lekshmanan)

-   rgw: add an option to recalculate user stats
    ([issue#23335](http://tracker.ceph.com/issues/23335),
    [pr#20853](https://github.com/ceph/ceph/pull/20853), Abhishek
    Lekshmanan)

-   rgw: add buffering filter to compression for fetch_remote_obj
    ([issue#23547](http://tracker.ceph.com/issues/23547),
    [pr#21479](https://github.com/ceph/ceph/pull/21479), Casey Bodley)

-   rgw: add cors header rule check in cors option request
    ([issue#22002](http://tracker.ceph.com/issues/22002),
    [pr#18556](https://github.com/ceph/ceph/pull/18556), yuliyang)

-   rgw: Add dynamic resharding documentation
    ([issue#21553](http://tracker.ceph.com/issues/21553),
    [pr#15941](https://github.com/ceph/ceph/pull/15941), Orit Wasserman)

-   rgw: add logs if get_data returns error in RGWPutObj::execute
    ([pr#18642](https://github.com/ceph/ceph/pull/18642), Zhang Shaowen)

-   rgw: add metadata and data sync related cmd into radosgw-admin usage
    ([pr#18921](https://github.com/ceph/ceph/pull/18921), lvshanchun)

-   rgw: add missing override in list_keys_init()
    ([pr#17254](https://github.com/ceph/ceph/pull/17254), Jos Collin)

-   rgw: add radosgw-admin sync error trim to trim sync error log
    ([pr#19854](https://github.com/ceph/ceph/pull/19854), fang yuxiang)

-   rgw: add reshard commands
    ([issue#21617](http://tracker.ceph.com/issues/21617),
    [pr#18180](https://github.com/ceph/ceph/pull/18180), Orit Wasserman)

-   

    rgw: address warnings due to incorrect format code ([pr#18796](https://github.com/ceph/ceph/pull/18796), J. Eric Ivancich)

    :   rgw: Add retry_raced_bucket_write

-   rgw: add rewrite cmd and options into radosgw-admin usage and doc
    ([pr#18918](https://github.com/ceph/ceph/pull/18918), Enming Zhang)

-   rgw: add ssl support to beast frontend
    ([issue#22832](http://tracker.ceph.com/issues/22832),
    [pr#20464](https://github.com/ceph/ceph/pull/20464), Casey Bodley)

-   rgw: add support for Swift\'s per storage policy statistics
    ([issue#17932](http://tracker.ceph.com/issues/17932),
    [pr#12704](https://github.com/ceph/ceph/pull/12704), Radoslaw
    Zarzynski)

-   rgw: add support for Swift\'s reversed account listings
    ([issue#21148](http://tracker.ceph.com/issues/21148),
    [pr#17320](https://github.com/ceph/ceph/pull/17320), Radoslaw
    Zarzynski)

-   rgw: add support for tagging and other conditionals in policy
    ([pr#17094](https://github.com/ceph/ceph/pull/17094), Abhishek
    Lekshmanan)

-   rgw: add tail tag to track tail instance
    ([issue#20234](http://tracker.ceph.com/issues/20234),
    [pr#16145](https://github.com/ceph/ceph/pull/16145), Yehuda Sadeh)

-   rgw: add tenant to shard_id in RGWDeleteLC::execute()
    ([pr#10460](https://github.com/ceph/ceph/pull/10460), Wei Qiaomiao)

-   

    rgw: add time skew check in function parse_v4_auth_header ([issue#22418](http://tracker.ceph.com/issues/22418), [pr#19476](https://github.com/ceph/ceph/pull/19476), Bingyin Zhang)

    :   rgw: Add try_refresh_bucket_info function

-   rgw: add xml output header in RGWCopyObj_ObjStore_S3 response msg
    ([issue#22416](http://tracker.ceph.com/issues/22416),
    [pr#19475](https://github.com/ceph/ceph/pull/19475), Enming Zhang)

-   rgw: adjust log format for lifecycle
    ([pr#19576](https://github.com/ceph/ceph/pull/19576), Bingyin Zhang)

-   rgw: admin api - add ability to sync user stats from admin api
    ([issue#21301](http://tracker.ceph.com/issues/21301),
    [pr#17589](https://github.com/ceph/ceph/pull/17589), Nathan Johnson)

-   rgw: Admin API Support for bucket quota change
    ([issue#21811](http://tracker.ceph.com/issues/21811),
    [pr#18324](https://github.com/ceph/ceph/pull/18324), Jeegn Chen)

-   rgw: admin rest api shouldn\'t return error when getting user\'s
    stats if the user hasn\'t create any bucket
    ([pr#21551](https://github.com/ceph/ceph/pull/21551), Zhang Shaowen)

-   rgw: allow beast frontend to listen on specific IP address
    ([issue#22778](http://tracker.ceph.com/issues/22778),
    [pr#20000](https://github.com/ceph/ceph/pull/20000), Yuan Zhou)

-   rgw: Allow swift acls to be deleted
    ([issue#22897](http://tracker.ceph.com/issues/22897),
    [pr#20471](https://github.com/ceph/ceph/pull/20471), Marcus Watts)

-   rgw: avoid logging keystone revocation messages when not configured
    ([issue#21400](http://tracker.ceph.com/issues/21400),
    [pr#17775](https://github.com/ceph/ceph/pull/17775), Abhishek
    Lekshmanan)

-   rgw: aws4 auth supports PutBucketRequestPayment
    ([issue#23803](http://tracker.ceph.com/issues/23803),
    [pr#21569](https://github.com/ceph/ceph/pull/21569), Casey Bodley)

-   rgw: AWS v4 authorization work when INIT_MULTIPART is chunked
    ([issue#22129](http://tracker.ceph.com/issues/22129),
    [pr#18956](https://github.com/ceph/ceph/pull/18956), Jeegn Chen)

-   rgw: beast frontend can listen on multiple endpoints
    ([issue#22779](http://tracker.ceph.com/issues/22779),
    [pr#20188](https://github.com/ceph/ceph/pull/20188), Casey Bodley)

-   rgw: beast frontend no longer experimental
    ([pr#21272](https://github.com/ceph/ceph/pull/21272), Casey Bodley)

-   rgw: Better ERANGE error message
    ([issue#22351](http://tracker.ceph.com/issues/22351),
    [pr#20023](https://github.com/ceph/ceph/pull/20023), Brad Hubbard)

-   rgw: break sending data-log list infinitely
    ([issue#20951](http://tracker.ceph.com/issues/20951),
    [pr#16926](https://github.com/ceph/ceph/pull/16926), fang.yuxiang)

-   rgw: bucket resharding should not update bucket ACL or user stats
    ([issue#22742](http://tracker.ceph.com/issues/22742),
    [issue#22124](http://tracker.ceph.com/issues/22124),
    [pr#20038](https://github.com/ceph/ceph/pull/20038), Orit Wasserman)

-   rgw: Cache on the barrelhead
    ([issue#22517](http://tracker.ceph.com/issues/22517),
    [pr#19581](https://github.com/ceph/ceph/pull/19581), Adam C.
    Emerson)

-   rgw: Cache Register!
    ([issue#22604](http://tracker.ceph.com/issues/22604),
    [issue#22603](http://tracker.ceph.com/issues/22603),
    [pr#20144](https://github.com/ceph/ceph/pull/20144), Adam C.
    Emerson)

-   rgw: can\'t download object with range when compression enabled
    ([issue#22852](http://tracker.ceph.com/issues/22852),
    [pr#20226](https://github.com/ceph/ceph/pull/20226), fang yuxiang)

-   rgw: ceph-dencoder: add missing begin_iter & end_iter item for
    RGWObjManifest ([pr#19509](https://github.com/ceph/ceph/pull/19509),
    wangsongbo)

-   rgw: ceph-dencoder: add support for cls_rgw_lc_obj_head
    ([pr#18920](https://github.com/ceph/ceph/pull/18920), Yao Zongyou)

-   rgw: ceph-dencoder: add support for RGWLifecycleConfiguration
    ([pr#18959](https://github.com/ceph/ceph/pull/18959), wangsongbo)

-   rgw: change ObjectCache::lru from deque back to list
    ([issue#22560](http://tracker.ceph.com/issues/22560),
    [pr#19768](https://github.com/ceph/ceph/pull/19768), Casey Bodley)

-   rgw: changes to support ragweed
    ([pr#13644](https://github.com/ceph/ceph/pull/13644), Yehuda Sadeh)

-   rgw: Check bucket CORS operations in policy
    ([issue#21578](http://tracker.ceph.com/issues/21578),
    [pr#18000](https://github.com/ceph/ceph/pull/18000), Adam C.
    Emerson)

-   rgw: Check bucket GetBucketLocation in policy
    ([issue#21582](http://tracker.ceph.com/issues/21582),
    [pr#18002](https://github.com/ceph/ceph/pull/18002), Adam C.
    Emerson)

-   rgw: Check bucket Website operations in policy
    ([issue#21597](http://tracker.ceph.com/issues/21597),
    [pr#18024](https://github.com/ceph/ceph/pull/18024), Adam C.
    Emerson)

-   rgw: check going_down() when lifecycle processing
    ([issue#22099](http://tracker.ceph.com/issues/22099),
    [pr#18846](https://github.com/ceph/ceph/pull/18846), Yao Zongyou)

-   rgw: Check payment operations in policy
    ([issue#21389](http://tracker.ceph.com/issues/21389),
    [pr#17742](https://github.com/ceph/ceph/pull/17742), Adam C.
    Emerson)

-   rgw: check read_op.read return value in RGWRados::copy_obj_data
    ([pr#18962](https://github.com/ceph/ceph/pull/18962), Enming Zhang)

-   rgw: civetweb fixes for v1.1 upgrade
    ([pr#21123](https://github.com/ceph/ceph/pull/21123), Abhishek
    Lekshmanan)

-   rgw: clean code with helper function dump_header_if_nonempty
    ([pr#18979](https://github.com/ceph/ceph/pull/18979), Xinying Song)

-   rgw: clean up and fix some bugs for encryption
    ([issue#21581](http://tracker.ceph.com/issues/21581),
    [pr#17882](https://github.com/ceph/ceph/pull/17882), Enming Zhang)

-   rgw: cleanup MIN macro with std::min
    ([pr#17546](https://github.com/ceph/ceph/pull/17546), Jiaying Ren)

-   rgw: cleanup unused parameters in RGWRados::copy_obj_data
    ([pr#18917](https://github.com/ceph/ceph/pull/18917), Enming Zhang)

-   rgw: cloud sync fixes
    ([pr#21648](https://github.com/ceph/ceph/pull/21648), Yehuda Sadeh)

-   rgw: cls/log: cls_log_list always returns next marker
    ([issue#20906](http://tracker.ceph.com/issues/20906),
    [pr#17024](https://github.com/ceph/ceph/pull/17024), Casey Bodley)

-   rgw: cls/rgw: fix bi_log_iterate_entries return wrong truncated
    ([issue#22737](http://tracker.ceph.com/issues/22737),
    [pr#20021](https://github.com/ceph/ceph/pull/20021), Tianshan Qu)

-   rgw: cls/rgw: Initialization of uninitialized members
    ([pr#16932](https://github.com/ceph/ceph/pull/16932), amitkuma)

-   rgw: cls/rgw: mtime in rgw_bucket_dir_entry_meta not really decoded
    ([issue#22148](http://tracker.ceph.com/issues/22148),
    [pr#18981](https://github.com/ceph/ceph/pull/18981), Yao Zongyou)

-   rgw: cls/rgw: remove unused variable bl
    ([pr#19570](https://github.com/ceph/ceph/pull/19570), Yao Zongyou)

-   rgw: cls/rgw: trim all usage entries in cls_rgw
    ([issue#22234](http://tracker.ceph.com/issues/22234),
    [pr#19131](https://github.com/ceph/ceph/pull/19131), Abhishek
    Lekshmanan)

-   rgw: cls_rgw: use more effective container operations in
    get_obj_vals ([pr#19272](https://github.com/ceph/ceph/pull/19272),
    Xinying Song)

-   rgw: comparison between signed and unsigned integer expressions
    ([pr#21105](https://github.com/ceph/ceph/pull/21105), ashitakasam)

-   rgw: consolidate code that implements hashing algorithms
    ([pr#18248](https://github.com/ceph/ceph/pull/18248), J. Eric
    Ivancich)

-   rgw: copy object add response error messages
    ([pr#18291](https://github.com/ceph/ceph/pull/18291), Enming Zhang)

-   rgw: correct comment in function parse_credentials
    ([pr#19275](https://github.com/ceph/ceph/pull/19275), Bingyin Zhang)

-   rgw: correct log output for metadata section name in
    RGWListBucketIndexesCR
    ([pr#19508](https://github.com/ceph/ceph/pull/19508), Xinying Song)

-   rgw: Correct permission evaluation to allow only admin users to work
    with Roles ([pr#20332](https://github.com/ceph/ceph/pull/20332),
    Pritha Srivastava)

-   rgw: correct typo refity to refit
    ([pr#19064](https://github.com/ceph/ceph/pull/19064), Bingyin Zhang)

-   rgw: correct typo UNKOWN to UNKNOWN
    ([pr#19273](https://github.com/ceph/ceph/pull/19273), Bingyin Zhang)

-   rgw: create sync-module instance when execute radosgw-admin data
    sync run ([issue#22080](http://tracker.ceph.com/issues/22080),
    [pr#18898](https://github.com/ceph/ceph/pull/18898), lvshanchun)

-   rgw: create sync-module instance when radosgw-admin sync run
    ([pr#20611](https://github.com/ceph/ceph/pull/20611), lvshanchun)

-   rgw: curl\* reuse and for debian, use openssl not gnutls
    ([pr#20635](https://github.com/ceph/ceph/pull/20635), Marcus Watts)

-   rgw: Data encryption is not follow the AWS agreement
    ([pr#15994](https://github.com/ceph/ceph/pull/15994), hechuang)

-   rgw: datalog list support \--shard-id and \--marker
    ([pr#20649](https://github.com/ceph/ceph/pull/20649), Tianshan Qu)

-   rgw: data sync: set num_shards when building full maps
    ([issue#22083](http://tracker.ceph.com/issues/22083),
    [pr#18852](https://github.com/ceph/ceph/pull/18852), Abhishek
    Lekshmanan)

-   rgw: Delete to_string functions. stringify defined in
    include/stringify.h can provide the same feature
    ([pr#18522](https://github.com/ceph/ceph/pull/18522), zhangwen)

-   rgw: disable dynamic resharding in multisite environment
    ([issue#21725](http://tracker.ceph.com/issues/21725),
    [pr#18184](https://github.com/ceph/ceph/pull/18184), Orit Wasserman)

-   rgw: do not reflect period if not current
    ([issue#22844](http://tracker.ceph.com/issues/22844),
    [pr#20212](https://github.com/ceph/ceph/pull/20212), Tianshan Qu)

-   rgw: do not update all gateway caches upon creation of system obj w/
    exclusive flag
    ([pr#19384](https://github.com/ceph/ceph/pull/19384), J. Eric
    Ivancich)

-   rgw: don\'t change rados object\'s mtime when update olh
    ([issue#21743](http://tracker.ceph.com/issues/21743),
    [pr#18214](https://github.com/ceph/ceph/pull/18214), Shasha Lu)

-   rgw: don\'t hold data_lock over frontend io
    ([pr#20621](https://github.com/ceph/ceph/pull/20621), Casey Bodley)

-   rgw: don\'t leak S3 LDAPHelper
    ([pr#12427](https://github.com/ceph/ceph/pull/12427), Matt Benjamin)

-   rgw: dont log EBUSY errors in \'sync error list\'
    ([issue#22473](http://tracker.ceph.com/issues/22473),
    [pr#19580](https://github.com/ceph/ceph/pull/19580), Casey Bodley)

-   rgw: dont reuse stale RGWObjectCtx for get_bucket_info()
    ([issue#21506](http://tracker.ceph.com/issues/21506),
    [pr#17916](https://github.com/ceph/ceph/pull/17916), Casey Bodley)

-   rgw: don\'t write bucket_header when it is not changed in
    bucket_link/unlink
    ([pr#17356](https://github.com/ceph/ceph/pull/17356), Shasha Lu)

-   rgw: don\'t write bucket_header when it is not changed in
    rgw_bucket_prepare_op
    ([pr#18763](https://github.com/ceph/ceph/pull/18763), Xinying Song)

-   rgw: download object might fail for local invariable uninitialized
    ([issue#23146](http://tracker.ceph.com/issues/23146),
    [pr#20612](https://github.com/ceph/ceph/pull/20612), fang yuxiang)

-   rgw: drop a repeated statement for encode_xml()
    ([pr#20195](https://github.com/ceph/ceph/pull/20195), luomuyao)

-   rgw: drop commented functions
    ([pr#19671](https://github.com/ceph/ceph/pull/19671), Jos Collin)

-   rgw: drop dump_uri_from_state() which isn\'t used anymore
    ([pr#19924](https://github.com/ceph/ceph/pull/19924), Radoslaw
    Zarzynski)

-   rgw: drop iter in rgw_op.cc
    ([pr#19583](https://github.com/ceph/ceph/pull/19583), Bingyin Zhang)

-   rgw: drop marker in RGWLC::process()
    ([pr#19591](https://github.com/ceph/ceph/pull/19591), Bingyin Zhang)

-   rgw: drop outdated function doc
    ([pr#18370](https://github.com/ceph/ceph/pull/18370), Jiaying Ren)

-   rgw: drop \"realm remove\" in radosgw-admin
    ([pr#18212](https://github.com/ceph/ceph/pull/18212), Shasha Lu)

-   rgw: drop redundant RGW_OP_STAT_OBJ check
    ([pr#19933](https://github.com/ceph/ceph/pull/19933), Bingyin Zhang)

-   rgw: drop the unnecessary handling of Swift\'s X-Storage-Policy on
    objects ([pr#16383](https://github.com/ceph/ceph/pull/16383),
    Jiaying Ren)

-   rgw: drop the unused function init_anon_user()
    ([pr#16874](https://github.com/ceph/ceph/pull/16874), Radoslaw
    Zarzynski)

-   rgw: Drop unnecessary return
    ([pr#17520](https://github.com/ceph/ceph/pull/17520), Jos Collin)

-   rgw: drop unused function apply_epoch
    ([pr#17593](https://github.com/ceph/ceph/pull/17593), Shasha Lu)

-   rgw: drop unused iter in XMLObj::find_first
    ([pr#19709](https://github.com/ceph/ceph/pull/19709), luomuyao)

-   rgw: drop unused variable bucket_instance_ids
    ([pr#19708](https://github.com/ceph/ceph/pull/19708), Bingyin Zhang)

-   rgw: drop unused variable in copy_obj_data()
    ([pr#18477](https://github.com/ceph/ceph/pull/18477), Enming Zhang)

-   rgw: drop unused vector elements
    ([pr#19815](https://github.com/ceph/ceph/pull/19815), Bingyin Zhang)

-   rgw: drop useless includes in rgw\_{main.cc, common.h}
    ([pr#19109](https://github.com/ceph/ceph/pull/19109), Jiaying Ren)

-   rgw: drop useless lines
    ([pr#19817](https://github.com/ceph/ceph/pull/19817), Bingyin Zhang)

-   rgw: drop useless type conversion
    ([pr#19824](https://github.com/ceph/ceph/pull/19824), Bingyin Zhang)

-   rgw: drop variable bl in rgw_op.cc
    ([pr#19584](https://github.com/ceph/ceph/pull/19584), Bingyin Zhang)

-   rgw: Drop #warning TODO
    ([issue#19851](http://tracker.ceph.com/issues/19851),
    [pr#17012](https://github.com/ceph/ceph/pull/17012), Jos Collin)

-   rgw: dump Last-Modified in Swift\'s responses for GET/HEAD on
    container ([issue#20883](http://tracker.ceph.com/issues/20883),
    [pr#16757](https://github.com/ceph/ceph/pull/16757), Radoslaw
    Zarzynski)

-   rgw: enable \'qlen\' & \'qactive\' performance counters
    ([pr#20842](https://github.com/ceph/ceph/pull/20842), Mark Kogan)

-   rgw: encoding fixes
    ([issue#23779](http://tracker.ceph.com/issues/23779),
    [pr#21500](https://github.com/ceph/ceph/pull/21500), Yehuda Sadeh)

-   rgw: Error check on return of read_line()
    ([pr#17880](https://github.com/ceph/ceph/pull/17880), Amit Kumar)

-   rgw: es module: set compression type correctly
    ([issue#22758](http://tracker.ceph.com/issues/22758),
    [pr#20796](https://github.com/ceph/ceph/pull/20796), Abhishek
    Lekshmanan)

-   rgw: evaluate the correct bucket action for GetACL bucket operation
    ([issue#21013](http://tracker.ceph.com/issues/21013),
    [pr#17050](https://github.com/ceph/ceph/pull/17050), Abhishek
    Lekshmanan)

-   

    rgw: exit early if rgw_bucket_set_attrs() fails ([pr#17041](https://github.com/ceph/ceph/pull/17041), dengxiafubi)

    :   rgw: Expire entries in bucket info cache

-   rgw_file: fix write error when the write offset overlaps
    ([issue#21455](http://tracker.ceph.com/issues/21455),
    [pr#17809](https://github.com/ceph/ceph/pull/17809), Yao Zongyou)

-   rgw: fix a bug in rgw cache in delete_system_obj and get_system_obj
    ([pr#10992](https://github.com/ceph/ceph/pull/10992), zhangshaowen)

-   rgw: fix accessing expired memory in PrefixableSignatureHelper
    ([issue#21085](http://tracker.ceph.com/issues/21085),
    [pr#17206](https://github.com/ceph/ceph/pull/17206), Radoslaw
    Zarzynski)

-   rgw: fix a typo in comment
    ([pr#19608](https://github.com/ceph/ceph/pull/19608), luomuyao)

-   rgw: fix a typo in comment
    ([pr#20164](https://github.com/ceph/ceph/pull/20164), luomuyao)

-   rgw: fix a typo in comment
    ([pr#20355](https://github.com/ceph/ceph/pull/20355), luomuyao)

-   rgw: fix a typo in rgw_perms\[\]
    ([pr#20024](https://github.com/ceph/ceph/pull/20024), luomuyao)

-   rgw: fix bilog entries on multipart complete
    ([issue#21772](http://tracker.ceph.com/issues/21772),
    [pr#18271](https://github.com/ceph/ceph/pull/18271), Casey Bodley)

-   rgw: fix BZ 1500904, stale bucket index entry remains after obj
    delete ([pr#18709](https://github.com/ceph/ceph/pull/18709), J. Eric
    Ivancich)

-   rgw: fix chained cache invalidation to prevent cache size growth
    ([issue#22410](http://tracker.ceph.com/issues/22410),
    [pr#19455](https://github.com/ceph/ceph/pull/19455), Mark Kogan)

-   rgw: Fix closing tag for Prefix
    ([pr#17663](https://github.com/ceph/ceph/pull/17663), Shasha Lu)

-   rgw: fix cls_bucket_head result order consistency
    ([pr#18700](https://github.com/ceph/ceph/pull/18700), Tianshan Qu)

-   rgw: fix collect()\'s return in coroutine
    ([pr#19606](https://github.com/ceph/ceph/pull/19606), Xinying Song)

-   rgw: fix command argument error for radosgw-admin
    ([issue#21723](http://tracker.ceph.com/issues/21723),
    [pr#18175](https://github.com/ceph/ceph/pull/18175), Yao Zongyou)

-   rgw: fix \'copy part\' without \'x-amz-copy-source-range\'
    ([issue#22729](http://tracker.ceph.com/issues/22729),
    [pr#20002](https://github.com/ceph/ceph/pull/20002), Malcolm Lee)

-   rgw: fix \'copy part\' without \'x-amz-copy-source-range\' when
    compression enabled
    ([issue#23196](http://tracker.ceph.com/issues/23196),
    [pr#20686](https://github.com/ceph/ceph/pull/20686), fang yuxiang)

-   rgw: fix crash with rgw_run_sync_thread false
    ([issue#20448](http://tracker.ceph.com/issues/20448),
    [pr#20769](https://github.com/ceph/ceph/pull/20769), Orit Wasserman)

-   rgw: Fix dereference of empty optional
    ([issue#21962](http://tracker.ceph.com/issues/21962),
    [pr#18602](https://github.com/ceph/ceph/pull/18602), Adam C.
    Emerson)

-   rgw: fix error handling for GET with ?torrent
    ([issue#23506](http://tracker.ceph.com/issues/23506),
    [pr#21576](https://github.com/ceph/ceph/pull/21576), Casey Bodley)

-   rgw: fix error handling in Browser Uploads
    ([pr#15054](https://github.com/ceph/ceph/pull/15054), Radoslaw
    Zarzynski)

-   rgw: fix error handling in ListBucketIndexesCR
    ([issue#21735](http://tracker.ceph.com/issues/21735),
    [pr#18198](https://github.com/ceph/ceph/pull/18198), Casey Bodley)

-   rgw: fixes for multisite replication of encrypted objects
    ([issue#20668](http://tracker.ceph.com/issues/20668),
    [issue#20671](http://tracker.ceph.com/issues/20671),
    [pr#16612](https://github.com/ceph/ceph/pull/16612), Casey Bodley)

-   rgw: fix extra_data_len handling in PutObj filters
    ([issue#21895](http://tracker.ceph.com/issues/21895),
    [pr#18489](https://github.com/ceph/ceph/pull/18489), Casey Bodley)

-   rgw: fix for empty query string in beast frontend
    ([issue#22797](http://tracker.ceph.com/issues/22797),
    [pr#20120](https://github.com/ceph/ceph/pull/20120), Casey Bodley)

-   rgw: fix for issue #21647
    ([issue#23859](http://tracker.ceph.com/issues/23859),
    [pr#21647](https://github.com/ceph/ceph/pull/21647), Yehuda Sadeh)

-   rgw: fix for pause in beast frontend
    ([issue#21831](http://tracker.ceph.com/issues/21831),
    [pr#18402](https://github.com/ceph/ceph/pull/18402), Casey Bodley)

-   rgw: fix for usage truncated flag
    ([pr#20926](https://github.com/ceph/ceph/pull/20926), Yehuda Sadeh,
    Greg Farnum, Robin H. Johnson)

-   rgw: Fix getter function names in RGWEnv
    ([pr#18377](https://github.com/ceph/ceph/pull/18377), Jos Collin)

-   rgw: fix GET website response error code
    ([issue#22272](http://tracker.ceph.com/issues/22272),
    [pr#19236](https://github.com/ceph/ceph/pull/19236), Dmitry Plyakin)

-   rgw: fix handling of ENOENT in RGWRadosGetOmapKeysCR
    ([pr#19878](https://github.com/ceph/ceph/pull/19878), Casey Bodley)

-   rgw: fix index cancel op miss update header
    ([pr#20396](https://github.com/ceph/ceph/pull/20396), Tianshan Qu)

-   rgw: Fix infinite call for bi list when resharding a bucket
    ([issue#22721](http://tracker.ceph.com/issues/22721),
    [pr#21584](https://github.com/ceph/ceph/pull/21584), Orit Wasserman)

-   rgw: fix lc process only schdule the first item of lc objects
    ([issue#21022](http://tracker.ceph.com/issues/21022),
    [pr#17061](https://github.com/ceph/ceph/pull/17061), Shasha Lu)

-   rgw:fix list objects with marker wrong result when bucket is enable
    versioning ([issue#21500](http://tracker.ceph.com/issues/21500),
    [pr#17934](https://github.com/ceph/ceph/pull/17934), yuliyang)

-   rgw: fix memory fragmentation problem reading data from client
    ([pr#20724](https://github.com/ceph/ceph/pull/20724), Marcus Watts)

-   rgw: Fix multisite Synchronization failed when read and write delete
    ... ([issue#22804](http://tracker.ceph.com/issues/22804),
    [pr#20814](https://github.com/ceph/ceph/pull/20814), Niu Pengju)

-   rgw: fix not responding when receiving SIGHUP signal
    ([pr#16854](https://github.com/ceph/ceph/pull/16854), Yao Zongyou)

-   rgw: fix null pointer crush
    ([pr#18861](https://github.com/ceph/ceph/pull/18861), Sibei Gao)

-   rgw: fix obj copied from remote gateway acl full_control issue
    ([issue#20658](http://tracker.ceph.com/issues/20658),
    [pr#16127](https://github.com/ceph/ceph/pull/16127), Enming Zhang)

-   rgw: fix opslog cannot record remote_addr
    ([issue#20931](http://tracker.ceph.com/issues/20931),
    [pr#16860](https://github.com/ceph/ceph/pull/16860), Jiaying Ren)

-   rgw: fix opslog can\'t record referrer when using curl as client
    ([issue#20935](http://tracker.ceph.com/issues/20935),
    [pr#16863](https://github.com/ceph/ceph/pull/16863), Jiaying Ren)

-   rgw: fix opslog uri as per Amazon s3
    ([issue#20971](http://tracker.ceph.com/issues/20971),
    [pr#16958](https://github.com/ceph/ceph/pull/16958), Jiaying Ren)

-   rgw: fix radosgw-admin bucket rm with \--purge-objects and
    \--bypass-gc ([issue#22122](http://tracker.ceph.com/issues/22122),
    [issue#19959](http://tracker.ceph.com/issues/19959),
    [pr#18922](https://github.com/ceph/ceph/pull/18922), Aleksei
    Gutikov)

-   rgw: fix radosgw-admin quota enable return value bug
    ([issue#21608](http://tracker.ceph.com/issues/21608),
    [pr#18057](https://github.com/ceph/ceph/pull/18057), baixueyu)

-   rgw: fix radosgw linkage with WITH_RADOSGW_BEAST_FRONTEND=OFF
    ([issue#23680](http://tracker.ceph.com/issues/23680),
    [pr#21380](https://github.com/ceph/ceph/pull/21380), Casey Bodley)

-   rgw: fix recursive lock
    ([pr#19430](https://github.com/ceph/ceph/pull/19430), Tianshan Qu)

-   rgw: fix resource leak in rgw_bucket.cc and rgw_user.cc
    ([issue#21214](http://tracker.ceph.com/issues/21214),
    [pr#17353](https://github.com/ceph/ceph/pull/17353), Luo Kexue)

-   rgw: fix return value of auth v2/v4
    ([issue#22439](http://tracker.ceph.com/issues/22439),
    [pr#19310](https://github.com/ceph/ceph/pull/19310), Bingyin Zhang)

-   rgw: fix rewrite a versioning object create a new object bug
    ([issue#21984](http://tracker.ceph.com/issues/21984),
    [pr#18662](https://github.com/ceph/ceph/pull/18662), Enming Zhang)

-   rgw: fix rewrite options usage text
    ([pr#18968](https://github.com/ceph/ceph/pull/18968), Jos Collin)

-   rgw: fix RGWCompletionManager get_next stuck after going down
    ([issue#22799](http://tracker.ceph.com/issues/22799),
    [pr#20095](https://github.com/ceph/ceph/pull/20095), Tianshan Qu)

-   rgw: fix RGWLibIO did not init RGWEnv
    ([pr#19065](https://github.com/ceph/ceph/pull/19065), Tianshan Qu)

-   rgw: fix s3 website redirection error
    ([pr#19252](https://github.com/ceph/ceph/pull/19252), yuliyang)

-   rgw: fix s3website redirect location string length
    ([pr#19826](https://github.com/ceph/ceph/pull/19826), yuliyang)

-   rgw: fix Swift container naming rules
    ([issue#19264](http://tracker.ceph.com/issues/19264),
    [pr#13992](https://github.com/ceph/ceph/pull/13992), Robin H.
    Johnson)

-   rgw: Fix swift object expiry not deleting objects
    ([issue#22084](http://tracker.ceph.com/issues/22084),
    [pr#18821](https://github.com/ceph/ceph/pull/18821), Pavan
    Rallabhandi)

-   rgw: fix sync status conflict with cloud sync
    ([pr#21425](https://github.com/ceph/ceph/pull/21425), Casey Bodley)

-   rgw: fix the bug of radowgw-admin zonegroup set requires realm
    ([issue#21583](http://tracker.ceph.com/issues/21583),
    [pr#19061](https://github.com/ceph/ceph/pull/19061), lvshanchun)

-   rgw: fix the max-uploads parameter not work
    ([issue#22825](http://tracker.ceph.com/issues/22825),
    [pr#20158](https://github.com/ceph/ceph/pull/20158), Xin Liao)

-   rgw: fix the return type is wrong
    ([pr#19773](https://github.com/ceph/ceph/pull/19773), hechuang)

-   rgw: fix total_time to msec as per AWS S3
    ([pr#17541](https://github.com/ceph/ceph/pull/17541), Jiaying Ren)

-   rgw: fix typo anynoymous to anonymous
    ([pr#19281](https://github.com/ceph/ceph/pull/19281), Bingyin Zhang)

-   rgw: fix typo compete to complete
    ([pr#19675](https://github.com/ceph/ceph/pull/19675), Bingyin Zhang)

-   rgw: Fix typo in comment
    ([pr#21032](https://github.com/ceph/ceph/pull/21032), Simran
    Singhal)

-   rgw: fix typo in GetOmapKeysCR
    ([pr#19713](https://github.com/ceph/ceph/pull/19713), lvshanchun)

-   rgw: fix typo signle to single
    ([pr#19517](https://github.com/ceph/ceph/pull/19517), Bingyin Zhang)

-   rgw: fix typo woild to would
    ([pr#19472](https://github.com/ceph/ceph/pull/19472), Bingyin Zhang)

-   rgw: Fix use after free in IAM policy parser
    ([pr#16823](https://github.com/ceph/ceph/pull/16823), Adam C.
    Emerson)

-   rgw: fix use of libcurl with empty header values
    ([issue#23663](http://tracker.ceph.com/issues/23663),
    [pr#21358](https://github.com/ceph/ceph/pull/21358), Casey Bodley)

-   rgw: format logs in file rgw_lc.cc
    ([pr#19615](https://github.com/ceph/ceph/pull/19615), Bingyin Zhang)

-   rgw: format rgw_bucket_dir_header in ceph-dencoder
    ([pr#19753](https://github.com/ceph/ceph/pull/19753), Bingyin Zhang)

-   

    rgw: gc use aio ([pr#20546](https://github.com/ceph/ceph/pull/20546), Yehuda Sadeh)

    :   rgw: Handle stale bucket info in RGWDeleteBucketPolicy rgw:
        Handle stale bucket info in RGWDeleteBucketWebsite rgw: Handle
        stale bucket info in RGWPutBucketPolicy rgw: Handle stale bucket
        info in RGWPutMetadataBucket rgw: Handle stale bucket info in
        RGWSetBucketVersioning rgw: Handle stale bucket info in
        RGWSetBucketWebsite

-   rgw: honor the tenant part of rgw_bucket during comparisons
    ([issue#20897](http://tracker.ceph.com/issues/20897),
    [pr#16796](https://github.com/ceph/ceph/pull/16796), Radoslaw
    Zarzynski)

-   rgw: iam policy printing cleanups
    ([pr#18961](https://github.com/ceph/ceph/pull/18961), Kefu Chai)

-   rgw: Ignoring the returned error
    ([pr#17907](https://github.com/ceph/ceph/pull/17907), Amit Kumar)

-   rgw: implement ipv4 aws:SourceIp condition for bucket policy
    ([pr#19167](https://github.com/ceph/ceph/pull/19167), yuliyang)

-   rgw: improve handling of Swift\'s error messages and limits
    ([issue#17938](http://tracker.ceph.com/issues/17938),
    [issue#21169](http://tracker.ceph.com/issues/21169),
    [issue#17935](http://tracker.ceph.com/issues/17935),
    [issue#17934](http://tracker.ceph.com/issues/17934),
    [issue#17936](http://tracker.ceph.com/issues/17936),
    [pr#15369](https://github.com/ceph/ceph/pull/15369), Radoslaw
    Zarzynski)

-   rgw: improve sync status: display behind bucket shards
    ([pr#20027](https://github.com/ceph/ceph/pull/20027), lvshanchun)

-   rgw: improve sync status
    ([pr#19573](https://github.com/ceph/ceph/pull/19573), lvshanchun)

-   rgw: include SSE-KMS headers in encrypted upload response
    ([issue#21576](http://tracker.ceph.com/issues/21576),
    [pr#17999](https://github.com/ceph/ceph/pull/17999), Casey Bodley)

-   rgw: incorporate the Transfer-Encoding fix for CivetWeb
    ([issue#21015](http://tracker.ceph.com/issues/21015),
    [pr#17072](https://github.com/ceph/ceph/pull/17072), Radoslaw
    Zarzynski)

-   rgw: Initialization of epoch,len
    ([pr#17722](https://github.com/ceph/ceph/pull/17722), Amit Kumar)

-   rgw: Initialize is_master, max_aio, size
    ([pr#16933](https://github.com/ceph/ceph/pull/16933), amitkuma)

-   rgw: Initializes uninitialized members
    ([pr#16855](https://github.com/ceph/ceph/pull/16855), Amit Kumar)

-   rgw: init oldest period after setting run_sync_thread
    ([issue#21996](http://tracker.ceph.com/issues/21996),
    [pr#18664](https://github.com/ceph/ceph/pull/18664), Orit Wasserman,
    Casey Bodley)

-   rgw: keep compression type consistent between parts of s3 Multipart
    ([pr#19740](https://github.com/ceph/ceph/pull/19740), fang yuxiang)

-   rgw: keystone: bump up logging when error is received
    ([issue#22151](http://tracker.ceph.com/issues/22151),
    [pr#18985](https://github.com/ceph/ceph/pull/18985), Abhishek
    Lekshmanan)

-   rgw:lc fix expiration time
    ([issue#21533](http://tracker.ceph.com/issues/21533),
    [pr#17824](https://github.com/ceph/ceph/pull/17824), Shasha Lu)

-   rgw: lc support Content-MD5 request header and fix a rgw crash bug
    ([issue#21980](http://tracker.ceph.com/issues/21980),
    [pr#18534](https://github.com/ceph/ceph/pull/18534), Enming Zhang)

-   rgw: lease_cr-\>go_down is called twice, remove the needless one
    ([pr#19394](https://github.com/ceph/ceph/pull/19394), Zhang Shaowen)

-   rgw: librgw: export multitenancy support
    ([pr#19358](https://github.com/ceph/ceph/pull/19358), Tao Chen)

-   rgw: librgw: fix shutdown err with resources uncleaned
    ([issue#22296](http://tracker.ceph.com/issues/22296),
    [pr#19279](https://github.com/ceph/ceph/pull/19279), Tao Chen)

-   rgw: lifecycle omap entry was removed in abnormal situation
    ([pr#19921](https://github.com/ceph/ceph/pull/19921), fang yuxiang)

-   rgw: list_objects() honors end_marker regardless of namespace
    ([issue#18977](http://tracker.ceph.com/issues/18977),
    [pr#15273](https://github.com/ceph/ceph/pull/15273), Radoslaw
    Zarzynski)

-   rgw: loadgen fix generate random object name rgw crash issue
    ([issue#22006](http://tracker.ceph.com/issues/22006),
    [pr#18536](https://github.com/ceph/ceph/pull/18536), Enming Zhang)

-   rgw: log the right http status code in civetweb frontend\'s access
    log ([issue#22538](http://tracker.ceph.com/issues/22538),
    [pr#19678](https://github.com/ceph/ceph/pull/19678), Yao Zongyou)

-   rgw: log unlink_instance mtime as object\'s mtime
    ([issue#18885](http://tracker.ceph.com/issues/18885),
    [pr#20016](https://github.com/ceph/ceph/pull/20016), Yehuda Sadeh)

-   rgw: lttng: Trace rgw data transfer, bi entry and object header
    update processes
    ([pr#20556](https://github.com/ceph/ceph/pull/20556), Yang Honggang)

-   rgw: make init env methods return an error
    ([issue#23039](http://tracker.ceph.com/issues/23039),
    [pr#20488](https://github.com/ceph/ceph/pull/20488), Abhishek
    Lekshmanan)

-   rgw: make radosgw object stat RGW_ATTR_COMPRESSION dump readable
    ([pr#19846](https://github.com/ceph/ceph/pull/19846), fang yuxiang)

-   rgw: mfa support
    ([pr#19283](https://github.com/ceph/ceph/pull/19283), Yehuda Sadeh)

-   rgw: mimic: rgw: policy: modify s3:ListBucketMultiPartUploads to
    s3:ListBucketMul
    ([issue#24062](http://tracker.ceph.com/issues/24062),
    [pr#21916](https://github.com/ceph/ceph/pull/21916), xiangxiang)

-   rgw: modify s3 type subuser access permissions fail through admin
    rest api ([issue#21983](http://tracker.ceph.com/issues/21983),
    [pr#18641](https://github.com/ceph/ceph/pull/18641), yuliyang)

-   rgw: move all pool creation into rgw_init_ioctx
    ([issue#23480](http://tracker.ceph.com/issues/23480),
    [pr#21534](https://github.com/ceph/ceph/pull/21534), Casey Bodley)

-   rgw: mrgw.sh uses instance name \'client.rgw\'
    ([pr#18404](https://github.com/ceph/ceph/pull/18404), Casey Bodley)

-   rgw: multisite log tracing
    ([pr#16492](https://github.com/ceph/ceph/pull/16492), Yehuda Sadeh,
    Casey Bodley)

-   rgw,nfs: Add hint to use -o sync when mouting
    ([pr#16210](https://github.com/ceph/ceph/pull/16210), Adam Kupczyk)

-   rgw: no need to deal with md5 header in get_data
    ([pr#19144](https://github.com/ceph/ceph/pull/19144), Zhang Shaowen)

-   rgw: optimize function abort_bucket_multiparts
    ([pr#19710](https://github.com/ceph/ceph/pull/19710), Bingyin Zhang)

-   rgw: optimize function bucket_lc_prepare
    ([pr#19613](https://github.com/ceph/ceph/pull/19613), Bingyin Zhang)

-   rgw: optimize function parse_raw_oid
    ([pr#19814](https://github.com/ceph/ceph/pull/19814), Bingyin Zhang)

-   rgw: optimize function RGWHandler::do_init_permissions
    ([pr#19700](https://github.com/ceph/ceph/pull/19700), Bingyin Zhang)

-   rgw: optimize memory usage in function rgw_bucket::get_key
    ([pr#19391](https://github.com/ceph/ceph/pull/19391), Bingyin Zhang)

-   rgw: optimize next start time for lifecycle
    ([pr#19596](https://github.com/ceph/ceph/pull/19596), Bingyin Zhang)

-   rgw: optimize the rgw-attr del code logic
    ([pr#18895](https://github.com/ceph/ceph/pull/18895), wangsongbo)

-   rgw: optimize time skew check
    ([pr#19511](https://github.com/ceph/ceph/pull/19511), Bingyin Zhang)

-   rgw: parse old rgw_obj with namespace correctly
    ([issue#22982](http://tracker.ceph.com/issues/22982),
    [pr#20425](https://github.com/ceph/ceph/pull/20425), Yehuda Sadeh)

-   rgw: policy: support for s3 conditionals in ListBucket Op
    ([pr#16628](https://github.com/ceph/ceph/pull/16628), Abhishek
    Lekshmanan)

-   rgw: Potential fix for possible 500 on POST
    ([pr#18954](https://github.com/ceph/ceph/pull/18954), Adam C.
    Emerson)

-   rgw: Prevent overflow of cached stats values
    ([issue#20934](http://tracker.ceph.com/issues/20934),
    [pr#17116](https://github.com/ceph/ceph/pull/17116), Aleksei
    Gutikov)

-   rgw: proper error message when tier_type does not exist
    ([issue#22469](http://tracker.ceph.com/issues/22469),
    [pr#19575](https://github.com/ceph/ceph/pull/19575), lvshanchun,
    Chang Liu)

-   rgw: pull up beast submodule and update frontend
    ([pr#17923](https://github.com/ceph/ceph/pull/17923), Casey Bodley)

-   rgw: put bucket policy panics RGW process
    ([issue#22541](http://tracker.ceph.com/issues/22541),
    [pr#19687](https://github.com/ceph/ceph/pull/19687), Bingyin Zhang)

-   rgw: radosgw-admin abort early for user stats for empty uids
    ([issue#23322](http://tracker.ceph.com/issues/23322),
    [pr#20846](https://github.com/ceph/ceph/pull/20846), Abhishek
    Lekshmanan)

-   rgw: radosgw-admin should not use metadata cache for readonly
    commands ([issue#23468](http://tracker.ceph.com/issues/23468),
    [pr#21129](https://github.com/ceph/ceph/pull/21129), Orit Wasserman)

-   rgw: radosgw-admin zonegroup get and zone get return defaults when
    there is no realm
    ([issue#21615](http://tracker.ceph.com/issues/21615),
    [pr#18667](https://github.com/ceph/ceph/pull/18667), lvshanchun)

-   rgw: radosgw: fix awsv4 header line sort order
    ([issue#21607](http://tracker.ceph.com/issues/21607),
    [pr#18046](https://github.com/ceph/ceph/pull/18046), Marcus Watts)

-   rgw: radosgw: usage: fix bytes_sent bug
    ([issue#19870](http://tracker.ceph.com/issues/19870),
    [pr#16834](https://github.com/ceph/ceph/pull/16834), Marcus Watts)

-   rgw: raise log level on coroutine shutdown errors
    ([issue#23974](http://tracker.ceph.com/issues/23974),
    [pr#21791](https://github.com/ceph/ceph/pull/21791), Casey Bodley)

-   rgw: Reinstating error codes mapping for Roles
    ([pr#20309](https://github.com/ceph/ceph/pull/20309), Pritha
    Srivastava)

-   rgw: reject encrypted object COPY before supported
    ([issue#23232](http://tracker.ceph.com/issues/23232),
    [pr#20739](https://github.com/ceph/ceph/pull/20739), Jeegn Chen)

-   rgw: release cls lock if taken in RGWCompleteMultipart
    ([issue#21596](http://tracker.ceph.com/issues/21596),
    [pr#18104](https://github.com/ceph/ceph/pull/18104), Matt Benjamin)

-   rgw: Remove assertions in IAM Policy
    ([pr#18225](https://github.com/ceph/ceph/pull/18225), Adam C.
    Emerson)

-   rgw: remove get_system_obj_attrs in function RGWDeleteLC::execute
    and RGWDeleteCORS::execute
    ([pr#19582](https://github.com/ceph/ceph/pull/19582), Bingyin Zhang)

-   rgw: remove placement_rule from rgw_link_bucket()
    ([issue#21990](http://tracker.ceph.com/issues/21990),
    [pr#18657](https://github.com/ceph/ceph/pull/18657), Casey Bodley)

-   rgw: remove redundant parenthesis in logs
    ([pr#19375](https://github.com/ceph/ceph/pull/19375), Bingyin Zhang)

-   rgw: remove redundant S3AnonymousEngine
    ([pr#19474](https://github.com/ceph/ceph/pull/19474), Bingyin Zhang)

-   rgw: remove redundant signature compare in LocalEngine::authenticate
    ([pr#19676](https://github.com/ceph/ceph/pull/19676), Bingyin Zhang)

-   rgw: Remove the useless output when list zones
    ([pr#17434](https://github.com/ceph/ceph/pull/17434), iliul)

-   rgw: remove unused cls_user_add_bucket
    ([pr#19917](https://github.com/ceph/ceph/pull/19917), Yao Zongyou)

-   rgw: remove unused disable_signal_fd
    ([pr#18875](https://github.com/ceph/ceph/pull/18875), Yao Zongyou)

-   rgw: remove unused function get_system_obj_attrs
    ([pr#19852](https://github.com/ceph/ceph/pull/19852), Yao Zongyou)

-   rgw: Remove unused Parameter in Function RGWConf::init()
    ([pr#17129](https://github.com/ceph/ceph/pull/17129), Wen Zhang)

-   rgw: remove unused param in AWSGeneralAbstractor::get_auth_data_v4
    ([pr#19250](https://github.com/ceph/ceph/pull/19250), Bingyin Zhang)

-   rgw: remove unused param in get_bucket_instance_policy_from_attr
    ([pr#19129](https://github.com/ceph/ceph/pull/19129), Bingyin Zhang)

-   rgw: remove unused variables
    ([pr#16649](https://github.com/ceph/ceph/pull/16649), Zhang Lei)

-   rgw: remove useless lines in RGWDeleteBucket::execute
    ([pr#19699](https://github.com/ceph/ceph/pull/19699), Bingyin Zhang)

-   rgw: reshard cancel command should clear bucket resharding flag
    ([issue#21619](http://tracker.ceph.com/issues/21619),
    [pr#21120](https://github.com/ceph/ceph/pull/21120), Orit Wasserman)

-   rgw: reshard should not update stats when linking new bucket
    instance ([issue#22124](http://tracker.ceph.com/issues/22124),
    [pr#19253](https://github.com/ceph/ceph/pull/19253), Orit Wasserman)

-   rgw: retry CORS put/delete operations on ECANCELLED
    ([issue#22517](http://tracker.ceph.com/issues/22517),
    [pr#19601](https://github.com/ceph/ceph/pull/19601), Adam C.
    Emerson)

-   rgw: return \'Access-Control-Allow-Origin\' header when the set and
    delete bucket website through XMLHttpRequest
    ([pr#17632](https://github.com/ceph/ceph/pull/17632), yuliyang)

-   rgw: return \'Access-Control-Allow-Origin\' header when the set
    bucket versioning through XMLHttpRequest
    ([pr#17631](https://github.com/ceph/ceph/pull/17631), yuliyang)

-   rgw: return bucket\'s location no matter which zonegroup it located
    in ([issue#21125](http://tracker.ceph.com/issues/21125),
    [pr#17250](https://github.com/ceph/ceph/pull/17250), Shasha Lu)

-   rgw: return EINVAL if max_keys can not convert correctly
    ([issue#23586](http://tracker.ceph.com/issues/23586),
    [pr#21285](https://github.com/ceph/ceph/pull/21285), yuliyang)

-   rgw: Return Error if Bucket Policy Contians Undefined Action
    ([pr#17433](https://github.com/ceph/ceph/pull/17433), zhangwen)

-   rgw: Returning when dst_ioctx.operate() returns error
    ([pr#17873](https://github.com/ceph/ceph/pull/17873), Amit Kumar)

-   rgw: return valid Location element, CompleteMultipartUpload
    ([pr#19902](https://github.com/ceph/ceph/pull/19902), Matt Benjamin)

-   rgw: revert PR #8765
    ([pr#16807](https://github.com/ceph/ceph/pull/16807), fang.yuxiang)

-   rgw: Revert \"radosgw: fix awsv4 header line sort order.\"
    ([issue#21832](http://tracker.ceph.com/issues/21832),
    [pr#18381](https://github.com/ceph/ceph/pull/18381), Casey Bodley)

-   rgw: Revert \"rgw_file: disable FLAG_EXACT_MATCH enforcement\"
    ([issue#22827](http://tracker.ceph.com/issues/22827),
    [pr#20171](https://github.com/ceph/ceph/pull/20171), Matt Benjamin)

-   rgw: Revert \"rgw: reshard should not update stats when linking new
    bucket instance\"
    ([pr#20052](https://github.com/ceph/ceph/pull/20052), Orit
    Wasserman)

-   rgw: rework json/xml escape usage follow #19806
    ([pr#19845](https://github.com/ceph/ceph/pull/19845), fang yuxiang)

-   rgw: rgw-admin: check input parameters for friendly prompt
    ([pr#17343](https://github.com/ceph/ceph/pull/17343), Yao Zongyou)

-   rgw: rgw-admin: check the data extra pool supports omap
    ([pr#18978](https://github.com/ceph/ceph/pull/18978), Yao Zongyou)

-   rgw: rgw-admin: properly filtering bucket stats by user_id or
    bucket_name ([pr#19401](https://github.com/ceph/ceph/pull/19401),
    Yao Zongyou)

-   rgw: rgw-admin: require \--yes-i-really-mean-it when using
    \--inconsistent_index
    ([issue#20777](http://tracker.ceph.com/issues/20777),
    [pr#17185](https://github.com/ceph/ceph/pull/17185), Orit Wasserman)

-   rgw: rgw-admin: support for processing all gc objects including
    unexpired ([pr#17482](https://github.com/ceph/ceph/pull/17482), Yao
    Zongyou)

-   rgw: RGW: change function parameters from value to refrence
    ([pr#18355](https://github.com/ceph/ceph/pull/18355), Sibei Gao)

-   rgw: RGWCivetWeb::read_data: fix arguments to mg_read() call
    ([issue#23596](http://tracker.ceph.com/issues/23596),
    [pr#21291](https://github.com/ceph/ceph/pull/21291), Nathan Cutler)

-   rgw: rgw clean-up: remove unreferenced pure virtual class
    StreamObjData
    ([pr#18799](https://github.com/ceph/ceph/pull/18799), J. Eric
    Ivancich)

-   rgw: rgw clean-up: remove unused var & func in
    RGWRados::SystemObject
    ([pr#18987](https://github.com/ceph/ceph/pull/18987), J. Eric
    Ivancich)

-   rgw: rgw cleanup: some unnecessary function called and repeated
    assignment ([pr#18817](https://github.com/ceph/ceph/pull/18817),
    Enming Zhang)

-   rgw: rgw cloud sync
    ([issue#21802](http://tracker.ceph.com/issues/21802),
    [pr#18932](https://github.com/ceph/ceph/pull/18932), lvshanchun,
    Yehuda Sadeh, Chang Liu, Abhishek Lekshmanan)

-   rgw: RGWEnv::set() takes std::string
    ([issue#22101](http://tracker.ceph.com/issues/22101),
    [pr#18866](https://github.com/ceph/ceph/pull/18866), Casey Bodley)

-   rgw: rgw_file: alternate fix deadlock on lru eviction
    ([pr#20034](https://github.com/ceph/ceph/pull/20034), Matt Benjamin)

-   rgw: rgw_file: avoid evaluating nullptr for readdir offset
    ([pr#20145](https://github.com/ceph/ceph/pull/20145), Matt Benjamin)

-   rgw: rgw_file: conditionally unlink handles when direct deleted
    ([issue#23299](http://tracker.ceph.com/issues/23299),
    [pr#20834](https://github.com/ceph/ceph/pull/20834), Matt Benjamin)

-   rgw: rgw_file: explicit NFSv3 open() emulation
    ([pr#18365](https://github.com/ceph/ceph/pull/18365), Matt Benjamin)

-   rgw: rgw_file: fix LRU lane lock in evict_block()
    ([issue#21141](http://tracker.ceph.com/issues/21141),
    [pr#17267](https://github.com/ceph/ceph/pull/17267), Matt Benjamin)

-   rgw: rgw_file: implement variant offset readdir processing
    ([pr#18335](https://github.com/ceph/ceph/pull/18335), Matt Benjamin)

-   rgw: rgw_file: introduce new fsid and rgw_mount
    ([pr#15330](https://github.com/ceph/ceph/pull/15330), Gui Hecheng)

-   rgw: rgw_file: set s-\>obj_size from bytes_written
    ([issue#21940](http://tracker.ceph.com/issues/21940),
    [pr#18571](https://github.com/ceph/ceph/pull/18571), Matt Benjamin)

-   rgw: rgw_file: Silence unused-function warnings
    ([pr#19278](https://github.com/ceph/ceph/pull/19278), Brad Hubbard)

-   rgw: RGW: fix a bug about inconsistent unit of comparison
    ([issue#21590](http://tracker.ceph.com/issues/21590),
    [pr#17958](https://github.com/ceph/ceph/pull/17958), gaosibei)

-   rgw: rgw.iam: change \'1\' to \'1ULL\' in function print_actions
    ([pr#18900](https://github.com/ceph/ceph/pull/18900), Bingyin Zhang)

-   rgw: rgw_lc: add support for optional filter argument and make ID
    optional ([issue#19587](http://tracker.ceph.com/issues/19587),
    [issue#20872](http://tracker.ceph.com/issues/20872),
    [pr#16818](https://github.com/ceph/ceph/pull/16818), Abhishek
    Lekshmanan)

-   rgw: rgw_lc: support for AWSv4 authentication
    ([pr#16734](https://github.com/ceph/ceph/pull/16734), Abhishek
    Lekshmanan)

-   rgw: rgw_log, rgw_file: account for new required envvars
    ([issue#21942](http://tracker.ceph.com/issues/21942),
    [pr#18572](https://github.com/ceph/ceph/pull/18572), Matt Benjamin)

-   rgw: Rgw master fix plus
    ([issue#21000](http://tracker.ceph.com/issues/21000),
    [issue#21003](http://tracker.ceph.com/issues/21003),
    [issue#20501](http://tracker.ceph.com/issues/20501),
    [pr#17040](https://github.com/ceph/ceph/pull/17040), Zhang Shaowen,
    Marcus Watts)

-   rgw: rgw, mon: normalize delete/remove in admin console
    (cleanup 22444)
    ([issue#14363](http://tracker.ceph.com/issues/14363),
    [issue#22444](http://tracker.ceph.com/issues/22444),
    [pr#19439](https://github.com/ceph/ceph/pull/19439), Jesse
    Williamson)

-   rgw: RGW: Multipart upload may double the quota
    ([issue#21586](http://tracker.ceph.com/issues/21586),
    [pr#17959](https://github.com/ceph/ceph/pull/17959), Sibei Gao)

-   rgw: rgw multisite: automated trimming for bucket index logs
    ([issue#18229](http://tracker.ceph.com/issues/18229),
    [pr#17761](https://github.com/ceph/ceph/pull/17761), Casey Bodley)

-   rgw: RGW NFS: mount cmdline example missing -osync
    ([pr#15855](https://github.com/ceph/ceph/pull/15855), Matt Benjamin)

-   rgw: RGW-NFS: Use rados cluster_stat to report filesystem usage
    ([issue#22202](http://tracker.ceph.com/issues/22202),
    [pr#20093](https://github.com/ceph/ceph/pull/20093), Supriti Singh)

-   rgw: rgw_op: Drop the Old LifecycleConfiguration from logs
    ([pr#16821](https://github.com/ceph/ceph/pull/16821), Abhishek
    Lekshmanan)

-   rgw: rgw_op: exit early if object has no attrs in GetObjectTagging
    ([issue#21010](http://tracker.ceph.com/issues/21010),
    [pr#17048](https://github.com/ceph/ceph/pull/17048), Abhishek
    Lekshmanan)

-   rgw: RGWPutLC return ERR_MALFORMED_XML when missing \<Rule\> tag in
    lifecycle.xml ([issue#21377](http://tracker.ceph.com/issues/21377),
    [pr#17683](https://github.com/ceph/ceph/pull/17683), Shasha Lu)

-   rgw: rgw_put_system_obj takes bufferlist
    ([pr#19897](https://github.com/ceph/ceph/pull/19897), Casey Bodley)

-   rgw: rgw_rados: set_attrs now sets the same time for BI & object
    ([issue#21200](http://tracker.ceph.com/issues/21200),
    [pr#17400](https://github.com/ceph/ceph/pull/17400), Abhishek
    Lekshmanan)

-   rgw: rgw/rgw_op.cc: Fix error message in
    rgw_user_get_all_buckets_stats
    ([pr#18781](https://github.com/ceph/ceph/pull/18781), iliul)

-   rgw: rgw: source data in \'default.rgw.buckets.data\' may not be
    deleted after inter-bucket copy
    ([issue#21819](http://tracker.ceph.com/issues/21819),
    [pr#18369](https://github.com/ceph/ceph/pull/18369), baixueyu)

-   rgw: RGW: support for tagging in lifecycle policies
    ([pr#17305](https://github.com/ceph/ceph/pull/17305), Abhishek
    Lekshmanan)

-   rgw: RGW: update S3 POST policy handling of Content-Type
    ([issue#20201](http://tracker.ceph.com/issues/20201),
    [pr#18658](https://github.com/ceph/ceph/pull/18658), Matt Benjamin)

-   rgw: rgw: use camelcase format in request headers
    ([pr#19210](https://github.com/ceph/ceph/pull/19210), lvshanchun,
    Chang Liu)

-   rgw: RGWUser::init no longer overwrites user_id
    ([issue#21685](http://tracker.ceph.com/issues/21685),
    [pr#18137](https://github.com/ceph/ceph/pull/18137), Casey Bodley)

-   rgw: S3 Bucket Policy Conditions IpAddress and NotIpAddress do not
    work ([issue#20991](http://tracker.ceph.com/issues/20991),
    [pr#17010](https://github.com/ceph/ceph/pull/17010), John Gibson)

-   rgw: s3website error handler uses original object name
    ([issue#23201](http://tracker.ceph.com/issues/23201),
    [pr#20693](https://github.com/ceph/ceph/pull/20693), Casey Bodley)

-   rgw:send x-amz-version-id header when upload files
    ([pr#18935](https://github.com/ceph/ceph/pull/18935), Xinying Song)

-   rgw: set bucket versioninig donot change versioning status if
    missing status in xml
    ([issue#21364](http://tracker.ceph.com/issues/21364),
    [pr#17662](https://github.com/ceph/ceph/pull/17662), Shasha Lu)

-   rgw: set num_shards on \'radosgw-admin data sync init\'
    ([issue#22083](http://tracker.ceph.com/issues/22083),
    [pr#18883](https://github.com/ceph/ceph/pull/18883), Casey Bodley)

-   rgw: set priority on perf counters
    ([pr#20006](https://github.com/ceph/ceph/pull/20006), John Spray)

-   rgw: set sync_from_all as true when no value is seen
    ([issue#22062](http://tracker.ceph.com/issues/22062),
    [pr#18926](https://github.com/ceph/ceph/pull/18926), Abhishek
    Lekshmanan)

-   rgw: setup locks for libopenssl
    ([issue#22951](http://tracker.ceph.com/issues/22951),
    [issue#23203](http://tracker.ceph.com/issues/23203),
    [pr#20390](https://github.com/ceph/ceph/pull/20390), Abhishek
    Lekshmanan, Jesse Williamson)

-   rgw: share time skew check between v2 and v4 auth
    ([pr#20013](https://github.com/ceph/ceph/pull/20013), Casey Bodley)

-   rgw: Silence maybe-uninitialized false positives
    ([pr#19274](https://github.com/ceph/ceph/pull/19274), Brad Hubbard)

-   rgw: silence not allow register storage class specifier warning
    ([pr#19859](https://github.com/ceph/ceph/pull/19859), Yao Zongyou)

-   rgw: simplify use of map::emplace in iam
    ([pr#18706](https://github.com/ceph/ceph/pull/18706), Casey Bodley)

-   rgw: Small refactor and two bug fixes
    ([issue#21901](http://tracker.ceph.com/issues/21901),
    [issue#21896](http://tracker.ceph.com/issues/21896),
    [pr#18606](https://github.com/ceph/ceph/pull/18606), Adam C.
    Emerson)

-   rgw: some cleanup for sync status
    ([pr#20894](https://github.com/ceph/ceph/pull/20894), Enming Zhang)

-   rgw: stop/join TokenCache revoke thread only if started
    ([issue#21666](http://tracker.ceph.com/issues/21666),
    [pr#18106](https://github.com/ceph/ceph/pull/18106), Karol Mroz)

-   rgw: stream metadata full sync init
    ([issue#18079](http://tracker.ceph.com/issues/18079),
    [pr#12429](https://github.com/ceph/ceph/pull/12429), Yehuda Sadeh)

-   rgw: submodule: update Beast to ceph/ceph-master branch
    ([pr#19182](https://github.com/ceph/ceph/pull/19182), Casey Bodley)

-   rgw: switch beast frontend back to stackful coroutine
    ([issue#20048](http://tracker.ceph.com/issues/20048),
    [pr#20449](https://github.com/ceph/ceph/pull/20449), Casey Bodley)

-   rgw: sync tracing fixes
    ([issue#22833](http://tracker.ceph.com/issues/22833),
    [pr#20191](https://github.com/ceph/ceph/pull/20191), Yehuda Sadeh)

-   rgw: tenant fixes for dynamic resharding
    ([issue#22046](http://tracker.ceph.com/issues/22046),
    [pr#18811](https://github.com/ceph/ceph/pull/18811), Orit Wasserman)

-   rgw,tests: fix s3atests that are failing for sometime
    ([pr#20678](https://github.com/ceph/ceph/pull/20678), Vasu Kulkarni)

-   rgw,tests: qa: fix overrides for openssl_keys task
    ([pr#20981](https://github.com/ceph/ceph/pull/20981), Casey Bodley)

-   rgw,tests: qa: re enable LC tests
    ([pr#17020](https://github.com/ceph/ceph/pull/17020), Abhishek
    Lekshmanan)

-   rgw,tests: qa/rgw: add beast frontend to some rgw suites
    ([pr#17977](https://github.com/ceph/ceph/pull/17977), Casey Bodley)

-   rgw,tests: qa/rgw: combine swift, s3tests, ragweed into single
    verify task ([pr#20756](https://github.com/ceph/ceph/pull/20756),
    Casey Bodley)

-   rgw,tests: qa/rgw: disable log trim in multisite suite
    ([pr#19438](https://github.com/ceph/ceph/pull/19438), Casey Bodley)

-   rgw,tests: qa/rgw: hadoop-s3a suite targets centos_latest
    ([pr#17777](https://github.com/ceph/ceph/pull/17777), Casey Bodley)

-   rgw,tests: qa/rgw: ignore errors from \'pool application enable\'
    ([issue#21715](http://tracker.ceph.com/issues/21715),
    [pr#18193](https://github.com/ceph/ceph/pull/18193), Casey Bodley)

-   rgw,tests: qa/rgw: remove some civetweb overrides for beast testing
    ([issue#23002](http://tracker.ceph.com/issues/23002),
    [pr#20440](https://github.com/ceph/ceph/pull/20440), Casey Bodley)

-   rgw,tests: qa/rgw: renamed ssl task to openssl_keys
    ([pr#20863](https://github.com/ceph/ceph/pull/20863), Ricardo Dias)

-   rgw,tests: qa/rgw: use \'ceph osd pool application enable\' on
    created pools ([pr#17162](https://github.com/ceph/ceph/pull/17162),
    Casey Bodley)

-   rgw,tests: qa/rgw: verify suite tests civetweb with ssl
    ([pr#20444](https://github.com/ceph/ceph/pull/20444), Casey Bodley)

-   rgw,tests: qa/smoke: add rgw crypto config for s3tests
    ([pr#17700](https://github.com/ceph/ceph/pull/17700), Casey Bodley)

-   rgw,tests: qa/tasks/swift: add support for the \"force-branch\"
    configurable ([pr#21027](https://github.com/ceph/ceph/pull/21027),
    Radoslaw Zarzynski)

-   rgw,tests: rgw, qa: integrate Tempest to verify RadosGW\'s
    compliance with Swift API
    ([pr#16344](https://github.com/ceph/ceph/pull/16344), Radoslaw
    Zarzynski)

-   rgw,tests: test/rgw: fix test_encrypted_object_sync for 3+ zones
    ([pr#17377](https://github.com/ceph/ceph/pull/17377), Casey Bodley)

-   rgw: the metavariables in frontends-related config won\'t be
    expanded ([pr#19689](https://github.com/ceph/ceph/pull/19689), root)

-   rgw,tools: tools/rgw: add script to inspect admin socket \"cr dump\"
    ([pr#15554](https://github.com/ceph/ceph/pull/15554), Casey Bodley)

-   rgw: Torrents are not supported for objects encrypted using SSE-C
    ([issue#21720](http://tracker.ceph.com/issues/21720),
    [pr#17956](https://github.com/ceph/ceph/pull/17956), Zhang Shaowen)

-   rgw: trim all spaces inside a metadata value
    ([issue#23301](http://tracker.ceph.com/issues/23301),
    [pr#20841](https://github.com/ceph/ceph/pull/20841), Orit Wasserman)

-   rgw: udpate radosgw-admin usage with bi purge
    ([pr#18245](https://github.com/ceph/ceph/pull/18245), Yao Zongyou)

-   rgw: unlink deleted bucket from bucket\'s owner
    ([issue#22248](http://tracker.ceph.com/issues/22248),
    [pr#20017](https://github.com/ceph/ceph/pull/20017), Casey Bodley)

-   rgw: unreachable return in RGWRados::trim_bi_log_entries
    ([pr#17367](https://github.com/ceph/ceph/pull/17367), Amit Kumar)

-   rgw: update life cycle related log level
    ([pr#18845](https://github.com/ceph/ceph/pull/18845), Yao Zongyou)

-   rgw: update outdated debug func name
    ([pr#17440](https://github.com/ceph/ceph/pull/17440), Jiaying Ren)

-   rgw: update quota is inconsistent at add/del object with compression
    ([issue#22568](http://tracker.ceph.com/issues/22568),
    [pr#19772](https://github.com/ceph/ceph/pull/19772), fang yuxiang)

-   rgw: update the usage read iterator in truncated scenario
    ([issue#21196](http://tracker.ceph.com/issues/21196),
    [pr#17939](https://github.com/ceph/ceph/pull/17939), Mark Kogan)

-   rgw: update usage() with status
    ([pr#18178](https://github.com/ceph/ceph/pull/18178), Jos Collin)

-   rgw: update vstart.sh to support rgw ssl port notation :
    \'\--rgw_port 443s\'
    ([issue#21151](http://tracker.ceph.com/issues/21151),
    [pr#17989](https://github.com/ceph/ceph/pull/17989), Mark Kogan)

-   rgw: upldate the max-buckets when the quota is uploaded
    ([pr#20063](https://github.com/ceph/ceph/pull/20063), zhaokun)

-   rgw: URL-decode S3 and Swift object-copy URLs
    ([issue#22121](http://tracker.ceph.com/issues/22121),
    [pr#19936](https://github.com/ceph/ceph/pull/19936), Matt Benjamin)

-   rgw: url_encode key name and instance in es sync module
    ([pr#20707](https://github.com/ceph/ceph/pull/20707), Chang Liu)

-   rgw: use explicit index pool placement
    ([issue#22928](http://tracker.ceph.com/issues/22928),
    [pr#20352](https://github.com/ceph/ceph/pull/20352), Yehuda Sadeh)

-   rgw: Use namespace for lc_pool and roles_pool
    ([issue#20177](http://tracker.ceph.com/issues/20177),
    [pr#16889](https://github.com/ceph/ceph/pull/16889), Orit Wasserman)

-   rgw: Various cleanups and options update in rgw_admin.cc
    ([pr#18302](https://github.com/ceph/ceph/pull/18302), Jos Collin)

-   rgw: vstart.sh: fix mstop.sh can not stop rgw
    ([pr#17438](https://github.com/ceph/ceph/pull/17438), Jiaying Ren)

-   rgw: \'zone placement\' commands validate compression type
    ([issue#21775](http://tracker.ceph.com/issues/21775),
    [pr#18273](https://github.com/ceph/ceph/pull/18273), Casey Bodley)

-   rocksdb: sync with upstream
    ([issue#21603](http://tracker.ceph.com/issues/21603),
    [pr#18262](https://github.com/ceph/ceph/pull/18262), Kefu Chai)

-   rpm: rm macros in comments
    ([issue#22250](http://tracker.ceph.com/issues/22250),
    [pr#17070](https://github.com/ceph/ceph/pull/17070), Ken Dreyer)

-   script/build-integration-branch: check errors
    ([pr#17578](https://github.com/ceph/ceph/pull/17578), Sage Weil)

-   script/build-integration-branch: python3 compatible and pep8 clean
    ([pr#18035](https://github.com/ceph/ceph/pull/18035), Kefu Chai)

-   scripts: new backport-create-issue script
    ([pr#21480](https://github.com/ceph/ceph/pull/21480), Nathan Cutler)

-   selinux: Allow ceph to execute ldconfig
    ([pr#21974](https://github.com/ceph/ceph/pull/21974), Boris Ranto)

-   selinux: Allow getattr on lnk sysfs files
    ([pr#17891](https://github.com/ceph/ceph/pull/17891), Boris Ranto)

-   spdk: advance to upstream dc82989d
    ([pr#20713](https://github.com/ceph/ceph/pull/20713), Nathan Cutler)

-   src: fix various log messages
    ([pr#21112](https://github.com/ceph/ceph/pull/21112), Gu Zhongyan)

-   src/msg/rdma: fixes failure on assert in notify()
    ([pr#17007](https://github.com/ceph/ceph/pull/17007), Alex Mikheev)

-   suites/cephmetrics: Add Centos 7
    ([pr#18594](https://github.com/ceph/ceph/pull/18594), Zack Cerza)

-   test: assert check for negative returns
    ([pr#17296](https://github.com/ceph/ceph/pull/17296), Amit Kumar)

-   test/fio: generate db histogram to help debug rocksdb performance
    ([pr#16808](https://github.com/ceph/ceph/pull/16808), Pan Liu,
    Xiaoyan Li)

-   test: fix bash path in shebangs (part 2)
    ([pr#17955](https://github.com/ceph/ceph/pull/17955), Alan Somers)

-   test: fix CLI unit formatting tests
    ([pr#22260](https://github.com/ceph/ceph/pull/22260), Jason
    Dillaman)

-   test: Incorrect conversion to double
    ([pr#18963](https://github.com/ceph/ceph/pull/18963), Amit Kumar)

-   test/librados: reorder ASSERT_EQ() arguments
    ([pr#16625](https://github.com/ceph/ceph/pull/16625), Yan Jun)

-   test,osd,kvstore_tool: silence warnings and prepare test buffer in
    the right way ([pr#18406](https://github.com/ceph/ceph/pull/18406),
    Adam C. Emerson)

-   tests: bluestore/fio: Fixed problem with all objects having the same
    hash ([pr#17770](https://github.com/ceph/ceph/pull/17770), Adam
    Kupczyk)

-   tests: CentOS 7.4 is now the latest
    ([pr#17776](https://github.com/ceph/ceph/pull/17776), Nathan Cutler)

-   tests - ceph-ansible vars additions
    ([issue#21822](http://tracker.ceph.com/issues/21822),
    [pr#18378](https://github.com/ceph/ceph/pull/18378), Yuri Weinstein)

-   tests: ceph-disk: ignore E722 in flake8 test
    ([issue#22207](http://tracker.ceph.com/issues/22207),
    [pr#19072](https://github.com/ceph/ceph/pull/19072), Nathan Cutler)

-   tests: ceph-disk: mock get fsid
    ([pr#19254](https://github.com/ceph/ceph/pull/19254), Kefu Chai)

-   tests: ceph-disk: Remove sitepackages=True
    ([issue#22823](http://tracker.ceph.com/issues/22823),
    [pr#20151](https://github.com/ceph/ceph/pull/20151), Brad Hubbard)

-   tests: ceph-objectstore-tool: don\'t destroy SnapMapper until the
    txn is completed
    ([issue#23121](http://tracker.ceph.com/issues/23121),
    [pr#20593](https://github.com/ceph/ceph/pull/20593), Kefu Chai)

-   tests: Changes required for teuthology\'s systemd support
    ([pr#18380](https://github.com/ceph/ceph/pull/18380), Zack Cerza)

-   tests: Check for empty output in test_dump_pgstate_history
    ([pr#20838](https://github.com/ceph/ceph/pull/20838), Brad Hubbard)

-   tests: cleanup: drop calamari tasks
    ([pr#17531](https://github.com/ceph/ceph/pull/17531), Nathan Cutler)

-   tests: cleanup: drop upgrade/jewel-x/point-to-point-x
    ([issue#22888](http://tracker.ceph.com/issues/22888),
    [pr#20245](https://github.com/ceph/ceph/pull/20245), Nathan Cutler)

-   tests: cmake,test/mgr: restructure dashboard tests and cmake related
    fixes ([pr#20768](https://github.com/ceph/ceph/pull/20768), Kefu
    Chai)

-   tests: common/obj_bencher: set {min,max}\_iops if runtime \< 1 sec
    ([pr#17182](https://github.com/ceph/ceph/pull/17182), Kefu Chai)

-   tests: c_read_operations.cc: Silence tautological-compare compiler
    warning ([pr#19953](https://github.com/ceph/ceph/pull/19953), Brad
    Hubbard)

-   tests: fix uninitialized value found by coverity scan
    ([pr#17895](https://github.com/ceph/ceph/pull/17895), J. Eric
    Ivancich)

-   tests: Increase sleep in test_pidfile.sh
    ([pr#17052](https://github.com/ceph/ceph/pull/17052), David Zafman)

-   tests: librgw_file: remove unused [using]{.title-ref} statement
    ([pr#17085](https://github.com/ceph/ceph/pull/17085), Yao Zongyou)

-   tests: mark_unfound_lost fix and some other minor changes
    ([issue#21907](http://tracker.ceph.com/issues/21907),
    [pr#18449](https://github.com/ceph/ceph/pull/18449), David Zafman)

-   tests: mgr/dashboard: Allow sourcing
    [run-backend-api-tests.sh]{.title-ref}
    ([pr#20874](https://github.com/ceph/ceph/pull/20874), Sebastian
    Wagner)

-   tests: mgr/dashboard: create venv for running tox
    ([pr#21490](https://github.com/ceph/ceph/pull/21490), Kefu Chai)

-   tests: mgr/dashboard: notification queue: fix priority tests
    ([pr#21147](https://github.com/ceph/ceph/pull/21147), Ricardo Dias)

-   tests: mimic: qa: fix test on \"ceph fs set cephfs allow_new_snaps\"
    ([pr#21830](https://github.com/ceph/ceph/pull/21830), Kefu Chai)

-   tests: mimic: qa/workunits/rados/test_envlibrados_for_rocksdb:
    install g++ not g++-4.7
    ([pr#22117](https://github.com/ceph/ceph/pull/22117), Kefu Chai)

-   tests: mimic: test: Need to escape parens in log-whitelist for grep
    ([pr#22075](https://github.com/ceph/ceph/pull/22075), David Zafman)

-   tests: mimic: test: wait_for_pg_stats() should do another check
    after last 13 secon...
    ([pr#22199](https://github.com/ceph/ceph/pull/22199), David Zafman)

-   tests: misc: Fix bash path in shebangs
    ([pr#16494](https://github.com/ceph/ceph/pull/16494), Alan Somers)

-   tests: mstart.sh: remove bashizm in /bin/sh script
    ([pr#18541](https://github.com/ceph/ceph/pull/18541), Mykola Golub)

-   tests: point-to-point-x: upgrade client.1 to -x along with cluster
    nodes ([issue#21499](http://tracker.ceph.com/issues/21499),
    [pr#17910](https://github.com/ceph/ceph/pull/17910), Nathan Cutler)

-   tests: qa: add cbt task for performance testing
    ([pr#17583](https://github.com/ceph/ceph/pull/17583), Neha Ojha)

-   tests: qa: add cosbench workloads and override teuthology default
    settings ([pr#21710](https://github.com/ceph/ceph/pull/21710), Neha
    Ojha)

-   tests/qa: Adding \$ distro mix - rgw
    ([pr#22070](https://github.com/ceph/ceph/pull/22070), Yuri
    Weinstein)

-   tests/qa: adding rados/.. dirs
    ([pr#22068](https://github.com/ceph/ceph/pull/22068), Yuri
    Weinstein)

-   tests: qa: add \"restful\" to ceph_mgr_modules in ceph-ansible suite
    ([pr#18634](https://github.com/ceph/ceph/pull/18634), Kefu Chai)

-   tests: qa: add simple and dirty script to find ports being used
    ([pr#19102](https://github.com/ceph/ceph/pull/19102), Joao Eduardo
    Luis)

-   tests: qa: big: add openstack.yaml
    ([pr#16864](https://github.com/ceph/ceph/pull/16864), Nathan Cutler)

-   tests: qa: clean up dnsmasq task and fix EPERM error
    ([pr#20680](https://github.com/ceph/ceph/pull/20680), Casey Bodley)

-   tests: qa: create_cache_pool no longer runs \'pool application
    enable\' ([issue#21155](http://tracker.ceph.com/issues/21155),
    [pr#17312](https://github.com/ceph/ceph/pull/17312), Casey Bodley)

-   tests: qa: decrease the msg_inject_socket_failures from 1/500 to
    1/1000 ([issue#22093](http://tracker.ceph.com/issues/22093),
    [pr#19542](https://github.com/ceph/ceph/pull/19542), Kefu Chai)

-   tests: qa: disable mon-health-to-clog in upgrade test
    ([pr#19233](https://github.com/ceph/ceph/pull/19233), Kefu Chai)

-   tests: qa: disable -Werror when compiling env_librados_test
    ([pr#21433](https://github.com/ceph/ceph/pull/21433), Kefu Chai)

-   tests: qa: do not \"ceph fs get cephfs\" w/o a cephfs fs
    ([pr#18533](https://github.com/ceph/ceph/pull/18533), Kefu Chai)

-   tests: qa: do not wait for down/out osd for pg convergence
    ([pr#18808](https://github.com/ceph/ceph/pull/18808), Kefu Chai)

-   tests/qa - enabled [ceph-deploy]{.title-ref} runs on
    [mira]{.title-ref} nodes
    ([pr#21253](https://github.com/ceph/ceph/pull/21253), Yuri
    Weinstein)

-   tests: qa: fix pool-quota related tests
    ([issue#21409](http://tracker.ceph.com/issues/21409),
    [pr#17763](https://github.com/ceph/ceph/pull/17763), xie xingguo)

-   tests: qa: Fix shebangs on openstack scripts
    ([pr#16546](https://github.com/ceph/ceph/pull/16546), Alan Somers)

-   tests: qa: reduce \"mon client hunt interval max multiple\" to 2 for
    all clients ([pr#21658](https://github.com/ceph/ceph/pull/21658),
    Kefu Chai)

-   tests: qa: reduce mon-client-hunt-interval-max-multiple to 2
    ([pr#18283](https://github.com/ceph/ceph/pull/18283), Kefu Chai)

-   tests: qa: revert \"qa: use config_path property instead of
    literal\" ([pr#17850](https://github.com/ceph/ceph/pull/17850),
    Patrick Donnelly)

-   tests: qa/run-standalone.sh: set PYTHONPATH for FreeBSD also
    ([pr#20646](https://github.com/ceph/ceph/pull/20646), Kefu Chai)

-   tests: qa: s/backfill/backfilling/
    ([pr#18235](https://github.com/ceph/ceph/pull/18235), Kefu Chai)

-   tests: qa/stanalone: pass options using \--\<option-name\>=\<value\>
    ([pr#19544](https://github.com/ceph/ceph/pull/19544), Kefu Chai)

-   tests: qa/standalone: Add trap for signals to restore the kernel
    core pattern ([pr#17026](https://github.com/ceph/ceph/pull/17026),
    David Zafman)

-   tests: qa/standalone/ceph-helpers.sh: provide argument to dirname
    ([issue#23805](http://tracker.ceph.com/issues/23805),
    [pr#21552](https://github.com/ceph/ceph/pull/21552), Nathan Cutler)

-   tests: qa/standalone/ceph-helpers.sh: silence ceph-disk
    DEPRECATION_WARNING
    ([pr#19478](https://github.com/ceph/ceph/pull/19478), Kefu Chai)

-   tests: qa/standalone: extract delete_pool()
    ([pr#20634](https://github.com/ceph/ceph/pull/20634), Kefu Chai)

-   tests: qa/standalone: misc fixes
    ([issue#20465](http://tracker.ceph.com/issues/20465),
    [issue#20921](http://tracker.ceph.com/issues/20921),
    [pr#16709](https://github.com/ceph/ceph/pull/16709), David Zafman)

-   tests: qa/standalone/mon/misc.sh: Add osdmap-prune tests
    ([issue#23621](http://tracker.ceph.com/issues/23621),
    [pr#21318](https://github.com/ceph/ceph/pull/21318), Brad Hubbard)

-   tests: qa/standalone/osd/osd-mark-down: create pool to get updated
    osdmap faster ([pr#18191](https://github.com/ceph/ceph/pull/18191),
    huangjun)

-   tests: qa/standalone: remove osd-map-max-advance related tests
    ([issue#22596](http://tracker.ceph.com/issues/22596),
    [pr#19816](https://github.com/ceph/ceph/pull/19816), Kefu Chai)

-   tests: qa/standalone: respect \$TEMPDIR
    ([pr#17747](https://github.com/ceph/ceph/pull/17747), Kefu Chai)

-   tests: qa/standalone/scrub/osd-scrub-repair.sh: add extents flag
    into object_info_t
    ([issue#21618](http://tracker.ceph.com/issues/21618),
    [pr#18094](https://github.com/ceph/ceph/pull/18094), xie xingguo)

-   tests: qa/standalone/scrub/osd-scrub-repair.sh: drop omap_digest
    flag ([pr#18150](https://github.com/ceph/ceph/pull/18150), xie
    xingguo, Sage Weil)

-   tests: qa/standalone:
    s/delete_erasure_pool/delete_erasure_coded_pool/
    ([pr#20667](https://github.com/ceph/ceph/pull/20667), Kefu Chai)

-   tests: qa: stop testing deprecated \"ceph osd create\"
    ([issue#21993](http://tracker.ceph.com/issues/21993),
    [pr#18659](https://github.com/ceph/ceph/pull/18659), Kefu Chai)

-   tests: qa/suites: add minimal performance suite
    ([pr#21104](https://github.com/ceph/ceph/pull/21104), Neha Ojha)

-   tests: qa/suites/cephmetrics: Updates for new version
    ([pr#21146](https://github.com/ceph/ceph/pull/21146), Zack Cerza)

-   tests: qa/suites: change fixed-2.yaml users to get 4 openstack disks
    ([pr#16873](https://github.com/ceph/ceph/pull/16873), Sage Weil)

-   tests: qa/suites: mds.0 -\> mds.a
    ([pr#20848](https://github.com/ceph/ceph/pull/20848), Sage Weil)

-   tests: qa/suites/rados: Disable scrub backoff
    ([issue#23578](http://tracker.ceph.com/issues/23578),
    [pr#21295](https://github.com/ceph/ceph/pull/21295), Brad Hubbard)

-   tests: qa/suites/rados/mgr/tasks/dashboard: add MDS_ALL_DOWN to
    whitelist ([pr#21549](https://github.com/ceph/ceph/pull/21549),
    Ricardo Dias)

-   tests: qa/suites/rados/mgr/tasks/dashboard_v2: add fail_on_skip =
    false ([pr#20925](https://github.com/ceph/ceph/pull/20925), Ricardo
    Dias)

-   tests: qa/suites/rados/multimon: whitelist mgr down vs clock skew
    test ([pr#16996](https://github.com/ceph/ceph/pull/16996), Sage
    Weil)

-   tests: qa/suites/rados/singleton: more whitelist
    ([pr#19225](https://github.com/ceph/ceph/pull/19225), Kefu Chai)

-   tests: qa/suites/rados/thrash-old-clients: ms_type=simple
    ([issue#23922](http://tracker.ceph.com/issues/23922),
    [pr#21739](https://github.com/ceph/ceph/pull/21739), Kefu Chai)

-   tests: qa/suites/rados/upgrade/jewel-x-singleton: tolerate sloppy
    past_intervals ([pr#17293](https://github.com/ceph/ceph/pull/17293),
    Kefu Chai)

-   tests: qa/suites/rest/basic/tasks/rest_test: more whitelisting
    ([issue#21425](http://tracker.ceph.com/issues/21425),
    [pr#17794](https://github.com/ceph/ceph/pull/17794), huangjun)

-   tests: qa/suites/rest/basic/tasks/rest_test: whiltelist OSD_DOWN
    ([issue#21425](http://tracker.ceph.com/issues/21425),
    [pr#18144](https://github.com/ceph/ceph/pull/18144), huangjun)

-   tests: qa/suites/upgarde/jewel-x/parallel: tolerate mgr warning
    ([pr#17203](https://github.com/ceph/ceph/pull/17203), Sage Weil)

-   tests: qa/suites/upgarde/jewel-x/point-to-point-x: disable app
    warnings ([pr#16947](https://github.com/ceph/ceph/pull/16947), Sage
    Weil)

-   tests: qa/suites: whitelist SLOW_OPS
    ([issue#23495](http://tracker.ceph.com/issues/23495),
    [pr#21324](https://github.com/ceph/ceph/pull/21324), Kefu Chai)

-   tests: qa/tasks: Add default timeout for wait for pg clean task
    ([pr#21313](https://github.com/ceph/ceph/pull/21313), Vasu Kulkarni)

-   tests: qa/tasks/ceph_deploy: gatherkeys before mgr deploy
    ([pr#17224](https://github.com/ceph/ceph/pull/17224), Sage Weil)

-   tests: qa/tasks/ceph_manager: use set_config on revived osd
    ([pr#20901](https://github.com/ceph/ceph/pull/20901), Neha Ojha)

-   tests: qa/tasks/mgr/dashboard: Fix login expires too soon
    ([pr#21021](https://github.com/ceph/ceph/pull/21021), Sebastian
    Wagner)

-   tests: qa/tasks: prolong revive_osd() timeout to 6 min
    ([issue#21474](http://tracker.ceph.com/issues/21474),
    [pr#17902](https://github.com/ceph/ceph/pull/17902), Kefu Chai)

-   tests: qa/tasks: prolong revive_osd() timeout to 6 min
    ([issue#21474](http://tracker.ceph.com/issues/21474),
    [pr#19024](https://github.com/ceph/ceph/pull/19024), Kefu Chai)

-   tests: qa/tasks: run cosbench using the CBT task
    ([pr#21656](https://github.com/ceph/ceph/pull/21656), Neha Ojha)

-   tests: qa/tasks: update ceph-deploy task to use newer ceph-volume
    syntax ([pr#19244](https://github.com/ceph/ceph/pull/19244), Vasu
    Kulkarni)

-   tests: qa/tests: Add additional required ceph-ansible vars due to
    upstream changes
    ([pr#17757](https://github.com/ceph/ceph/pull/17757), Vasu Kulkarni)

-   tests: qa/tests: add ceph-deploy upgrade tests
    ([issue#20950](http://tracker.ceph.com/issues/20950),
    [pr#16826](https://github.com/ceph/ceph/pull/16826), Vasu Kulkarni)

-   tests: qa/tests: add openstack volume info + lvs for ceph-volume
    ([pr#20243](https://github.com/ceph/ceph/pull/20243), Vasu Kulkarni)

-   tests: qa/tests: Fix get_system_type failure due to invalid remote
    name ([pr#17650](https://github.com/ceph/ceph/pull/17650), Vasu
    Kulkarni)

-   tests: qa/tests: fix rbd pool creation for systemd tests
    ([pr#17536](https://github.com/ceph/ceph/pull/17536), Vasu Kulkarni)

-   tests: \[qa/tests\]: misc ceph-ansible fixes and udpate
    ([pr#17096](https://github.com/ceph/ceph/pull/17096), Vasu Kulkarni)

-   tests: qa/tests/rados: Remove unsupported 2-size-1-min-size config
    ([pr#17576](https://github.com/ceph/ceph/pull/17576), Vasu Kulkarni)

-   tests: qa/tests: use ceph-deploy stable branch for single node tests
    ([pr#20979](https://github.com/ceph/ceph/pull/20979), Vasu Kulkarni)

-   tests: qa/tests: Various whitelists for smoke suite
    ([issue#21376](http://tracker.ceph.com/issues/21376),
    [pr#17680](https://github.com/ceph/ceph/pull/17680), Vasu Kulkarni)

-   tests: qa/tests: Wip ceph deploy upgrade
    ([pr#17651](https://github.com/ceph/ceph/pull/17651), Vasu Kulkarni)

-   tests: qa/workunits/rados/test_large_omap_detection: Scrub pgs
    instead of OSDs
    ([pr#21410](https://github.com/ceph/ceph/pull/21410), Brad Hubbard)

-   tests: qa/workunits: silence py warnings for ceph-disk tests
    ([issue#22154](http://tracker.ceph.com/issues/22154),
    [pr#19075](https://github.com/ceph/ceph/pull/19075), Kefu Chai)

-   tests: rados: Copy payload in ceph_perf_msgr_client
    ([issue#22100](http://tracker.ceph.com/issues/22100),
    [pr#18862](https://github.com/ceph/ceph/pull/18862), Jeegn Chen)

-   tests: rados: Intializing members class StriperTest
    ([pr#16843](https://github.com/ceph/ceph/pull/16843), amitkuma)

-   tests: remove TestPGLog ASSERT_DEATH test
    ([issue#23504](http://tracker.ceph.com/issues/23504),
    [pr#21117](https://github.com/ceph/ceph/pull/21117), Nathan Cutler)

-   tests: run-standalone.sh improve error message
    ([pr#17093](https://github.com/ceph/ceph/pull/17093), David Zafman)

-   tests: run-standalone.sh skip core_pattern if already set
    ([pr#17098](https://github.com/ceph/ceph/pull/17098), David Zafman)

-   tests: test/admin_socket_output: add \--vstart=path/to/asok option
    ([pr#20371](https://github.com/ceph/ceph/pull/20371), Kefu Chai)

-   tests: test/admin_socket_output: better error reporting
    ([pr#20409](https://github.com/ceph/ceph/pull/20409), Brad Hubbard)

-   tests: test/admin_socket_output: switch to
    std::experimental::filesystem
    ([pr#20307](https://github.com/ceph/ceph/pull/20307), Kefu Chai)

-   tests: test/ceph_test_objectstore: make settings update and restore
    less error prone
    ([pr#21145](https://github.com/ceph/ceph/pull/21145), Igor Fedotov)

-   tests: test: checking negative returns from creat()
    ([pr#18090](https://github.com/ceph/ceph/pull/18090), amitkuma)

-   tests: test/CMakeLists: disable test_pidfile.sh
    ([issue#20975](http://tracker.ceph.com/issues/20975),
    [pr#16977](https://github.com/ceph/ceph/pull/16977), Sage Weil)

-   tests: test/CMakeLists: disable test-pidfile.sh
    ([pr#17401](https://github.com/ceph/ceph/pull/17401), Sage Weil)

-   tests: test/coredumpctl: support freebsd
    ([pr#17447](https://github.com/ceph/ceph/pull/17447), Kefu Chai)

-   tests: test/dashboard: hardcode .coverage path to workaround tox
    bugs ([pr#21485](https://github.com/ceph/ceph/pull/21485), Kefu
    Chai)

-   tests: test/dashboard: specify workdir using tox.ini
    ([issue#23709](http://tracker.ceph.com/issues/23709),
    [pr#21416](https://github.com/ceph/ceph/pull/21416), Kefu Chai)

-   tests: test: Don\'t dump core when using EXPECT_DEATH
    ([pr#17390](https://github.com/ceph/ceph/pull/17390), Kefu Chai)

-   tests: test/fio: extend fio objectstore plugin to better simulate
    OSD behavior ([pr#19101](https://github.com/ceph/ceph/pull/19101),
    Igor Fedotov)

-   tests: test/fio: fix building of the fio_ceph_objectstore plugin
    ([pr#18332](https://github.com/ceph/ceph/pull/18332), Radoslaw
    Zarzynski)

-   tests: test: Fix and enable test_pidfile.sh
    ([issue#20770](http://tracker.ceph.com/issues/20770),
    [pr#16987](https://github.com/ceph/ceph/pull/16987), David Zafman)

-   tests: test: Fix ceph-objectstore-tool usage check
    ([pr#17785](https://github.com/ceph/ceph/pull/17785), David Zafman)

-   tests: test: fix misc fiemap testing
    ([issue#21716](http://tracker.ceph.com/issues/21716),
    [pr#18240](https://github.com/ceph/ceph/pull/18240), Kefu Chai, Ning
    Yao)

-   tests: test: Initialization of \*comp_racing_read class CopyFromOp
    ([pr#17369](https://github.com/ceph/ceph/pull/17369), Amit Kumar)

-   tests: test: Initializing ChunkReadOp members
    ([pr#19334](https://github.com/ceph/ceph/pull/19334), amitkuma)

-   tests: test/journal: Initialize member variable m_work_queue
    ([pr#17089](https://github.com/ceph/ceph/pull/17089), amitkuma)

-   tests: test/librados: be more tolerant with timed lock tests
    ([issue#20086](http://tracker.ceph.com/issues/20086),
    [pr#20161](https://github.com/ceph/ceph/pull/20161), Kefu Chai)

-   tests: test/librados: increase pgp_num along with pg_num
    ([issue#23763](http://tracker.ceph.com/issues/23763),
    [pr#21555](https://github.com/ceph/ceph/pull/21555), Kefu Chai)

-   tests: test/librados: s/invoke_result_t/result_of_t/
    ([pr#20379](https://github.com/ceph/ceph/pull/20379), Kefu Chai)

-   tests: test/librados_test_stub: pass snap context to zero op
    ([pr#17186](https://github.com/ceph/ceph/pull/17186), Mykola Golub)

-   tests: test/log: fix for crash with libc++
    ([pr#20233](https://github.com/ceph/ceph/pull/20233), Casey Bodley)

-   tests: test: Make clearer by moving code out of loop
    ([pr#20759](https://github.com/ceph/ceph/pull/20759), David Zafman)

-   tests: test/objectstore/test_bluefs: cleanups
    ([pr#17909](https://github.com/ceph/ceph/pull/17909), Kefu Chai)

-   tests: test: only test dashboard_v2 when it is enabled
    ([pr#20777](https://github.com/ceph/ceph/pull/20777), Willem Jan
    Withagen)

-   tests: test: only test enabled python bindings
    ([pr#21293](https://github.com/ceph/ceph/pull/21293), Kefu Chai)

-   tests: test/osd: initialize Non-static class members in
    WeightedTestGenerator
    ([pr#15922](https://github.com/ceph/ceph/pull/15922), Jos Collin)

-   tests: test/osd: Non-static class members not initialized in
    UnsetRedirectOp
    ([pr#15921](https://github.com/ceph/ceph/pull/15921), Jos Collin)

-   tests: test/osd: silence warnings from -Wsign-compare
    ([pr#17027](https://github.com/ceph/ceph/pull/17027), Jos Collin)

-   tests: test: put new BlueStore tests un ifdef WITH_BLUESTORE
    ([pr#20576](https://github.com/ceph/ceph/pull/20576), Willem Jan
    Withagen)

-   tests: test:qa:infra - Run update daily and use bash
    ([pr#21218](https://github.com/ceph/ceph/pull/21218), David
    Galloway)

-   tests: test:qa:infra - teuthology crontab items as of 3/27/18
    ([pr#21075](https://github.com/ceph/ceph/pull/21075), Yuri
    Weinstein)

-   tests: test: reduce the chance to have degraded PGs
    ([issue#22711](http://tracker.ceph.com/issues/22711),
    [pr#20046](https://github.com/ceph/ceph/pull/20046), Kefu Chai)

-   tests: test: remove distro_version assert in distro detect test
    ([pr#21052](https://github.com/ceph/ceph/pull/21052), Shengjing Zhu)

-   tests: test: Replace bc command with printf command
    ([pr#21013](https://github.com/ceph/ceph/pull/21013), David Zafman)

-   tests: test: silence warning from -Wsign-compare
    ([pr#17790](https://github.com/ceph/ceph/pull/17790), Jos Collin)

-   tests: test: silence warnings from -Wsign-compare
    ([pr#17962](https://github.com/ceph/ceph/pull/17962), Jos Collin)

-   tests: tests - Replaced requests for \"centos 7.3\" to centos_latest
    ([pr#19262](https://github.com/ceph/ceph/pull/19262), Yuri
    Weinstein)

-   tests: test/store_test: fix FTBFS as Sequencer is removed
    ([pr#20382](https://github.com/ceph/ceph/pull/20382), Kefu Chai)

-   tests: test/store_test: update Many4KWritesTest\* test cases to
    finalize with...
    ([pr#20230](https://github.com/ceph/ceph/pull/20230), Igor Fedotov)

-   tests: test/throttle: kill tests exercising dtor of Throttle classes
    ([pr#17442](https://github.com/ceph/ceph/pull/17442), Kefu Chai)

-   tests: test/unittest_bufferlist: check retvals of syscalls
    ([pr#18238](https://github.com/ceph/ceph/pull/18238), Kefu Chai)

-   tests: test/unittest_pg_log: silence gcc warning
    ([pr#17328](https://github.com/ceph/ceph/pull/17328), Kefu Chai)

-   tests: test: Use jq in a compatible way and for easier diff analysis
    ([pr#21450](https://github.com/ceph/ceph/pull/21450), David Zafman)

-   tests: test: Whitelist corrections
    ([pr#22167](https://github.com/ceph/ceph/pull/22167), David Zafman)

-   tests,tools: crushtool: print error message to stderr not dout(1)
    ([issue#21758](http://tracker.ceph.com/issues/21758),
    [pr#18242](https://github.com/ceph/ceph/pull/18242), Kefu Chai)

-   tests: unittest_crypto: Don\'t exceed limit for getentropy
    ([pr#18505](https://github.com/ceph/ceph/pull/18505), Brad Hubbard)

-   tests: vstart: fix initial start when there is no ceph.conf
    ([pr#21019](https://github.com/ceph/ceph/pull/21019), Jianpeng Ma)

-   The Day Has Come!
    ([pr#19657](https://github.com/ceph/ceph/pull/19657), Adam C.
    Emerson)

-   tools: Align use of uint64_t in service_daemon::AttributeType
    ([pr#16938](https://github.com/ceph/ceph/pull/16938), James Page)

-   tools: ceph-disk: erase 110MB for nuking existing bluestore
    ([issue#22354](http://tracker.ceph.com/issues/22354),
    [pr#20400](https://github.com/ceph/ceph/pull/20400), Kefu Chai)

-   tools: ceph-disk: fix \'\--runtime\' omission for ceph-osd service
    ([issue#21498](http://tracker.ceph.com/issues/21498),
    [pr#17904](https://github.com/ceph/ceph/pull/17904), Carl Xiong)

-   tools: ceph-disk: fix signed integer is greater than maximum when
    call major ([pr#19196](https://github.com/ceph/ceph/pull/19196),
    Song Shun)

-   tools: ceph-disk: include output of failed command in exception
    ([pr#20497](https://github.com/ceph/ceph/pull/20497), Kefu Chai)

-   tools: ceph-disk: more precise error message when a disk is
    specified ([pr#18018](https://github.com/ceph/ceph/pull/18018), Kefu
    Chai)

-   tools: ceph-disk: reduce the scope of activate_lock
    ([pr#20114](https://github.com/ceph/ceph/pull/20114), zhaokun)

-   tools: ceph-disk: retry on OSError
    ([issue#21728](http://tracker.ceph.com/issues/21728),
    [pr#18162](https://github.com/ceph/ceph/pull/18162), Kefu Chai)

-   tools: ceph-disk: unlock all partitions when activate
    ([pr#17363](https://github.com/ceph/ceph/pull/17363), Kefu Chai)

-   tools: ceph-disk: write log to /var/log/ceph not to /var/run/ceph
    ([pr#18375](https://github.com/ceph/ceph/pull/18375), Kefu Chai)

-   tools: ceph: fixes for \"tell \<service\>.\*\" command
    ([issue#21230](http://tracker.ceph.com/issues/21230),
    [pr#17463](https://github.com/ceph/ceph/pull/17463), Kefu Chai)

-   tools: ceph-kvstore-tool: make it a bit more friendly
    ([pr#21477](https://github.com/ceph/ceph/pull/21477), Sage Weil)

-   tools: ceph-kvstore-tool: use unique_ptr\<\> to manage the lifecycle
    of bluestore ([pr#18221](https://github.com/ceph/ceph/pull/18221),
    Kefu Chai)

-   tools: ceph-objectstore-tool: Add option \"dump-import\" to examine
    an export ([issue#22086](http://tracker.ceph.com/issues/22086),
    [pr#19368](https://github.com/ceph/ceph/pull/19368), David Zafman)

-   tools: ceph-objectstore-tool: Fix set-size to clear data_digest if
    changing ... ([pr#18885](https://github.com/ceph/ceph/pull/18885),
    David Zafman)

-   tools: ceph-objectstore-tool: \"\$OBJ get-omaphdr\" and \"\$OBJ
    list-omap\" scan all pgs instead of using specific pg
    ([issue#21327](http://tracker.ceph.com/issues/21327),
    [pr#17985](https://github.com/ceph/ceph/pull/17985), David Zafman)

-   tools: ceph-objectstore-tool: skip object with generated version
    ([pr#18507](https://github.com/ceph/ceph/pull/18507), huangjun)

-   tools: ceph-syn: silence clang analyzer warning
    ([pr#18577](https://github.com/ceph/ceph/pull/18577), Kefu Chai)

-   tools: ceph-volume: Use a delimited CLI output parser instead of
    JSON ([pr#17097](https://github.com/ceph/ceph/pull/17097), Alfredo
    Deza)

-   tools: cleanup: rip out ceph-rest-api
    ([issue#21264](http://tracker.ceph.com/issues/21264),
    [issue#22457](http://tracker.ceph.com/issues/22457),
    [pr#17530](https://github.com/ceph/ceph/pull/17530), Nathan Cutler)

-   tools: correct total size formatting
    ([pr#21641](https://github.com/ceph/ceph/pull/21641), Zheng Yin)

-   tools: crushtool: add \--add-bucket and \--move options
    ([pr#20183](https://github.com/ceph/ceph/pull/20183), Kefu Chai)

-   tools: FreeBSD basic getopt does not use \--options
    ([pr#21148](https://github.com/ceph/ceph/pull/21148), Willem Jan
    Withagen)

-   tools: Initialization of \*server, command variables
    ([pr#17135](https://github.com/ceph/ceph/pull/17135), amitkuma)

-   tools: make rados get/put/append command help txt clear
    ([issue#22958](http://tracker.ceph.com/issues/22958),
    [pr#20363](https://github.com/ceph/ceph/pull/20363), lvshuhua)

-   tools: Modify \"rados df\" header\'s alignment
    ([pr#17549](https://github.com/ceph/ceph/pull/17549), iliul)

-   tools: rados add a cli option to clear omap keys
    ([issue#22255](http://tracker.ceph.com/issues/22255),
    [pr#19180](https://github.com/ceph/ceph/pull/19180), Abhishek
    Lekshmanan)

-   tools: rados/tool: fixup rados stat command hint
    ([pr#16983](https://github.com/ceph/ceph/pull/16983), huanwen ren)

-   tools: script: build-integration-branch: avoid Unicode error
    ([issue#24003](http://tracker.ceph.com/issues/24003),
    [pr#21918](https://github.com/ceph/ceph/pull/21918), Nathan Cutler)

-   tools: script: ceph-release-notes: minor fixes for split_component
    ([pr#16605](https://github.com/ceph/ceph/pull/16605), Abhishek
    Lekshmanan)

-   tools: Special scrub handling of hinfo_key errors
    ([issue#23428](http://tracker.ceph.com/issues/23428),
    [issue#23364](http://tracker.ceph.com/issues/23364),
    [pr#20947](https://github.com/ceph/ceph/pull/20947), David Zafman)

-   tools: src/vstart.sh: default os to filestore for FreeBSD
    ([pr#17454](https://github.com/ceph/ceph/pull/17454), xie xingguo)

-   tools: stop.sh: add ceph configure file location
    ([pr#20888](https://github.com/ceph/ceph/pull/20888), Jianpeng Ma)

-   tools: tools/ceph-conf: dump parsed config in plain text or as json
    ([issue#21862](http://tracker.ceph.com/issues/21862),
    [pr#18350](https://github.com/ceph/ceph/pull/18350), Piotr Dałek)

-   tools: tools/ceph_monstore_tool: include mgrmap in initial paxos
    epoch ([issue#22266](http://tracker.ceph.com/issues/22266),
    [pr#19780](https://github.com/ceph/ceph/pull/19780), Kefu Chai)

-   tools: tools/ceph_monstore_tool: rebuild initial mgrmap also
    ([issue#22266](http://tracker.ceph.com/issues/22266),
    [pr#19238](https://github.com/ceph/ceph/pull/19238), Kefu Chai)

-   tools: tools/ceph-objectstore-tool: command to trim the pg log
    ([issue#23242](http://tracker.ceph.com/issues/23242),
    [pr#20786](https://github.com/ceph/ceph/pull/20786), Josh Durgin,
    David Zafman)

-   tools: tools/ceph_objectstore_tool: fix \'dup\' unable to duplicate
    meta PG ([pr#17572](https://github.com/ceph/ceph/pull/17572), xie
    xingguo)

-   tools: tools/rados: improve the ls command usage
    ([pr#21553](https://github.com/ceph/ceph/pull/21553), Li Wang)

-   tools: tools: rados: make -f be \--format for consistency with ceph
    tool ([issue#15904](http://tracker.ceph.com/issues/15904),
    [pr#20147](https://github.com/ceph/ceph/pull/20147), Nathan Cutler)

-   tools: tools/rados: use the monotonic clock in rados bench
    ([issue#21375](http://tracker.ceph.com/issues/21375),
    [pr#18588](https://github.com/ceph/ceph/pull/18588), Mohamad Gebai)

-   tools: update monstore tool for fsmap, mgrmap
    ([issue#21577](http://tracker.ceph.com/issues/21577),
    [pr#18005](https://github.com/ceph/ceph/pull/18005), John Spray)

-   tools: Use \--no-mon-config so ceph_objectstore_tool.py test
    doesn\'t hang ([pr#21274](https://github.com/ceph/ceph/pull/21274),
    David Zafman)

-   tools: vstart.sh: move rgw configuration to client.rgw section
    ([pr#18331](https://github.com/ceph/ceph/pull/18331), Yan Jun)

-   tools: vstart.sh: use bluestore as default osd objectstore backend
    ([pr#17100](https://github.com/ceph/ceph/pull/17100), mychoxin)

-   vstart: fix option (due to quotes) and allow disabling dashboard
    ([issue#23345](http://tracker.ceph.com/issues/23345),
    [pr#20986](https://github.com/ceph/ceph/pull/20986), Joao Eduardo
    Luis)

-   vstart.sh: fix a typo
    ([pr#18729](https://github.com/ceph/ceph/pull/18729), iliul)

-   vstart.sh: Fix help text in vstart.sh
    ([pr#21071](https://github.com/ceph/ceph/pull/21071), Marc Koderer)

-   vstart.sh: quote cmd params when display executing cmd
    ([pr#17057](https://github.com/ceph/ceph/pull/17057), Jiaying Ren)

-   vstart.sh: quote command only when necessary
    ([pr#18181](https://github.com/ceph/ceph/pull/18181), Kefu Chai)

-   vstart.sh: should quote the parameters to get them quoted
    ([pr#18523](https://github.com/ceph/ceph/pull/18523), Kefu Chai)

-   vstart.sh: simplify the objectstore related logic
    ([pr#17749](https://github.com/ceph/ceph/pull/17749), Kefu Chai)
