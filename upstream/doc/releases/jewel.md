# Jewel

Jewel is the 10th stable release of Ceph. It is named after the jewel
squid (Histioteuthis reversa).

## v10.2.11 Jewel

This point releases brings a number of important bugfixes and has a few
important security fixes. This is expected to be the last Jewel release.
We recommend all Jewel 10.2.x users to upgrade.

### Notable Changes

-   CVE 2018-1128: auth: cephx authorizer subject to replay attack
    ([issue#24836](http://tracker.ceph.com/issues/24836), Sage Weil)
-   CVE 2018-1129: auth: cephx signature check is weak
    ([issue#24837](http://tracker.ceph.com/issues/24837), Sage Weil)
-   CVE 2018-10861: mon: auth checks not correct for pool ops
    ([issue#24838](http://tracker.ceph.com/issues/24838), Jason
    Dillaman)
-   The RBD C API\'s rbd_discard method and the C++ API\'s
    Image::discard method now enforce a maximum length of 2GB. This
    restriction prevents overflow of the result code.
-   New OSDs will now use rocksdb for omap data by default, rather than
    leveldb. omap is used by RGW bucket indexes and CephFS directories,
    and when a single leveldb grows to 10s of GB with a high write or
    delete workload, it can lead to high latency when leveldb\'s
    single-threaded compaction cannot keep up. rocksdb supports multiple
    threads for compaction, which avoids this problem.
-   The CephFS client now catches failures to clear dentries during
    startup and refuses to start as consistency and untrimmable cache
    issues may develop. The new option
    client_die_on_failed_dentry_invalidate (default: true) may be turned
    off to allow the client to proceed (dangerous!).
-   In 10.2.10 and earlier releases, keyring caps were not checked for
    validity, so the caps string could be anything. As of 10.2.11, caps
    strings are validated and providing a keyring with an invalid caps
    string to, e.g., \"ceph auth add\" will result in an error.

### Changelog

-   admin: bump sphinx to 1.6
    ([issue#21717](http://tracker.ceph.com/issues/21717),
    [pr#18166](https://github.com/ceph/ceph/pull/18166), Kefu Chai,
    Alfredo Deza)
-   auth: ceph auth add does not sanity-check caps
    ([issue#22525](http://tracker.ceph.com/issues/22525),
    [pr#21367](https://github.com/ceph/ceph/pull/21367), Jing Li, Nathan
    Cutler, Kefu Chai, Sage Weil)
-   build/ops: rpm: bump epoch ahead of ceph-common in RHEL base
    ([issue#20508](http://tracker.ceph.com/issues/20508),
    [pr#21190](https://github.com/ceph/ceph/pull/21190), Ken Dreyer)
-   build/ops: upstart: radosgw-all does not start on boot if ceph-base
    is not installed
    ([issue#18313](http://tracker.ceph.com/issues/18313),
    [pr#16294](https://github.com/ceph/ceph/pull/16294), Ken Dreyer)
-   ceph_authtool: add mode option
    ([issue#23513](http://tracker.ceph.com/issues/23513),
    [pr#21197](https://github.com/ceph/ceph/pull/21197), Sébastien Han)
-   ceph-disk: factor out the retry logic into a decorator
    ([issue#21728](http://tracker.ceph.com/issues/21728),
    [pr#18169](https://github.com/ceph/ceph/pull/18169), Kefu Chai)
-   ceph-disk: fix \--runtime omission when enabling
    ceph-osd@\$ID.service units for device-backed OSDs
    ([issue#21498](http://tracker.ceph.com/issues/21498),
    [pr#17942](https://github.com/ceph/ceph/pull/17942), Carl Xiong)
-   ceph-disk flake8 test fails on very old, and very new, versions of
    flake8 ([issue#22207](http://tracker.ceph.com/issues/22207),
    [pr#19153](https://github.com/ceph/ceph/pull/19153), Nathan Cutler)
-   cephfs: ceph.in: pass RADOS inst to LibCephFS
    ([issue#21406](http://tracker.ceph.com/issues/21406),
    [issue#21967](http://tracker.ceph.com/issues/21967),
    [pr#19907](https://github.com/ceph/ceph/pull/19907), Patrick
    Donnelly)
-   cephfs: client::mkdirs not handle well when two clients send mkdir
    request for a same dir
    ([issue#20592](http://tracker.ceph.com/issues/20592),
    [pr#20271](https://github.com/ceph/ceph/pull/20271), dongdong tao)
-   cephfs: client: prevent fallback to remount when
    dentry_invalidate_cb is true but root-\>dir is NULL
    ([issue#23211](http://tracker.ceph.com/issues/23211),
    [pr#21189](https://github.com/ceph/ceph/pull/21189), Zhi Zhang)
-   cephfs: fix tmap_upgrade crash
    ([issue#23529](http://tracker.ceph.com/issues/23529),
    [pr#21208](https://github.com/ceph/ceph/pull/21208), \"Yan, Zheng\")
-   cephfs: fuse client: ::rmdir() uses a deleted memory structure of
    dentry leads ...
    ([issue#22536](http://tracker.ceph.com/issues/22536),
    [pr#19993](https://github.com/ceph/ceph/pull/19993), YunfeiGuan)
-   cephfs-journal-tool: add \"set pool_id\" option
    ([issue#22631](http://tracker.ceph.com/issues/22631),
    [pr#20111](https://github.com/ceph/ceph/pull/20111), dongdong tao)
-   cephfs-journal-tool: move shutdown to the deconstructor of
    MDSUtility ([issue#22734](http://tracker.ceph.com/issues/22734),
    [pr#20333](https://github.com/ceph/ceph/pull/20333), dongdong tao)
-   cephfs: osdc: \"FAILED assert(bh-\>last_write_tid \> tid)\" in
    powercycle-wip-yuri-master-1.19.18-distro-basic-smithi
    ([issue#22741](http://tracker.ceph.com/issues/22741),
    [pr#20312](https://github.com/ceph/ceph/pull/20312), \"Yan, Zheng\")
-   cephfs: osdc/Journaler: make sure flush() writes enough data
    ([issue#22824](http://tracker.ceph.com/issues/22824),
    [pr#20435](https://github.com/ceph/ceph/pull/20435), \"Yan, Zheng\")
-   cephfs: Processes stuck waiting for write with ceph-fuse
    ([issue#22008](http://tracker.ceph.com/issues/22008),
    [issue#22207](http://tracker.ceph.com/issues/22207),
    [pr#19141](https://github.com/ceph/ceph/pull/19141), \"Yan, Zheng\")
-   ceph-fuse: failure to remount in startup test does not handle
    client_die_on_failed_remount properly
    ([issue#22269](http://tracker.ceph.com/issues/22269),
    [pr#21162](https://github.com/ceph/ceph/pull/21162), Patrick
    Donnelly)
-   ceph.in: bypass codec when writing raw binary data
    ([issue#23185](http://tracker.ceph.com/issues/23185),
    [pr#20763](https://github.com/ceph/ceph/pull/20763), Oleh Prypin)
-   ceph-objectstore-tool command to trim the pg log
    ([issue#23242](http://tracker.ceph.com/issues/23242),
    [pr#20882](https://github.com/ceph/ceph/pull/20882), Josh Durgin,
    David Zafman)
-   ceph-objectstore-tool: \"\$OBJ get-omaphdr\" and \"\$OBJ list-omap\"
    scan all pgs instead of using specific pg
    ([issue#21327](http://tracker.ceph.com/issues/21327),
    [pr#20284](https://github.com/ceph/ceph/pull/20284), David Zafman)
-   ceph.restart + ceph_manager.wait_for_clean is racy
    ([issue#15778](http://tracker.ceph.com/issues/15778),
    [pr#20508](https://github.com/ceph/ceph/pull/20508), Warren Usui,
    Sage Weil)
-   ceph_volume_client: fix setting caps for IDs
    ([issue#21501](http://tracker.ceph.com/issues/21501),
    [pr#18084](https://github.com/ceph/ceph/pull/18084), Ramana Raja)
-   class rbd.Image discard\-\-\--OSError: \[errno 2147483648\] error
    discarding region
    ([issue#16465](http://tracker.ceph.com/issues/16465),
    [issue#21966](http://tracker.ceph.com/issues/21966),
    [pr#20287](https://github.com/ceph/ceph/pull/20287), Nathan Cutler,
    Huan Zhang, Jason Dillaman)
-   cli/crushtools/build.t sometimes fails in jenkins\' make check run
    ([issue#21758](http://tracker.ceph.com/issues/21758),
    [pr#21158](https://github.com/ceph/ceph/pull/21158), Kefu Chai)
-   client reconnect gather race
    ([issue#22263](http://tracker.ceph.com/issues/22263),
    [pr#21163](https://github.com/ceph/ceph/pull/21163), \"Yan, Zheng\")
-   client: release revoking Fc after invalidate cache
    ([issue#22652](http://tracker.ceph.com/issues/22652),
    [pr#19975](https://github.com/ceph/ceph/pull/19975), \"Yan, Zheng\")
-   client: set client_try_dentry_invalidate to false by default
    ([issue#21423](http://tracker.ceph.com/issues/21423),
    [pr#17925](https://github.com/ceph/ceph/pull/17925), \"Yan, Zheng\")
-   \[cli\] rename of non-existent image results in seg fault
    ([issue#21248](http://tracker.ceph.com/issues/21248),
    [pr#20280](https://github.com/ceph/ceph/pull/20280), Jason Dillaman)
-   CLI unit formatting tests are broken
    ([issue#24733](http://tracker.ceph.com/issues/24733),
    [pr#22913](https://github.com/ceph/ceph/pull/22913), Jason Dillaman)
-   common: compute SimpleLRU\'s size with contents.size() instead of
    lru.... ([issue#22613](http://tracker.ceph.com/issues/22613),
    [pr#19978](https://github.com/ceph/ceph/pull/19978), Xuehan Xu)
-   common/config: set rocksdb_cache_size to OPT_U64
    ([issue#22104](http://tracker.ceph.com/issues/22104),
    [pr#18850](https://github.com/ceph/ceph/pull/18850), Vikhyat Umrao,
    liuhongtong)
-   common: fix typo in rados bench write JSON output
    ([issue#24199](http://tracker.ceph.com/issues/24199),
    [pr#22407](https://github.com/ceph/ceph/pull/22407), Sandor
    Zeestraten)
-   config: lower default omap entries recovered at once
    ([issue#21897](http://tracker.ceph.com/issues/21897),
    [pr#19927](https://github.com/ceph/ceph/pull/19927), Josh Durgin)
-   core: Addition of online osd \'omap\'compaction command
    ([issue#19592](http://tracker.ceph.com/issues/19592),
    [pr#17101](https://github.com/ceph/ceph/pull/17101), liuchang0812,
    Sage Weil)
-   core: global/signal_handler.cc: fix typo
    ([issue#21432](http://tracker.ceph.com/issues/21432),
    [pr#17883](https://github.com/ceph/ceph/pull/17883), Kefu Chai)
-   core: librados: Double free in rados_getxattrs_next
    ([issue#22042](http://tracker.ceph.com/issues/22042),
    [pr#20381](https://github.com/ceph/ceph/pull/20381), Gu Zhongyan)
-   core: Objecter::C_ObjectOperation_sparse_read throws/catches
    exceptions on -ENOENT
    ([issue#21844](http://tracker.ceph.com/issues/21844),
    [pr#18743](https://github.com/ceph/ceph/pull/18743), Jason Dillaman)
-   Deleting a pool with active notify linger ops can result in seg
    fault ([issue#23966](http://tracker.ceph.com/issues/23966),
    [pr#22188](https://github.com/ceph/ceph/pull/22188), Kefu Chai,
    Jason Dillaman)
-   doc: clarify Path Restriction instructions
    ([issue#16906](http://tracker.ceph.com/issues/16906),
    [pr#19795](https://github.com/ceph/ceph/pull/19795), huanwen ren)
-   doc: clarify Path Restriction instructions
    ([issue#16906](http://tracker.ceph.com/issues/16906),
    [pr#19840](https://github.com/ceph/ceph/pull/19840), Drunkard Zhang)
-   doc: remove region from INSTALL CEPH OBJECT GATEWAY
    ([issue#21610](http://tracker.ceph.com/issues/21610),
    [pr#18303](https://github.com/ceph/ceph/pull/18303), Orit Wasserman)
-   Filestore rocksdb compaction readahead option not set by default
    ([issue#21505](http://tracker.ceph.com/issues/21505),
    [pr#20446](https://github.com/ceph/ceph/pull/20446), Mark Nelson)
-   follow-on: osd: be_select_auth_object() sanity check oi soid
    ([issue#20471](http://tracker.ceph.com/issues/20471),
    [pr#20622](https://github.com/ceph/ceph/pull/20622), David Zafman)
-   HashIndex: randomize split threshold by a configurable amount
    ([issue#15835](http://tracker.ceph.com/issues/15835),
    [pr#19906](https://github.com/ceph/ceph/pull/19906), Josh Durgin)
-   include/fs_types: fix unsigned integer overflow
    ([issue#22494](http://tracker.ceph.com/issues/22494),
    [pr#19611](https://github.com/ceph/ceph/pull/19611), runsisi)
-   install-deps.sh: point gcc to the one shipped by distro
    ([issue#22220](http://tracker.ceph.com/issues/22220),
    [pr#19461](https://github.com/ceph/ceph/pull/19461), Kefu Chai)
-   install-deps.sh: readlink /usr/bin/gcc not
    /usr/bin/x86_64-linux-gnu-gcc
    ([issue#22220](http://tracker.ceph.com/issues/22220),
    [pr#19521](https://github.com/ceph/ceph/pull/19521), Kefu Chai)
-   install-deps.sh: update g++ symlink also
    ([issue#22220](http://tracker.ceph.com/issues/22220),
    [pr#19656](https://github.com/ceph/ceph/pull/19656), Kefu Chai)
-   journal: Message too long error when appending journal
    ([issue#23526](http://tracker.ceph.com/issues/23526),
    [pr#21215](https://github.com/ceph/ceph/pull/21215), Mykola Golub)
-   \[journal\] tags are not being expired if no other clients are
    registered ([issue#21960](http://tracker.ceph.com/issues/21960),
    [pr#20282](https://github.com/ceph/ceph/pull/20282), Jason Dillaman)
-   legal: remove doc license ambiguity
    ([issue#23336](http://tracker.ceph.com/issues/23336),
    [pr#20999](https://github.com/ceph/ceph/pull/20999), Nathan Cutler)
-   librados: copy out data to users\' buffer for xio
    ([issue#20616](http://tracker.ceph.com/issues/20616),
    [pr#17594](https://github.com/ceph/ceph/pull/17594), Vu Pham)
-   librbd: cannot clone all image-metas if we have more than 64
    key/value pairs
    ([issue#21814](http://tracker.ceph.com/issues/21814),
    [pr#21228](https://github.com/ceph/ceph/pull/21228), PCzhangPC)
-   librbd: cannot copy all image-metas if we have more than 64
    key/value pairs
    ([issue#21815](http://tracker.ceph.com/issues/21815),
    [pr#21203](https://github.com/ceph/ceph/pull/21203), PCzhangPC)
-   librbd: create+truncate for whole-object layered discards
    ([issue#23285](http://tracker.ceph.com/issues/23285),
    [pr#21219](https://github.com/ceph/ceph/pull/21219), Jason Dillaman)
-   librbd: list_children should not attempt to refresh image
    ([issue#21670](http://tracker.ceph.com/issues/21670),
    [pr#21224](https://github.com/ceph/ceph/pull/21224), Jason Dillaman)
-   librbd: object map batch update might cause OSD suicide timeout
    ([issue#22716](http://tracker.ceph.com/issues/22716),
    [issue#21797](http://tracker.ceph.com/issues/21797),
    [pr#21220](https://github.com/ceph/ceph/pull/21220), Song Shun,
    Jason Dillaman)
-   librbd: set deleted parent pointer to null
    ([issue#22158](http://tracker.ceph.com/issues/22158),
    [pr#19098](https://github.com/ceph/ceph/pull/19098), Jason Dillaman)
-   log: Fix AddressSanitizer: new-delete-type-mismatch
    ([issue#23324](http://tracker.ceph.com/issues/23324),
    [pr#21084](https://github.com/ceph/ceph/pull/21084), Brad Hubbard)
-   mds: FAILED assert(get_version() \< pv) in CDir::mark_dirty
    ([issue#21584](http://tracker.ceph.com/issues/21584),
    [pr#21156](https://github.com/ceph/ceph/pull/21156), Yan, Zheng,
    \"Yan, Zheng\")
-   mds: fix dump last_sent
    ([issue#22562](http://tracker.ceph.com/issues/22562),
    [pr#19961](https://github.com/ceph/ceph/pull/19961), dongdong tao)
-   mds: fix integer overflow
    ([issue#21067](http://tracker.ceph.com/issues/21067),
    [pr#17188](https://github.com/ceph/ceph/pull/17188), Henry Chang)
-   mds: fix scrub crash
    ([issue#22730](http://tracker.ceph.com/issues/22730),
    [pr#20335](https://github.com/ceph/ceph/pull/20335), dongdong tao)
-   mds: session reference leak
    ([issue#22821](http://tracker.ceph.com/issues/22821),
    [pr#21175](https://github.com/ceph/ceph/pull/21175), Nathan Cutler,
    \"Yan, Zheng\")
-   mds: unbalanced auth_pin/auth_unpin in RecoveryQueue code
    ([issue#22647](http://tracker.ceph.com/issues/22647),
    [pr#20067](https://github.com/ceph/ceph/pull/20067), \"Yan, Zheng\")
-   mds: underwater dentry check in CDir::\_omap_fetched is racy
    ([issue#23032](http://tracker.ceph.com/issues/23032),
    [pr#21185](https://github.com/ceph/ceph/pull/21185), Yan, Zheng)
-   mon/LogMonitor: call no_reply() on ignored log message
    ([issue#24180](http://tracker.ceph.com/issues/24180),
    [pr#22431](https://github.com/ceph/ceph/pull/22431), Sage Weil)
-   mon/MDSMonitor: no_reply on MMDSLoadTargets
    ([issue#23769](http://tracker.ceph.com/issues/23769),
    [pr#22189](https://github.com/ceph/ceph/pull/22189), Sage Weil)
-   mon/OSDMonitor.cc: fix expected_num_objects interpret error
    ([issue#22530](http://tracker.ceph.com/issues/22530),
    [pr#22050](https://github.com/ceph/ceph/pull/22050), Yang Honggang)
-   mon/OSDMonitor: fix dividing by zero in OSDUtilizationDumper
    ([issue#22662](http://tracker.ceph.com/issues/22662),
    [pr#20344](https://github.com/ceph/ceph/pull/20344), Mingxin Liu)
-   ObjectStore/StoreTest.FiemapHoles/3 fails with kstore
    ([issue#21716](http://tracker.ceph.com/issues/21716),
    [pr#20143](https://github.com/ceph/ceph/pull/20143), Kefu Chai, Ning
    Yao)
-   osd: also check the exsistence of clone obc for \"CEPH_SNAPDIR\"
    requests ([issue#17445](http://tracker.ceph.com/issues/17445),
    [pr#17707](https://github.com/ceph/ceph/pull/17707), Xuehan Xu)
-   osdc/Objecter: prevent double-invocation of linger op callback
    ([issue#23872](http://tracker.ceph.com/issues/23872),
    [pr#21754](https://github.com/ceph/ceph/pull/21754), Jason Dillaman)
-   osd: objecter sends out of sync with pg epochs for proxied ops
    ([issue#22123](http://tracker.ceph.com/issues/22123),
    [pr#20518](https://github.com/ceph/ceph/pull/20518), Sage Weil)
-   osd ops (sent and?) arrive at osd out of order
    ([issue#19133](http://tracker.ceph.com/issues/19133),
    [issue#19139](http://tracker.ceph.com/issues/19139),
    [pr#17893](https://github.com/ceph/ceph/pull/17893), Jianpeng Ma,
    Sage Weil)
-   osd: OSDMap cache assert on shutdown
    ([issue#21737](http://tracker.ceph.com/issues/21737),
    [pr#21184](https://github.com/ceph/ceph/pull/21184), Greg Farnum)
-   osd: osd_scrub_during_recovery only considers primary, not replicas
    ([issue#18206](http://tracker.ceph.com/issues/18206),
    [pr#17815](https://github.com/ceph/ceph/pull/17815), David Zafman)
-   osd/PrimaryLogPG: dump snap_trimq size
    ([issue#22448](http://tracker.ceph.com/issues/22448),
    [pr#21200](https://github.com/ceph/ceph/pull/21200), Piotr Dałek)
-   osd: recover_replicas: object added to missing set for backfill, but
    is not in recovering, error!
    ([issue#18162](http://tracker.ceph.com/issues/18162),
    [issue#14513](http://tracker.ceph.com/issues/14513),
    [pr#18690](https://github.com/ceph/ceph/pull/18690), huangjun,
    Adam C. Emerson, David Zafman)
-   osd: replica read can trigger cache promotion
    ([issue#20919](http://tracker.ceph.com/issues/20919),
    [pr#21199](https://github.com/ceph/ceph/pull/21199), Sage Weil)
-   osd: update heartbeat peers when a new OSD is added
    ([issue#18004](http://tracker.ceph.com/issues/18004),
    [pr#20108](https://github.com/ceph/ceph/pull/20108), Pan Liu)
-   performance: Only scan for omap corruption once
    ([issue#21328](http://tracker.ceph.com/issues/21328),
    [pr#18951](https://github.com/ceph/ceph/pull/18951), David Zafman)
-   qa: failures from pjd fstest
    ([issue#21383](http://tracker.ceph.com/issues/21383),
    [pr#21152](https://github.com/ceph/ceph/pull/21152), \"Yan, Zheng\")
-   qa: src/test/libcephfs/test.cc:376: Expected: (len) \> (0), actual:
    -34 vs 0 ([issue#22221](http://tracker.ceph.com/issues/22221),
    [pr#21172](https://github.com/ceph/ceph/pull/21172), Patrick
    Donnelly)
-   qa: use xfs instead of btrfs w/ filestore
    ([issue#20169](http://tracker.ceph.com/issues/20169),
    [issue#20911](http://tracker.ceph.com/issues/20911),
    [pr#18165](https://github.com/ceph/ceph/pull/18165), Sage Weil)
-   qa: use xfs instead of btrfs w/ filestore
    ([issue#21481](http://tracker.ceph.com/issues/21481),
    [pr#17847](https://github.com/ceph/ceph/pull/17847), Patrick
    Donnelly)
-   radosgw: fix awsv4 header line sort order
    ([issue#21607](http://tracker.ceph.com/issues/21607),
    [pr#18080](https://github.com/ceph/ceph/pull/18080), Marcus Watts)
-   rbd: clean up warnings when mirror commands used on non-setup pool
    ([issue#21319](http://tracker.ceph.com/issues/21319),
    [pr#21227](https://github.com/ceph/ceph/pull/21227), Jason Dillaman)
-   rbd: disk usage on empty pool no longer returns an error message
    ([issue#22200](http://tracker.ceph.com/issues/22200),
    [pr#19186](https://github.com/ceph/ceph/pull/19186), Jason Dillaman)
-   \[rbd\] image-meta list does not return all entries
    ([issue#21179](http://tracker.ceph.com/issues/21179),
    [pr#20281](https://github.com/ceph/ceph/pull/20281), Jason Dillaman)
-   rbd: is_qemu_running in qemu_rebuild_object_map.sh and
    qemu_dynamic_features.sh may return false positive
    ([issue#23502](http://tracker.ceph.com/issues/23502),
    [pr#21207](https://github.com/ceph/ceph/pull/21207), Mykola Golub)
-   rbd: \[journal\] allocating a new tag after acquiring the lock
    should use on-disk committed position
    ([issue#22945](http://tracker.ceph.com/issues/22945),
    [pr#21206](https://github.com/ceph/ceph/pull/21206), Jason Dillaman)
-   rbd: librbd: filter out potential race with image rename
    ([issue#18435](http://tracker.ceph.com/issues/18435),
    [pr#19855](https://github.com/ceph/ceph/pull/19855), Jason Dillaman)
-   rbd ls -l crashes with SIGABRT
    ([issue#21558](http://tracker.ceph.com/issues/21558),
    [pr#19801](https://github.com/ceph/ceph/pull/19801), Jason Dillaman)
-   rbd-mirror: cluster watcher should ensure it has latest OSD map
    ([issue#22461](http://tracker.ceph.com/issues/22461),
    [pr#19644](https://github.com/ceph/ceph/pull/19644), Jason Dillaman)
-   rbd-mirror: fix potential infinite loop when formatting status
    message ([issue#22932](http://tracker.ceph.com/issues/22932),
    [pr#20418](https://github.com/ceph/ceph/pull/20418), Mykola Golub)
-   rbd-mirror: ignore permission errors on rbd_mirroring object
    ([issue#20571](http://tracker.ceph.com/issues/20571),
    [pr#21225](https://github.com/ceph/ceph/pull/21225), Jason Dillaman)
-   rbd-mirror: strip environment/CLI overrides for remote cluster
    ([issue#21894](http://tracker.ceph.com/issues/21894),
    [pr#21223](https://github.com/ceph/ceph/pull/21223), Jason Dillaman)
-   \[rbd-nbd\] Fedora does not register resize events
    ([issue#22131](http://tracker.ceph.com/issues/22131),
    [pr#19115](https://github.com/ceph/ceph/pull/19115), Jason Dillaman)
-   rbd-nbd: fix ebusy when do map
    ([issue#23528](http://tracker.ceph.com/issues/23528),
    [pr#21232](https://github.com/ceph/ceph/pull/21232), Li Wang)
-   rbd: possible deadlock in various maintenance operations
    ([issue#22120](http://tracker.ceph.com/issues/22120),
    [pr#20285](https://github.com/ceph/ceph/pull/20285), Jason Dillaman)
-   rbd: rbd crashes during map
    ([issue#21808](http://tracker.ceph.com/issues/21808),
    [pr#18843](https://github.com/ceph/ceph/pull/18843), Peter Keresztes
    Schmidt)
-   rbd: rbd-mirror split brain test case can have a false-positive
    failure until teuthology
    ([issue#22485](http://tracker.ceph.com/issues/22485),
    [pr#21205](https://github.com/ceph/ceph/pull/21205), Jason Dillaman)
-   rbd: TestLibRBD.RenameViaLockOwner may still fail with -ENOENT
    ([issue#23068](http://tracker.ceph.com/issues/23068),
    [pr#20627](https://github.com/ceph/ceph/pull/20627), Mykola Golub)
-   repair_test fails due to race with osd start
    ([issue#20705](http://tracker.ceph.com/issues/20705),
    [pr#20146](https://github.com/ceph/ceph/pull/20146), Sage Weil)
-   rgw: 15912 15673 (Fix duplicate tag removal during GC, cls/refcount:
    store and use list of retired tags)
    ([issue#20107](http://tracker.ceph.com/issues/20107),
    [pr#16708](https://github.com/ceph/ceph/pull/16708), Jens Rosenboom)
-   rgw: abort in listing mapped nbd devices when running in a container
    ([issue#22012](http://tracker.ceph.com/issues/22012),
    [issue#22011](http://tracker.ceph.com/issues/22011),
    [pr#20286](https://github.com/ceph/ceph/pull/20286), Li Wang, Pan
    Liu)
-   rgw: add ability to sync user stats from admin api
    ([issue#21301](http://tracker.ceph.com/issues/21301),
    [pr#20179](https://github.com/ceph/ceph/pull/20179), Nathan Johnson)
-   rgw: add cors header rule check in cors option request
    ([issue#22002](http://tracker.ceph.com/issues/22002),
    [pr#19057](https://github.com/ceph/ceph/pull/19057), yuliyang)
-   rgw: add radosgw-admin sync error trim to trim sync error log
    ([issue#23287](http://tracker.ceph.com/issues/23287),
    [pr#21210](https://github.com/ceph/ceph/pull/21210), fang yuxiang)
-   rgw: add xml output header in RGWCopyObj_ObjStore_S3 response msg
    ([issue#22416](http://tracker.ceph.com/issues/22416),
    [pr#19887](https://github.com/ceph/ceph/pull/19887), Enming Zhang)
-   rgw: automated trimming of datalog and mdlog
    ([issue#18227](http://tracker.ceph.com/issues/18227),
    [pr#20061](https://github.com/ceph/ceph/pull/20061), Casey Bodley)
-   rgw: bi list entry count incremented on error, distorting error code
    ([issue#21205](http://tracker.ceph.com/issues/21205),
    [pr#18207](https://github.com/ceph/ceph/pull/18207), Nathan Cutler)
-   rgw: boto3 v4 SignatureDoesNotMatch failure due to sorting of
    sse-kms headers
    ([issue#21832](http://tracker.ceph.com/issues/21832),
    [pr#18772](https://github.com/ceph/ceph/pull/18772), Nathan Cutler)
-   rgw: bucket resharding should not update bucket ACL or user stats
    ([issue#22124](http://tracker.ceph.com/issues/22124),
    [pr#20421](https://github.com/ceph/ceph/pull/20421), Orit Wasserman)
-   rgw: copying part without http header x-amz-copy-source-range will
    be mistaken for copying object
    ([issue#22729](http://tracker.ceph.com/issues/22729),
    [pr#21294](https://github.com/ceph/ceph/pull/21294), Malcolm Lee)
-   rgw: core dump, recursive lock of RGWKeystoneTokenCache
    ([issue#23171](http://tracker.ceph.com/issues/23171),
    [pr#20639](https://github.com/ceph/ceph/pull/20639), Mark Kogan,
    Adam Kupczyk)
-   rgw: data sync of versioned objects, note updating bi marker
    ([issue#18885](http://tracker.ceph.com/issues/18885),
    [pr#21213](https://github.com/ceph/ceph/pull/21213), Yehuda Sadeh)
-   rgw: dont log EBUSY errors in \'sync error list\'
    ([issue#22473](http://tracker.ceph.com/issues/22473),
    [pr#19908](https://github.com/ceph/ceph/pull/19908), Casey Bodley)
-   rgw: ECANCELED in rgw_get_system_obj() leads to infinite loop
    ([issue#17996](http://tracker.ceph.com/issues/17996),
    [pr#20561](https://github.com/ceph/ceph/pull/20561), Yehuda Sadeh)
-   rgw: file deadlock on lru evicting
    ([issue#22736](http://tracker.ceph.com/issues/22736),
    [pr#20076](https://github.com/ceph/ceph/pull/20076), Matt Benjamin)
-   rgw: file write error
    ([issue#21455](http://tracker.ceph.com/issues/21455),
    [pr#18304](https://github.com/ceph/ceph/pull/18304), Yao Zongyou)
-   rgw: fix chained cache invalidation to prevent cache size growth
    ([issue#22410](http://tracker.ceph.com/issues/22410),
    [pr#19469](https://github.com/ceph/ceph/pull/19469), Mark Kogan)
-   rgw: fix doubled underscore with s3/swift server-side copy
    ([issue#22529](http://tracker.ceph.com/issues/22529),
    [pr#19747](https://github.com/ceph/ceph/pull/19747), Matt Benjamin)
-   rgw: fix GET website response error code
    ([issue#22272](http://tracker.ceph.com/issues/22272),
    [pr#19488](https://github.com/ceph/ceph/pull/19488), Dmitry Plyakin)
-   rgw: fix index update in dir_suggest_changes
    ([issue#24280](http://tracker.ceph.com/issues/24280),
    [pr#22677](https://github.com/ceph/ceph/pull/22677), Tianshan Qu)
-   rgw: fix marker encoding problem
    ([issue#20463](http://tracker.ceph.com/issues/20463),
    [pr#17731](https://github.com/ceph/ceph/pull/17731), Orit Wasserman,
    Marcus Watts)
-   rgw: fix swift anonymous access
    ([issue#22259](http://tracker.ceph.com/issues/22259),
    [pr#19194](https://github.com/ceph/ceph/pull/19194), Marcus Watts)
-   rgw: Fix swift object expiry not deleting objects
    ([issue#22084](http://tracker.ceph.com/issues/22084),
    [pr#18925](https://github.com/ceph/ceph/pull/18925), Pavan
    Rallabhandi)
-   rgw: fix the bug that part\'s index can\'t be removed after
    completing ([issue#19604](http://tracker.ceph.com/issues/19604),
    [pr#16763](https://github.com/ceph/ceph/pull/16763), Zhang Shaowen,
    Matt Benjamin)
-   rgw: fix the max-uploads parameter not work
    ([issue#22825](http://tracker.ceph.com/issues/22825),
    [pr#20479](https://github.com/ceph/ceph/pull/20479), Xin Liao)
-   rgw: inefficient buffer usage for PUTs
    ([issue#23207](http://tracker.ceph.com/issues/23207),
    [pr#21098](https://github.com/ceph/ceph/pull/21098), Marcus Watts)
-   rgw: libcurl & ssl fixes
    ([issue#22951](http://tracker.ceph.com/issues/22951),
    [issue#23203](http://tracker.ceph.com/issues/23203),
    [issue#23162](http://tracker.ceph.com/issues/23162),
    [pr#20749](https://github.com/ceph/ceph/pull/20749), Marcus Watts,
    Abhishek Lekshmanan, Jesse Williamson)
-   rgw: list bucket which enable versioning get wrong result when user
    marker ([issue#21500](http://tracker.ceph.com/issues/21500),
    [pr#20291](https://github.com/ceph/ceph/pull/20291), yuliyang)
-   rgw: log includes zero byte sometimes
    ([issue#20037](http://tracker.ceph.com/issues/20037),
    [pr#17151](https://github.com/ceph/ceph/pull/17151), Abhishek
    Lekshmanan)
-   rgw: make init env methods return an error
    ([issue#23039](http://tracker.ceph.com/issues/23039),
    [pr#20800](https://github.com/ceph/ceph/pull/20800), Abhishek
    Lekshmanan)
-   RGW: Multipart upload may double the quota
    ([issue#21586](http://tracker.ceph.com/issues/21586),
    [pr#18121](https://github.com/ceph/ceph/pull/18121), Sibei Gao, Matt
    Benjamin)
-   rgw: multisite: data sync status advances despite failure in
    RGWListBucketIndexesCR
    ([issue#21735](http://tracker.ceph.com/issues/21735),
    [pr#20269](https://github.com/ceph/ceph/pull/20269), Casey Bodley)
-   rgw: multisite: Get bucket location which is located in another
    zonegroup, will return 301 Moved Permanently
    ([issue#21125](http://tracker.ceph.com/issues/21125),
    [pr#18305](https://github.com/ceph/ceph/pull/18305), Shasha Lu,
    lvshuhua, Jiaying Ren)
-   rgw: null instance mtime incorrect when enable versioning
    ([issue#21743](http://tracker.ceph.com/issues/21743),
    [pr#20262](https://github.com/ceph/ceph/pull/20262), Shasha Lu)
-   rgw: radosgw-admin: add an option to reset user stats
    ([issue#23335](http://tracker.ceph.com/issues/23335),
    [issue#23322](http://tracker.ceph.com/issues/23322),
    [pr#20877](https://github.com/ceph/ceph/pull/20877), Abhishek
    Lekshmanan)
-   rgw: release cls lock if taken in RGWCompleteMultipart
    ([issue#21596](http://tracker.ceph.com/issues/21596),
    [issue#22368](http://tracker.ceph.com/issues/22368),
    [pr#18116](https://github.com/ceph/ceph/pull/18116), Casey Bodley,
    Matt Benjamin)
-   rgw: resharding needs to set back the bucket ACL after link
    ([issue#22742](http://tracker.ceph.com/issues/22742),
    [pr#20039](https://github.com/ceph/ceph/pull/20039), Orit Wasserman)
-   rgw: resolve Random 500 errors in Swift PutObject (22517)
    ([issue#22517](http://tracker.ceph.com/issues/22517),
    [issue#21560](http://tracker.ceph.com/issues/21560),
    [pr#19769](https://github.com/ceph/ceph/pull/19769), Adam C.
    Emerson, Matt Benjamin)
-   rgw: rgw_file: recursive lane lock can occur in LRU drain
    ([issue#20374](http://tracker.ceph.com/issues/20374),
    [pr#17149](https://github.com/ceph/ceph/pull/17149), Matt Benjamin)
-   rgw: S3 POST policy should not require Content-Type
    ([issue#20201](http://tracker.ceph.com/issues/20201),
    [pr#19635](https://github.com/ceph/ceph/pull/19635), Matt Benjamin)
-   rgw: s3website error handler uses original object name
    ([issue#23201](http://tracker.ceph.com/issues/23201),
    [issue#20307](http://tracker.ceph.com/issues/20307),
    [pr#21100](https://github.com/ceph/ceph/pull/21100), liuhong, Casey
    Bodley)
-   rgw: segfaults after running radosgw-admin data sync init
    ([issue#22083](http://tracker.ceph.com/issues/22083),
    [pr#19783](https://github.com/ceph/ceph/pull/19783), Casey Bodley,
    Abhishek Lekshmanan)
-   rgw: segmentation fault when starting radosgw after reverting
    .rgw.root ([issue#21996](http://tracker.ceph.com/issues/21996),
    [pr#20292](https://github.com/ceph/ceph/pull/20292), Orit Wasserman,
    Casey Bodley)
-   rgw: stale bucket index entry remains after object deletion
    ([issue#22555](http://tracker.ceph.com/issues/22555),
    [pr#20293](https://github.com/ceph/ceph/pull/20293), J. Eric
    Ivancich)
-   rgw: system user can\'t delete bucket completely
    ([issue#22248](http://tracker.ceph.com/issues/22248),
    [pr#21212](https://github.com/ceph/ceph/pull/21212), Casey Bodley)
-   rgw: tcmalloc ([issue#23469](http://tracker.ceph.com/issues/23469),
    [pr#21073](https://github.com/ceph/ceph/pull/21073), Matt Benjamin)
-   rgw: upldate the max-buckets when the quota is uploaded
    ([issue#22745](http://tracker.ceph.com/issues/22745),
    [pr#20496](https://github.com/ceph/ceph/pull/20496), zhaokun)
-   rgw: user creation can overwrite existing user even if different uid
    is given ([issue#21685](http://tracker.ceph.com/issues/21685),
    [pr#20074](https://github.com/ceph/ceph/pull/20074), Casey Bodley)
-   RHEL 7.3 Selinux denials at OSD start
    ([issue#19200](http://tracker.ceph.com/issues/19200),
    [pr#18780](https://github.com/ceph/ceph/pull/18780), Boris Ranto)
-   scrub errors not cleared on replicas can cause inconsistent pg state
    when replica takes over primary
    ([issue#23267](http://tracker.ceph.com/issues/23267),
    [pr#21194](https://github.com/ceph/ceph/pull/21194), David Zafman)
-   snapset xattr corruption propagated from primary to other shards
    ([issue#20186](http://tracker.ceph.com/issues/20186),
    [issue#18409](http://tracker.ceph.com/issues/18409),
    [issue#21907](http://tracker.ceph.com/issues/21907),
    [pr#20331](https://github.com/ceph/ceph/pull/20331), David Zafman)
-   systemd: Add explicit Before=ceph.target
    ([issue#21477](http://tracker.ceph.com/issues/21477),
    [pr#17841](https://github.com/ceph/ceph/pull/17841), Tim Serong)
-   table of contents doesn\'t render for luminous/jewel docs
    ([issue#23780](http://tracker.ceph.com/issues/23780),
    [pr#21503](https://github.com/ceph/ceph/pull/21503), Alfredo Deza)
-   test: Adjust for Jewel quirk caused of differences with master
    ([issue#23006](http://tracker.ceph.com/issues/23006),
    [pr#20463](https://github.com/ceph/ceph/pull/20463), David Zafman)
-   test/CMakeLists: disable test_pidfile.sh
    ([issue#20975](http://tracker.ceph.com/issues/20975),
    [pr#20557](https://github.com/ceph/ceph/pull/20557), Sage Weil)
-   test_health_warnings.sh can fail
    ([issue#21121](http://tracker.ceph.com/issues/21121),
    [pr#20289](https://github.com/ceph/ceph/pull/20289), Sage Weil)
-   test/librbd: fixed metadata tests under upgrade scenarios
    ([issue#21911](http://tracker.ceph.com/issues/21911),
    [pr#18548](https://github.com/ceph/ceph/pull/18548), Jason Dillaman)
-   test/librbd: utilize unique pool for cache tier testing
    ([issue#11502](http://tracker.ceph.com/issues/11502),
    [pr#20524](https://github.com/ceph/ceph/pull/20524), Jason Dillaman)
-   tests: rbd_mirror_helpers.sh request_resync_image function saves
    image id to wrong variable
    ([issue#21663](http://tracker.ceph.com/issues/21663),
    [pr#19804](https://github.com/ceph/ceph/pull/19804), Jason Dillaman)
-   tests: test_admin_socket.sh may fail on wait_for_clean
    ([issue#23499](http://tracker.ceph.com/issues/23499),
    [pr#21125](https://github.com/ceph/ceph/pull/21125), Mykola Golub)
-   tests: tests/librbd: updated test_notify to handle new release lock
    semantics ([issue#21912](http://tracker.ceph.com/issues/21912),
    [pr#18560](https://github.com/ceph/ceph/pull/18560), Jason Dillaman)
-   tests: unittest_pglog timeout
    ([issue#23504](http://tracker.ceph.com/issues/23504),
    [issue#18030](http://tracker.ceph.com/issues/18030),
    [pr#21135](https://github.com/ceph/ceph/pull/21135), Nathan Cutler,
    Loic Dachary)
-   tools: ceph-objectstore-tool set-size should clear data-digest
    ([issue#22112](http://tracker.ceph.com/issues/22112),
    [pr#20070](https://github.com/ceph/ceph/pull/20070), David Zafman)
-   Ubuntu amd64 client can not discover the ubuntu arm64 ceph cluster
    ([issue#19705](http://tracker.ceph.com/issues/19705),
    [pr#18294](https://github.com/ceph/ceph/pull/18294), Kefu Chai)

## v10.2.10 Jewel

This point release brings a number of important bugfixes in all major
components of Ceph, we recommend all Jewel 10.2.x users to upgrade.

For a detailed list of changes refer to :download: [the complete
changelog \<../changelog/v10.2.10txt\>]{.title-ref}

### Notable Changes

-   build/ops: Add fix subcommand to ceph-disk, fix SELinux denials, and
    speed up upgrade from non-SELinux enabled ceph to an SELinux enabled
    one ([issue#20077](http://tracker.ceph.com/issues/20077),
    [issue#20184](http://tracker.ceph.com/issues/20184),
    [issue#19545](http://tracker.ceph.com/issues/19545),
    [pr#14346](https://github.com/ceph/ceph/pull/14346), Boris Ranto)
-   build/ops: deb: Fix logrotate packaging
    ([issue#19938](http://tracker.ceph.com/issues/19938),
    [pr#15428](https://github.com/ceph/ceph/pull/15428), Nathan Cutler)
-   build/ops: extended, customizable systemd ceph-disk timeout
    ([issue#18740](http://tracker.ceph.com/issues/18740),
    [pr#15051](https://github.com/ceph/ceph/pull/15051), Alexey
    Sheplyakov)
-   build/ops: rpm: fix python-Sphinx package name for SUSE
    ([issue#19924](http://tracker.ceph.com/issues/19924),
    [pr#15196](https://github.com/ceph/ceph/pull/15196), Nathan Cutler,
    Jan Matejek)
-   build/ops: rpm: set subman cron attributes in spec file
    ([issue#20074](http://tracker.ceph.com/issues/20074),
    [pr#15473](https://github.com/ceph/ceph/pull/15473), Thomas Serlin)
-   cephfs: ceph-fuse segfaults at mount time, assert in
    ceph::log::Log::stop
    ([issue#18157](http://tracker.ceph.com/issues/18157),
    [pr#16963](https://github.com/ceph/ceph/pull/16963), Greg Farnum)
-   cephfs: df reports negative disk \"used\" value when quota exceed
    ([issue#20178](http://tracker.ceph.com/issues/20178),
    [pr#16151](https://github.com/ceph/ceph/pull/16151), John Spray)
-   cephfs: get_quota_root sends lookupname op for every buffered write
    ([issue#20945](http://tracker.ceph.com/issues/20945),
    [pr#17396](https://github.com/ceph/ceph/pull/17396), Dan van der
    Ster)
-   cephfs: osdc/Filer: truncate large file party by party
    ([issue#19755](http://tracker.ceph.com/issues/19755),
    [pr#15442](https://github.com/ceph/ceph/pull/15442), \"Yan, Zheng\")
-   core: an OSD was seen getting ENOSPC even with
    osd_failsafe_full_ratio passed
    ([issue#20544](http://tracker.ceph.com/issues/20544),
    [issue#16878](http://tracker.ceph.com/issues/16878),
    [issue#19733](http://tracker.ceph.com/issues/19733),
    [issue#15912](http://tracker.ceph.com/issues/15912),
    [pr#15050](https://github.com/ceph/ceph/pull/15050), Sage Weil,
    David Zafman)
-   core: disable skewed utilization warning by default
    ([issue#20730](http://tracker.ceph.com/issues/20730),
    [pr#17210](https://github.com/ceph/ceph/pull/17210), David Zafman)
-   core: interval_set: optimize intersect_of insert operations
    ([issue#21229](http://tracker.ceph.com/issues/21229),
    [pr#17514](https://github.com/ceph/ceph/pull/17514), Zac Medico)
-   core: kv: let ceph_logger destructed after db reset
    ([issue#21336](http://tracker.ceph.com/issues/21336),
    [pr#17626](https://github.com/ceph/ceph/pull/17626), wumingqiao)
-   core: test_envlibrados_for_rocksdb.yaml fails on crypto restart
    ([issue#19741](http://tracker.ceph.com/issues/19741),
    [pr#16293](https://github.com/ceph/ceph/pull/16293), Kefu Chai)
-   libradosstriper silently fails to delete empty objects in jewel
    ([issue#20325](http://tracker.ceph.com/issues/20325),
    [pr#15760](https://github.com/ceph/ceph/pull/15760), Stan K)
-   librbd: fail IO request when exclusive lock cannot be obtained
    ([issue#20168](http://tracker.ceph.com/issues/20168),
    [issue#21251](http://tracker.ceph.com/issues/21251),
    [pr#17402](https://github.com/ceph/ceph/pull/17402), Jason Dillaman)
-   librbd: prevent self-blacklisting during break lock
    ([issue#18666](http://tracker.ceph.com/issues/18666),
    [pr#17412](https://github.com/ceph/ceph/pull/17412), Jason Dillaman)
-   librbd: reacquire lock should update lock owner client id
    ([issue#19929](http://tracker.ceph.com/issues/19929),
    [pr#17385](https://github.com/ceph/ceph/pull/17385), Jason Dillaman)
-   mds: damage reporting by ino number is useless
    ([issue#18509](http://tracker.ceph.com/issues/18509),
    [issue#16016](http://tracker.ceph.com/issues/16016),
    [pr#14699](https://github.com/ceph/ceph/pull/14699), John Spray,
    Michal Jarzabek)
-   mds: log rotation doesn\'t work if mds has respawned
    ([issue#19291](http://tracker.ceph.com/issues/19291),
    [pr#14673](https://github.com/ceph/ceph/pull/14673), Patrick
    Donnelly)
-   mds: save projected path into inode_t::stray_prior_path
    ([issue#20340](http://tracker.ceph.com/issues/20340),
    [pr#16150](https://github.com/ceph/ceph/pull/16150), \"Yan, Zheng\")
-   mon: crash on shutdown, lease_ack_timeout event
    ([issue#19825](http://tracker.ceph.com/issues/19825),
    [pr#15083](https://github.com/ceph/ceph/pull/15083), Kefu Chai,
    Michal Jarzabek, Alexey Sheplyakov)
-   mon: Disallow enabling \'hashpspool\' option to a pool without some
    kind of \--i-understand-this-will-remap-all-pgs flag
    ([issue#18468](http://tracker.ceph.com/issues/18468),
    [pr#13507](https://github.com/ceph/ceph/pull/13507), Vikhyat Umrao)
-   mon: factor mon_osd_full_ratio into MAX AVAIL calc
    ([issue#18522](http://tracker.ceph.com/issues/18522),
    [pr#15236](https://github.com/ceph/ceph/pull/15236), Sage Weil)
-   mon: fail to form large quorum; msg/async busy loop
    ([issue#20230](http://tracker.ceph.com/issues/20230),
    [pr#15726](https://github.com/ceph/ceph/pull/15726), Haomai Wang,
    Michal Jarzabek)
-   mon: fix force_pg_create pg stuck in creating bug
    ([issue#18298](http://tracker.ceph.com/issues/18298),
    [pr#17008](https://github.com/ceph/ceph/pull/17008), Alexey
    Sheplyakov)
-   mon: osd crush set crushmap need sanity check
    ([issue#19302](http://tracker.ceph.com/issues/19302),
    [pr#16144](https://github.com/ceph/ceph/pull/16144), Loic Dachary)
-   osd: Add heartbeat message for Jumbo Frames (MTU 9000)
    ([issue#20087](http://tracker.ceph.com/issues/20087),
    [issue#20323](http://tracker.ceph.com/issues/20323),
    [pr#16059](https://github.com/ceph/ceph/pull/16059), Piotr Dałek,
    Sage Weil, Greg Farnum)
-   osd: fix infinite loops in fiemap
    ([issue#19996](http://tracker.ceph.com/issues/19996),
    [pr#15189](https://github.com/ceph/ceph/pull/15189), Sage Weil, Ning
    Yao)
-   osd: leaked MOSDMap
    ([issue#18293](http://tracker.ceph.com/issues/18293),
    [pr#14943](https://github.com/ceph/ceph/pull/14943), Sage Weil)
-   osd: objecter full_try behavior not consistent with osd
    ([issue#19430](http://tracker.ceph.com/issues/19430),
    [pr#15474](https://github.com/ceph/ceph/pull/15474), Sage Weil)
-   osd: omap threadpool heartbeat is only reset every 100 values
    ([issue#20375](http://tracker.ceph.com/issues/20375),
    [pr#16167](https://github.com/ceph/ceph/pull/16167), Josh Durgin)
-   osd: osd_internal_types: wake snaptrimmer on put_read lock, too
    ([issue#19131](http://tracker.ceph.com/issues/19131),
    [pr#16015](https://github.com/ceph/ceph/pull/16015), Sage Weil)
-   osd: PrimaryLogPG: do not call on_shutdown() if (pg.deleting)
    ([issue#19902](http://tracker.ceph.com/issues/19902),
    [pr#15065](https://github.com/ceph/ceph/pull/15065), Kefu Chai)
-   osd: rados ls on pool with no access returns no error
    ([issue#20043](http://tracker.ceph.com/issues/20043),
    [issue#19790](http://tracker.ceph.com/issues/19790),
    [pr#16473](https://github.com/ceph/ceph/pull/16473), Nathan Cutler,
    Kefu Chai, John Spray, Sage Weil, Brad Hubbard)
-   osd: ReplicatedPG: solve cache tier osd high memory consumption
    ([issue#20464](http://tracker.ceph.com/issues/20464),
    [pr#16169](https://github.com/ceph/ceph/pull/16169), Peng Xie)
-   osd: Reset() snaptrimmer on shutdown and do not default-abort on
    leaked pg refs ([issue#19931](http://tracker.ceph.com/issues/19931),
    [pr#15322](https://github.com/ceph/ceph/pull/15322), Greg Farnum)
-   osd: scrub_to specifies clone ver, but transaction include head
    write ver ([issue#20041](http://tracker.ceph.com/issues/20041),
    [pr#16405](https://github.com/ceph/ceph/pull/16405), David Zafman)
-   osd: unlock sdata_op_ordering_lock with sdata_lock hold to avoid
    missing wakeup signal
    ([issue#20427](http://tracker.ceph.com/issues/20427),
    [pr#15947](https://github.com/ceph/ceph/pull/15947), Alexey
    Sheplyakov)
-   qa: add a sleep after restarting osd before \"tell\"ing it
    ([issue#16239](http://tracker.ceph.com/issues/16239),
    [pr#15475](https://github.com/ceph/ceph/pull/15475), Kefu Chai)
-   rbd: api: is_exclusive_lock_owner shouldn\'t return -EBUSY
    ([issue#20182](http://tracker.ceph.com/issues/20182),
    [pr#16296](https://github.com/ceph/ceph/pull/16296), Jason Dillaman)
-   rbd: cli: ensure positional arguments exist before casting
    ([issue#20185](http://tracker.ceph.com/issues/20185),
    [pr#16295](https://github.com/ceph/ceph/pull/16295), Jason Dillaman)
-   rbd: cli: map with cephx disabled results in error message
    ([issue#19035](http://tracker.ceph.com/issues/19035),
    [pr#16297](https://github.com/ceph/ceph/pull/16297), Jason Dillaman)
-   rbd: default features should be negotiated with the OSD
    ([issue#17010](http://tracker.ceph.com/issues/17010),
    [pr#14874](https://github.com/ceph/ceph/pull/14874), Mykola Golub,
    Jason Dillaman)
-   rbd: Enabling mirroring for a pool with clones may fail
    ([issue#19798](http://tracker.ceph.com/issues/19798),
    [issue#19130](http://tracker.ceph.com/issues/19130),
    [pr#14663](https://github.com/ceph/ceph/pull/14663), Mykola Golub,
    Jason Dillaman)
-   rbd-mirror: image sync should send NOCACHE advise flag
    ([issue#17127](http://tracker.ceph.com/issues/17127),
    [pr#16285](https://github.com/ceph/ceph/pull/16285), Mykola Golub)
-   rbd: object-map: batch updates during trim operation
    ([issue#17356](http://tracker.ceph.com/issues/17356),
    [pr#15460](https://github.com/ceph/ceph/pull/15460), Mykola Golub,
    Venky Shankar, Nathan Cutler)
-   rbd: Potential IO hang if image is flattened while read request is
    in-flight ([issue#19832](http://tracker.ceph.com/issues/19832),
    [pr#15464](https://github.com/ceph/ceph/pull/15464), Jason Dillaman)
-   rbd: rbd_clone_copy_on_read ineffective with exclusive-lock
    ([issue#18888](http://tracker.ceph.com/issues/18888),
    [pr#16124](https://github.com/ceph/ceph/pull/16124), Nathan Cutler,
    Venky Shankar, Jason Dillaman)
-   rbd: rbd-mirror: ensure missing images are re-synced when detected
    ([issue#19811](http://tracker.ceph.com/issues/19811),
    [pr#15488](https://github.com/ceph/ceph/pull/15488), Jason Dillaman)
-   rbd: rbd-mirror: failover and failback of unmodified image results
    in split-brain ([issue#19858](http://tracker.ceph.com/issues/19858),
    [pr#14977](https://github.com/ceph/ceph/pull/14977), Jason Dillaman)
-   rbd: rbd-nbd: kernel reported invalid device size (0,
    expected 1073741824)
    ([issue#19871](http://tracker.ceph.com/issues/19871),
    [pr#15463](https://github.com/ceph/ceph/pull/15463), Mykola Golub)
-   rgw: add the remove-x-delete feature to cancel swift object
    expiration ([issue#19074](http://tracker.ceph.com/issues/19074),
    [pr#14659](https://github.com/ceph/ceph/pull/14659), Jing Wenjun)
-   rgw: aws4: add rgw_s3_auth_aws4_force_boto2_compat conf option
    ([issue#16463](http://tracker.ceph.com/issues/16463),
    [pr#17009](https://github.com/ceph/ceph/pull/17009), Javier M.
    Mellid)
-   rgw: bucket index check in radosgw-admin removes valid index
    ([issue#18470](http://tracker.ceph.com/issues/18470),
    [pr#16856](https://github.com/ceph/ceph/pull/16856), Zhang Shaowen,
    Pavan Rallabhandi)
-   rgw: cls: ceph::timespan tag_timeout wrong units
    ([issue#20380](http://tracker.ceph.com/issues/20380),
    [pr#16289](https://github.com/ceph/ceph/pull/16289), Matt Benjamin)
-   rgw: Custom data header support
    ([issue#19644](http://tracker.ceph.com/issues/19644),
    [pr#15966](https://github.com/ceph/ceph/pull/15966), Pavan
    Rallabhandi)
-   rgw: datalog trim can\'t work as expected
    ([issue#20190](http://tracker.ceph.com/issues/20190),
    [pr#16299](https://github.com/ceph/ceph/pull/16299), Zhang Shaowen)
-   rgw: Delete non-empty bucket in slave zonegroup
    ([issue#19313](http://tracker.ceph.com/issues/19313),
    [pr#15477](https://github.com/ceph/ceph/pull/15477), Zhang Shaowen)
-   rgw: Do not decrement stats cache when the cache values are zero
    ([issue#20661](http://tracker.ceph.com/issues/20661),
    [issue#20934](http://tracker.ceph.com/issues/20934),
    [pr#16720](https://github.com/ceph/ceph/pull/16720), Aleksei
    Gutikov, Pavan Rallabhandi)
-   rgw: fix crash caused by shard id out of range when listing data log
    ([issue#19732](http://tracker.ceph.com/issues/19732),
    [pr#15465](https://github.com/ceph/ceph/pull/15465), redickwang)
-   rgw: fix hangs in RGWRealmReloader::reload on SIGHUP
    ([issue#20686](http://tracker.ceph.com/issues/20686),
    [pr#17281](https://github.com/ceph/ceph/pull/17281), fang.yuxiang)
-   rgw: fix infinite loop in rest api for log list
    ([issue#20386](http://tracker.ceph.com/issues/20386),
    [pr#15988](https://github.com/ceph/ceph/pull/15988), xierui, Casey
    Bodley)
-   rgw: fix race in RGWCompleteMultipart
    ([issue#20861](http://tracker.ceph.com/issues/20861),
    [pr#16767](https://github.com/ceph/ceph/pull/16767), Abhishek
    Varshney, Matt Benjamin)
-   rgw: Fix up to 1000 entries at a time in check_bad_index_multipart
    ([issue#20772](http://tracker.ceph.com/issues/20772),
    [pr#16880](https://github.com/ceph/ceph/pull/16880), Orit Wasserman,
    Matt Benjamin)
-   rgw: folders starting with \_ underscore are not in bucket index
    ([issue#19432](http://tracker.ceph.com/issues/19432),
    [pr#16276](https://github.com/ceph/ceph/pull/16276), Giovani
    Rinaldi, Orit Wasserman)
-   rgw: \'gc list \--include-all\' command infinite loop the first 1000
    items ([issue#19978](http://tracker.ceph.com/issues/19978),
    [pr#15719](https://github.com/ceph/ceph/pull/15719), Shasha Lu, fang
    yuxiang)
-   rgw: meta sync thread crash at RGWMetaSyncShardCR
    ([issue#20251](http://tracker.ceph.com/issues/20251),
    [pr#16711](https://github.com/ceph/ceph/pull/16711), fang yuxiang,
    Nathan Cutler)
-   rgw: multipart copy-part remove \'/\' for s3 java sdk request header
    ([issue#20075](http://tracker.ceph.com/issues/20075),
    [pr#16266](https://github.com/ceph/ceph/pull/16266), donglingpeng)
-   rgw: multipart parts on versioned bucket create versioned bucket
    index entries ([issue#19604](http://tracker.ceph.com/issues/19604),
    [issue#17964](http://tracker.ceph.com/issues/17964),
    [pr#17278](https://github.com/ceph/ceph/pull/17278), Zhang Shaowen)
-   rgw: multisite: after CreateBucket is forwarded to master, local
    bucket may use different value for bucket index shards
    ([issue#19745](http://tracker.ceph.com/issues/19745),
    [pr#15450](https://github.com/ceph/ceph/pull/15450), Shasha Lu)
-   rgw: multisite: bucket zonegroup redirect not working
    ([issue#19488](http://tracker.ceph.com/issues/19488),
    [pr#15448](https://github.com/ceph/ceph/pull/15448), Casey Bodley)
-   rgw: multisite: fixes for meta sync across periods
    ([issue#18639](http://tracker.ceph.com/issues/18639),
    [pr#15556](https://github.com/ceph/ceph/pull/15556), Casey Bodley)
-   rgw: multisite: lock is not released when
    RGWMetaSyncShardCR::full_sync() fails to write marker
    ([issue#18077](http://tracker.ceph.com/issues/18077),
    [pr#17155](https://github.com/ceph/ceph/pull/17155), Zhang Shaowen)
-   rgw: multisite: log_meta on secondary zone causes continuous loop of
    metadata sync ([issue#20357](http://tracker.ceph.com/issues/20357),
    [issue#20244](http://tracker.ceph.com/issues/20244),
    [pr#17148](https://github.com/ceph/ceph/pull/17148), Orit Wasserman,
    Casey Bodley)
-   rgw: multisite: memory leak on failed lease in RGWDataSyncShardCR
    ([issue#19861](http://tracker.ceph.com/issues/19861),
    [issue#19834](http://tracker.ceph.com/issues/19834),
    [issue#19446](http://tracker.ceph.com/issues/19446),
    [pr#15457](https://github.com/ceph/ceph/pull/15457), Casey Bodley,
    weiqiaomiao)
-   rgw: multisite: operating bucket\'s acl&cors is not restricted on
    slave zone ([issue#16888](http://tracker.ceph.com/issues/16888),
    [pr#15453](https://github.com/ceph/ceph/pull/15453), Casey Bodley,
    Shasha Lu, Guo Zhandong)
-   rgw: multisite: realm rename does not propagate to other clusters
    ([issue#19746](http://tracker.ceph.com/issues/19746),
    [pr#15454](https://github.com/ceph/ceph/pull/15454), Casey Bodley)
-   rgw: multisite: rest api fails to decode large period on \"period
    commit\" ([issue#19505](http://tracker.ceph.com/issues/19505),
    [pr#15447](https://github.com/ceph/ceph/pull/15447), Casey Bodley)
-   rgw: multisite: RGWPeriodPuller does not call RGWPeriod::reflect()
    on new period ([issue#19816](http://tracker.ceph.com/issues/19816),
    [issue#19817](http://tracker.ceph.com/issues/19817),
    [pr#17167](https://github.com/ceph/ceph/pull/17167), Casey Bodley)
-   rgw: multisite: RGWRadosRemoveOmapKeysCR::request_complete return
    val is wrong ([issue#20539](http://tracker.ceph.com/issues/20539),
    [pr#17156](https://github.com/ceph/ceph/pull/17156), Shasha Lu)
-   rgw: not initialized pointer cause rgw crash with ec data pool
    ([issue#20542](http://tracker.ceph.com/issues/20542),
    [pr#17164](https://github.com/ceph/ceph/pull/17164), Aleksei
    Gutikov, fang yuxiang)
-   rgw: radosgw-admin: bucket rm with \--bypass-gc and without
    \--purge-data doesn\'t throw error message
    ([issue#20688](http://tracker.ceph.com/issues/20688),
    [pr#17159](https://github.com/ceph/ceph/pull/17159), Abhishek
    Varshney)
-   rgw: radosgw-admin data sync run crash
    ([issue#20423](http://tracker.ceph.com/issues/20423),
    [pr#17165](https://github.com/ceph/ceph/pull/17165), Shasha Lu)
-   rgw: radosgw-admin: fix bucket limit check argparse, div(0)
    ([issue#20966](http://tracker.ceph.com/issues/20966),
    [pr#16952](https://github.com/ceph/ceph/pull/16952), Matt Benjamin)
-   rgw: reduce log level of \'storing entry at\' in cls_log
    ([issue#19835](http://tracker.ceph.com/issues/19835),
    [pr#15455](https://github.com/ceph/ceph/pull/15455), Willem Jan
    Withagen)
-   rgw: remove unnecessary \'error in read_id for object name:
    default\' ([issue#19922](http://tracker.ceph.com/issues/19922),
    [pr#15197](https://github.com/ceph/ceph/pull/15197), weiqiaomiao)
-   rgw: replace \'+\' with \"%20\" in canonical query string for s3 v4
    auth ([issue#20501](http://tracker.ceph.com/issues/20501),
    [pr#16951](https://github.com/ceph/ceph/pull/16951), Zhang Shaowen,
    Matt Benjamin)
-   rgw: rgw_common.cc: modify the end check in RGWHTTPArgs::sys_get
    ([issue#16072](http://tracker.ceph.com/issues/16072),
    [pr#16268](https://github.com/ceph/ceph/pull/16268), zhao kun)
-   rgw: rgw_file: cannot delete bucket w/uxattrs
    ([issue#20061](http://tracker.ceph.com/issues/20061),
    [issue#20047](http://tracker.ceph.com/issues/20047),
    [issue#19214](http://tracker.ceph.com/issues/19214),
    [issue#20045](http://tracker.ceph.com/issues/20045),
    [pr#15459](https://github.com/ceph/ceph/pull/15459), Matt Benjamin)
-   rgw: rgw_file: fix size and (c\|m)time unix attrs in write_finish
    ([issue#19653](http://tracker.ceph.com/issues/19653),
    [pr#15449](https://github.com/ceph/ceph/pull/15449), Matt Benjamin)
-   rgw: rgw_file: incorrect lane lock behavior in evict_block()
    ([issue#21141](http://tracker.ceph.com/issues/21141),
    [pr#17597](https://github.com/ceph/ceph/pull/17597), Matt Benjamin)
-   rgw: rgw_file: prevent conflict of mkdir between restarts
    ([issue#20275](http://tracker.ceph.com/issues/20275),
    [pr#17147](https://github.com/ceph/ceph/pull/17147), Gui Hecheng)
-   rgw: rgw_file: v3 write timer does not close open handles
    ([issue#19932](http://tracker.ceph.com/issues/19932),
    [pr#15456](https://github.com/ceph/ceph/pull/15456), Matt Benjamin)
-   rgw: Segmentation fault when exporting rgw bucket in nfs-ganesha
    ([issue#20663](http://tracker.ceph.com/issues/20663),
    [pr#17285](https://github.com/ceph/ceph/pull/17285), Matt Benjamin)
-   rgw: send data-log list infinitely
    ([issue#20951](http://tracker.ceph.com/issues/20951),
    [pr#17287](https://github.com/ceph/ceph/pull/17287), fang.yuxiang)
-   rgw: set latest object\'s acl failed
    ([issue#18649](http://tracker.ceph.com/issues/18649),
    [pr#15451](https://github.com/ceph/ceph/pull/15451), Zhang Shaowen)
-   rgw: Truncated objects
    ([issue#20107](http://tracker.ceph.com/issues/20107),
    [pr#17166](https://github.com/ceph/ceph/pull/17166), Yehuda Sadeh)
-   rgw: uninitialized memory is accessed during creation of bucket\'s
    metadata ([issue#20774](http://tracker.ceph.com/issues/20774),
    [pr#17280](https://github.com/ceph/ceph/pull/17280), Radoslaw
    Zarzynski)
-   rgw: usage logging on tenated buckets causes invalid memory reads
    ([issue#20779](http://tracker.ceph.com/issues/20779),
    [pr#17279](https://github.com/ceph/ceph/pull/17279), Radoslaw
    Zarzynski)
-   rgw: user quota did not work well on multipart upload
    ([issue#19285](http://tracker.ceph.com/issues/19285),
    [issue#19602](http://tracker.ceph.com/issues/19602),
    [pr#17277](https://github.com/ceph/ceph/pull/17277), Zhang Shaowen)
-   rgw: VersionIdMarker and NextVersionIdMarker are not returned when
    listing object versions
    ([issue#19886](http://tracker.ceph.com/issues/19886),
    [pr#16316](https://github.com/ceph/ceph/pull/16316), Zhang Shaowen)
-   rgw: when uploading objects continuously into a versioned bucket,
    some objects will not sync
    ([issue#18208](http://tracker.ceph.com/issues/18208),
    [pr#15452](https://github.com/ceph/ceph/pull/15452), lvshuhua)
-   tools: ceph cli: Rados object in state configuring race
    ([issue#16477](http://tracker.ceph.com/issues/16477),
    [pr#15762](https://github.com/ceph/ceph/pull/15762), Loic Dachary)
-   tools: ceph-disk: dmcrypt cluster must default to ceph
    ([issue#20893](http://tracker.ceph.com/issues/20893),
    [pr#16870](https://github.com/ceph/ceph/pull/16870), Loic Dachary)
-   tools: ceph-disk: don\'t activate suppressed journal devices
    ([issue#19489](http://tracker.ceph.com/issues/19489),
    [pr#16703](https://github.com/ceph/ceph/pull/16703), David
    Disseldorp)
-   tools: ceph-disk: separate ceph-osd \--check-needs-\* logs
    ([issue#19888](http://tracker.ceph.com/issues/19888),
    [pr#15503](https://github.com/ceph/ceph/pull/15503), Loic Dachary)
-   tools: ceph-disk: systemd unit timesout too quickly
    ([issue#20229](http://tracker.ceph.com/issues/20229),
    [pr#17133](https://github.com/ceph/ceph/pull/17133), Loic Dachary)
-   tools: ceph-disk: Use stdin for \'config-key put\' command
    ([issue#21059](http://tracker.ceph.com/issues/21059),
    [pr#17084](https://github.com/ceph/ceph/pull/17084), Brad Hubbard,
    Loic Dachary, Sage Weil)
-   tools: libradosstriper processes arbitrary printf placeholders in
    user input ([issue#20240](http://tracker.ceph.com/issues/20240),
    [pr#17574](https://github.com/ceph/ceph/pull/17574), Stan K)

## v10.2.9 Jewel

This point release fixes a regression introduced in v10.2.8.

We recommend that all Jewel users upgrade.

For more detailed information, see
`the complete changelog <../changelog/v10.2.9.txt>`{.interpreted-text
role="download"}.

### Notable Changes

-   cephfs: Damaged MDS with 10.2.8
    ([issue#20599](http://tracker.ceph.com/issues/20599),
    [pr#16282](https://github.com/ceph/ceph/pull/16282), Nathan Cutler)

## v10.2.8 Jewel

This point release brought a number of important bugfixes in all major
components of Ceph. However, it also introduced a regression that could
cause MDS damage, and a new release, v10.2.9, was published to address
this. Therefore, Jewel users should *not* upgrade to this version -
instead, we recommend upgrading directly to v10.2.9.

For more detailed information, see
`the complete changelog <../changelog/v10.2.8.txt>`{.interpreted-text
role="download"}.

### OSD Removal Caveat

There was a bug introduced in Jewel (#19119) that broke the mapping
behavior when an \"out\" OSD that still existed in the CRUSH map was
removed with \'osd rm\'. This could result in \'misdirected op\' and
other errors. The bug is now fixed, but the fix itself introduces the
same risk because the behavior may vary between clients and OSDs. To
avoid problems, please ensure that all OSDs are removed from the CRUSH
map before deleting them. That is, be sure to do:

    ceph osd crush rm osd.123

before:

    ceph osd rm osd.123

### Snap Trimmer Improvements

This release greatly improves control and throttling of the snap
trimmer. It introduces the \"osd max trimming pgs\" option (defaulting
to 2), which limits how many PGs on an OSD can be trimming snapshots at
a time. And it restores the safe use of the \"osd snap trim sleep\"
option, which defaults to 0 but otherwise adds the given number of
seconds in delay between every dispatch of trim operations to the
underlying system.

### Other Notable Changes

-   build/ops: \"osd marked itself down\" will not recognised if host
    runs mon + osd on shutdown/reboot
    ([issue#18516](http://tracker.ceph.com/issues/18516),
    [pr#13492](https://github.com/ceph/ceph/pull/13492), Boris Ranto)
-   build/ops: ceph-base package missing dependency for psmisc
    ([issue#19129](http://tracker.ceph.com/issues/19129),
    [pr#13786](https://github.com/ceph/ceph/pull/13786), Nathan Cutler)
-   build/ops: enable build of ceph-resource-agents package on rpm-based
    os ([issue#17613](http://tracker.ceph.com/issues/17613),
    [issue#19546](http://tracker.ceph.com/issues/19546),
    [pr#13606](https://github.com/ceph/ceph/pull/13606), Nathan Cutler)
-   build/ops: rbdmap.service not included in debian packaging
    (jewel-only) ([issue#19547](http://tracker.ceph.com/issues/19547),
    [pr#14383](https://github.com/ceph/ceph/pull/14383), Ken Dreyer)
-   cephfs: Journaler may execute on_safe contexts prematurely
    ([issue#20055](http://tracker.ceph.com/issues/20055),
    [pr#15468](https://github.com/ceph/ceph/pull/15468), \"Yan, Zheng\")
-   cephfs: MDS assert failed when shutting down
    ([issue#19204](http://tracker.ceph.com/issues/19204),
    [pr#14683](https://github.com/ceph/ceph/pull/14683), John Spray)
-   cephfs: MDS goes readonly writing backtrace for a file whose data
    pool has been removed
    ([issue#19401](http://tracker.ceph.com/issues/19401),
    [pr#14682](https://github.com/ceph/ceph/pull/14682), John Spray)
-   cephfs: MDS server crashes due to inconsistent metadata
    ([issue#19406](http://tracker.ceph.com/issues/19406),
    [pr#14676](https://github.com/ceph/ceph/pull/14676), John Spray)
-   cephfs: No output for ceph mds rmfailed 0 \--yes-i-really-mean-it
    command ([issue#16709](http://tracker.ceph.com/issues/16709),
    [pr#14674](https://github.com/ceph/ceph/pull/14674), John Spray)
-   cephfs: Test failure: test_data_isolated
    (tasks.cephfs.test_volume_client.TestVolumeClient)
    ([issue#18914](http://tracker.ceph.com/issues/18914),
    [pr#14685](https://github.com/ceph/ceph/pull/14685), \"Yan, Zheng\")
-   cephfs: Test failure: test_open_inode
    ([issue#18661](http://tracker.ceph.com/issues/18661),
    [pr#14669](https://github.com/ceph/ceph/pull/14669), John Spray)
-   cephfs: The mount point break off when mds switch hanppened
    ([issue#19437](http://tracker.ceph.com/issues/19437),
    [pr#14679](https://github.com/ceph/ceph/pull/14679), Guan yunfei)
-   cephfs: ceph-fuse does not recover after lost connection to MDS
    ([issue#16743](http://tracker.ceph.com/issues/16743),
    [issue#18757](http://tracker.ceph.com/issues/18757),
    [pr#14698](https://github.com/ceph/ceph/pull/14698), Kefu Chai,
    Henrik Korkuc, Patrick Donnelly)
-   cephfs: client: fix the cross-quota rename boundary check conditions
    ([issue#18699](http://tracker.ceph.com/issues/18699),
    [pr#14667](https://github.com/ceph/ceph/pull/14667), Greg Farnum)
-   cephfs: mds is crushed, after I set about 400 64KB xattr kv pairs to
    a file ([issue#19033](http://tracker.ceph.com/issues/19033),
    [pr#14684](https://github.com/ceph/ceph/pull/14684), Yang Honggang)
-   cephfs: non-local quota changes not visible until some IO is done
    ([issue#17939](http://tracker.ceph.com/issues/17939),
    [pr#15466](https://github.com/ceph/ceph/pull/15466), John Spray,
    Nathan Cutler)
-   cephfs: normalize file open flags internally used by cephfs
    ([issue#18872](http://tracker.ceph.com/issues/18872),
    [issue#19890](http://tracker.ceph.com/issues/19890),
    [pr#15000](https://github.com/ceph/ceph/pull/15000), Jan Fajerski,
    \"Yan, Zheng\")
-   common: monitor creation with IPv6 public network segfaults
    ([issue#19371](http://tracker.ceph.com/issues/19371),
    [pr#14324](https://github.com/ceph/ceph/pull/14324), Fabian
    Grünbichler)
-   common: radosstriper: protect aio_write API from calls with 0 bytes
    ([issue#14609](http://tracker.ceph.com/issues/14609),
    [pr#13254](https://github.com/ceph/ceph/pull/13254), Sebastien
    Ponce)
-   core: Objecter::epoch_barrier isn\'t respected in \_op_submit()
    ([issue#19396](http://tracker.ceph.com/issues/19396),
    [pr#14332](https://github.com/ceph/ceph/pull/14332), Ilya Dryomov)
-   core: clear divergent_priors set off disk
    ([issue#17916](http://tracker.ceph.com/issues/17916),
    [pr#14596](https://github.com/ceph/ceph/pull/14596), Greg Farnum)
-   core: improve snap trimming, enable restriction of parallelism
    ([issue#19241](http://tracker.ceph.com/issues/19241),
    [pr#14492](https://github.com/ceph/ceph/pull/14492), Samuel Just,
    Greg Farnum)
-   core: os/filestore/HashIndex: be loud about splits
    ([issue#18235](http://tracker.ceph.com/issues/18235),
    [pr#13788](https://github.com/ceph/ceph/pull/13788), Dan van der
    Ster)
-   core: os/filestore: fix clang static check warn use-after-free
    ([issue#19311](http://tracker.ceph.com/issues/19311),
    [pr#14044](https://github.com/ceph/ceph/pull/14044), liuchang0812,
    yaoning)
-   core: transient jerasure unit test failures
    ([issue#18070](http://tracker.ceph.com/issues/18070),
    [issue#17762](http://tracker.ceph.com/issues/17762),
    [issue#18128](http://tracker.ceph.com/issues/18128),
    [issue#17951](http://tracker.ceph.com/issues/17951),
    [pr#14701](https://github.com/ceph/ceph/pull/14701), Kefu Chai, Pan
    Liu, Loic Dachary, Jason Dillaman)
-   core: two instances of omap_digest mismatch
    ([issue#18533](http://tracker.ceph.com/issues/18533),
    [pr#14204](https://github.com/ceph/ceph/pull/14204), Samuel Just,
    David Zafman)
-   doc: Improvements to crushtool manpage
    ([issue#19649](http://tracker.ceph.com/issues/19649),
    [pr#14635](https://github.com/ceph/ceph/pull/14635), Loic Dachary,
    Nathan Cutler)
-   doc: PendingReleaseNotes: note about 19119
    ([issue#19119](http://tracker.ceph.com/issues/19119),
    [pr#13732](https://github.com/ceph/ceph/pull/13732), Sage Weil)
-   doc: admin ops: fix the quota section
    ([issue#19397](http://tracker.ceph.com/issues/19397),
    [pr#14654](https://github.com/ceph/ceph/pull/14654), Chu, Hua-Rong)
-   doc: radosgw-admin: add the \'object stat\' command to usage
    ([issue#19013](http://tracker.ceph.com/issues/19013),
    [pr#13872](https://github.com/ceph/ceph/pull/13872), Pavan
    Rallabhandi)
-   doc: rgw S3 create bucket should not do response in json
    ([issue#18889](http://tracker.ceph.com/issues/18889),
    [pr#13874](https://github.com/ceph/ceph/pull/13874), Abhishek
    Lekshmanan)
-   fs: Invalid error code returned by MDS is causing a kernel client
    WARNING ([issue#19205](http://tracker.ceph.com/issues/19205),
    [pr#13831](https://github.com/ceph/ceph/pull/13831), Jan Fajerski,
    xie xingguo)
-   librbd: Incomplete declaration for ContextWQ in librbd/Journal.h
    ([issue#18862](http://tracker.ceph.com/issues/18862),
    [pr#14152](https://github.com/ceph/ceph/pull/14152), Boris Ranto)
-   librbd: Issues with C API image metadata retrieval functions
    ([issue#19588](http://tracker.ceph.com/issues/19588),
    [pr#14666](https://github.com/ceph/ceph/pull/14666), Mykola Golub)
-   librbd: Possible deadlock performing a synchronous API action while
    refresh in-progress
    ([issue#18419](http://tracker.ceph.com/issues/18419),
    [pr#13154](https://github.com/ceph/ceph/pull/13154), Jason Dillaman)
-   librbd: is_exclusive_lock_owner API should ping OSD
    ([issue#19287](http://tracker.ceph.com/issues/19287),
    [pr#14481](https://github.com/ceph/ceph/pull/14481), Jason Dillaman)
-   librbd: remove image header lock assertions
    ([issue#18244](http://tracker.ceph.com/issues/18244),
    [pr#13809](https://github.com/ceph/ceph/pull/13809), Jason Dillaman)
-   mds: C_MDSInternalNoop::complete doesn\'t free itself
    ([issue#19501](http://tracker.ceph.com/issues/19501),
    [pr#14677](https://github.com/ceph/ceph/pull/14677), \"Yan, Zheng\")
-   mds: Too many stat ops when trying to probe a large file
    ([issue#19955](http://tracker.ceph.com/issues/19955),
    [pr#15472](https://github.com/ceph/ceph/pull/15472), \"Yan, Zheng\")
-   mds: avoid reusing deleted inode in
    StrayManager::\_purge_stray_logged
    ([issue#18877](http://tracker.ceph.com/issues/18877),
    [pr#14670](https://github.com/ceph/ceph/pull/14670), Zhi Zhang)
-   mds: enable start when session ino info is corrupt
    ([issue#19708](http://tracker.ceph.com/issues/19708),
    [issue#16842](http://tracker.ceph.com/issues/16842),
    [pr#14700](https://github.com/ceph/ceph/pull/14700), John Spray)
-   mds: fragment space check can cause replayed request fail
    ([issue#18660](http://tracker.ceph.com/issues/18660),
    [pr#14668](https://github.com/ceph/ceph/pull/14668), \"Yan, Zheng\")
-   mds: heartbeat timeout during rejoin, when working with large amount
    of caps/inodes ([issue#19118](http://tracker.ceph.com/issues/19118),
    [pr#14672](https://github.com/ceph/ceph/pull/14672), John Spray)
-   mds: issue new caps when sending reply to client
    ([issue#19635](http://tracker.ceph.com/issues/19635),
    [pr#15438](https://github.com/ceph/ceph/pull/15438), \"Yan, Zheng\")
-   mon: OSDMonitor: make \'osd crush move \...\' work on osds
    ([issue#18587](http://tracker.ceph.com/issues/18587),
    [pr#13261](https://github.com/ceph/ceph/pull/13261), Sage Weil)
-   mon: fix \'sortbitwise\' warning on jewel
    ([issue#20578](http://tracker.ceph.com/issues/20578),
    [pr#15208](https://github.com/ceph/ceph/pull/15208), huanwen ren,
    Sage Weil)
-   mon: make get_mon_log_message() atomic
    ([issue#19427](http://tracker.ceph.com/issues/19427),
    [pr#14587](https://github.com/ceph/ceph/pull/14587), Kefu Chai)
-   mon: remove bad rocksdb option
    ([issue#19392](http://tracker.ceph.com/issues/19392),
    [pr#14236](https://github.com/ceph/ceph/pull/14236), Sage Weil)
-   msg: IPv6 Heartbeat packets are not marked with DSCP QoS - simple
    messenger ([issue#18887](http://tracker.ceph.com/issues/18887),
    [pr#13450](https://github.com/ceph/ceph/pull/13450), Yan Jun,
    Robin H. Johnson)
-   msg: set close on exec flag
    ([issue#16390](http://tracker.ceph.com/issues/16390),
    [pr#13585](https://github.com/ceph/ceph/pull/13585), Kefu Chai)
-   osd: \--flush-journal: sporadic segfaults on exit
    ([issue#18820](http://tracker.ceph.com/issues/18820),
    [pr#13477](https://github.com/ceph/ceph/pull/13477), Alexey
    Sheplyakov)
-   osd: Give requested scrubs a higher priority
    ([issue#15789](http://tracker.ceph.com/issues/15789),
    [pr#14686](https://github.com/ceph/ceph/pull/14686), David Zafman)
-   osd: Implement asynchronous scrub sleep
    ([issue#19986](http://tracker.ceph.com/issues/19986),
    [issue#19497](http://tracker.ceph.com/issues/19497),
    [pr#15529](https://github.com/ceph/ceph/pull/15529), Brad Hubbard)
-   osd: Object level shard errors are tracked and used if no auth
    available ([issue#20089](http://tracker.ceph.com/issues/20089),
    [pr#15416](https://github.com/ceph/ceph/pull/15416), David Zafman)
-   osd: ReplicatedPG: try with pool\'s use-gmt setting if hitset
    archive not found
    ([issue#19185](http://tracker.ceph.com/issues/19185),
    [pr#13827](https://github.com/ceph/ceph/pull/13827), Kefu Chai)
-   osd: allow client throttler to be adjusted on-fly, without restart
    ([issue#18791](http://tracker.ceph.com/issues/18791),
    [pr#13214](https://github.com/ceph/ceph/pull/13214), Piotr Dałek)
-   osd: bypass readonly ops when osd full
    ([issue#19394](http://tracker.ceph.com/issues/19394),
    [pr#14181](https://github.com/ceph/ceph/pull/14181), Jianpeng Ma,
    yaoning)
-   osd: degraded and misplaced status output inaccurate
    ([issue#18619](http://tracker.ceph.com/issues/18619),
    [pr#14325](https://github.com/ceph/ceph/pull/14325), David Zafman)
-   osd: new added OSD always down when full flag is set
    ([issue#15025](http://tracker.ceph.com/issues/15025),
    [pr#14326](https://github.com/ceph/ceph/pull/14326), Mingxin Liu)
-   osd: pg_pool_t::encode(): be compatible with Hammer \<= 0.94.6
    ([issue#19508](http://tracker.ceph.com/issues/19508),
    [pr#14392](https://github.com/ceph/ceph/pull/14392), Alexey
    Sheplyakov)
-   osd: pre-jewel \"osd rm\" incrementals are misinterpreted
    ([issue#19119](http://tracker.ceph.com/issues/19119),
    [pr#13884](https://github.com/ceph/ceph/pull/13884), Ilya Dryomov)
-   osd: preserve allocation hint attribute during recovery
    ([issue#19083](http://tracker.ceph.com/issues/19083),
    [pr#13647](https://github.com/ceph/ceph/pull/13647), yaoning)
-   osd: promote throttle parameters are reversed
    ([issue#19773](http://tracker.ceph.com/issues/19773),
    [pr#14791](https://github.com/ceph/ceph/pull/14791), Mark Nelson)
-   osd: reindex properly on pg log split
    ([issue#18975](http://tracker.ceph.com/issues/18975),
    [pr#14047](https://github.com/ceph/ceph/pull/14047), Alexey
    Sheplyakov)
-   osd: restrict want_acting to up+acting on recovery completion
    ([issue#18929](http://tracker.ceph.com/issues/18929),
    [pr#13541](https://github.com/ceph/ceph/pull/13541), Sage Weil)
-   rbd-nbd: check /sys/block/nbdX/size to ensure kernel mapped
    correctly ([issue#18335](http://tracker.ceph.com/issues/18335),
    [pr#13932](https://github.com/ceph/ceph/pull/13932), Mykola Golub,
    Alexey Sheplyakov)
-   rbd: \[api\] temporarily restrict (rbd\_)mirror_peer_add from adding
    multiple peers ([issue#19256](http://tracker.ceph.com/issues/19256),
    [pr#14664](https://github.com/ceph/ceph/pull/14664), Jason Dillaman)
-   rbd: qemu crash triggered by network issues
    ([issue#18436](http://tracker.ceph.com/issues/18436),
    [pr#13244](https://github.com/ceph/ceph/pull/13244), Jason Dillaman)
-   rbd: rbd \--pool=x rename y z does not work
    ([issue#18326](http://tracker.ceph.com/issues/18326),
    [pr#14148](https://github.com/ceph/ceph/pull/14148), Gaurav Kumar
    Garg)
-   rbd: systemctl stop rbdmap unmaps all rbds and not just the ones in
    /etc/ceph/rbdmap
    ([issue#18884](http://tracker.ceph.com/issues/18884),
    [issue#18262](http://tracker.ceph.com/issues/18262),
    [pr#14083](https://github.com/ceph/ceph/pull/14083), David
    Disseldorp, Nathan Cutler)
-   rgw: \"cluster \[WRN\] bad locator \@X on object \@X\....\" in
    cluster log ([issue#18980](http://tracker.ceph.com/issues/18980),
    [pr#14064](https://github.com/ceph/ceph/pull/14064), Casey Bodley)
-   rgw: \'radosgw-admin sync status\' on master zone of non-master
    zonegroup ([issue#18091](http://tracker.ceph.com/issues/18091),
    [pr#13779](https://github.com/ceph/ceph/pull/13779), Jing Wenjun)
-   rgw: Change loglevel to 20 for \'System already converted\' message
    ([issue#18919](http://tracker.ceph.com/issues/18919),
    [pr#13834](https://github.com/ceph/ceph/pull/13834), Vikhyat Umrao)
-   rgw: Use decoded URI when verifying TempURL
    ([issue#18590](http://tracker.ceph.com/issues/18590),
    [pr#13724](https://github.com/ceph/ceph/pull/13724), Alexey
    Sheplyakov)
-   rgw: a few cases where rgw_obj is incorrectly initialized
    ([issue#19096](http://tracker.ceph.com/issues/19096),
    [pr#13842](https://github.com/ceph/ceph/pull/13842), Yehuda Sadeh)
-   rgw: add apis to support ragweed suite
    ([issue#19804](http://tracker.ceph.com/issues/19804),
    [pr#14851](https://github.com/ceph/ceph/pull/14851), Yehuda Sadeh)
-   rgw: add bucket size limit check to radosgw-admin
    ([issue#17925](http://tracker.ceph.com/issues/17925),
    [pr#14787](https://github.com/ceph/ceph/pull/14787), Matt Benjamin)
-   rgw: allow system users to read SLO parts
    ([issue#19027](http://tracker.ceph.com/issues/19027),
    [pr#14752](https://github.com/ceph/ceph/pull/14752), Casey Bodley)
-   rgw: don\'t return skew time in pre-signed url
    ([issue#18828](http://tracker.ceph.com/issues/18828),
    [issue#18829](http://tracker.ceph.com/issues/18829),
    [pr#14605](https://github.com/ceph/ceph/pull/14605), liuchang0812)
-   rgw: failure to create s3 type subuser from admin rest api
    ([issue#16682](http://tracker.ceph.com/issues/16682),
    [pr#14815](https://github.com/ceph/ceph/pull/14815), snakeAngel2015)
-   rgw: fix break inside of yield in RGWFetchAllMetaCR
    ([issue#17655](http://tracker.ceph.com/issues/17655),
    [pr#14066](https://github.com/ceph/ceph/pull/14066), Casey Bodley)
-   rgw: fix failed to create bucket if a non-master zonegroup has a
    single zone ([issue#19756](http://tracker.ceph.com/issues/19756),
    [pr#14766](https://github.com/ceph/ceph/pull/14766), weiqiaomiao)
-   rgw: health check errors out incorrectly
    ([issue#19025](http://tracker.ceph.com/issues/19025),
    [pr#13865](https://github.com/ceph/ceph/pull/13865), Pavan
    Rallabhandi)
-   rgw: list_plain_entries() stops before bi_log entries
    ([issue#19876](http://tracker.ceph.com/issues/19876),
    [pr#15383](https://github.com/ceph/ceph/pull/15383), Casey Bodley)
-   rgw: multisite: fetch_remote_obj() gets wrong version when copying
    from remote ([issue#19599](http://tracker.ceph.com/issues/19599),
    [pr#14607](https://github.com/ceph/ceph/pull/14607), Zhang Shaowen,
    Casey Bodley)
-   rgw: multisite: some yields in RGWMetaSyncShardCR::full_sync()
    resume in incremental_sync()
    ([issue#18076](http://tracker.ceph.com/issues/18076),
    [pr#13837](https://github.com/ceph/ceph/pull/13837), Casey Bodley,
    Abhishek Lekshmanan)
-   rgw: only append zonegroups to rest params if not empty
    ([issue#20078](http://tracker.ceph.com/issues/20078),
    [pr#15312](https://github.com/ceph/ceph/pull/15312), Yehuda Sadeh,
    Karol Mroz)
-   rgw: pullup civet chunked
    ([issue#19736](http://tracker.ceph.com/issues/19736),
    [pr#14776](https://github.com/ceph/ceph/pull/14776), Matt Benjamin)
-   rgw: rgw_file: fix event expire check, don\'t expire directories
    being read ([issue#19623](http://tracker.ceph.com/issues/19623),
    [issue#19270](http://tracker.ceph.com/issues/19270),
    [issue#19625](http://tracker.ceph.com/issues/19625),
    [issue#19624](http://tracker.ceph.com/issues/19624),
    [issue#19634](http://tracker.ceph.com/issues/19634),
    [issue#19435](http://tracker.ceph.com/issues/19435),
    [pr#14653](https://github.com/ceph/ceph/pull/14653), Gui Hecheng,
    Matt Benjamin)
-   rgw: swift: disable revocation thread under certain circumstances
    ([issue#19499](http://tracker.ceph.com/issues/19499),
    [issue#9493](http://tracker.ceph.com/issues/9493),
    [pr#14789](https://github.com/ceph/ceph/pull/14789), Marcus Watts)
-   rgw: the swift container acl does not support field .ref
    ([issue#18484](http://tracker.ceph.com/issues/18484),
    [pr#13833](https://github.com/ceph/ceph/pull/13833), Jing Wenjun)
-   rgw: typo in rgw_admin.cc
    ([issue#19026](http://tracker.ceph.com/issues/19026),
    [pr#13863](https://github.com/ceph/ceph/pull/13863), Ronak Jain)
-   rgw: unsafe access in RGWListBucket_ObjStore_SWIFT::send_response()
    ([issue#19249](http://tracker.ceph.com/issues/19249),
    [pr#14661](https://github.com/ceph/ceph/pull/14661), Yehuda Sadeh)
-   rgw: upgrade to multisite v2 fails if there is a zone without zone
    info ([issue#19231](http://tracker.ceph.com/issues/19231),
    [pr#14136](https://github.com/ceph/ceph/pull/14136), Danny Al-Gaaf,
    Orit Wasserman)
-   rgw: use separate http_manager for read_sync_status
    ([issue#19236](http://tracker.ceph.com/issues/19236),
    [pr#14195](https://github.com/ceph/ceph/pull/14195), Casey Bodley,
    Shasha Lu)
-   rgw: when converting region_map we need to use rgw_zone_root_pool
    ([issue#19195](http://tracker.ceph.com/issues/19195),
    [pr#14143](https://github.com/ceph/ceph/pull/14143), Orit Wasserman)
-   rgw: zonegroupmap set does not work
    ([issue#19498](http://tracker.ceph.com/issues/19498),
    [issue#18725](http://tracker.ceph.com/issues/18725),
    [pr#14660](https://github.com/ceph/ceph/pull/14660), Orit Wasserman,
    Casey Bodley)
-   rgw:fix memory leaks in data/md sync
    ([issue#20088](http://tracker.ceph.com/issues/20088),
    [pr#15382](https://github.com/ceph/ceph/pull/15382), weiqiaomiao)
-   tests: \'ceph auth import -i\' overwrites caps, should alert user
    before overwrite
    ([issue#18932](http://tracker.ceph.com/issues/18932),
    [pr#13544](https://github.com/ceph/ceph/pull/13544), Vikhyat Umrao)
-   tests: New upgrade test for #19508
    ([issue#19829](http://tracker.ceph.com/issues/19829),
    [issue#19508](http://tracker.ceph.com/issues/19508),
    [pr#14930](https://github.com/ceph/ceph/pull/14930), Nathan Cutler)
-   tests: \[ FAILED \] TestLibRBD.ImagePollIO in
    upgrade:client-upgrade-kraken-distro-basic-smithi
    ([issue#18617](http://tracker.ceph.com/issues/18617),
    [pr#13107](https://github.com/ceph/ceph/pull/13107), Jason Dillaman)
-   tests: \[librados_test_stub\] cls_cxx_map_get_XYZ methods don\'t
    return correct value
    ([issue#19597](http://tracker.ceph.com/issues/19597),
    [pr#14665](https://github.com/ceph/ceph/pull/14665), Jason Dillaman)
-   tests: additional rbd-mirror test stability improvements
    ([issue#18935](http://tracker.ceph.com/issues/18935),
    [pr#14154](https://github.com/ceph/ceph/pull/14154), Jason Dillaman)
-   tests: api_misc: \[ FAILED \]
    LibRadosMiscConnectFailure.ConnectFailure
    ([issue#15368](http://tracker.ceph.com/issues/15368),
    [pr#14763](https://github.com/ceph/ceph/pull/14763), Sage Weil)
-   tests: buffer overflow in test LibCephFS.DirLs
    ([issue#18941](http://tracker.ceph.com/issues/18941),
    [pr#14671](https://github.com/ceph/ceph/pull/14671), \"Yan, Zheng\")
-   tests: clone workunit using the branch specified by task
    ([issue#19429](http://tracker.ceph.com/issues/19429),
    [pr#14371](https://github.com/ceph/ceph/pull/14371), Kefu Chai, Dan
    Mick)
-   tests: drop upgrade/hammer-jewel-x
    ([issue#20574](http://tracker.ceph.com/issues/20574),
    [pr#15933](https://github.com/ceph/ceph/pull/15933), Nathan Cutler)
-   tests: dummy suite fails in OpenStack
    ([issue#18259](http://tracker.ceph.com/issues/18259),
    [pr#14070](https://github.com/ceph/ceph/pull/14070), Nathan Cutler)
-   tests: eliminate race condition in Thrasher constructor
    ([issue#18799](http://tracker.ceph.com/issues/18799),
    [pr#13608](https://github.com/ceph/ceph/pull/13608), Nathan Cutler)
-   tests: enable quotas for pre-luminous quota tests
    ([issue#20412](http://tracker.ceph.com/issues/20412),
    [pr#15936](https://github.com/ceph/ceph/pull/15936), Patrick
    Donnelly)
-   tests: fix oversight in yaml comment
    ([issue#20581](http://tracker.ceph.com/issues/20581),
    [pr#14449](https://github.com/ceph/ceph/pull/14449), Nathan Cutler)
-   tests: move swift.py task from teuthology to ceph, phase one (jewel)
    ([issue#20392](http://tracker.ceph.com/issues/20392),
    [pr#15870](https://github.com/ceph/ceph/pull/15870), Nathan Cutler,
    Sage Weil, Warren Usui, Greg Farnum, Ali Maredia, Tommi Virtanen,
    Zack Cerza, Sam Lang, Yehuda Sadeh, Joe Buck, Josh Durgin)
-   tests: qa/Fixed upgrade sequence to 10.2.0 -\> 10.2.7 -\> latest -x
    (10.2.8) ([issue#20572](http://tracker.ceph.com/issues/20572),
    [pr#16089](https://github.com/ceph/ceph/pull/16089), Yuri Weinstein)
-   tests: qa/suites/upgrade/hammer-x: set \"sortbitwise\" for jewel
    clusters ([issue#20342](http://tracker.ceph.com/issues/20342),
    [pr#15842](https://github.com/ceph/ceph/pull/15842), Nathan Cutler)
-   tests: qa/workunits/rados/test-upgrade-\*: whitelist tests for
    master (part 1)
    ([issue#20577](http://tracker.ceph.com/issues/20577),
    [pr#15360](https://github.com/ceph/ceph/pull/15360), Sage Weil)
-   tests: qa/workunits/rados/test-upgrade-\*: whitelist tests for
    master (part 2)
    ([issue#20576](http://tracker.ceph.com/issues/20576),
    [pr#15778](https://github.com/ceph/ceph/pull/15778), Kefu Chai)
-   tests: qa/workunits/rados/test-upgrade-\*: whitelist tests the right
    way ([issue#20575](http://tracker.ceph.com/issues/20575),
    [pr#15824](https://github.com/ceph/ceph/pull/15824), Kefu Chai)
-   tests: rados: sleep before ceph tell osd.0 flush_pg_stats after
    restart ([issue#16239](http://tracker.ceph.com/issues/16239),
    [issue#20489](http://tracker.ceph.com/issues/20489),
    [pr#14710](https://github.com/ceph/ceph/pull/14710), Kefu Chai,
    Nathan Cutler)
-   tests: run upgrade/client-upgrade on latest CentOS 7.3
    ([issue#20573](http://tracker.ceph.com/issues/20573),
    [pr#16088](https://github.com/ceph/ceph/pull/16088), Nathan Cutler)
-   tests: run-rbd-unit-tests.sh assert in lockdep_will_lock,
    TestLibRBD.ObjectMapConsistentSnap
    ([issue#17447](http://tracker.ceph.com/issues/17447),
    [pr#14150](https://github.com/ceph/ceph/pull/14150), Jason Dillaman)
-   tests: systemd test backport to jewel
    ([issue#19717](http://tracker.ceph.com/issues/19717),
    [pr#14694](https://github.com/ceph/ceph/pull/14694), Vasu Kulkarni)
-   tests: test/librados/tmap_migrate: g_ceph_context-\>put() upon
    return ([issue#20579](http://tracker.ceph.com/issues/20579),
    [pr#14809](https://github.com/ceph/ceph/pull/14809), Kefu Chai)
-   tests: test_notify.py: rbd.InvalidArgument: error updating features
    for image test_notify_clone2
    ([issue#19692](http://tracker.ceph.com/issues/19692),
    [pr#14680](https://github.com/ceph/ceph/pull/14680), Jason Dillaman)
-   tests: upgrade/hammer-x failing with OSD has the store locked when
    Thrasher runs ceph-objectstore-tool on down PG
    ([issue#19556](http://tracker.ceph.com/issues/19556),
    [pr#14416](https://github.com/ceph/ceph/pull/14416), Nathan Cutler)
-   tests: upgrade:hammer-x/stress-split-erasure-code-x86_64 fails in
    10.2.8 integration testing
    ([issue#20413](http://tracker.ceph.com/issues/20413),
    [pr#15904](https://github.com/ceph/ceph/pull/15904), Nathan Cutler)
-   tools: brag fails to count \"in\" mds
    ([issue#19192](http://tracker.ceph.com/issues/19192),
    [pr#14112](https://github.com/ceph/ceph/pull/14112), Oleh Prypin,
    Peng Zhang)
-   tools: ceph-disk does not support cluster names different than
    \'ceph\' ([issue#17821](http://tracker.ceph.com/issues/17821),
    [pr#14765](https://github.com/ceph/ceph/pull/14765), Loic Dachary)
-   tools: ceph-disk: Racing between partition creation and device node
    creation ([issue#19428](http://tracker.ceph.com/issues/19428),
    [pr#14329](https://github.com/ceph/ceph/pull/14329), Erwan Velu)
-   tools: ceph-disk: bluestore \--setgroup incorrectly set with user
    ([issue#18955](http://tracker.ceph.com/issues/18955),
    [pr#13489](https://github.com/ceph/ceph/pull/13489), craigchi)
-   tools: ceph-disk: ceph-disk list reports mount error for OSD having
    mount options with SELinux context
    ([issue#17331](http://tracker.ceph.com/issues/17331),
    [pr#14402](https://github.com/ceph/ceph/pull/14402), Brad Hubbard)
-   tools: ceph-disk: do not setup_statedir on trigger
    ([issue#19941](http://tracker.ceph.com/issues/19941),
    [pr#15504](https://github.com/ceph/ceph/pull/15504), Loic Dachary)
-   tools: ceph-disk: enable directory backed OSD at boot time
    ([issue#19628](http://tracker.ceph.com/issues/19628),
    [pr#14602](https://github.com/ceph/ceph/pull/14602), Loic Dachary)
-   tools: rados: RadosImport::import should return an error if
    Rados::connect fails
    ([issue#19319](http://tracker.ceph.com/issues/19319),
    [pr#14113](https://github.com/ceph/ceph/pull/14113), Brad Hubbard)

## v10.2.7 Jewel

This point release fixes several important bugs in RBD mirroring, librbd
& RGW.

We recommend that all v10.2.x users upgrade.

For more detailed information, see
`the complete changelog <../changelog/v10.2.7.txt>`{.interpreted-text
role="download"}.

### Notable Changes

-   librbd: possible race in ExclusiveLock handle_peer_notification
    ([issue#19368](http://tracker.ceph.com/issues/19368),
    [pr#14233](https://github.com/ceph/ceph/pull/14233), Mykola Golub)
-   osd: Increase priority for inactive PGs backfill
    ([issue#18350](http://tracker.ceph.com/issues/18350),
    [pr#13232](https://github.com/ceph/ceph/pull/13232), Bartłomiej
    Święcki)
-   osd: Scrub improvements and other fixes
    ([issue#17857](http://tracker.ceph.com/issues/17857),
    [issue#18114](http://tracker.ceph.com/issues/18114),
    [issue#13937](http://tracker.ceph.com/issues/13937),
    [issue#18113](http://tracker.ceph.com/issues/18113),
    [pr#13146](https://github.com/ceph/ceph/pull/13146), Kefu Chai,
    David Zafman)
-   osd: fix OSD network address in OSD heartbeat_check log message
    ([issue#18657](http://tracker.ceph.com/issues/18657),
    [pr#13108](https://github.com/ceph/ceph/pull/13108), Vikhyat Umrao)
-   rbd-mirror: deleting a snapshot during sync can result in read
    errors ([issue#18990](http://tracker.ceph.com/issues/18990),
    [pr#13596](https://github.com/ceph/ceph/pull/13596), Jason Dillaman)
-   rgw: \'period update\' does not remove short_zone_ids of deleted
    zones ([issue#15618](http://tracker.ceph.com/issues/15618),
    [pr#14140](https://github.com/ceph/ceph/pull/14140), Casey Bodley)
-   rgw: DUMPABLE flag is cleared by setuid preventing coredumps
    ([issue#19089](http://tracker.ceph.com/issues/19089),
    [pr#13844](https://github.com/ceph/ceph/pull/13844), Brad Hubbard)
-   rgw: clear data_sync_cr if RGWDataSyncControlCR fails
    ([issue#17569](http://tracker.ceph.com/issues/17569),
    [pr#13886](https://github.com/ceph/ceph/pull/13886), Casey Bodley)
-   rgw: fix openssl
    ([issue#11239](http://tracker.ceph.com/issues/11239),
    [issue#19098](http://tracker.ceph.com/issues/19098),
    [issue#16535](http://tracker.ceph.com/issues/16535),
    [pr#14215](https://github.com/ceph/ceph/pull/14215), Marcus Watts)
-   rgw: fix swift cannot disable object versioning with empty
    X-Versions-Location
    ([issue#18852](http://tracker.ceph.com/issues/18852),
    [pr#13823](https://github.com/ceph/ceph/pull/13823), Jing Wenjun)
-   rgw: librgw: RGWLibFS::setattr fails on directories
    ([issue#18808](http://tracker.ceph.com/issues/18808),
    [pr#13778](https://github.com/ceph/ceph/pull/13778), Matt Benjamin)
-   rgw: make sending Content-Length in 204 and 304 controllable
    ([issue#16602](http://tracker.ceph.com/issues/16602),
    [pr#13503](https://github.com/ceph/ceph/pull/13503), Radoslaw
    Zarzynski, Matt Benjamin)
-   rgw: multipart uploads copy part support
    ([issue#12790](http://tracker.ceph.com/issues/12790),
    [pr#13219](https://github.com/ceph/ceph/pull/13219), Yehuda Sadeh,
    Javier M. Mellid, Matt Benjamin)
-   rgw: multisite: RGWMetaSyncShardControlCR gives up on EIO
    ([issue#19019](http://tracker.ceph.com/issues/19019),
    [pr#13867](https://github.com/ceph/ceph/pull/13867), Casey Bodley)
-   rgw: radosgw/swift: clean up flush / newline behavior
    ([issue#18473](http://tracker.ceph.com/issues/18473),
    [pr#14100](https://github.com/ceph/ceph/pull/14100), Nathan Cutler,
    Marcus Watts, Matt Benjamin)
-   rgw: radosgw/swift: clean up flush / newline behavior.
    ([issue#18473](http://tracker.ceph.com/issues/18473),
    [pr#13143](https://github.com/ceph/ceph/pull/13143), Marcus Watts,
    Matt Benjamin)
-   rgw: rgw_fh: RGWFileHandle dtor must also cond-unlink from FHCache
    ([issue#19112](http://tracker.ceph.com/issues/19112),
    [pr#14231](https://github.com/ceph/ceph/pull/14231), Matt Benjamin)
-   rgw: rgw_file: avoid interning .. in FHCache table and don\'t ref
    for them ([issue#19036](http://tracker.ceph.com/issues/19036),
    [pr#13848](https://github.com/ceph/ceph/pull/13848), Matt Benjamin)
-   rgw: rgw_file: interned RGWFileHandle objects need parent refs
    ([issue#18650](http://tracker.ceph.com/issues/18650),
    [pr#13583](https://github.com/ceph/ceph/pull/13583), Matt Benjamin)
-   rgw: rgw_file: restore (corrected) fix for dir partial match (return
    of FLAG_EXACT_MATCH)
    ([issue#19060](http://tracker.ceph.com/issues/19060),
    [issue#18992](http://tracker.ceph.com/issues/18992),
    [issue#19059](http://tracker.ceph.com/issues/19059),
    [pr#13858](https://github.com/ceph/ceph/pull/13858), Matt Benjamin)
-   rgw: rgw_file: FHCache residence check should be exhaustive
    ([issue#19111](http://tracker.ceph.com/issues/19111),
    [pr#14169](https://github.com/ceph/ceph/pull/14169), Matt Benjamin)
-   rgw: rgw_file: ensure valid_s3_object_name for directories, too
    ([issue#19066](http://tracker.ceph.com/issues/19066),
    [pr#13717](https://github.com/ceph/ceph/pull/13717), Matt Benjamin)
-   rgw: rgw_file: fix marker computation
    ([issue#19018](http://tracker.ceph.com/issues/19018),
    [issue#18989](http://tracker.ceph.com/issues/18989),
    [issue#18992](http://tracker.ceph.com/issues/18992),
    [issue#18991](http://tracker.ceph.com/issues/18991),
    [pr#13869](https://github.com/ceph/ceph/pull/13869), Matt Benjamin)
-   rgw: rgw_file: wip dir orphan
    ([issue#18992](http://tracker.ceph.com/issues/18992),
    [issue#18989](http://tracker.ceph.com/issues/18989),
    [issue#19018](http://tracker.ceph.com/issues/19018),
    [issue#18991](http://tracker.ceph.com/issues/18991),
    [pr#14205](https://github.com/ceph/ceph/pull/14205), Gui Hecheng,
    Matt Benjamin)
-   rgw: rgw_file: various fixes
    ([pr#14206](https://github.com/ceph/ceph/pull/14206), Matt Benjamin)
-   rgw: rgw_file: expand argv
    ([pr#14230](https://github.com/ceph/ceph/pull/14230), Matt Benjamin)

## v10.2.6 Jewel

This point release fixes several important bugs in RBD mirroring, RGW
multi-site, CephFS, and RADOS.

We recommend that all v10.2.x users upgrade.

For more detailed information, see
`the complete changelog <../changelog/v10.2.6.txt>`{.interpreted-text
role="download"}.

### OSDs No Longer Send ENXIO by Default

In previous versions, if a client sent an op to the wrong OSD, the OSD
would reply with ENXIO. The rationale here is that the client or OSD is
clearly buggy and we want to surface the error as clearly as possible.
We now only send the ENXIO reply if the osd_enxio_on_misdirected_op
option is enabled (it\'s off by default). This means that a VM using
librbd that previously would have gotten an EIO and gone read-only will
now see a blocked/hung IO instead.

### Other Notable Changes

-   build/ops: add hostname sanity check to run-{c}make-check.sh
    ([issue#18134](http://tracker.ceph.com/issues/18134),
    [pr#12302](http://github.com/ceph/ceph/pull/12302), Nathan Cutler)

-   build/ops: add ldap lib to rgw lib deps based on build config
    ([issue#17313](http://tracker.ceph.com/issues/17313),
    [pr#13183](http://github.com/ceph/ceph/pull/13183), Nathan Cutler)

-   build/ops: ceph-create-keys loops forever
    ([issue#17753](http://tracker.ceph.com/issues/17753),
    [pr#11884](http://github.com/ceph/ceph/pull/11884), Alfredo Deza)

-   build/ops: ceph daemons DUMPABLE flag is cleared by setuid
    preventing coredumps
    ([issue#17650](http://tracker.ceph.com/issues/17650),
    [pr#11736](http://github.com/ceph/ceph/pull/11736), Patrick
    Donnelly)

-   build/ops: fixed compilation error when \--with-radowsgw=no
    ([issue#18512](http://tracker.ceph.com/issues/18512),
    [pr#12729](http://github.com/ceph/ceph/pull/12729), Pan Liu)

-   build/ops: fixed the issue when \--disable-server, compilation
    fails. ([issue#18120](http://tracker.ceph.com/issues/18120),
    [pr#12239](http://github.com/ceph/ceph/pull/12239), Pan Liu)

-   build/ops: fix undefined crypto references with \--with-xio
    ([issue#18133](http://tracker.ceph.com/issues/18133),
    [pr#12296](http://github.com/ceph/ceph/pull/12296), Nathan Cutler)

-   build/ops: install-deps.sh based on /etc/os-release
    ([issue#18466](http://tracker.ceph.com/issues/18466),
    [issue#18198](http://tracker.ceph.com/issues/18198),
    [pr#12405](http://github.com/ceph/ceph/pull/12405), Jan Fajerski,
    Nitin A Kamble, Nathan Cutler)

-   build/ops: Remove the runtime dependency on lsb_release
    ([issue#17425](http://tracker.ceph.com/issues/17425),
    [pr#11875](http://github.com/ceph/ceph/pull/11875), John Coyle, Brad
    Hubbard)

-   build/ops: rpm: /etc/ceph/rbdmap is packaged with executable access
    rights ([issue#17395](http://tracker.ceph.com/issues/17395),
    [pr#11855](http://github.com/ceph/ceph/pull/11855), Ken Dreyer)

-   build/ops: selinux: Allow ceph to manage tmp files
    ([issue#17436](http://tracker.ceph.com/issues/17436),
    [pr#13048](http://github.com/ceph/ceph/pull/13048), Boris Ranto)

-   build/ops: systemd: Restart Mon after 10s in case of failure
    ([issue#18635](http://tracker.ceph.com/issues/18635),
    [pr#13058](http://github.com/ceph/ceph/pull/13058), Wido den
    Hollander)

-   build/ops: systemd restarts Ceph Mon to quickly after failing to
    start ([issue#18635](http://tracker.ceph.com/issues/18635),
    [pr#13184](http://github.com/ceph/ceph/pull/13184), Wido den
    Hollander)

-   ceph-disk: fix flake8 errors
    ([issue#17898](http://tracker.ceph.com/issues/17898),
    [pr#11976](http://github.com/ceph/ceph/pull/11976), Ken Dreyer)

-   cephfs: fuse client crash when adding a new osd
    ([issue#17270](http://tracker.ceph.com/issues/17270),
    [pr#11860](http://github.com/ceph/ceph/pull/11860), John Spray)

-   cli: ceph-disk: convert none str to str before printing it
    ([issue#18371](http://tracker.ceph.com/issues/18371),
    [pr#13187](http://github.com/ceph/ceph/pull/13187), Kefu Chai)

-   client: Fix lookup of \"/..\" in jewel
    ([issue#18408](http://tracker.ceph.com/issues/18408),
    [pr#12766](http://github.com/ceph/ceph/pull/12766), Jeff Layton)

-   client: fix stale entries in command table
    ([issue#17974](http://tracker.ceph.com/issues/17974),
    [pr#12137](http://github.com/ceph/ceph/pull/12137), John Spray)

-   client: populate metadata during mount
    ([issue#18361](http://tracker.ceph.com/issues/18361),
    [pr#13085](http://github.com/ceph/ceph/pull/13085), John Spray)

-   cli: implement functionality for adding, editing and removing omap
    values with binary keys
    ([issue#18123](http://tracker.ceph.com/issues/18123),
    [pr#12755](http://github.com/ceph/ceph/pull/12755), Jason Dillaman)

-   common: Improve linux dcache hash algorithm
    ([issue#17599](http://tracker.ceph.com/issues/17599),
    [pr#11529](http://github.com/ceph/ceph/pull/11529), Yibo Cai)

-   common: utime.h: fix timezone issue in [round_to]()\* funcs.
    ([issue#14862](http://tracker.ceph.com/issues/14862),
    [pr#11508](http://github.com/ceph/ceph/pull/11508), Zhao Chao)

-   doc: Python Swift client commands in Quick Developer Guide don\'t
    match configuration in vstart.sh
    ([issue#17746](http://tracker.ceph.com/issues/17746),
    [pr#13043](http://github.com/ceph/ceph/pull/13043), Ronak Jain)

-   librbd: allow to open an image without opening parent image
    ([issue#18325](http://tracker.ceph.com/issues/18325),
    [pr#13130](http://github.com/ceph/ceph/pull/13130), Ricardo Dias)

-   librbd: metadata_set API operation should not change global config
    setting ([issue#18465](http://tracker.ceph.com/issues/18465),
    [pr#13168](http://github.com/ceph/ceph/pull/13168), Mykola Golub)

-   librbd: new API method to force break a peer\'s exclusive lock
    ([issue#15632](http://tracker.ceph.com/issues/15632),
    [issue#16773](http://tracker.ceph.com/issues/16773),
    [issue#17188](http://tracker.ceph.com/issues/17188),
    [issue#16988](http://tracker.ceph.com/issues/16988),
    [issue#17210](http://tracker.ceph.com/issues/17210),
    [issue#17251](http://tracker.ceph.com/issues/17251),
    [issue#18429](http://tracker.ceph.com/issues/18429),
    [issue#17227](http://tracker.ceph.com/issues/17227),
    [issue#18327](http://tracker.ceph.com/issues/18327),
    [issue#17015](http://tracker.ceph.com/issues/17015),
    [pr#12890](http://github.com/ceph/ceph/pull/12890), Danny Al-Gaaf,
    Mykola Golub, Jason Dillaman)

-   librbd: properly order concurrent updates to the object map
    ([issue#16176](http://tracker.ceph.com/issues/16176),
    [pr#12909](http://github.com/ceph/ceph/pull/12909), Jason Dillaman)

-   librbd: restore journal access when force disabling mirroring
    ([issue#17588](http://tracker.ceph.com/issues/17588),
    [pr#11916](http://github.com/ceph/ceph/pull/11916), Mykola Golub)

-   mds: Cannot create deep directories when caps contain path=/somepath
    ([issue#17858](http://tracker.ceph.com/issues/17858),
    [pr#12154](http://github.com/ceph/ceph/pull/12154), Patrick
    Donnelly)

-   mds: cephfs metadata pool: deep-scrub error omap_digest != best
    guess omap_digest
    ([issue#17177](http://tracker.ceph.com/issues/17177),
    [pr#12380](http://github.com/ceph/ceph/pull/12380), Yan, Zheng)

-   mds: cephfs test failures (ceph.com/qa is broken, should be
    download.ceph.com/qa)
    ([issue#18574](http://tracker.ceph.com/issues/18574),
    [pr#13023](http://github.com/ceph/ceph/pull/13023), John Spray)

-   mds: ceph-fuse crash during snapshot tests
    ([issue#18460](http://tracker.ceph.com/issues/18460),
    [pr#13120](http://github.com/ceph/ceph/pull/13120), Yan, Zheng)

-   mds: ceph_volume_client: fix recovery from partial auth update
    ([issue#17216](http://tracker.ceph.com/issues/17216),
    [pr#11656](http://github.com/ceph/ceph/pull/11656), Ramana Raja)

-   mds: ceph_volume_client.py : Error: Can\'t handle arrays of
    non-strings ([issue#17800](http://tracker.ceph.com/issues/17800),
    [pr#12325](http://github.com/ceph/ceph/pull/12325), Ramana Raja)

-   mds: Cleanly reject session evict command when in replay
    ([issue#17801](http://tracker.ceph.com/issues/17801),
    [pr#12153](http://github.com/ceph/ceph/pull/12153), Yan, Zheng)

-   mds: client segfault on ceph_rmdir path /
    ([issue#9935](http://tracker.ceph.com/issues/9935),
    [pr#13029](http://github.com/ceph/ceph/pull/13029), Michal Jarzabek)

-   mds: Clients without pool-changing caps shouldn\'t be allowed to
    change pool_namespace
    ([issue#17798](http://tracker.ceph.com/issues/17798),
    [pr#12155](http://github.com/ceph/ceph/pull/12155), John Spray)

-   mds: Decode errors on backtrace will crash MDS
    ([issue#18311](http://tracker.ceph.com/issues/18311),
    [pr#12836](http://github.com/ceph/ceph/pull/12836), Nathan Cutler,
    John Spray)

-   mds: false failing to respond to cache pressure warning
    ([issue#17611](http://tracker.ceph.com/issues/17611),
    [pr#11861](http://github.com/ceph/ceph/pull/11861), Yan, Zheng)

-   mds: finish clientreplay requests before requesting active state
    ([issue#18461](http://tracker.ceph.com/issues/18461),
    [pr#13113](http://github.com/ceph/ceph/pull/13113), Yan, Zheng)

-   mds: fix incorrect assertion in Server::\_dir_is_nonempty()
    ([issue#18578](http://tracker.ceph.com/issues/18578),
    [pr#13459](http://github.com/ceph/ceph/pull/13459), Yan, Zheng)

-   mds: fix MDSMap upgrade decoding
    ([issue#17837](http://tracker.ceph.com/issues/17837),
    [pr#13139](http://github.com/ceph/ceph/pull/13139), John Spray,
    Patrick Donnelly)

-   mds: fix missing ll_get for ll_walk
    ([issue#18086](http://tracker.ceph.com/issues/18086),
    [pr#13125](http://github.com/ceph/ceph/pull/13125), Gui Hecheng)

-   mds: Fix mount root for ceph_mount users and change tarball format
    ([issue#18312](http://tracker.ceph.com/issues/18312),
    [issue#18254](http://tracker.ceph.com/issues/18254),
    [pr#12592](http://github.com/ceph/ceph/pull/12592), Jeff Layton)

-   mds: fix null pointer dereference in Locker::handle_client_caps
    ([issue#18306](http://tracker.ceph.com/issues/18306),
    [pr#13060](http://github.com/ceph/ceph/pull/13060), Yan, Zheng)

-   mds: lookup of /.. in returns -ENOENT
    ([issue#18408](http://tracker.ceph.com/issues/18408),
    [pr#12783](http://github.com/ceph/ceph/pull/12783), Jeff Layton)

-   mds: MDS crashes on missing metadata object
    ([issue#18179](http://tracker.ceph.com/issues/18179),
    [pr#13119](http://github.com/ceph/ceph/pull/13119), Yan, Zheng)

-   mds: mds fails to respawn if executable has changed
    ([issue#17531](http://tracker.ceph.com/issues/17531),
    [pr#11873](http://github.com/ceph/ceph/pull/11873), Patrick
    Donnelly)

-   mds: MDS: false failing to respond to cache pressure warning
    ([issue#17716](http://tracker.ceph.com/issues/17716),
    [pr#11856](http://github.com/ceph/ceph/pull/11856), Yan, Zheng)

-   mds: MDS goes damaged on blacklist (failed to read JournalPointer:
    -108 ((108) Cannot send after transport endpoint shutdown)
    ([issue#17236](http://tracker.ceph.com/issues/17236),
    [pr#11413](http://github.com/ceph/ceph/pull/11413), John Spray)

-   mds: MDS long-time blocked ops. ceph-fuse locks up with getattr of
    file ([issue#17275](http://tracker.ceph.com/issues/17275),
    [pr#11858](http://github.com/ceph/ceph/pull/11858), Yan, Zheng)

-   mds: speed up readdir by skipping unwanted dn
    ([issue#18519](http://tracker.ceph.com/issues/18519),
    [pr#12921](http://github.com/ceph/ceph/pull/12921), Xiaoxi Chen)

-   mds: standby-replay daemons can sometimes miss events
    ([issue#17954](http://tracker.ceph.com/issues/17954),
    [pr#13126](http://github.com/ceph/ceph/pull/13126), John Spray)

-   mon: cache tiering: base pool last_force_resend not respected
    (racing read got wrong version)
    ([issue#18366](http://tracker.ceph.com/issues/18366),
    [pr#13115](http://github.com/ceph/ceph/pull/13115), Sage Weil)

-   mon: ceph osd down detection behaviour
    ([issue#18104](http://tracker.ceph.com/issues/18104),
    [pr#12677](http://github.com/ceph/ceph/pull/12677), xie xingguo)

-   mon: Error EINVAL: removing mon.a at 172.21.15.16:6789/0, there will
    be 1 monitors ([issue#17725](http://tracker.ceph.com/issues/17725),
    [pr#11999](http://github.com/ceph/ceph/pull/11999), Joao Eduardo
    Luis)

-   mon: health does not report pgs stuck in more than one state
    ([issue#17515](http://tracker.ceph.com/issues/17515),
    [pr#11660](http://github.com/ceph/ceph/pull/11660), Sage Weil)

-   mon: monitor assertion failure when deactivating mds in (invalid)
    fscid 0 ([issue#17518](http://tracker.ceph.com/issues/17518),
    [pr#11862](http://github.com/ceph/ceph/pull/11862), Patrick
    Donnelly)

-   mon: monitor cannot start because of FAILED assert(info.state ==
    MDSMap::STATE_STANDBY)
    ([issue#18166](http://tracker.ceph.com/issues/18166),
    [pr#13123](http://github.com/ceph/ceph/pull/13123), John Spray,
    Patrick Donnelly)

-   mon: osd flag health message is misleading
    ([issue#18175](http://tracker.ceph.com/issues/18175),
    [pr#13117](http://github.com/ceph/ceph/pull/13117), Sage Weil)

-   mon: OSDMonitor: clear jewel+ feature bits when talking to Hammer
    OSD ([issue#18582](http://tracker.ceph.com/issues/18582),
    [pr#13131](http://github.com/ceph/ceph/pull/13131), Piotr Dałek)

-   mon: OSDs marked OUT wrongly after monitor failover
    ([issue#17719](http://tracker.ceph.com/issues/17719),
    [pr#11947](http://github.com/ceph/ceph/pull/11947), Dong Wu)

-   mon: peon wrongly delete routed pg stats op before receive pg stats
    ack ([issue#18458](http://tracker.ceph.com/issues/18458),
    [pr#13045](http://github.com/ceph/ceph/pull/13045), Mingxin Liu)

-   mon: send updated monmap to its subscribers
    ([issue#17558](http://tracker.ceph.com/issues/17558),
    [pr#11743](http://github.com/ceph/ceph/pull/11743), Kefu Chai)

-   msgr: don\'t truncate message sequence to 32-bits
    ([issue#16122](http://tracker.ceph.com/issues/16122),
    [pr#12416](http://github.com/ceph/ceph/pull/12416), Yan, Zheng)

-   msgr: msg/simple: clear_pipe when wait() is mopping up pipes
    ([issue#15784](http://tracker.ceph.com/issues/15784),
    [pr#13062](http://github.com/ceph/ceph/pull/13062), Sage Weil)

-   msgr: msg/simple/Pipe: error decoding addr
    ([issue#18072](http://tracker.ceph.com/issues/18072),
    [pr#12291](http://github.com/ceph/ceph/pull/12291), Sage Weil)

-   osd: Add config option to disable new scrubs during recovery
    ([issue#17866](http://tracker.ceph.com/issues/17866),
    [pr#11944](http://github.com/ceph/ceph/pull/11944), Wido den
    Hollander)

-   osd: collection_list shadow return value \#
    ([issue#17713](http://tracker.ceph.com/issues/17713),
    [pr#11737](http://github.com/ceph/ceph/pull/11737), Haomai Wang)

-   osd: do not send ENXIO on misdirected op by default
    ([issue#18751](http://tracker.ceph.com/issues/18751),
    [pr#13255](http://github.com/ceph/ceph/pull/13255), Sage Weil)

-   osd: FileStore: fiemap cannot be totally retrieved in xfs when the
    number of extents \> 1364
    ([issue#17610](http://tracker.ceph.com/issues/17610),
    [pr#11998](http://github.com/ceph/ceph/pull/11998), Kefu Chai, Ning
    Yao)

-   osd: leveldb corruption leads to Operation not permitted not handled
    and assert ([issue#18037](http://tracker.ceph.com/issues/18037),
    [pr#12789](http://github.com/ceph/ceph/pull/12789), Nathan Cutler)

-   osd: limit omap data in push op
    ([issue#16128](http://tracker.ceph.com/issues/16128),
    [pr#11991](http://github.com/ceph/ceph/pull/11991), Wanlong Gao)

-   osd: osd crashes when radosgw-admin bi list \--max-entries=1 command
    runing ([issue#17745](http://tracker.ceph.com/issues/17745),
    [pr#11758](http://github.com/ceph/ceph/pull/11758), weiqiaomiao)

-   osd: osd_max_backfills default has changed, documentation should
    reflect that. ([issue#17701](http://tracker.ceph.com/issues/17701),
    [pr#11735](http://github.com/ceph/ceph/pull/11735), huangjun)

-   osd: OSDMonitor: only reject MOSDBoot based on up_from if inst
    matches ([issue#17899](http://tracker.ceph.com/issues/17899),
    [pr#12868](http://github.com/ceph/ceph/pull/12868), Samuel Just)

-   osd: osd/PG: publish PG stats when backfill-related states change
    ([issue#18369](http://tracker.ceph.com/issues/18369),
    [pr#12875](http://github.com/ceph/ceph/pull/12875), Alexey
    Sheplyakov, Sage Weil)

-   osd: Remove extra call to reg_next_scrub() during splits
    ([issue#16474](http://tracker.ceph.com/issues/16474),
    [pr#11606](http://github.com/ceph/ceph/pull/11606), David Zafman)

-   osd: Revert \"Merge pull request #12978 from
    asheplyakov/jewel-18581\"
    ([issue#18809](http://tracker.ceph.com/issues/18809),
    [pr#13280](http://github.com/ceph/ceph/pull/13280), Samuel Just)

-   osd: update_log_missing does not order correctly with osd_ops
    ([issue#17789](http://tracker.ceph.com/issues/17789),
    [pr#11997](http://github.com/ceph/ceph/pull/11997), Samuel Just)

-   qa/tasks: backport rbd_fio fixes to jewel
    ([issue#13512](http://tracker.ceph.com/issues/13512),
    [pr#13104](http://github.com/ceph/ceph/pull/13104), Ilya Dryomov)

-   qa/tasks/workunits: backport misc fixes to jewel
    ([issue#18336](http://tracker.ceph.com/issues/18336),
    [pr#12912](http://github.com/ceph/ceph/pull/12912), Sage Weil)

-   rados: crash adding snap to purged_snaps in
    ReplicatedPG::WaitingOnReplicas (part 2)
    ([issue#15943](http://tracker.ceph.com/issues/15943),
    [issue#18504](http://tracker.ceph.com/issues/18504),
    [pr#12791](http://github.com/ceph/ceph/pull/12791), Samuel Just)

-   rados: Memory leaks in object_list_begin and object_list_end
    ([issue#18252](http://tracker.ceph.com/issues/18252),
    [pr#13118](http://github.com/ceph/ceph/pull/13118), Brad Hubbard)

-   rados: The request lock RPC message might be incorrectly ignored
    ([issue#17030](http://tracker.ceph.com/issues/17030),
    [pr#10865](http://github.com/ceph/ceph/pull/10865), Jason Dillaman)

-   rbd: add image id block name prefix APIs
    ([issue#18270](http://tracker.ceph.com/issues/18270),
    [pr#12529](http://github.com/ceph/ceph/pull/12529), Jason Dillaman)

-   rbd: add max_part and nbds_max options in rbd nbd map, in order to
    keep consistent with
    ([issue#18186](http://tracker.ceph.com/issues/18186),
    [pr#12426](http://github.com/ceph/ceph/pull/12426), Pan Liu)

-   rbd: Attempting to remove an image w/ incompatible features results
    in partial removal
    ([issue#18315](http://tracker.ceph.com/issues/18315),
    [pr#13156](http://github.com/ceph/ceph/pull/13156), Dongsheng Yang)

-   rbd: bench-write will crash if \--io-size is 4G
    ([issue#18422](http://tracker.ceph.com/issues/18422),
    [pr#13129](http://github.com/ceph/ceph/pull/13129), Gaurav Kumar
    Garg)

-   rbd: diff calculate can hide parent extents when examining first
    snapshot in clone
    ([issue#18068](http://tracker.ceph.com/issues/18068),
    [pr#12322](http://github.com/ceph/ceph/pull/12322), Jason Dillaman)

-   rbd: Exclusive lock improperly initialized on read-only image when
    using snap_set API
    ([issue#17618](http://tracker.ceph.com/issues/17618),
    [pr#11852](http://github.com/ceph/ceph/pull/11852), Jason Dillaman)

-   rbd: FAILED assert(m_processing == 0) while running
    test_lock_fence.sh
    ([issue#17973](http://tracker.ceph.com/issues/17973),
    [pr#12323](http://github.com/ceph/ceph/pull/12323), Venky Shankar)

-   rbd: Improve error reporting from rbd feature enable/disable
    ([issue#16985](http://tracker.ceph.com/issues/16985),
    [pr#13157](http://github.com/ceph/ceph/pull/13157), Gaurav Kumar
    Garg)

-   rbd: JournalMetadata flooding with errors when being blacklisted
    ([issue#18243](http://tracker.ceph.com/issues/18243),
    [pr#12739](http://github.com/ceph/ceph/pull/12739), Jason Dillaman)

-   rbd: librbd: use proper snapshot when computing diff parent overlap
    ([issue#18200](http://tracker.ceph.com/issues/18200),
    [pr#12649](http://github.com/ceph/ceph/pull/12649), Xiaoxi Chen)

-   rbd: partition func should be enabled When load nbd.ko for rbd-nbd
    ([issue#18115](http://tracker.ceph.com/issues/18115),
    [pr#12754](http://github.com/ceph/ceph/pull/12754), Pan Liu)

-   rbd: Potential race when removing two-way mirroring image
    ([issue#18447](http://tracker.ceph.com/issues/18447),
    [pr#13233](http://github.com/ceph/ceph/pull/13233), Mykola Golub)

-   rbd: \[qa\] crash in journal-enabled fsx run
    ([issue#18618](http://tracker.ceph.com/issues/18618),
    [pr#13128](http://github.com/ceph/ceph/pull/13128), Jason Dillaman)

-   rbd: \'rbd du\' of missing image does not return error
    ([issue#16987](http://tracker.ceph.com/issues/16987),
    [pr#11854](http://github.com/ceph/ceph/pull/11854), Dongsheng Yang)

-   rbd: rbd-mirror: gmock warnings in bootstrap request unit tests
    ([issue#18048](http://tracker.ceph.com/issues/18048),
    [issue#18012](http://tracker.ceph.com/issues/18012),
    [issue#18156](http://tracker.ceph.com/issues/18156),
    [issue#16991](http://tracker.ceph.com/issues/16991),
    [issue#18051](http://tracker.ceph.com/issues/18051),
    [pr#12425](http://github.com/ceph/ceph/pull/12425), Mykola Golub)

-   rbd: rbd-mirror: image sync object map reload logs message
    ([issue#16179](http://tracker.ceph.com/issues/16179),
    [pr#12753](http://github.com/ceph/ceph/pull/12753), runsisi)

-   rbd: rbd-mirror: snap protect of non-layered image results in
    split-brain ([issue#16962](http://tracker.ceph.com/issues/16962),
    [pr#11869](http://github.com/ceph/ceph/pull/11869), Mykola Golub)

-   rbd: \[rbd-mirror\] sporadic image replayer shut down failure
    ([issue#18441](http://tracker.ceph.com/issues/18441),
    [pr#13155](http://github.com/ceph/ceph/pull/13155), Jason Dillaman)

-   rbd: rbd-nbd: disallow mapping images \>2TB in size
    ([issue#17219](http://tracker.ceph.com/issues/17219),
    [pr#11870](http://github.com/ceph/ceph/pull/11870), Mykola Golub)

-   rbd: rbd-nbd: invalid error code for \"failed to read nbd request\"
    messages ([issue#18242](http://tracker.ceph.com/issues/18242),
    [pr#12756](http://github.com/ceph/ceph/pull/12756), Mykola Golub)

-   rbd: status json format has duplicated/overwritten key
    ([issue#18261](http://tracker.ceph.com/issues/18261),
    [pr#12741](http://github.com/ceph/ceph/pull/12741), Mykola Golub)

-   rbd: TestLibRBD.DiscardAfterWrite doesn\'t handle
    rbd_skip_partial_discard = true
    ([issue#17750](http://tracker.ceph.com/issues/17750),
    [pr#11853](http://github.com/ceph/ceph/pull/11853), Jason Dillaman)

-   rbd: truncate can cause unflushed snapshot data lose
    ([issue#17193](http://tracker.ceph.com/issues/17193),
    [pr#12324](http://github.com/ceph/ceph/pull/12324), Yan, Zheng)

-   

    ReplicatedBackend

    :   take read locks for clone sources during recovery
        ([issue#17831](http://tracker.ceph.com/issues/17831),
        [issue#18583](http://tracker.ceph.com/issues/18583),
        [pr#12978](http://github.com/ceph/ceph/pull/12978), Samuel Just)

-   rgw: add option to log custom HTTP headers (rgw_log_http_headers)
    ([issue#18891](http://tracker.ceph.com/issues/18891),
    [pr#12490](http://github.com/ceph/ceph/pull/12490), Matt Benjamin)

-   rgw: add suport for Swift-at-root dependent features of Swift API
    ([issue#18526](http://tracker.ceph.com/issues/18526),
    [issue#16673](http://tracker.ceph.com/issues/16673),
    [pr#11497](http://github.com/ceph/ceph/pull/11497), Pritha
    Srivastava, Radoslaw Zarzynski, Pete Zaitcev, Abhishek Lekshmanan)

-   rgw: add support for the prefix parameter in account listing of
    Swift API ([issue#17931](http://tracker.ceph.com/issues/17931),
    [pr#12258](http://github.com/ceph/ceph/pull/12258), Radoslaw
    Zarzynski)

-   rgw: Add workaround for upgrade issues for older jewel versions
    ([issue#17820](http://tracker.ceph.com/issues/17820),
    [pr#12316](http://github.com/ceph/ceph/pull/12316), Orit Wasserman)

-   rgw: be aware abount tenants on cls_user_bucket -\> rgw_bucket
    conversion ([issue#18364](http://tracker.ceph.com/issues/18364),
    [issue#16355](http://tracker.ceph.com/issues/16355),
    [pr#13276](http://github.com/ceph/ceph/pull/13276), Radoslaw
    Zarzynski)

-   rgw: bucket check remove \_[multipart]() prefix
    ([issue#13724](http://tracker.ceph.com/issues/13724),
    [pr#11470](http://github.com/ceph/ceph/pull/11470), Weijun Duan)

-   rgw: bucket resharding
    ([issue#17549](http://tracker.ceph.com/issues/17549),
    [issue#17550](http://tracker.ceph.com/issues/17550),
    [pr#13341](http://github.com/ceph/ceph/pull/13341), Yehuda Sadeh,
    Robin H. Johnson)

-   rgw: disable virtual hosting of buckets when no hostnames are
    configured ([issue#17440](http://tracker.ceph.com/issues/17440),
    [issue#15975](http://tracker.ceph.com/issues/15975),
    [issue#17136](http://tracker.ceph.com/issues/17136),
    [pr#11760](http://github.com/ceph/ceph/pull/11760), Casey Bodley,
    Robin H. Johnson)

-   rgw: do not abort when accept a CORS request with short origin
    ([issue#18187](http://tracker.ceph.com/issues/18187),
    [pr#12397](http://github.com/ceph/ceph/pull/12397), LiuYang)

-   rgw: don\'t store empty chains in gc
    ([issue#17897](http://tracker.ceph.com/issues/17897),
    [pr#12174](http://github.com/ceph/ceph/pull/12174), Yehuda Sadeh)

-   rgw:fix for deleting objects name beginning and ending with
    underscores of one bucket using POST method of js sdk.
    ([issue#17888](http://tracker.ceph.com/issues/17888),
    [pr#12320](http://github.com/ceph/ceph/pull/12320), Casey Bodley)

-   rgw: fix period update crash
    ([issue#18631](http://tracker.ceph.com/issues/18631),
    [pr#13273](http://github.com/ceph/ceph/pull/13273), Orit Wasserman)

-   rgw: fix put_acls for objects starting and ending with underscore
    ([issue#17625](http://tracker.ceph.com/issues/17625),
    [pr#11675](http://github.com/ceph/ceph/pull/11675), Orit Wasserman)

-   rgw: fix use of marker in List::list_objects()
    ([issue#18331](http://tracker.ceph.com/issues/18331),
    [pr#13358](http://github.com/ceph/ceph/pull/13358), Yehuda Sadeh)

-   rgw: for the create_bucket api, if the input creation_time is zero,
    we ... ([issue#16597](http://tracker.ceph.com/issues/16597),
    [pr#11990](http://github.com/ceph/ceph/pull/11990), weiqiaomiao)

-   rgw: Have a flavor of bucket deletion in radosgw-admin to bypass
    garbage collection
    ([issue#15557](http://tracker.ceph.com/issues/15557),
    [pr#10661](http://github.com/ceph/ceph/pull/10661), Pavan
    Rallabhandi)

-   rgw: json encode/decode of RGWBucketInfo missing index_type field
    ([issue#17755](http://tracker.ceph.com/issues/17755),
    [pr#11759](http://github.com/ceph/ceph/pull/11759), Yehuda Sadeh)

-   rgw: ldap: enforce simple_bind w/LDAPv3 redux
    ([issue#18339](http://tracker.ceph.com/issues/18339),
    [pr#12678](http://github.com/ceph/ceph/pull/12678), Weibing Zhang)

-   rgw: leak from RGWMetaSyncShardCR::incremental_sync
    ([issue#18412](http://tracker.ceph.com/issues/18412),
    [issue#18300](http://tracker.ceph.com/issues/18300),
    [pr#13004](http://github.com/ceph/ceph/pull/13004), Casey Bodley,
    Sage Weil)

-   rgw: leak in RGWFetchAllMetaCR
    ([issue#17812](http://tracker.ceph.com/issues/17812),
    [pr#11872](http://github.com/ceph/ceph/pull/11872), Casey Bodley)

-   rgw: librgw: objects created from s3 apis are not visible from nfs
    mount point ([issue#18651](http://tracker.ceph.com/issues/18651),
    [pr#13177](http://github.com/ceph/ceph/pull/13177), Matt Benjamin)

-   rgw: log name instead of id for SystemMetaObj on failure
    ([issue#15776](http://tracker.ceph.com/issues/15776),
    [pr#12622](http://github.com/ceph/ceph/pull/12622), Wido den
    Hollander, Abhishek Lekshmanan)

-   rgw: multimds: mds entering up:replay and processing down mds aborts
    ([issue#17670](http://tracker.ceph.com/issues/17670),
    [pr#11857](http://github.com/ceph/ceph/pull/11857), Patrick
    Donnelly)

-   rgw: multipart upload copy
    ([issue#12790](http://tracker.ceph.com/issues/12790),
    [pr#13068](http://github.com/ceph/ceph/pull/13068), Yehuda Sadeh,
    Javier M. Mellid, Matt Benjamin)

-   rgw: multisite: after finishing full sync on a bucket, incremental
    sync starts over from the beginning
    ([issue#17661](http://tracker.ceph.com/issues/17661),
    [issue#17624](http://tracker.ceph.com/issues/17624),
    [pr#11864](http://github.com/ceph/ceph/pull/11864), Zengran Zhang,
    Casey Bodley)

-   rgw: multisite: assert(next) failed in RGWMetaSyncCR
    ([issue#17044](http://tracker.ceph.com/issues/17044),
    [pr#11477](http://github.com/ceph/ceph/pull/11477), Casey Bodley)

-   rgw: multisite: coroutine deadlock assertion on error in
    FetchAllMetaCR ([issue#17571](http://tracker.ceph.com/issues/17571),
    [pr#11866](http://github.com/ceph/ceph/pull/11866), Casey Bodley)

-   rgw: multisite: coroutine deadlock in RGWMetaSyncCR after ECANCELED
    errors ([issue#17465](http://tracker.ceph.com/issues/17465),
    [pr#12738](http://github.com/ceph/ceph/pull/12738), Casey Bodley)

-   rgw: multisite doesn\'t retry RGWFetchAllMetaCR on failed lease
    ([issue#17047](http://tracker.ceph.com/issues/17047),
    [pr#11476](http://github.com/ceph/ceph/pull/11476), Casey Bodley)

-   rgw: multisite: ECANCELED & 500 error on bucket delete
    ([issue#17698](http://tracker.ceph.com/issues/17698),
    [pr#12044](http://github.com/ceph/ceph/pull/12044), Casey Bodley)

-   rgw: multisite: failed assertion in \'radosgw-admin bucket sync
    status\' ([issue#18083](http://tracker.ceph.com/issues/18083),
    [pr#12314](http://github.com/ceph/ceph/pull/12314), Casey Bodley)

-   rgw: multisite: fix ref counting of completions
    ([issue#17792](http://tracker.ceph.com/issues/17792),
    [issue#18414](http://tracker.ceph.com/issues/18414),
    [issue#17793](http://tracker.ceph.com/issues/17793),
    [issue#18407](http://tracker.ceph.com/issues/18407),
    [pr#13001](http://github.com/ceph/ceph/pull/13001), Casey Bodley)

-   rgw: multisite: metadata master can get the wrong value for
    \'oldest_log_period\'
    ([issue#16894](http://tracker.ceph.com/issues/16894),
    [pr#11868](http://github.com/ceph/ceph/pull/11868), Casey Bodley)

-   rgw: multisite: obsolete \'radosgw-admin period prepare\' command
    ([issue#17387](http://tracker.ceph.com/issues/17387),
    [pr#11574](http://github.com/ceph/ceph/pull/11574), Gaurav Kumar
    Garg)

-   rgw: multisite: race between ReadSyncStatus and InitSyncStatus leads
    to EIO errors ([issue#17568](http://tracker.ceph.com/issues/17568),
    [pr#11865](http://github.com/ceph/ceph/pull/11865), Casey Bodley)

-   rgw: multisite requests failing with \'400 Bad Request\' with
    civetweb 1.8 ([issue#17822](http://tracker.ceph.com/issues/17822),
    [pr#12313](http://github.com/ceph/ceph/pull/12313), Casey Bodley)

-   rgw: multisite: segfault after changing value of
    rgw_data_log_num_shards
    ([issue#18488](http://tracker.ceph.com/issues/18488),
    [pr#13180](http://github.com/ceph/ceph/pull/13180), Casey Bodley)

-   rgw: multisite: sync status reports master is on a different period
    ([issue#18064](http://tracker.ceph.com/issues/18064),
    [pr#13175](http://github.com/ceph/ceph/pull/13175), Abhishek
    Lekshmanan)

-   rgw: multisite upgrade from hammer -\> jewel ignores
    rgw_region_root_pool
    ([issue#17963](http://tracker.ceph.com/issues/17963),
    [pr#12156](http://github.com/ceph/ceph/pull/12156), Casey Bodley)

-   rgw: radosgw-admin period update reverts deleted zonegroup
    ([issue#17239](http://tracker.ceph.com/issues/17239),
    [pr#13171](http://github.com/ceph/ceph/pull/13171), Orit Wasserman)

-   rgw: Realm set does not create a new period
    ([issue#18333](http://tracker.ceph.com/issues/18333),
    [pr#13182](http://github.com/ceph/ceph/pull/13182), Orit Wasserman)

-   rgw: remove spurious mount entries for RGW buckets
    ([issue#17850](http://tracker.ceph.com/issues/17850),
    [pr#12045](http://github.com/ceph/ceph/pull/12045), Matt Benjamin)

-   rgw: Replacing \'+\' with \"%20\" in canonical uri for s3 v4 auth.
    ([issue#17076](http://tracker.ceph.com/issues/17076),
    [pr#12542](http://github.com/ceph/ceph/pull/12542), Pritha
    Srivastava)

-   rgw: rgw-admin: missing command to modify placement targets
    ([issue#18078](http://tracker.ceph.com/issues/18078),
    [pr#12428](http://github.com/ceph/ceph/pull/12428), Yehuda Sadeh,
    Casey Bodley)

-   rgw: RGWRados::get_system_obj() sends unnecessary stat request
    before read ([issue#17580](http://tracker.ceph.com/issues/17580),
    [pr#11867](http://github.com/ceph/ceph/pull/11867), Casey Bodley)

-   rgw: rgw_rest_s3: apply missed base64 try-catch
    ([issue#17663](http://tracker.ceph.com/issues/17663),
    [pr#11672](http://github.com/ceph/ceph/pull/11672), Matt Benjamin)

-   rgw: RGW will not list Argonaut-era bucket via HTTP (but
    radosgw-admin works)
    ([issue#17372](http://tracker.ceph.com/issues/17372),
    [pr#11863](http://github.com/ceph/ceph/pull/11863), Yehuda Sadeh)

-   rgw: sends omap_getvals with (u64)-1 limit
    ([issue#17985](http://tracker.ceph.com/issues/17985),
    [pr#12419](http://github.com/ceph/ceph/pull/12419), Yehuda Sadeh,
    Sage Weil)

-   rgw: slave zonegroup cannot enable the bucket versioning
    ([issue#18003](http://tracker.ceph.com/issues/18003),
    [pr#13173](http://github.com/ceph/ceph/pull/13173), Orit Wasserman)

-   rgw: TempURL properly handles accounts created with the implicit
    tenant ([issue#17961](http://tracker.ceph.com/issues/17961),
    [pr#12079](http://github.com/ceph/ceph/pull/12079), Radoslaw
    Zarzynski)

-   rgw: the value of total_time is wrong in the result of
    \'radosgw-admin log show\' opt
    ([issue#17598](http://tracker.ceph.com/issues/17598),
    [pr#11876](http://github.com/ceph/ceph/pull/11876), weiqiaomiao)

-   rgw: Unable to commit period zonegroup change
    ([issue#17364](http://tracker.ceph.com/issues/17364),
    [pr#12315](http://github.com/ceph/ceph/pull/12315), Orit Wasserman)

-   rgw: valgrind \"invalid read size 4\" RGWGetObj
    ([issue#18071](http://tracker.ceph.com/issues/18071),
    [pr#12997](http://github.com/ceph/ceph/pull/12997), Matt Benjamin)

-   rgw: work around curl_multi_wait bug with non-blocking reads
    ([issue#15915](http://tracker.ceph.com/issues/15915),
    [issue#16368](http://tracker.ceph.com/issues/16368),
    [issue#16695](http://tracker.ceph.com/issues/16695),
    [pr#11627](http://github.com/ceph/ceph/pull/11627), John Coyle,
    Casey Bodley)

-   tests: add require_jewel_osds before upgrading last hammer node
    ([issue#18719](http://tracker.ceph.com/issues/18719),
    [pr#13161](http://github.com/ceph/ceph/pull/13161), Nathan Cutler)

-   tests: add require_jewel_osds to upgrade/hammer-x/tiering
    ([issue#18920](http://tracker.ceph.com/issues/18920),
    [pr#13404](http://github.com/ceph/ceph/pull/13404), Nathan Cutler)

-   tests: assertion failure in a radosgw-admin related task
    ([issue#17167](http://tracker.ceph.com/issues/17167),
    [pr#12764](http://github.com/ceph/ceph/pull/12764), Orit Wasserman)

-   tests: Cannot reserve CentOS 7.2 smithi machines
    ([issue#18416](http://tracker.ceph.com/issues/18416),
    [issue#18401](http://tracker.ceph.com/issues/18401),
    [pr#13050](http://github.com/ceph/ceph/pull/13050), Nathan Cutler,
    Sage Weil, Yuri Weinstein)

-   tests: ignore bogus ceph-objectstore-tool error in ceph_manager
    ([issue#16263](http://tracker.ceph.com/issues/16263),
    [pr#13240](http://github.com/ceph/ceph/pull/13240), Nathan Cutler,
    Kefu Chai)

-   tests: objecter_requests workunit fails on wip branches
    ([issue#18393](http://tracker.ceph.com/issues/18393),
    [pr#12761](http://github.com/ceph/ceph/pull/12761), Sage Weil)

-   tests: qa/suites/upgrade/hammer-x: break stress split ec symlinks
    ([issue#19006](http://tracker.ceph.com/issues/19006),
    [pr#13533](http://github.com/ceph/ceph/pull/13533), Nathan Cutler)

-   tests: qa/suites/upgrade/hammer-x/stress-split: finish thrashing
    before final upgrade
    ([issue#19004](http://tracker.ceph.com/issues/19004),
    [pr#13222](http://github.com/ceph/ceph/pull/13222), Sage Weil)

-   tests: qa/tasks/ceph_deploy.py: use dev option
    ([issue#18736](http://tracker.ceph.com/issues/18736),
    [pr#13106](http://github.com/ceph/ceph/pull/13106), Vasu Kulkarni)

-   tests: qa/workunits/rbd: use more recent qemu-iotests that support
    Xenial ([issue#18149](http://tracker.ceph.com/issues/18149),
    [issue#10773](http://tracker.ceph.com/issues/10773),
    [pr#13103](http://github.com/ceph/ceph/pull/13103), Jason Dillaman)

-   tests: remove qa/suites/buildpackages
    ([issue#18846](http://tracker.ceph.com/issues/18846),
    [pr#13299](http://github.com/ceph/ceph/pull/13299), Loic Dachary)

-   tests: SUSE yaml facets in qa/distros/all are out of date
    ([issue#18856](http://tracker.ceph.com/issues/18856),
    [issue#18846](http://tracker.ceph.com/issues/18846),
    [pr#13331](http://github.com/ceph/ceph/pull/13331), Nathan Cutler)

-   tests: update rbd/singleton/all/formatted-output.yaml to support
    ceph-ci ([issue#18440](http://tracker.ceph.com/issues/18440),
    [pr#12822](http://github.com/ceph/ceph/pull/12822), Nathan Cutler,
    Venky Shankar)

-   tests: update Ubuntu image url after ceph.com refactor
    ([issue#18542](http://tracker.ceph.com/issues/18542),
    [pr#12959](http://github.com/ceph/ceph/pull/12959), Jason Dillaman)

-   tests: upgrade:hammer-x: install firefly only on Ubuntu 14.04
    ([issue#18089](http://tracker.ceph.com/issues/18089),
    [pr#13153](http://github.com/ceph/ceph/pull/13153), Nathan Cutler)

-   tests: use ceph-jewel branch for s3tests
    ([issue#18384](http://tracker.ceph.com/issues/18384),
    [pr#12745](http://github.com/ceph/ceph/pull/12745), Nathan Cutler)

-   tests: Workunits needlessly wget from git.ceph.com
    ([issue#18336](http://tracker.ceph.com/issues/18336),
    [issue#18271](http://tracker.ceph.com/issues/18271),
    [issue#18388](http://tracker.ceph.com/issues/18388),
    [pr#12686](http://github.com/ceph/ceph/pull/12686), Nathan Cutler,
    Sage Weil)

-   test: temporarily disable fork()\'ing tests
    ([issue#16556](http://tracker.ceph.com/issues/16556),
    [issue#17832](http://tracker.ceph.com/issues/17832),
    [pr#11953](http://github.com/ceph/ceph/pull/11953), John Spray)

-   test: test fails due to The UNIX domain socket path
    ([issue#16014](http://tracker.ceph.com/issues/16014),
    [pr#12151](http://github.com/ceph/ceph/pull/12151), Loic Dachary)

-   tools: ceph-disk: ceph-disk@.service races with ceph-osd@.service
    ([issue#17889](http://tracker.ceph.com/issues/17889),
    [issue#17813](http://tracker.ceph.com/issues/17813),
    [pr#12147](http://github.com/ceph/ceph/pull/12147), Loic Dachary)

-   tools: ceph-disk \--dmcrypt create must not require admin key
    ([issue#17849](http://tracker.ceph.com/issues/17849),
    [pr#12033](http://github.com/ceph/ceph/pull/12033), Loic Dachary)

-   tools: ceph-disk prepare writes osd log 0 with root owner
    ([issue#18538](http://tracker.ceph.com/issues/18538),
    [pr#13025](http://github.com/ceph/ceph/pull/13025), Samuel Matzek)

-   tools: crushtool \--compile is create output despite of missing item
    ([issue#17306](http://tracker.ceph.com/issues/17306),
    [pr#11410](http://github.com/ceph/ceph/pull/11410), Kefu Chai)

-   tools: rados bench seq must verify the hostname
    ([issue#17526](http://tracker.ceph.com/issues/17526),
    [pr#13049](http://github.com/ceph/ceph/pull/13049), Loic Dachary)

-   tools: snapshotted RBD extent objects can\'t be manually evicted
    from a cache tier
    ([issue#17896](http://tracker.ceph.com/issues/17896),
    [pr#11968](http://github.com/ceph/ceph/pull/11968), Mingxin Liu)

-   tools: systemd/ceph-disk: reduce ceph-disk flock contention
    ([issue#18049](http://tracker.ceph.com/issues/18049),
    [issue#13160](http://tracker.ceph.com/issues/13160),
    [pr#12210](http://github.com/ceph/ceph/pull/12210), David
    Disseldorp)

## v10.2.5 Jewel

This point release fixes an important [regression introduced in
v10.2.4](http://tracker.ceph.com/issues/18185).

We recommend that all v10.2.x users upgrade.

### Notable Changes

For more detailed information, see
`the complete changelog <../changelog/v10.2.5.txt>`{.interpreted-text
role="download"}.

-   msg/simple/Pipe: avoid returning 0 on poll timeout
    ([issue#18185](http://tracker.ceph.com/issues/18185),
    [pr#12376](https://github.com/ceph/ceph/pull/12376), Sage Weil)

## v10.2.4 Jewel

This point release fixes several important bugs in RBD mirroring, RGW
multi-site, CephFS, and RADOS.

We recommend that all v10.2.x users upgrade. Also note the following
when upgrading from hammer

### Upgrading from hammer

When the last hammer OSD in a cluster containing jewel MONs is upgraded
to jewel, as of 10.2.4 the jewel MONs will issue this warning: \"all
OSDs are running jewel or later but the \'require_jewel_osds\' osdmap
flag is not set\" and change the cluster health status to HEALTH_WARN.

This is a signal for the admin to do \"ceph osd set
require_jewel_osds\" - by doing this, the upgrade path is complete and
no more pre-Jewel OSDs may be added to the cluster.

### Notable Changes

For more detailed information, see
`the complete changelog <../changelog/v10.2.4.txt>`{.interpreted-text
role="download"}.

-   build/ops: aarch64: Compiler-based detection of crc32 extended CPU
    type is broken ([issue#17516](http://tracker.ceph.com/issues/17516),
    [pr#11492](http://github.com/ceph/ceph/pull/11492), Alexander Graf)
-   build/ops: allow building RGW with LDAP disabled
    ([issue#17312](http://tracker.ceph.com/issues/17312),
    [pr#11478](http://github.com/ceph/ceph/pull/11478), Daniel
    Gryniewicz)
-   build/ops: backport \'logrotate: Run as root/ceph\'
    ([issue#17381](http://tracker.ceph.com/issues/17381),
    [pr#11201](http://github.com/ceph/ceph/pull/11201), Boris Ranto)
-   build/ops: ceph installs stuff in %\_udevrulesdir but does not own
    that directory ([issue#16949](http://tracker.ceph.com/issues/16949),
    [pr#10862](http://github.com/ceph/ceph/pull/10862), Nathan Cutler)
-   build/ops: ceph-osd-prestart.sh fails confusingly when data
    directory does not exist
    ([issue#17091](http://tracker.ceph.com/issues/17091),
    [pr#10812](http://github.com/ceph/ceph/pull/10812), Nathan Cutler)
-   build/ops: disable LTTng-UST in openSUSE builds
    ([issue#16937](http://tracker.ceph.com/issues/16937),
    [pr#10794](http://github.com/ceph/ceph/pull/10794), Michel Normand)
-   build/ops: i386 tarball gitbuilder failure on master
    ([issue#16398](http://tracker.ceph.com/issues/16398),
    [pr#10855](http://github.com/ceph/ceph/pull/10855), Vikhyat Umrao,
    Kefu Chai)
-   build/ops: include more files in \"make dist\" tarball
    ([issue#17560](http://tracker.ceph.com/issues/17560),
    [pr#11431](http://github.com/ceph/ceph/pull/11431), Ken Dreyer)
-   build/ops: incorrect value of CINIT_FLAG_DEFER_DROP_PRIVILEGES
    ([issue#16663](http://tracker.ceph.com/issues/16663),
    [pr#10278](http://github.com/ceph/ceph/pull/10278), Casey Bodley)
-   build/ops: remove SYSTEMD_RUN from initscript
    ([issue#7627](http://tracker.ceph.com/issues/7627),
    [issue#16441](http://tracker.ceph.com/issues/16441),
    [issue#16440](http://tracker.ceph.com/issues/16440),
    [pr#9872](http://github.com/ceph/ceph/pull/9872), Vladislav
    Odintsov)
-   build/ops: systemd: add install section to rbdmap.service file
    ([issue#17541](http://tracker.ceph.com/issues/17541),
    [pr#11158](http://github.com/ceph/ceph/pull/11158), Jelle vd Kooij)
-   common: Enable/Disable of features is allowed even the features are
    already enabled/disabled
    ([issue#16079](http://tracker.ceph.com/issues/16079),
    [pr#11460](http://github.com/ceph/ceph/pull/11460), Lu Shi)
-   common: Log.cc: Assign LOG_INFO priority to syslog calls
    ([issue#15808](http://tracker.ceph.com/issues/15808),
    [pr#11231](http://github.com/ceph/ceph/pull/11231), Brad Hubbard)
-   common: Proxied operations shouldn\'t result in error messages if
    replayed ([issue#16130](http://tracker.ceph.com/issues/16130),
    [pr#11461](http://github.com/ceph/ceph/pull/11461), Vikhyat Umrao)
-   common: Request exclusive lock if owner sends -ENOTSUPP for proxied
    maintenance op ([issue#16171](http://tracker.ceph.com/issues/16171),
    [pr#10784](http://github.com/ceph/ceph/pull/10784), Jason Dillaman)
-   common: msgr/async: Messenger thread long time lock hold risk
    ([issue#15758](http://tracker.ceph.com/issues/15758),
    [pr#10761](http://github.com/ceph/ceph/pull/10761), Wei Jin)
-   doc: fix description for rsize and rasize
    ([issue#17357](http://tracker.ceph.com/issues/17357),
    [pr#11171](http://github.com/ceph/ceph/pull/11171), Andreas
    Gerstmayr)
-   filestore: can get stuck in an unbounded loop during scrub
    ([issue#17859](http://tracker.ceph.com/issues/17859),
    [pr#12001](http://github.com/ceph/ceph/pull/12001), Sage Weil)
-   fs: Failure in snaptest-git-ceph.sh
    ([issue#17172](http://tracker.ceph.com/issues/17172),
    [pr#11419](http://github.com/ceph/ceph/pull/11419), Yan, Zheng)
-   fs: Log path as well as ino when detecting metadata damage
    ([issue#16973](http://tracker.ceph.com/issues/16973),
    [pr#11418](http://github.com/ceph/ceph/pull/11418), John Spray)
-   fs: client: FAILED assert(root_ancestor-\>qtree == \_\_null)
    ([issue#16066](http://tracker.ceph.com/issues/16066),
    [issue#16067](http://tracker.ceph.com/issues/16067),
    [pr#10107](http://github.com/ceph/ceph/pull/10107), Yan, Zheng)
-   fs: client: add missing client_lock for get_root
    ([issue#17197](http://tracker.ceph.com/issues/17197),
    [pr#10921](http://github.com/ceph/ceph/pull/10921), Patrick
    Donnelly)
-   fs: client: fix shutdown with open inodes
    ([issue#16764](http://tracker.ceph.com/issues/16764),
    [pr#10958](http://github.com/ceph/ceph/pull/10958), John Spray)
-   fs: client: nlink count is not maintained correctly
    ([issue#16668](http://tracker.ceph.com/issues/16668),
    [pr#10877](http://github.com/ceph/ceph/pull/10877), Jeff Layton)
-   fs: multimds: allow_multimds not required when max_mds is set in
    ceph.conf at startup
    ([issue#17105](http://tracker.ceph.com/issues/17105),
    [pr#10997](http://github.com/ceph/ceph/pull/10997), Patrick
    Donnelly)
-   librados: memory leaks from ceph::crypto (WITH_NSS)
    ([issue#17205](http://tracker.ceph.com/issues/17205),
    [pr#11409](http://github.com/ceph/ceph/pull/11409), Casey Bodley)
-   librados: modify Pipe::connect() to return the error code
    ([issue#15308](http://tracker.ceph.com/issues/15308),
    [pr#11193](http://github.com/ceph/ceph/pull/11193), Vikhyat Umrao)
-   librados: remove new setxattr overload to avoid breaking the C++ ABI
    ([issue#18058](http://tracker.ceph.com/issues/18058),
    [pr#12207](http://github.com/ceph/ceph/pull/12207), Josh Durgin)
-   librbd: cannot disable journaling or remove non-mirrored,
    non-primary image
    ([issue#16740](http://tracker.ceph.com/issues/16740),
    [pr#11337](http://github.com/ceph/ceph/pull/11337), Jason Dillaman)
-   librbd: discard after write can result in assertion failure
    ([issue#17695](http://tracker.ceph.com/issues/17695),
    [pr#11644](http://github.com/ceph/ceph/pull/11644), Jason Dillaman)
-   librbd::Operations: update notification failed: (2) No such file or
    directory ([issue#17549](http://tracker.ceph.com/issues/17549),
    [pr#11420](http://github.com/ceph/ceph/pull/11420), Jason Dillaman)
-   mds: Crash in Client::\_invalidate_kernel_dcache when reconnecting
    during unmount ([issue#17253](http://tracker.ceph.com/issues/17253),
    [pr#11414](http://github.com/ceph/ceph/pull/11414), Yan, Zheng)
-   mds: Duplicate damage table entries
    ([issue#17173](http://tracker.ceph.com/issues/17173),
    [pr#11412](http://github.com/ceph/ceph/pull/11412), John Spray)
-   mds: Failure in dirfrag.sh
    ([issue#17286](http://tracker.ceph.com/issues/17286),
    [pr#11416](http://github.com/ceph/ceph/pull/11416), Yan, Zheng)
-   mds: Failure in snaptest-git-ceph.sh
    ([issue#17271](http://tracker.ceph.com/issues/17271),
    [pr#11415](http://github.com/ceph/ceph/pull/11415), Yan, Zheng)
-   mon: Ceph Status - Segmentation Fault
    ([issue#16266](http://tracker.ceph.com/issues/16266),
    [pr#11408](http://github.com/ceph/ceph/pull/11408), Brad Hubbard)
-   mon: Display full flag in ceph status if full flag is set
    ([issue#15809](http://tracker.ceph.com/issues/15809),
    [pr#9388](http://github.com/ceph/ceph/pull/9388), Vikhyat Umrao)
-   mon: Error EINVAL: removing mon.a at 172.21.15.16:6789/0, there will
    be 1 monitors ([issue#17725](http://tracker.ceph.com/issues/17725),
    [pr#12267](http://github.com/ceph/ceph/pull/12267), Joao Eduardo
    Luis)
-   mon: OSDMonitor: only reject MOSDBoot based on up_from if inst
    matches ([issue#17899](http://tracker.ceph.com/issues/17899),
    [pr#12067](http://github.com/ceph/ceph/pull/12067), Samuel Just)
-   mon: OSDMonitor: Missing nearfull flag set
    ([issue#17390](http://tracker.ceph.com/issues/17390),
    [pr#11272](http://github.com/ceph/ceph/pull/11272), Igor Podoski)
-   mon: Upgrading 0.94.6 -\> 0.94.9 saturating mon node networking
    ([issue#17365](http://tracker.ceph.com/issues/17365),
    [issue#17386](http://tracker.ceph.com/issues/17386),
    [pr#11679](http://github.com/ceph/ceph/pull/11679), Sage Weil, xie
    xingguo)
-   mon: ceph mon Segmentation fault after set crush_ruleset ceph 10.2.2
    ([issue#16653](http://tracker.ceph.com/issues/16653),
    [pr#10861](http://github.com/ceph/ceph/pull/10861), song baisen)
-   mon: crash: crush/CrushWrapper.h: 940: FAILED
    assert(successful_detach)
    ([issue#16525](http://tracker.ceph.com/issues/16525),
    [pr#10496](http://github.com/ceph/ceph/pull/10496), Kefu Chai)
-   mon: don\'t crash on invalid standby_for_fscid
    ([issue#17466](http://tracker.ceph.com/issues/17466),
    [pr#11389](http://github.com/ceph/ceph/pull/11389), John Spray)
-   mon: fix missing osd metadata (again)
    ([issue#17685](http://tracker.ceph.com/issues/17685),
    [pr#11642](http://github.com/ceph/ceph/pull/11642), John Spray)
-   mon: osdmonitor: decouple adjust_heartbeat_grace and
    min_down_reporters
    ([issue#17055](http://tracker.ceph.com/issues/17055),
    [pr#10757](http://github.com/ceph/ceph/pull/10757), Zengran Zhang)
-   mon: the %USED of ceph df is wrong
    ([issue#16933](http://tracker.ceph.com/issues/16933),
    [pr#10860](http://github.com/ceph/ceph/pull/10860), Kefu Chai)
-   osd: condition OSDMap encoding on features
    ([issue#18015](http://tracker.ceph.com/issues/18015),
    [pr#12167](http://github.com/ceph/ceph/pull/12167), Sage Weil)
-   osd: PG::\_update_calc_stats wrong for CRUSH_ITEM_NONE up set items
    ([issue#16998](http://tracker.ceph.com/issues/16998),
    [pr#10883](http://github.com/ceph/ceph/pull/10883), Samuel Just)
-   osd: PG::choose_acting valgrind error or ./common/hobject.h: 182:
    FAILED assert(!max \|\| (\*this == hobject_t(hobject_t::get_max())))
    ([issue#13967](http://tracker.ceph.com/issues/13967),
    [pr#10885](http://github.com/ceph/ceph/pull/10885), Tao Chang)
-   osd: Potential crash during journal::Replay shut down
    ([issue#16433](http://tracker.ceph.com/issues/16433),
    [pr#10645](http://github.com/ceph/ceph/pull/10645), Jason Dillaman)
-   osd: add peer_addr in heartbeat_check log message
    ([issue#15762](http://tracker.ceph.com/issues/15762),
    [pr#9739](http://github.com/ceph/ceph/pull/9739), Vikhyat Umrao,
    Sage Weil)
-   osd: adjust scrub boundary to object without SnapSet
    ([issue#17470](http://tracker.ceph.com/issues/17470),
    [pr#11311](http://github.com/ceph/ceph/pull/11311), Samuel Just)
-   osd: ceph osd df does not show summarized info correctly if one or
    more OSDs are out
    ([issue#16706](http://tracker.ceph.com/issues/16706),
    [pr#10759](http://github.com/ceph/ceph/pull/10759), xie xingguo)
-   osd: journal: do not prematurely flag object recorder as closed
    ([issue#17590](http://tracker.ceph.com/issues/17590),
    [pr#11634](http://github.com/ceph/ceph/pull/11634), Jason Dillaman)
-   osd: mark_all_unfound_lost() leaves unapplied changes
    ([issue#16156](http://tracker.ceph.com/issues/16156),
    [pr#10886](http://github.com/ceph/ceph/pull/10886), Samuel Just)
-   osd: segfault in ObjectCacher::FlusherThread
    ([issue#16610](http://tracker.ceph.com/issues/16610),
    [pr#10864](http://github.com/ceph/ceph/pull/10864), Yan, Zheng)
-   qa: remove EnumerateObjects from librados upgrade tests
    ([pr#11728](https://github.com/ceph/ceph/pull/11728), Josh Durgin)
-   rbd: Disabling pool mirror mode with registered peers results
    orphaned mirrored images
    ([issue#16984](http://tracker.ceph.com/issues/16984),
    [pr#10857](http://github.com/ceph/ceph/pull/10857), Jason Dillaman)
-   rbd: ImageWatcher: use after free within C_UnwatchAndFlush
    ([issue#17289](http://tracker.ceph.com/issues/17289),
    [issue#17254](http://tracker.ceph.com/issues/17254),
    [pr#11466](http://github.com/ceph/ceph/pull/11466), Jason Dillaman)
-   rbd: Prevent the creation of a clone from a non-primary mirrored
    image ([issue#16449](http://tracker.ceph.com/issues/16449),
    [pr#10650](http://github.com/ceph/ceph/pull/10650), Mykola Golub)
-   rbd: RBD should restrict mirror enable/disable actions on
    parents/clones ([issue#16056](http://tracker.ceph.com/issues/16056),
    [pr#11459](http://github.com/ceph/ceph/pull/11459), zhuangzeqiang)
-   rbd: TestJournalReplay: sporadic assert(m_state == STATE_READY \|\|
    m_state == STATE_STOPPING) failure
    ([issue#17566](http://tracker.ceph.com/issues/17566),
    [pr#11590](http://github.com/ceph/ceph/pull/11590), Jason Dillaman)
-   rbd: bench io-size should not be larger than image size
    ([issue#16967](http://tracker.ceph.com/issues/16967),
    [pr#10796](http://github.com/ceph/ceph/pull/10796), Jason Dillaman)
-   rbd: ceph 10.2.2 rbd status on image format 2 returns (2) No such
    file or directory
    ([issue#16887](http://tracker.ceph.com/issues/16887),
    [pr#10652](http://github.com/ceph/ceph/pull/10652), Jason Dillaman)
-   rbd: helgrind: TestLibRBD.TestIOPP potential deadlock closing an
    image with read-ahead enabled
    ([issue#17198](http://tracker.ceph.com/issues/17198),
    [pr#11463](http://github.com/ceph/ceph/pull/11463), Jason Dillaman)
-   rbd: image.stat() call in librbdpy fails sometimes
    ([issue#17310](http://tracker.ceph.com/issues/17310),
    [pr#11464](http://github.com/ceph/ceph/pull/11464), Jason Dillaman)
-   rbd: krbd qa scripts and concurrent.sh test fix
    ([issue#17223](http://tracker.ceph.com/issues/17223),
    [pr#11018](http://github.com/ceph/ceph/pull/11018), Ilya Dryomov)
-   rbd: krbd-related CLI patches
    ([issue#17554](http://tracker.ceph.com/issues/17554),
    [pr#11400](http://github.com/ceph/ceph/pull/11400), Ilya Dryomov)
-   rbd: mirror: improve resiliency of stress test case
    ([issue#16855](http://tracker.ceph.com/issues/16855),
    [issue#16555](http://tracker.ceph.com/issues/16555),
    [issue#14738](http://tracker.ceph.com/issues/14738),
    [issue#15259](http://tracker.ceph.com/issues/15259),
    [issue#17446](http://tracker.ceph.com/issues/17446),
    [issue#17355](http://tracker.ceph.com/issues/17355),
    [issue#16538](http://tracker.ceph.com/issues/16538),
    [issue#16974](http://tracker.ceph.com/issues/16974),
    [issue#17283](http://tracker.ceph.com/issues/17283),
    [issue#17317](http://tracker.ceph.com/issues/17317),
    [issue#17416](http://tracker.ceph.com/issues/17416),
    [issue#16227](http://tracker.ceph.com/issues/16227),
    [pr#11433](http://github.com/ceph/ceph/pull/11433), Mykola Golub,
    Ricardo Dias, Jason Dillaman)
-   rbd: rbd-nbd IO hang
    ([issue#16921](http://tracker.ceph.com/issues/16921),
    [pr#11467](http://github.com/ceph/ceph/pull/11467), Jason Dillaman)
-   rbd: update_features API needs to support backwards/forward
    compatibility ([issue#17330](http://tracker.ceph.com/issues/17330),
    [pr#11462](http://github.com/ceph/ceph/pull/11462), Jason Dillaman)
-   rgw: COPY broke multipart files uploaded under dumpling
    ([issue#16435](http://tracker.ceph.com/issues/16435),
    [pr#10866](http://github.com/ceph/ceph/pull/10866), Yehuda Sadeh)
-   rgw: Config parameter rgw keystone make new tenants in radosgw
    multitenancy does not work
    ([issue#17293](http://tracker.ceph.com/issues/17293),
    [pr#11473](http://github.com/ceph/ceph/pull/11473), SirishaGuduru)
-   rgw: Do not archive metadata by default
    ([issue#17256](http://tracker.ceph.com/issues/17256),
    [pr#11321](http://github.com/ceph/ceph/pull/11321), Pavan
    Rallabhandi, Matt Benjamin)
-   rgw: ERROR: got unexpected error when trying to read object: -2
    ([issue#17111](http://tracker.ceph.com/issues/17111),
    [pr#11472](http://github.com/ceph/ceph/pull/11472), Yang Honggang)
-   rgw: Modification for TEST S3 ACCESS section in INSTALL CEPH OBJECT
    GATEWAY page ([issue#15603](http://tracker.ceph.com/issues/15603),
    [pr#11475](http://github.com/ceph/ceph/pull/11475), la-sguduru)
-   rgw: RGW loses realm/period/zonegroup/zone data: period overwritten
    if somewhere in the cluster is still running Hammer
    ([issue#17371](http://tracker.ceph.com/issues/17371),
    [pr#11519](http://github.com/ceph/ceph/pull/11519), Orit Wasserman)
-   rgw: RGWDataSyncCR fails on errors from RGWListBucketIndexesCR
    ([issue#17073](http://tracker.ceph.com/issues/17073),
    [pr#11330](http://github.com/ceph/ceph/pull/11330), Casey Bodley)
-   rgw: S3 object versioning fails when applied on a non-master zone
    ([issue#16494](http://tracker.ceph.com/issues/16494),
    [pr#11367](http://github.com/ceph/ceph/pull/11367), Yehuda Sadeh)
-   rgw: add orphan options to radosgw-admin \--help and man page
    ([issue#17281](http://tracker.ceph.com/issues/17281),
    [issue#17280](http://tracker.ceph.com/issues/17280),
    [pr#11139](http://github.com/ceph/ceph/pull/11139), Ken Dreyer,
    Thomas Serlin)
-   rgw: back off bucket sync on failures, don\'t store marker
    ([issue#16742](http://tracker.ceph.com/issues/16742),
    [pr#11021](http://github.com/ceph/ceph/pull/11021), Yehuda Sadeh)
-   rgw: combined LDAP backports
    ([issue#17544](http://tracker.ceph.com/issues/17544),
    [issue#17185](http://tracker.ceph.com/issues/17185),
    [pr#11332](http://github.com/ceph/ceph/pull/11332), Harald Klein,
    Matt Benjamin)
-   rgw: cors auto memleak
    ([issue#16564](http://tracker.ceph.com/issues/16564),
    [pr#10656](http://github.com/ceph/ceph/pull/10656), Yan Jun)
-   rgw: default quota fixes
    ([issue#16410](http://tracker.ceph.com/issues/16410),
    [pr#10832](http://github.com/ceph/ceph/pull/10832), Pavan
    Rallabhandi, Daniel Gryniewicz)
-   rgw: doc: description of multipart part entity is wrong
    ([issue#17504](http://tracker.ceph.com/issues/17504),
    [pr#11342](http://github.com/ceph/ceph/pull/11342), weiqiaomiao)
-   rgw: don\'t loop forever when reading data from 0 sized segment.
    ([issue#17692](http://tracker.ceph.com/issues/17692),
    [pr#11626](http://github.com/ceph/ceph/pull/11626), Marcus Watts)
-   rgw: fix put_acls for objects starting and ending with underscore
    ([issue#17625](http://tracker.ceph.com/issues/17625),
    [pr#11669](http://github.com/ceph/ceph/pull/11669), Orit Wasserman)
-   rgw: fix regression with handling double underscore
    ([issue#17443](http://tracker.ceph.com/issues/17443),
    [issue#16856](http://tracker.ceph.com/issues/16856),
    [pr#11563](http://github.com/ceph/ceph/pull/11563), Yehuda Sadeh,
    Orit Wasserman)
-   rgw: handle empty POST condition
    ([issue#17635](http://tracker.ceph.com/issues/17635),
    [pr#11662](http://github.com/ceph/ceph/pull/11662), Yehuda Sadeh)
-   rgw: metadata sync can skip markers for failed/incomplete entries
    ([issue#16759](http://tracker.ceph.com/issues/16759),
    [pr#10657](http://github.com/ceph/ceph/pull/10657), Yehuda Sadeh)
-   rgw: nfs backports
    ([issue#17393](http://tracker.ceph.com/issues/17393),
    [issue#17311](http://tracker.ceph.com/issues/17311),
    [issue#17367](http://tracker.ceph.com/issues/17367),
    [issue#17319](http://tracker.ceph.com/issues/17319),
    [issue#17321](http://tracker.ceph.com/issues/17321),
    [issue#17322](http://tracker.ceph.com/issues/17322),
    [issue#17323](http://tracker.ceph.com/issues/17323),
    [issue#17325](http://tracker.ceph.com/issues/17325),
    [issue#17326](http://tracker.ceph.com/issues/17326),
    [issue#17327](http://tracker.ceph.com/issues/17327),
    [pr#11335](http://github.com/ceph/ceph/pull/11335), Min Chen, Yan
    Jun, Weibing Zhang, Matt Benjamin)
-   rgw: period commit loses zonegroup changes: region_map converted
    repeatedly ([issue#17051](http://tracker.ceph.com/issues/17051),
    [pr#10890](http://github.com/ceph/ceph/pull/10890), Casey Bodley)
-   rgw: period commit return error when the current period has a
    zonegroup which doesn\'t have a master zone
    ([issue#17110](http://tracker.ceph.com/issues/17110),
    [pr#10867](http://github.com/ceph/ceph/pull/10867), weiqiaomiao)
-   rgw: radosgw daemon core when reopen logs
    ([issue#17036](http://tracker.ceph.com/issues/17036),
    [pr#10868](http://github.com/ceph/ceph/pull/10868), weiqiaomiao)
-   rgw: rgw file uses too much CPU in gc/idle thread
    ([issue#16976](http://tracker.ceph.com/issues/16976),
    [pr#10889](http://github.com/ceph/ceph/pull/10889), Matt Benjamin)
-   rgw: s3tests-test-readwrite failing with 500
    ([issue#16930](http://tracker.ceph.com/issues/16930),
    [pr#11471](http://github.com/ceph/ceph/pull/11471), Yehuda Sadeh)
-   rgw: upgrade from old multisite to new multisite fails
    ([issue#16751](http://tracker.ceph.com/issues/16751),
    [pr#10891](http://github.com/ceph/ceph/pull/10891), Orit Wasserman)
-   rgw:response information is error when geting token of swift account
    ([issue#15195](http://tracker.ceph.com/issues/15195),
    [pr#11474](http://github.com/ceph/ceph/pull/11474), Qiankun Zheng)
-   rgw:user email can modify to empty when it has values
    ([issue#13286](http://tracker.ceph.com/issues/13286),
    [pr#11469](http://github.com/ceph/ceph/pull/11469), Yehuda Sadeh,
    Weijun Duan)
-   tests: ceph-disk must ignore debug monc
    ([issue#17607](http://tracker.ceph.com/issues/17607),
    [pr#11548](http://github.com/ceph/ceph/pull/11548), Loic Dachary)
-   tests: fix TestClsRbd.mirror_image failure in
    upgrade:jewel-x-master-distro-basic-vps
    ([issue#16529](http://tracker.ceph.com/issues/16529),
    [pr#10888](http://github.com/ceph/ceph/pull/10888), Jason Dillaman)
-   tests: scsi_debug fails /dev/disk/by-partuuid
    ([issue#17100](http://tracker.ceph.com/issues/17100),
    [pr#11411](http://github.com/ceph/ceph/pull/11411), Loic Dachary)
-   tests: test/ceph_test_msgr: do not use <Message::middle> for holding
    transient... ([issue#17365](http://tracker.ceph.com/issues/17365),
    [issue#17728](http://tracker.ceph.com/issues/17728),
    [issue#16955](http://tracker.ceph.com/issues/16955),
    [pr#11742](http://github.com/ceph/ceph/pull/11742), Haomai Wang,
    Kefu Chai, Michal Jarzabek, Sage Weil)
-   tools: Missing comma in ceph-create-keys causes concatenation of
    arguments ([issue#17815](http://tracker.ceph.com/issues/17815),
    [pr#11822](http://github.com/ceph/ceph/pull/11822), Patrick
    Donnelly)
-   tools: add a tool to rebuild mon store from OSD
    ([issue#17179](http://tracker.ceph.com/issues/17179),
    [issue#17400](http://tracker.ceph.com/issues/17400),
    [pr#11126](http://github.com/ceph/ceph/pull/11126), Kefu Chai, xie
    xingguo)
-   tools: ceph-create-keys: sometimes blocks forever if mds allow is
    set ([issue#16255](http://tracker.ceph.com/issues/16255),
    [pr#11417](http://github.com/ceph/ceph/pull/11417), John Spray)
-   tools: ceph-disk should timeout when a lock cannot be acquired
    ([issue#16580](http://tracker.ceph.com/issues/16580),
    [pr#10758](http://github.com/ceph/ceph/pull/10758), Loic Dachary)
-   tools: ceph-disk: expected systemd unit failures are confusing
    ([issue#15990](http://tracker.ceph.com/issues/15990),
    [pr#10884](http://github.com/ceph/ceph/pull/10884), Boris Ranto)
-   tools: ceph-disk: using a regular file as a journal fails
    ([issue#16280](http://tracker.ceph.com/issues/16280),
    [issue#17662](http://tracker.ceph.com/issues/17662),
    [pr#11657](http://github.com/ceph/ceph/pull/11657), Jayashree
    Candadai, Anirudha Bose, Loic Dachary, Shylesh Kumar)
-   tools: ceph-objectstore-tool crashes if \--journal-path
    \<a-directory\>
    ([issue#17307](http://tracker.ceph.com/issues/17307),
    [pr#11407](http://github.com/ceph/ceph/pull/11407), Kefu Chai)
-   tools: ceph-objectstore-tool: add a way to split filestore
    directories offline
    ([issue#17220](http://tracker.ceph.com/issues/17220),
    [pr#11252](http://github.com/ceph/ceph/pull/11252), Josh Durgin)
-   tools: ceph-post-file: use new ssh key
    ([issue#14267](http://tracker.ceph.com/issues/14267),
    [pr#11746](http://github.com/ceph/ceph/pull/11746), David Galloway)

## v10.2.3 Jewel

This point release fixes several important bugs in RBD mirroring, RGW
multi-site, CephFS, and RADOS.

We recommend that all v10.2.x users upgrade.

For more detailed information, see
`the complete changelog <../changelog/v10.2.3.txt>`{.interpreted-text
role="download"}.

### Notable Changes

-   build/ops: 60-ceph-partuuid-workaround-rules still needed by debian
    jessie (udev 215-17)
    ([issue#16351](http://tracker.ceph.com/issues/16351),
    [pr#10653](http://github.com/ceph/ceph/pull/10653), runsisi, Loic
    Dachary)
-   build/ops: ceph Resource Agent does not work with systemd
    ([issue#14828](http://tracker.ceph.com/issues/14828),
    [pr#9917](http://github.com/ceph/ceph/pull/9917), Nathan Cutler)
-   build/ops: ceph-base requires parted
    ([issue#16095](http://tracker.ceph.com/issues/16095),
    [pr#10008](http://github.com/ceph/ceph/pull/10008), Ken Dreyer)
-   build/ops: ceph-osd-prestart.sh contains Upstart-specific code
    ([issue#15984](http://tracker.ceph.com/issues/15984),
    [pr#10364](http://github.com/ceph/ceph/pull/10364), Nathan Cutler)
-   build/ops: mount.ceph: move from ceph-base to ceph-common and add
    symlink in /sbin for SUSE
    ([issue#16598](http://tracker.ceph.com/issues/16598),
    [issue#16645](http://tracker.ceph.com/issues/16645),
    [pr#10357](http://github.com/ceph/ceph/pull/10357), Nathan Cutler,
    Dan Horák, Ricardo Dias, Kefu Chai)
-   build/ops: need rocksdb commit 7ca731b12ce for ppc64le build
    ([issue#17092](http://tracker.ceph.com/issues/17092),
    [pr#10816](http://github.com/ceph/ceph/pull/10816), Nathan Cutler)
-   build/ops: rpm: OBS needs ExclusiveArch
    ([issue#16936](http://tracker.ceph.com/issues/16936),
    [pr#10614](http://github.com/ceph/ceph/pull/10614), Michel Normand)
-   cli: ceph command line tool chokes on ceph --w (the dash is unicode
    \'en dash\' &ndash, copy-paste to reproduce)
    ([issue#12287](http://tracker.ceph.com/issues/12287),
    [pr#10420](http://github.com/ceph/ceph/pull/10420), Oleh Prypin,
    Kefu Chai)
-   common: expose buffer const_iterator symbols
    ([issue#16899](http://tracker.ceph.com/issues/16899),
    [pr#10552](http://github.com/ceph/ceph/pull/10552), Noah Watkins)
-   common: global-init: fixup chown of the run directory along with log
    and asok files ([issue#15607](http://tracker.ceph.com/issues/15607),
    [pr#8754](http://github.com/ceph/ceph/pull/8754), Karol Mroz)
-   fs: ceph-fuse: link to libtcmalloc or jemalloc
    ([issue#16655](http://tracker.ceph.com/issues/16655),
    [pr#10303](http://github.com/ceph/ceph/pull/10303), Yan, Zheng)
-   fs: client: crash in unmount when fuse_use_invalidate_cb is enabled
    ([issue#16137](http://tracker.ceph.com/issues/16137),
    [pr#10106](http://github.com/ceph/ceph/pull/10106), Yan, Zheng)
-   fs: client: fstat cap release
    ([issue#15723](http://tracker.ceph.com/issues/15723),
    [pr#9562](http://github.com/ceph/ceph/pull/9562), Yan, Zheng, Noah
    Watkins)
-   fs: essential backports for OpenStack Manila
    ([issue#15406](http://tracker.ceph.com/issues/15406),
    [issue#15614](http://tracker.ceph.com/issues/15614),
    [issue#15615](http://tracker.ceph.com/issues/15615),
    [pr#10453](http://github.com/ceph/ceph/pull/10453), John Spray,
    Ramana Raja, Xiaoxi Chen)
-   fs: fix double-unlock on shutdown
    ([issue#17126](http://tracker.ceph.com/issues/17126),
    [pr#10847](http://github.com/ceph/ceph/pull/10847), Greg Farnum)
-   fs: fix mdsmap print_summary with standby replays
    ([issue#15705](http://tracker.ceph.com/issues/15705),
    [pr#9547](http://github.com/ceph/ceph/pull/9547), John Spray)
-   fs: fuse mounted file systems fails SAMBA CTDB ping_pong rw test
    with v9.0.2 ([issue#12653](http://tracker.ceph.com/issues/12653),
    [issue#15634](http://tracker.ceph.com/issues/15634),
    [pr#10108](http://github.com/ceph/ceph/pull/10108), Yan, Zheng)
-   librados: Missing export for rados_aio_get_version in
    src/include/rados/librados.h
    ([issue#15535](http://tracker.ceph.com/issues/15535),
    [pr#9574](http://github.com/ceph/ceph/pull/9574), Jim Wright)
-   librados: osd: bad flags can crash the osd
    ([issue#16012](http://tracker.ceph.com/issues/16012),
    [pr#9997](http://github.com/ceph/ceph/pull/9997), Sage Weil)
-   librbd: Close journal and object map before flagging exclusive lock
    as released ([issue#16450](http://tracker.ceph.com/issues/16450),
    [pr#10053](http://github.com/ceph/ceph/pull/10053), Jason Dillaman)
-   librbd: Crash when utilizing advisory locking API functions
    ([issue#16364](http://tracker.ceph.com/issues/16364),
    [pr#10051](http://github.com/ceph/ceph/pull/10051), Jason Dillaman)
-   librbd: ExclusiveLock object leaked when switching to snapshot
    ([issue#16446](http://tracker.ceph.com/issues/16446),
    [pr#10054](http://github.com/ceph/ceph/pull/10054), Jason Dillaman)
-   librbd: FAILED assert(object_no \< m_object_map.size())
    ([issue#16561](http://tracker.ceph.com/issues/16561),
    [pr#10647](http://github.com/ceph/ceph/pull/10647), Jason Dillaman)
-   librbd: Image removal doesn\'t necessarily clean up all
    rbd_mirroring entries
    ([issue#16471](http://tracker.ceph.com/issues/16471),
    [pr#10009](http://github.com/ceph/ceph/pull/10009), Jason Dillaman)
-   librbd: Object map/fast-diff invalidated if journal replays the same
    snap remove event
    ([issue#16350](http://tracker.ceph.com/issues/16350),
    [pr#10010](http://github.com/ceph/ceph/pull/10010), Jason Dillaman)
-   librbd: Timeout sending mirroring notification shouldn\'t result in
    failure ([issue#16470](http://tracker.ceph.com/issues/16470),
    [pr#10052](http://github.com/ceph/ceph/pull/10052), Jason Dillaman)
-   librbd: Whitelist EBUSY error from snap unprotect for journal replay
    ([issue#16445](http://tracker.ceph.com/issues/16445),
    [pr#10055](http://github.com/ceph/ceph/pull/10055), Jason Dillaman)
-   librbd: cancel all tasks should wait until finisher is done
    ([issue#16517](http://tracker.ceph.com/issues/16517),
    [pr#9752](http://github.com/ceph/ceph/pull/9752), Haomai Wang)
-   librbd: delay acquiring lock if image watch has failed
    ([issue#16923](http://tracker.ceph.com/issues/16923),
    [pr#10827](http://github.com/ceph/ceph/pull/10827), Jason Dillaman)
-   librbd: fix missing return statement if failed to get mirror image
    state ([issue#16600](http://tracker.ceph.com/issues/16600),
    [pr#10144](http://github.com/ceph/ceph/pull/10144), runsisi)
-   librbd: flag image as updated after proxying maintenance op
    ([issue#16404](http://tracker.ceph.com/issues/16404),
    [pr#9883](http://github.com/ceph/ceph/pull/9883), Jason Dillaman)
-   librbd: mkfs.xfs slow performance with discards and object map
    ([issue#16707](http://tracker.ceph.com/issues/16707),
    [issue#16689](http://tracker.ceph.com/issues/16689),
    [pr#10649](http://github.com/ceph/ceph/pull/10649), Jason Dillaman)
-   librbd: potential use after free on refresh error
    ([issue#16519](http://tracker.ceph.com/issues/16519),
    [pr#9952](http://github.com/ceph/ceph/pull/9952), Mykola Golub)
-   librbd: rbd-nbd does not properly handle resize notifications
    ([issue#15715](http://tracker.ceph.com/issues/15715),
    [pr#10679](http://github.com/ceph/ceph/pull/10679), Mykola Golub)
-   librbd: the option \'rbd_cache_writethrough_until_flush=true\'
    dosn\'t work ([issue#16740](http://tracker.ceph.com/issues/16740),
    [issue#16386](http://tracker.ceph.com/issues/16386),
    [issue#16708](http://tracker.ceph.com/issues/16708),
    [issue#16654](http://tracker.ceph.com/issues/16654),
    [issue#16478](http://tracker.ceph.com/issues/16478),
    [pr#10797](http://github.com/ceph/ceph/pull/10797), Mykola Golub,
    xinxin shu, Xiaowei Chen, Jason Dillaman)
-   mds: tell command blocks forever with async messenger
    (TestVolumeClient.test_evict_client failure)
    ([issue#16288](http://tracker.ceph.com/issues/16288),
    [pr#10501](http://github.com/ceph/ceph/pull/10501), Douglas Fuller)
-   mds: Confusing MDS log message when shut down with stalled journaler
    reads ([issue#15689](http://tracker.ceph.com/issues/15689),
    [pr#9557](http://github.com/ceph/ceph/pull/9557), John Spray)
-   mds: Deadlock on shutdown active rank while busy with metadata IO
    ([issue#16042](http://tracker.ceph.com/issues/16042),
    [pr#10502](http://github.com/ceph/ceph/pull/10502), Patrick
    Donnelly)
-   mds: Failing file operations on kernel based cephfs mount point
    leaves unaccessible file behind on hammer 0.94.7
    ([issue#16013](http://tracker.ceph.com/issues/16013),
    [pr#10199](http://github.com/ceph/ceph/pull/10199), Yan, Zheng)
-   mds: Fix shutting down mds timed-out due to deadlock
    ([issue#16396](http://tracker.ceph.com/issues/16396),
    [pr#10500](http://github.com/ceph/ceph/pull/10500), Zhi Zhang)
-   mds: MDSMonitor fixes
    ([issue#16136](http://tracker.ceph.com/issues/16136),
    [pr#9561](http://github.com/ceph/ceph/pull/9561), xie xingguo)
-   mds: MDSMonitor::check_subs() is very buggy
    ([issue#16022](http://tracker.ceph.com/issues/16022),
    [pr#10103](http://github.com/ceph/ceph/pull/10103), Yan, Zheng)
-   mds: <Session::check_access>() is buggy
    ([issue#16358](http://tracker.ceph.com/issues/16358),
    [pr#10105](http://github.com/ceph/ceph/pull/10105), Yan, Zheng)
-   mds: StrayManager.cc: 520: FAILED assert(dnl-\>is_primary())
    ([issue#15920](http://tracker.ceph.com/issues/15920),
    [pr#9559](http://github.com/ceph/ceph/pull/9559), Yan, Zheng)
-   mds: enforce a dirfrag limit on entries
    ([issue#16164](http://tracker.ceph.com/issues/16164),
    [pr#10104](http://github.com/ceph/ceph/pull/10104), Patrick
    Donnelly)
-   mds: fix SnapRealm::have_past_parents_open()
    ([issue#16299](http://tracker.ceph.com/issues/16299),
    [pr#10499](http://github.com/ceph/ceph/pull/10499), Yan, Zheng)
-   mds: fix getattr starve setattr
    ([issue#16154](http://tracker.ceph.com/issues/16154),
    [pr#9560](http://github.com/ceph/ceph/pull/9560), Yan, Zheng)
-   mds: wrongly treat symlink inode as normal file/dir when symlink
    inode is stale on kcephfs
    ([issue#15702](http://tracker.ceph.com/issues/15702),
    [pr#9405](http://github.com/ceph/ceph/pull/9405), Zhi Zhang)
-   mon: \"mon metadata\" fails when only one monitor exists
    ([issue#15866](http://tracker.ceph.com/issues/15866),
    [pr#10654](http://github.com/ceph/ceph/pull/10654), John Spray, Kefu
    Chai)
-   mon: Monitor: validate prefix on handle_command()
    ([issue#16297](http://tracker.ceph.com/issues/16297),
    [pr#10036](http://github.com/ceph/ceph/pull/10036), You Ji)
-   mon: OSDMonitor: drop pg temps from not the current primary
    ([issue#16127](http://tracker.ceph.com/issues/16127),
    [pr#9998](http://github.com/ceph/ceph/pull/9998), Samuel Just)
-   mon: prepare_pgtemp needs to only update up_thru if newer than the
    existing one ([issue#16185](http://tracker.ceph.com/issues/16185),
    [pr#10001](http://github.com/ceph/ceph/pull/10001), Samuel Just)
-   msgr: AsyncConnection::lockmsg/async lockdep cycle:
    AsyncMessenger::lock, MDSDaemon::mds_lock, AsyncConnection::lock
    ([issue#16237](http://tracker.ceph.com/issues/16237),
    [pr#10004](http://github.com/ceph/ceph/pull/10004), Haomai Wang)
-   msgr: async messenger mon crash
    ([issue#16378](http://tracker.ceph.com/issues/16378),
    [issue#16418](http://tracker.ceph.com/issues/16418),
    [pr#9996](http://github.com/ceph/ceph/pull/9996), Haomai Wang)
-   msgr: backports of all asyncmsgr fixes to jewel
    ([issue#15503](http://tracker.ceph.com/issues/15503),
    [issue#15372](http://tracker.ceph.com/issues/15372),
    [pr#9633](http://github.com/ceph/ceph/pull/9633), Yan Jun, Haomai
    Wang, Piotr Dałek)
-   msgr: msg/async: connection race hang
    ([issue#15849](http://tracker.ceph.com/issues/15849),
    [pr#10003](http://github.com/ceph/ceph/pull/10003), Haomai Wang)
-   osd: FileStore: umount hang because sync thread doesn\'t exit
    ([issue#15695](http://tracker.ceph.com/issues/15695),
    [pr#9105](http://github.com/ceph/ceph/pull/9105), Kefu Chai)
-   osd: Fixes for list-inconsistent-\*
    ([issue#15766](http://tracker.ceph.com/issues/15766),
    [issue#16192](http://tracker.ceph.com/issues/16192),
    [issue#15719](http://tracker.ceph.com/issues/15719),
    [pr#9565](http://github.com/ceph/ceph/pull/9565), David Zafman)
-   osd: New pools have bogus stuck inactive/unclean HEALTH_ERR messages
    until they are first active and clean
    ([issue#14952](http://tracker.ceph.com/issues/14952),
    [pr#10007](http://github.com/ceph/ceph/pull/10007), Sage Weil)
-   osd: OSD crash with Hammer to Jewel Upgrade: void
    FileStore::init_temp_collections()
    ([issue#16672](http://tracker.ceph.com/issues/16672),
    [pr#10561](http://github.com/ceph/ceph/pull/10561), David Zafman)
-   osd: OSD failed to subscribe skipped osdmaps after ceph osd pause
    ([issue#17023](http://tracker.ceph.com/issues/17023),
    [pr#10804](http://github.com/ceph/ceph/pull/10804), Kefu Chai)
-   osd: ObjectCacher split BufferHead read fix
    ([issue#16002](http://tracker.ceph.com/issues/16002),
    [pr#10074](http://github.com/ceph/ceph/pull/10074), Greg Farnum)
-   osd: ReplicatedBackend doesn\'t increment stats on pull, only push
    ([issue#16277](http://tracker.ceph.com/issues/16277),
    [pr#10421](http://github.com/ceph/ceph/pull/10421), Kefu Chai)
-   osd: Scrub error: 0/1 pinned
    ([issue#15952](http://tracker.ceph.com/issues/15952),
    [pr#9576](http://github.com/ceph/ceph/pull/9576), Samuel Just)
-   osd: crash adding snap to purged_snaps in
    ReplicatedPG::WaitingOnReplicas
    ([issue#15943](http://tracker.ceph.com/issues/15943),
    [pr#9575](http://github.com/ceph/ceph/pull/9575), Samuel Just)
-   osd: partprobe intermittent issues during ceph-disk prepare
    ([issue#15176](http://tracker.ceph.com/issues/15176),
    [pr#10497](http://github.com/ceph/ceph/pull/10497), Marius Vollmer,
    Loic Dachary)
-   osd: saw valgrind issues in ReplicatedPG::new_repop
    ([issue#16801](http://tracker.ceph.com/issues/16801),
    [pr#10760](http://github.com/ceph/ceph/pull/10760), Kefu Chai)
-   osd: sparse_read on ec pool should return extends with correct
    offset ([issue#16138](http://tracker.ceph.com/issues/16138),
    [pr#10006](http://github.com/ceph/ceph/pull/10006), kofiliu)
-   osd:sched_time not actually randomized
    ([issue#15890](http://tracker.ceph.com/issues/15890),
    [pr#9578](http://github.com/ceph/ceph/pull/9578), xie xingguo)
-   rbd: ImageReplayer::is_replaying does not include flush state
    ([issue#16970](http://tracker.ceph.com/issues/16970),
    [pr#10790](http://github.com/ceph/ceph/pull/10790), Jason Dillaman)
-   rbd: Journal duplicate op detection can cause lockdep error
    ([issue#16363](http://tracker.ceph.com/issues/16363),
    [pr#10044](http://github.com/ceph/ceph/pull/10044), Jason Dillaman)
-   rbd: Journal needs to handle duplicate maintenance op tids
    ([issue#16362](http://tracker.ceph.com/issues/16362),
    [pr#10045](http://github.com/ceph/ceph/pull/10045), Jason Dillaman)
-   rbd: Unable to disable journaling feature if in unexpected mirror
    state ([issue#16348](http://tracker.ceph.com/issues/16348),
    [pr#10042](http://github.com/ceph/ceph/pull/10042), Jason Dillaman)
-   rbd: bashism in src/rbdmap
    ([issue#16608](http://tracker.ceph.com/issues/16608),
    [pr#10786](http://github.com/ceph/ceph/pull/10786), Jason Dillaman)
-   rbd: doc: format 2 now is the default image format
    ([issue#17026](http://tracker.ceph.com/issues/17026),
    [pr#10732](http://github.com/ceph/ceph/pull/10732), Chengwei Yang)
-   rbd: hen journaling is enabled, a flush request shouldn\'t flush the
    cache ([issue#15761](http://tracker.ceph.com/issues/15761),
    [pr#10041](http://github.com/ceph/ceph/pull/10041), Yuan Zhou)
-   rbd: possible race condition during journal transition from replay
    to ready ([issue#16198](http://tracker.ceph.com/issues/16198),
    [pr#10047](http://github.com/ceph/ceph/pull/10047), Jason Dillaman)
-   rbd: qa/workunits/rbd: respect RBD_CREATE_ARGS environment variable
    ([issue#16289](http://tracker.ceph.com/issues/16289),
    [pr#9721](http://github.com/ceph/ceph/pull/9721), Mykola Golub)
-   rbd: rbd-mirror should disable proxied maintenance ops for
    non-primary image
    ([issue#16411](http://tracker.ceph.com/issues/16411),
    [pr#10050](http://github.com/ceph/ceph/pull/10050), Jason Dillaman)
-   rbd: rbd-mirror: FAILED assert(m_local_image_ctx-\>object_map !=
    nullptr) ([issue#16558](http://tracker.ceph.com/issues/16558),
    [pr#10646](http://github.com/ceph/ceph/pull/10646), Jason Dillaman)
-   rbd: rbd-mirror: FAILED assert(m_on_update_status_finish == nullptr)
    ([issue#16956](http://tracker.ceph.com/issues/16956),
    [pr#10792](http://github.com/ceph/ceph/pull/10792), Jason Dillaman)
-   rbd: rbd-mirror: FAILED assert(m_state == STATE_STOPPING)
    ([issue#16980](http://tracker.ceph.com/issues/16980),
    [pr#10791](http://github.com/ceph/ceph/pull/10791), Jason Dillaman)
-   rbd: rbd-mirror: ensure replay status formatter has completed before
    stopping replay
    ([issue#16352](http://tracker.ceph.com/issues/16352),
    [pr#10043](http://github.com/ceph/ceph/pull/10043), Jason Dillaman)
-   rbd: rbd-mirror: include local pool id in resync throttle unique key
    ([issue#16536](http://tracker.ceph.com/issues/16536),
    [issue#15239](http://tracker.ceph.com/issues/15239),
    [issue#16488](http://tracker.ceph.com/issues/16488),
    [issue#16491](http://tracker.ceph.com/issues/16491),
    [issue#16329](http://tracker.ceph.com/issues/16329),
    [issue#15108](http://tracker.ceph.com/issues/15108),
    [issue#15670](http://tracker.ceph.com/issues/15670),
    [pr#10678](http://github.com/ceph/ceph/pull/10678), Ricardo Dias,
    Jason Dillaman)
-   rbd: rbd-mirror: potential race condition accessing local image
    journal ([issue#16230](http://tracker.ceph.com/issues/16230),
    [pr#10046](http://github.com/ceph/ceph/pull/10046), Jason Dillaman)
-   rbd: rbd-mirror: reduce memory footprint during journal replay
    ([issue#16321](http://tracker.ceph.com/issues/16321),
    [issue#16489](http://tracker.ceph.com/issues/16489),
    [issue#16622](http://tracker.ceph.com/issues/16622),
    [issue#16539](http://tracker.ceph.com/issues/16539),
    [issue#16223](http://tracker.ceph.com/issues/16223),
    [issue#16349](http://tracker.ceph.com/issues/16349),
    [pr#10684](http://github.com/ceph/ceph/pull/10684), Mykola Golub,
    Jason Dillaman)
-   rgw: A query on a static large object fails with 404 error
    ([issue#16015](http://tracker.ceph.com/issues/16015),
    [pr#9544](http://github.com/ceph/ceph/pull/9544), Radoslaw
    Zarzynski)
-   rgw: Add zone rename to radosgw_admin
    ([issue#16934](http://tracker.ceph.com/issues/16934),
    [pr#10663](http://github.com/ceph/ceph/pull/10663), Shilpa
    Jagannath)
-   rgw: Bucket index shards orphaned after bucket delete
    ([issue#16412](http://tracker.ceph.com/issues/16412),
    [pr#10525](http://github.com/ceph/ceph/pull/10525), Orit Wasserman)
-   rgw: Bug when using port 443s in rgw.
    ([issue#16548](http://tracker.ceph.com/issues/16548),
    [pr#10664](http://github.com/ceph/ceph/pull/10664), Pritha
    Srivastava)
-   rgw: Fallback to Host header for bucket name.
    ([issue#15975](http://tracker.ceph.com/issues/15975),
    [pr#10693](http://github.com/ceph/ceph/pull/10693), Robin H.
    Johnson)
-   rgw: Fix civetweb IPv6
    ([issue#16928](http://tracker.ceph.com/issues/16928),
    [pr#10580](http://github.com/ceph/ceph/pull/10580), Robin H.
    Johnson)
-   rgw: Increase log level for messages occuring while running rgw
    admin command ([issue#16935](http://tracker.ceph.com/issues/16935),
    [pr#10765](http://github.com/ceph/ceph/pull/10765), Shilpa
    Jagannath)
-   rgw: No Last-Modified, Content-Size and X-Object-Manifest headers if
    no segments in DLO manifest
    ([issue#15812](http://tracker.ceph.com/issues/15812),
    [pr#9265](http://github.com/ceph/ceph/pull/9265), Radoslaw
    Zarzynski)
-   rgw: RGWPeriodPuller tries to pull from itself
    ([issue#16939](http://tracker.ceph.com/issues/16939),
    [pr#10764](http://github.com/ceph/ceph/pull/10764), Casey Bodley)
-   rgw: Set Access-Control-Allow-Origin to a Asterisk if allowed in a
    rule ([issue#15348](http://tracker.ceph.com/issues/15348),
    [pr#9453](http://github.com/ceph/ceph/pull/9453), Wido den
    Hollander)
-   rgw: Swift API returns double space usage and objects of account
    metadata ([issue#16188](http://tracker.ceph.com/issues/16188),
    [pr#10148](http://github.com/ceph/ceph/pull/10148), Albert Tu)
-   rgw: account/container metadata not actually present in a request
    are deleted during POST through Swift API
    ([issue#15977](http://tracker.ceph.com/issues/15977),
    [issue#15779](http://tracker.ceph.com/issues/15779),
    [pr#9542](http://github.com/ceph/ceph/pull/9542), Radoslaw
    Zarzynski)
-   rgw: add socket backlog setting for via ceph.conf
    ([issue#16406](http://tracker.ceph.com/issues/16406),
    [pr#10216](http://github.com/ceph/ceph/pull/10216), Feng Guo)
-   rgw: add tenant support to multisite sync
    ([issue#16469](http://tracker.ceph.com/issues/16469),
    [issue#16121](http://tracker.ceph.com/issues/16121),
    [issue#16665](http://tracker.ceph.com/issues/16665),
    [pr#10845](http://github.com/ceph/ceph/pull/10845), Yehuda Sadeh,
    Josh Durgin, Casey Bodley, Pritha Srivastava)
-   rgw: add_zone only clears master_zone if \--master=false
    ([issue#15901](http://tracker.ceph.com/issues/15901),
    [pr#9327](http://github.com/ceph/ceph/pull/9327), Casey Bodley)
-   rgw: aws4 parsing issue
    ([issue#15940](http://tracker.ceph.com/issues/15940),
    [issue#15939](http://tracker.ceph.com/issues/15939),
    [pr#9545](http://github.com/ceph/ceph/pull/9545), Yehuda Sadeh)
-   rgw: aws4: add STREAMING-AWS4-HMAC-SHA256-PAYLOAD support
    ([issue#16146](http://tracker.ceph.com/issues/16146),
    [pr#10167](http://github.com/ceph/ceph/pull/10167), Radoslaw
    Zarzynski, Javier M. Mellid)
-   rgw: backport merge of static sites fixes
    ([issue#15555](http://tracker.ceph.com/issues/15555),
    [issue#15532](http://tracker.ceph.com/issues/15532),
    [issue#15531](http://tracker.ceph.com/issues/15531),
    [pr#9568](http://github.com/ceph/ceph/pull/9568), Robin H. Johnson)
-   rgw: can set negative max_buckets on RGWUserInfo
    ([issue#14534](http://tracker.ceph.com/issues/14534),
    [pr#10655](http://github.com/ceph/ceph/pull/10655), Yehuda Sadeh)
-   rgw: cleanup radosgw-admin temp command as it was deprecated
    ([issue#16023](http://tracker.ceph.com/issues/16023),
    [pr#9390](http://github.com/ceph/ceph/pull/9390), Vikhyat Umrao)
-   rgw: comparing return code to ERR_NOT_MODIFIED in rgw_rest_s3.cc
    (needs minus sign)
    ([issue#16327](http://tracker.ceph.com/issues/16327),
    [pr#9790](http://github.com/ceph/ceph/pull/9790), Nathan Cutler)
-   rgw: custom metadata aren\'t camelcased in Swift\'s responses
    ([issue#15902](http://tracker.ceph.com/issues/15902),
    [pr#9267](http://github.com/ceph/ceph/pull/9267), Radoslaw
    Zarzynski)
-   rgw: data sync stops after getting error in all data log sync shards
    ([issue#16530](http://tracker.ceph.com/issues/16530),
    [pr#10073](http://github.com/ceph/ceph/pull/10073), Yehuda Sadeh)
-   rgw: default zone and zonegroup cannot be added to a realm
    ([issue#16839](http://tracker.ceph.com/issues/16839),
    [pr#10658](http://github.com/ceph/ceph/pull/10658), Casey Bodley)
-   rgw: document multi tenancy
    ([issue#16635](http://tracker.ceph.com/issues/16635),
    [pr#10217](http://github.com/ceph/ceph/pull/10217), Pete Zaitcev)
-   rgw: don\'t unregister request if request is not connected to
    manager ([issue#15911](http://tracker.ceph.com/issues/15911),
    [pr#9242](http://github.com/ceph/ceph/pull/9242), Yehuda Sadeh)
-   rgw: failed to create bucket after upgrade from hammer to jewel
    ([issue#16627](http://tracker.ceph.com/issues/16627),
    [pr#10524](http://github.com/ceph/ceph/pull/10524), Orit Wasserman)
-   rgw: fix ldap bindpw parsing
    ([issue#16286](http://tracker.ceph.com/issues/16286),
    [pr#10518](http://github.com/ceph/ceph/pull/10518), Matt Benjamin)
-   rgw: fix multi-delete query param parsing.
    ([issue#16618](http://tracker.ceph.com/issues/16618),
    [pr#10188](http://github.com/ceph/ceph/pull/10188), Robin H.
    Johnson)
-   rgw: improve support for Swift\'s object versioning.
    ([issue#15925](http://tracker.ceph.com/issues/15925),
    [pr#10710](http://github.com/ceph/ceph/pull/10710), Radoslaw
    Zarzynski)
-   rgw: initial slashes are not properly handled in Swift\'s BulkDelete
    ([issue#15948](http://tracker.ceph.com/issues/15948),
    [pr#9316](http://github.com/ceph/ceph/pull/9316), Radoslaw
    Zarzynski)
-   rgw: master: build failures with boost \> 1.58
    ([issue#16392](http://tracker.ceph.com/issues/16392),
    [issue#16391](http://tracker.ceph.com/issues/16391),
    [pr#10026](http://github.com/ceph/ceph/pull/10026), Abhishek
    Lekshmanan)
-   rgw: multisite segfault on \~RGWRealmWatcher if realm was deleted
    ([issue#16817](http://tracker.ceph.com/issues/16817),
    [pr#10660](http://github.com/ceph/ceph/pull/10660), Casey Bodley)
-   rgw: multisite sync races with deletes
    ([issue#16222](http://tracker.ceph.com/issues/16222),
    [issue#16464](http://tracker.ceph.com/issues/16464),
    [issue#16220](http://tracker.ceph.com/issues/16220),
    [issue#16143](http://tracker.ceph.com/issues/16143),
    [pr#10293](http://github.com/ceph/ceph/pull/10293), Yehuda Sadeh,
    Casey Bodley)
-   rgw: multisite: preserve zone\'s extra pool
    ([issue#16712](http://tracker.ceph.com/issues/16712),
    [pr#10537](http://github.com/ceph/ceph/pull/10537), Abhishek
    Lekshmanan)
-   rgw: object expirer\'s hints might be trimmed without processing in
    some circumstances
    ([issue#16705](http://tracker.ceph.com/issues/16705),
    [issue#16684](http://tracker.ceph.com/issues/16684),
    [pr#10763](http://github.com/ceph/ceph/pull/10763), Radoslaw
    Zarzynski)
-   rgw: radosgw-admin failure for user create after upgrade from hammer
    to jewel ([issue#15937](http://tracker.ceph.com/issues/15937),
    [pr#9294](http://github.com/ceph/ceph/pull/9294), Orit Wasserman,
    Abhishek Lekshmanan)
-   rgw: radosgw-admin: EEXIST messages for create operations
    ([issue#15720](http://tracker.ceph.com/issues/15720),
    [pr#9268](http://github.com/ceph/ceph/pull/9268), Abhishek
    Lekshmanan)
-   rgw: radosgw-admin: inconsistency in uid/email handling
    ([issue#13598](http://tracker.ceph.com/issues/13598),
    [pr#10520](http://github.com/ceph/ceph/pull/10520), Matt Benjamin)
-   rgw: realm pull fails when using apache frontend
    ([issue#15846](http://tracker.ceph.com/issues/15846),
    [pr#9266](http://github.com/ceph/ceph/pull/9266), Orit Wasserman)
-   rgw: retry on bucket sync errors
    ([issue#16108](http://tracker.ceph.com/issues/16108),
    [pr#9425](http://github.com/ceph/ceph/pull/9425), Yehuda Sadeh)
-   rgw: s3website: x-amz-website-redirect-location header returns
    malformed HTTP response
    ([issue#15531](http://tracker.ceph.com/issues/15531),
    [pr#9099](http://github.com/ceph/ceph/pull/9099), Robin H. Johnson)
-   rgw: segfault in RGWOp_MDLog_Notify
    ([issue#16666](http://tracker.ceph.com/issues/16666),
    [pr#10662](http://github.com/ceph/ceph/pull/10662), Casey Bodley)
-   rgw: segmentation fault on error_repo in data sync
    ([issue#16603](http://tracker.ceph.com/issues/16603),
    [pr#10523](http://github.com/ceph/ceph/pull/10523), Casey Bodley)
-   rgw: selinux denials in RGW
    ([issue#16126](http://tracker.ceph.com/issues/16126),
    [pr#10519](http://github.com/ceph/ceph/pull/10519), Boris Ranto)
-   rgw: support size suffixes for \--max-size in radosgw-admin command
    ([issue#16004](http://tracker.ceph.com/issues/16004),
    [pr#9743](http://github.com/ceph/ceph/pull/9743), Vikhyat Umrao)
-   rgw: updating CORS/ACLs might not work in some circumstances
    ([issue#15976](http://tracker.ceph.com/issues/15976),
    [pr#9543](http://github.com/ceph/ceph/pull/9543), Radoslaw
    Zarzynski)
-   rgw: use zone endpoints instead of zonegroup endpoints
    ([issue#16834](http://tracker.ceph.com/issues/16834),
    [pr#10659](http://github.com/ceph/ceph/pull/10659), Casey Bodley)
-   tests: improve rbd-mirror test case coverage
    ([issue#16197](http://tracker.ceph.com/issues/16197),
    [pr#9631](http://github.com/ceph/ceph/pull/9631), Mykola Golub,
    Jason Dillaman)
-   tests: rados/test.sh workunit timesout on OpenStack
    ([issue#15403](http://tracker.ceph.com/issues/15403),
    [pr#8904](http://github.com/ceph/ceph/pull/8904), Loic Dachary)
-   tools: ceph-disk: Accept bcache devices as data disks
    ([issue#13278](http://tracker.ceph.com/issues/13278),
    [pr#8497](http://github.com/ceph/ceph/pull/8497), Peter Sabaini)
-   tools: rados: Add cleanup message with time to rados bench output
    ([issue#15704](http://tracker.ceph.com/issues/15704),
    [pr#9740](http://github.com/ceph/ceph/pull/9740), Vikhyat Umrao)
-   tools: src/script/subman fails with KeyError: \'nband\'
    ([issue#16961](http://tracker.ceph.com/issues/16961),
    [pr#10625](http://github.com/ceph/ceph/pull/10625), Loic Dachary,
    Ali Maredia)

## v10.2.2 Jewel

This point release fixes several important bugs in RBD mirroring, RGW
multi-site, CephFS, and RADOS.

We recommend that all v10.2.x users upgrade.

For more detailed information, see
`the complete changelog <../changelog/v10.2.2.txt>`{.interpreted-text
role="download"}.

### Notable Changes

-   ceph: cli: exception when pool name has non-ascii characters
    ([issue#15913](http://tracker.ceph.com/issues/15913),
    [pr#9320](http://github.com/ceph/ceph/pull/9320), Ricardo Dias)
-   ceph-disk: workaround gperftool hang
    ([issue#13522](http://tracker.ceph.com/issues/13522),
    [issue#16103](http://tracker.ceph.com/issues/16103),
    [pr#9427](http://github.com/ceph/ceph/pull/9427), Loic Dachary)
-   cephfs: backports needed for Manila
    ([issue#15599](http://tracker.ceph.com/issues/15599),
    [issue#15417](http://tracker.ceph.com/issues/15417),
    [issue#15045](http://tracker.ceph.com/issues/15045),
    [pr#9430](http://github.com/ceph/ceph/pull/9430), John Spray, Ramana
    Raja, Xiaoxi Chen)
-   ceph.spec.in: drop support for RHEL\<7 and SUSE\<1210 in jewel and
    above ([issue#15725](http://tracker.ceph.com/issues/15725),
    [issue#15627](http://tracker.ceph.com/issues/15627),
    [issue#13445](http://tracker.ceph.com/issues/13445),
    [issue#15822](http://tracker.ceph.com/issues/15822),
    [issue#15472](http://tracker.ceph.com/issues/15472),
    [issue#15987](http://tracker.ceph.com/issues/15987),
    [issue#15516](http://tracker.ceph.com/issues/15516),
    [issue#15549](http://tracker.ceph.com/issues/15549),
    [pr#8938](http://github.com/ceph/ceph/pull/8938), Boris Ranto, Sage
    Weil, Nathan Cutler, Lars Marowsky-Bree)
-   ceph_test_librbd_fsx crashes during journal replay shut down
    ([issue#16123](http://tracker.ceph.com/issues/16123),
    [pr#9556](http://github.com/ceph/ceph/pull/9556), Jason Dillaman)
-   client: fix bugs accidentally disabling readahead
    ([issue#16024](http://tracker.ceph.com/issues/16024),
    [pr#9656](http://github.com/ceph/ceph/pull/9656), Patrick Donnelly,
    Greg Farnum)
-   cls_journal: initialize empty commit position upon client register
    ([issue#15757](http://tracker.ceph.com/issues/15757),
    [pr#9376](http://github.com/ceph/ceph/pull/9376), runsisi, Venky
    Shankar)
-   cls::rbd: mirror_image_status_list returned max 64 items
    ([pr#9069](http://github.com/ceph/ceph/pull/9069), Mykola Golub)
-   cls_rbd: mirror image status summary should read full directory
    ([issue#16178](http://tracker.ceph.com/issues/16178),
    [pr#9608](http://github.com/ceph/ceph/pull/9608), Jason Dillaman)
-   common: BackoffThrottle spins unnecessarily with very small backoff
    while the throttle is full
    ([issue#15953](http://tracker.ceph.com/issues/15953),
    [pr#9579](http://github.com/ceph/ceph/pull/9579), Samuel Just)
-   common: Do not link lttng into libglobal
    ([pr#9194](http://github.com/ceph/ceph/pull/9194), Karol Mroz)
-   debian: install systemd target files
    ([issue#15573](http://tracker.ceph.com/issues/15573),
    [pr#8815](http://github.com/ceph/ceph/pull/8815), Kefu Chai, Sage
    Weil)
-   doc: update mirroring guide to include pool/image status commands
    ([issue#15746](http://tracker.ceph.com/issues/15746),
    [pr#9180](http://github.com/ceph/ceph/pull/9180), Mykola Golub)
-   librbd: Disabling journaling feature results in \"Transport endpoint
    is not connected\" error
    ([issue#15863](http://tracker.ceph.com/issues/15863),
    [pr#9548](http://github.com/ceph/ceph/pull/9548), Yuan Zhou)
-   librbd: do not shut down exclusive lock while acquiring\'
    ([issue#16291](http://tracker.ceph.com/issues/16291),
    [issue#16260](http://tracker.ceph.com/issues/16260),
    [pr#9691](http://github.com/ceph/ceph/pull/9691), Jason Dillaman)
-   librbd: Initial python APIs to support mirroring
    ([issue#15656](http://tracker.ceph.com/issues/15656),
    [pr#9550](http://github.com/ceph/ceph/pull/9550), Mykola Golub)
-   librbd: journal IO error results in failed assertion in
    AioCompletion ([issue#16077](http://tracker.ceph.com/issues/16077),
    [issue#15034](http://tracker.ceph.com/issues/15034),
    [issue#15791](http://tracker.ceph.com/issues/15791),
    [pr#9611](http://github.com/ceph/ceph/pull/9611), Hector Martin,
    Jason Dillaman)
-   librbd: journal: live replay might skip entries from previous object
    set ([issue#15864](http://tracker.ceph.com/issues/15864),
    [issue#15665](http://tracker.ceph.com/issues/15665),
    [pr#9217](http://github.com/ceph/ceph/pull/9217), Jason Dillaman)
-   librbd: journal: support asynchronous shutdown
    ([issue#15949](http://tracker.ceph.com/issues/15949),
    [issue#14530](http://tracker.ceph.com/issues/14530),
    [issue#15993](http://tracker.ceph.com/issues/15993),
    [pr#9373](http://github.com/ceph/ceph/pull/9373), Jason Dillaman)
-   librbd: Metadata config overrides are applied synchronously
    ([issue#15928](http://tracker.ceph.com/issues/15928),
    [pr#9318](http://github.com/ceph/ceph/pull/9318), Jason Dillaman)
-   librbd: Object Map is showing as invalid, even when Object Map is
    disabled for that Image.
    ([issue#16076](http://tracker.ceph.com/issues/16076),
    [pr#9555](http://github.com/ceph/ceph/pull/9555), xinxin shu)
-   librbd: prevent error messages when journal externally disabled
    ([issue#16114](http://tracker.ceph.com/issues/16114),
    [pr#9610](http://github.com/ceph/ceph/pull/9610), Zhiqiang Wang,
    Jason Dillaman)
-   librbd: recursive lock possible when disabling journaling
    ([issue#16235](http://tracker.ceph.com/issues/16235),
    [pr#9654](http://github.com/ceph/ceph/pull/9654), Jason Dillaman)
-   librbd: refresh image if needed in mirror functions
    ([issue#16096](http://tracker.ceph.com/issues/16096),
    [pr#9609](http://github.com/ceph/ceph/pull/9609), Jon Bernard)
-   librbd: remove should ignore mirror errors from older OSDs
    ([issue#16268](http://tracker.ceph.com/issues/16268),
    [pr#9692](http://github.com/ceph/ceph/pull/9692), Jason Dillaman)
-   librbd: reuse ImageCtx::finisher and SafeTimer for lots of images
    case ([issue#13938](http://tracker.ceph.com/issues/13938),
    [pr#9580](http://github.com/ceph/ceph/pull/9580), Haomai Wang)
-   librbd: validate image metadata configuration overrides
    ([issue#15522](http://tracker.ceph.com/issues/15522),
    [pr#9554](http://github.com/ceph/ceph/pull/9554), zhuangzeqiang)
-   mds: order directories by hash and fix simultaneous readdir races
    ([issue#15508](http://tracker.ceph.com/issues/15508),
    [pr#9655](http://github.com/ceph/ceph/pull/9655), Yan, Zheng, Greg
    Farnum)
-   mon: Hammer (0.94.3) OSD does not delete old OSD Maps in a timely
    fashion (maybe at all?)
    ([issue#13990](http://tracker.ceph.com/issues/13990),
    [pr#9100](http://github.com/ceph/ceph/pull/9100), Kefu Chai)
-   mon/Monitor: memory leak on Monitor::handle_ping()
    ([issue#15793](http://tracker.ceph.com/issues/15793),
    [pr#9270](http://github.com/ceph/ceph/pull/9270), xie xingguo)
-   osd: acting_primary not updated on split
    ([issue#15523](http://tracker.ceph.com/issues/15523),
    [pr#8968](http://github.com/ceph/ceph/pull/8968), Sage Weil)
-   osd: boot race with noup being set
    ([issue#15678](http://tracker.ceph.com/issues/15678),
    [pr#9101](http://github.com/ceph/ceph/pull/9101), Sage Weil)
-   osd: deadlock in OSD::\_committed_osd_maps
    ([issue#15701](http://tracker.ceph.com/issues/15701),
    [pr#9103](http://github.com/ceph/ceph/pull/9103), Xinze Chi)
-   osd: hobject_t::get_max() vs is_max() discrepancy
    ([issue#16113](http://tracker.ceph.com/issues/16113),
    [pr#9614](http://github.com/ceph/ceph/pull/9614), Samuel Just)
-   osd:
    LibRadosWatchNotifyPPTests/LibRadosWatchNotifyPP.WatchNotify2Timeout/1
    segv ([issue#15760](http://tracker.ceph.com/issues/15760),
    [pr#9104](http://github.com/ceph/ceph/pull/9104), Sage Weil)
-   osd: remove reliance on FLAG_OMAP for reads
    ([pr#9638](http://github.com/ceph/ceph/pull/9638), Samuel Just)
-   osd valgrind invalid reads/writes
    ([issue#15870](http://tracker.ceph.com/issues/15870),
    [pr#9237](http://github.com/ceph/ceph/pull/9237), Samuel Just)
-   pybind: rbd API should default features parameter to None
    ([issue#15982](http://tracker.ceph.com/issues/15982),
    [pr#9553](http://github.com/ceph/ceph/pull/9553), Mykola Golub)
-   qa: dynamic_features.sh races with image deletion
    ([issue#15500](http://tracker.ceph.com/issues/15500),
    [pr#9552](http://github.com/ceph/ceph/pull/9552), Mykola Golub)
-   qa/workunits: ensure replay has started before checking position
    ([issue#16248](http://tracker.ceph.com/issues/16248),
    [pr#9674](http://github.com/ceph/ceph/pull/9674), Jason Dillaman)
-   qa/workunits/rbd: fixed rbd_mirror teuthology runtime errors
    ([pr#9232](http://github.com/ceph/ceph/pull/9232), Jason Dillaman)
-   radosgw-admin: fix \'period push\' handling of \--url
    ([issue#15926](http://tracker.ceph.com/issues/15926),
    [pr#9210](http://github.com/ceph/ceph/pull/9210), Casey Bodley)
-   rbd-mirror: Delete local image mirror when remote image mirroring is
    disabled ([issue#15916](http://tracker.ceph.com/issues/15916),
    [issue#14421](http://tracker.ceph.com/issues/14421),
    [pr#9372](http://github.com/ceph/ceph/pull/9372), runsisi, Mykola
    Golub, Ricardo Dias)
-   rbd-mirror: do not propagate deletions when pool unavailable
    ([issue#16229](http://tracker.ceph.com/issues/16229),
    [pr#9630](http://github.com/ceph/ceph/pull/9630), Jason Dillaman)
-   rbd-mirror: do not re-use image id from mirror directory if creating
    image ([issue#16253](http://tracker.ceph.com/issues/16253),
    [pr#9673](http://github.com/ceph/ceph/pull/9673), Jason Dillaman)
-   rbd-mirror: FAILED assert(!m_status_watcher)
    ([issue#16245](http://tracker.ceph.com/issues/16245),
    [issue#16290](http://tracker.ceph.com/issues/16290),
    [pr#9690](http://github.com/ceph/ceph/pull/9690), Mykola Golub)
-   rbd-mirror: fix deletion propagation edge cases
    ([issue#16226](http://tracker.ceph.com/issues/16226),
    [pr#9629](http://github.com/ceph/ceph/pull/9629), Jason Dillaman)
-   rbd-mirror: fix journal shut down ordering
    ([issue#16165](http://tracker.ceph.com/issues/16165),
    [pr#9628](http://github.com/ceph/ceph/pull/9628), Jason Dillaman)
-   rbd-mirror: potential crash during image status update
    ([issue#15909](http://tracker.ceph.com/issues/15909),
    [pr#9226](http://github.com/ceph/ceph/pull/9226), Mykola Golub,
    Jason Dillaman)
-   rbd-mirror: refresh image after creating sync point
    ([issue#16196](http://tracker.ceph.com/issues/16196),
    [pr#9627](http://github.com/ceph/ceph/pull/9627), Jason Dillaman)
-   rbd-mirror: replicate cloned images
    ([issue#14937](http://tracker.ceph.com/issues/14937),
    [pr#9423](http://github.com/ceph/ceph/pull/9423), Jason Dillaman)
-   rbd-mirror should disable the rbd cache for local images
    ([issue#15930](http://tracker.ceph.com/issues/15930),
    [pr#9317](http://github.com/ceph/ceph/pull/9317), Jason Dillaman)
-   rbd-mirror: support bootstrap canceling
    ([issue#16201](http://tracker.ceph.com/issues/16201),
    [pr#9612](http://github.com/ceph/ceph/pull/9612), Mykola Golub)
-   rbd-mirror: support multiple replicated pools
    ([issue#16045](http://tracker.ceph.com/issues/16045),
    [pr#9409](http://github.com/ceph/ceph/pull/9409), Jason Dillaman)
-   rgw: fix manager selection when APIs customized
    ([issue#15974](http://tracker.ceph.com/issues/15974),
    [issue#15973](http://tracker.ceph.com/issues/15973),
    [pr#9245](http://github.com/ceph/ceph/pull/9245), Robin H. Johnson)
-   rgw: keep track of written_objs correctly
    ([issue#15886](http://tracker.ceph.com/issues/15886),
    [pr#9239](http://github.com/ceph/ceph/pull/9239), Yehuda Sadeh)
-   rpm: ceph gid mismatch on upgrade from hammer with pre-existing ceph
    user (SUSE) ([issue#15869](http://tracker.ceph.com/issues/15869),
    [pr#9424](http://github.com/ceph/ceph/pull/9424), Nathan Cutler)
-   systemd: ceph-{mds,mon,osd,radosgw} systemd unit files need
    wants=time-sync.target
    ([issue#15419](http://tracker.ceph.com/issues/15419),
    [pr#8802](http://github.com/ceph/ceph/pull/8802), Nathan Cutler)
-   test: failure in journal.sh workunit test
    ([issue#16011](http://tracker.ceph.com/issues/16011),
    [pr#9377](http://github.com/ceph/ceph/pull/9377), Mykola Golub)
-   tests: rm -fr /tmp/\*virtualenv\*
    ([issue#16087](http://tracker.ceph.com/issues/16087),
    [pr#9403](http://github.com/ceph/ceph/pull/9403), Loic Dachary)

## v10.2.1 Jewel

This is the first bugfix release for Jewel. It contains several annoying
packaging and init system fixes and a range of important bugfixes across
RBD, RGW, and CephFS.

We recommend that all v10.2.x users upgrade.

For more detailed information, see
`the complete changelog <../changelog/v10.2.1.txt>`{.interpreted-text
role="download"}.

### Notable Changes

-   cephfs: CephFSVolumeClient should isolate volumes by RADOS namespace
    ([issue#15400](http://tracker.ceph.com/issues/15400),
    [pr#8787](http://github.com/ceph/ceph/pull/8787), Xiaoxi Chen)
-   cephfs: handle standby-replay nodes properly in upgrades
    ([issue#15591](http://tracker.ceph.com/issues/15591),
    [pr#8971](http://github.com/ceph/ceph/pull/8971), John Spray)
-   ceph-{mds,mon,osd} packages need scriptlets with systemd code
    ([issue#14941](http://tracker.ceph.com/issues/14941),
    [pr#8801](http://github.com/ceph/ceph/pull/8801), Boris Ranto,
    Nathan Cutler)
-   ceph_test_keyvaluedb: fix
    ([issue#15435](http://tracker.ceph.com/issues/15435),
    [pr#9051](http://github.com/ceph/ceph/pull/9051), Allen Samuels,
    Sage Weil)
-   cmake: add missing source file to rbd_mirror/image_replayer
    ([pr#9052](http://github.com/ceph/ceph/pull/9052), Casey Bodley)
-   cmake: fix rbd compile errors
    ([pr#9076](http://github.com/ceph/ceph/pull/9076), runsisi, Jason
    Dillaman)
-   journal: incorrectly computed object offset within set
    ([issue#15765](http://tracker.ceph.com/issues/15765),
    [pr#9038](http://github.com/ceph/ceph/pull/9038), Jason Dillaman)
-   librbd: client-side handling for incompatible object map sizes
    ([issue#15642](http://tracker.ceph.com/issues/15642),
    [pr#9039](http://github.com/ceph/ceph/pull/9039), Jason Dillaman)
-   librbd: constrain size of AioWriteEvent journal entries
    ([issue#15750](http://tracker.ceph.com/issues/15750),
    [pr#9048](http://github.com/ceph/ceph/pull/9048), Jason Dillaman)
-   librbd: does not crash if image header is too short
    ([pr#9044](http://github.com/ceph/ceph/pull/9044), Kefu Chai)
-   librbd: Errors encountered disabling object-map while flatten is
    in-progress ([issue#15572](http://tracker.ceph.com/issues/15572),
    [pr#8869](http://github.com/ceph/ceph/pull/8869), Jason Dillaman)
-   librbd: fix get/list mirror image status API
    ([issue#15771](http://tracker.ceph.com/issues/15771),
    [pr#9036](http://github.com/ceph/ceph/pull/9036), Mykola Golub)
-   librbd: Parent image is closed twice if error encountered while
    opening ([issue#15574](http://tracker.ceph.com/issues/15574),
    [pr#8867](http://github.com/ceph/ceph/pull/8867), Jason Dillaman)
-   librbd: possible double-free of object map invalidation request upon
    error ([issue#15643](http://tracker.ceph.com/issues/15643),
    [pr#8865](http://github.com/ceph/ceph/pull/8865), runsisi)
-   librbd: possible race condition leads to use-after-free
    ([issue#15690](http://tracker.ceph.com/issues/15690),
    [pr#9009](http://github.com/ceph/ceph/pull/9009), Jason Dillaman)
-   librbd: potential concurrent event processing during journal replay
    ([issue#15755](http://tracker.ceph.com/issues/15755),
    [pr#9040](http://github.com/ceph/ceph/pull/9040), Jason Dillaman)
-   librbd: Potential double free of SetSnapRequest instance
    ([issue#15571](http://tracker.ceph.com/issues/15571),
    [pr#8803](http://github.com/ceph/ceph/pull/8803), runsisi)
-   librbd: put the validation of image snap context earlier
    ([pr#9046](http://github.com/ceph/ceph/pull/9046), runsisi)
-   librbd: reduce log level for image format 1 warning
    ([issue#15577](http://tracker.ceph.com/issues/15577),
    [pr#9003](http://github.com/ceph/ceph/pull/9003), Jason Dillaman)
-   mds/MDSAuthCap parse no longer fails on paths with hyphens
    ([issue#15465](http://tracker.ceph.com/issues/15465),
    [pr#8969](http://github.com/ceph/ceph/pull/8969), John Spray)
-   mds: MDS incarnation no longer gets lost after remove filesystem
    ([issue#15399](http://tracker.ceph.com/issues/15399),
    [pr#8970](http://github.com/ceph/ceph/pull/8970), John Spray)
-   mon/OSDMonitor: avoid underflow in reweight-by-utilization if
    max_change=1 ([issue#15655](http://tracker.ceph.com/issues/15655),
    [pr#9006](http://github.com/ceph/ceph/pull/9006), Samuel Just)
-   python: clone operation will fail if config overridden with \"rbd
    default format = 1\"
    ([issue#15685](http://tracker.ceph.com/issues/15685),
    [pr#8972](http://github.com/ceph/ceph/pull/8972), Jason Dillaman)
-   radosgw-admin: add missing \--zonegroup-id to usage
    ([issue#15650](http://tracker.ceph.com/issues/15650),
    [pr#9019](http://github.com/ceph/ceph/pull/9019), Casey Bodley)
-   radosgw-admin: update usage for zone\[group\] modify
    ([issue#15651](http://tracker.ceph.com/issues/15651),
    [pr#9016](http://github.com/ceph/ceph/pull/9016), Casey Bodley)
-   radosgw-admin: zonegroup remove command
    ([issue#15684](http://tracker.ceph.com/issues/15684),
    [pr#9015](http://github.com/ceph/ceph/pull/9015), Casey Bodley)
-   rbd CLI to retrieve rbd mirror state for a pool / specific image
    ([issue#15144](http://tracker.ceph.com/issues/15144),
    [issue#14420](http://tracker.ceph.com/issues/14420),
    [pr#8868](http://github.com/ceph/ceph/pull/8868), Mykola Golub)
-   rbd disk-usage CLI command should support calculating full image
    usage ([issue#14540](http://tracker.ceph.com/issues/14540),
    [pr#8870](http://github.com/ceph/ceph/pull/8870), Jason Dillaman)
-   rbd: helpful error message on map failure
    ([issue#15721](http://tracker.ceph.com/issues/15721),
    [pr#9041](http://github.com/ceph/ceph/pull/9041), Venky Shankar)
-   rbd: help message distinction between commands and aliases
    ([issue#15521](http://tracker.ceph.com/issues/15521),
    [pr#9004](http://github.com/ceph/ceph/pull/9004), Yongqiang He)
-   rbd-mirror: admin socket commands to start/stop/restart mirroring
    ([issue#15718](http://tracker.ceph.com/issues/15718),
    [pr#9010](http://github.com/ceph/ceph/pull/9010), Mykola Golub, Josh
    Durgin)
-   rbd-mirror can crash if start up is interrupted
    ([issue#15630](http://tracker.ceph.com/issues/15630),
    [pr#8866](http://github.com/ceph/ceph/pull/8866), Jason Dillaman)
-   rbd-mirror: image sync needs to handle snapshot size and protection
    status ([issue#15110](http://tracker.ceph.com/issues/15110),
    [pr#9050](http://github.com/ceph/ceph/pull/9050), Jason Dillaman)
-   rbd-mirror: lockdep error during bootstrap
    ([issue#15664](http://tracker.ceph.com/issues/15664),
    [pr#9008](http://github.com/ceph/ceph/pull/9008), Jason Dillaman)
-   rbd-nbd: fix rbd-nbd aio callback error handling
    ([issue#15604](http://tracker.ceph.com/issues/15604),
    [pr#9005](http://github.com/ceph/ceph/pull/9005), Chang-Yi Lee)
-   rgw: add AWS4 completion support for RGW_OP_SET_BUCKET_WEBSITE
    ([issue#15626](http://tracker.ceph.com/issues/15626),
    [pr#9018](http://github.com/ceph/ceph/pull/9018), Javier M. Mellid)
-   rgw admin output
    ([issue#15747](http://tracker.ceph.com/issues/15747),
    [pr#9054](http://github.com/ceph/ceph/pull/9054), Casey Bodley)
-   rgw: fix issue #15597
    ([issue#15597](http://tracker.ceph.com/issues/15597),
    [pr#9020](http://github.com/ceph/ceph/pull/9020), Yehuda Sadeh)
-   rgw: fix printing wrong X-Storage-Url in Swift\'s TempAuth.
    ([issue#15667](http://tracker.ceph.com/issues/15667),
    [pr#9021](http://github.com/ceph/ceph/pull/9021), Radoslaw
    Zarzynski)
-   rgw: handle stripe transition when flushing final pending_data_bl
    ([issue#15745](http://tracker.ceph.com/issues/15745),
    [pr#9053](http://github.com/ceph/ceph/pull/9053), Yehuda Sadeh)
-   rgw: leak fixes
    ([issue#15792](http://tracker.ceph.com/issues/15792),
    [pr#9022](http://github.com/ceph/ceph/pull/9022), Yehuda Sadeh)
-   rgw: multisite: Issues with Deleting Buckets
    ([issue#15540](http://tracker.ceph.com/issues/15540),
    [pr#8930](http://github.com/ceph/ceph/pull/8930), Abhishek
    Lekshmanan)
-   rgw: period commit fix
    ([issue#15828](http://tracker.ceph.com/issues/15828),
    [pr#9081](http://github.com/ceph/ceph/pull/9081), Casey Bodley)
-   rgw: period delete fixes
    ([issue#15469](http://tracker.ceph.com/issues/15469),
    [pr#9047](http://github.com/ceph/ceph/pull/9047), Casey Bodley)
-   rgw: radosgw-admin zone set cuts pool names short if name starts
    with a period ([issue#15598](http://tracker.ceph.com/issues/15598),
    [pr#9029](http://github.com/ceph/ceph/pull/9029), Yehuda Sadeh)
-   rgw: segfault at RGWAsyncGetSystemObj
    ([issue#15565](http://tracker.ceph.com/issues/15565),
    [issue#15625](http://tracker.ceph.com/issues/15625),
    [pr#9017](http://github.com/ceph/ceph/pull/9017), Yehuda Sadeh)
-   several backports
    ([issue#15588](http://tracker.ceph.com/issues/15588),
    [issue#15655](http://tracker.ceph.com/issues/15655),
    [pr#8853](http://github.com/ceph/ceph/pull/8853), Alexandre
    Derumier, xie xingguo, Alfredo Deza)
-   systemd: fix typo in preset file
    ([pr#8843](http://github.com/ceph/ceph/pull/8843), Nathan Cutler)
-   tests: make check fails on ext4
    ([issue#15837](http://tracker.ceph.com/issues/15837),
    [pr#9063](http://github.com/ceph/ceph/pull/9063), Loic Dachary, Sage
    Weil)

## v10.2.0 Jewel

This major release of Ceph is the foundation for the next long-term
stable release series. There have been many major changes since the
Infernalis (9.2.x) and Hammer (0.94.x) releases, and the upgrade process
is non-trivial. Please read these release notes carefully.

### Major Changes from Infernalis

-   *CephFS*:
    -   This is the first release in which CephFS is declared stable!
        Several features are disabled by default, including snapshots
        and multiple active MDS servers.
    -   The repair and disaster recovery tools are now feature-complete.
    -   A new cephfs-volume-manager module is included that provides a
        high-level interface for creating \"shares\" for OpenStack
        Manila and similar projects.
    -   There is now experimental support for multiple CephFS file
        systems within a single cluster.
-   *RGW*:
    -   The multisite feature has been almost completely rearchitected
        and rewritten to support any number of clusters/sites,
        bidirectional fail-over, and active/active configurations.
    -   You can now access radosgw buckets via NFS (experimental).
    -   The AWS4 authentication protocol is now supported.
    -   There is now support for S3 request payer buckets.
    -   The new multitenancy infrastructure improves compatibility with
        Swift, which provides a separate container namespace for each
        user/tenant.
    -   The OpenStack Keystone v3 API is now supported. There are a
        range of other small Swift API features and compatibility
        improvements as well, including bulk delete and SLO (static
        large objects).
-   *RBD*:
    -   There is new support for mirroring (asynchronous replication) of
        RBD images across clusters. This is implemented as a per-RBD
        image journal that can be streamed across a WAN to another site,
        and a new rbd-mirror daemon that performs the cross-cluster
        replication.
    -   The exclusive-lock, object-map, fast-diff, and journaling
        features can be enabled or disabled dynamically. The
        deep-flatten features can be disabled dynamically but not
        re-enabled.
    -   The RBD CLI has been rewritten to provide command-specific help
        and full bash completion support.
    -   RBD snapshots can now be renamed.
-   *RADOS*:
    -   BlueStore, a new OSD backend, is included as an experimental
        feature. The plan is for it to become the default backend in the
        K or L release.
    -   The OSD now persists scrub results and provides a librados API
        to query results in detail.
    -   We have revised our documentation to recommend *against* using
        ext4 as the underlying filesystem for Ceph OSD daemons due to
        problems supporting our long object name handling.

### Major Changes from Hammer

-   *General*:
    -   Ceph daemons are now managed via systemd (with the exception of
        Ubuntu Trusty, which still uses upstart).
    -   Ceph daemons run as \'ceph\' user instead of \'root\'.
    -   On Red Hat distros, there is also an SELinux policy.
-   *RADOS*:
    -   The RADOS cache tier can now proxy write operations to the base
        tier, allowing writes to be handled without forcing migration of
        an object into the cache.
    -   The SHEC erasure coding support is no longer flagged as
        experimental. SHEC trades some additional storage space for
        faster repair.
    -   There is now a unified queue (and thus prioritization) of client
        IO, recovery, scrubbing, and snapshot trimming.
    -   There have been many improvements to low-level repair tooling
        (ceph-objectstore-tool).
    -   The internal ObjectStore API has been significantly cleaned up
        in order to facilitate new storage backends like BlueStore.
-   *RGW*:
    -   The Swift API now supports object expiration.
    -   There are many Swift API compatibility improvements.
-   *RBD*:
    -   The `rbd du` command shows actual usage (quickly, when
        object-map is enabled).
    -   The object-map feature has seen many stability improvements.
    -   The object-map and exclusive-lock features can be enabled or
        disabled dynamically.
    -   You can now store user metadata and set persistent librbd
        options associated with individual images.
    -   The new deep-flatten features allow flattening of a clone and
        all of its snapshots. (Previously snapshots could not be
        flattened.)
    -   The export-diff command is now faster (it uses aio). There is
        also a new fast-diff feature.
    -   The \--size argument can be specified with a suffix for units
        (e.g., `--size 64G`).
    -   There is a new `rbd status` command that, for now, shows who has
        the image open/mapped.
-   *CephFS*:
    -   You can now rename snapshots.
    -   There have been ongoing improvements around administration,
        diagnostics, and the check and repair tools.
    -   The caching and revocation of client cache state due to unused
        inodes has been dramatically improved.
    -   The ceph-fuse client behaves better on 32-bit hosts.

### Distro compatibility

Starting with Infernalis, we have dropped support for many older
distributions so that we can move to a newer compiler toolchain (e.g.,
C++11). Although it is still possible to build Ceph on older
distributions by installing backported development tools, we are not
building and publishing release packages for ceph.com.

We now build packages for the following distributions and architectures:

-   x86_64:
    -   CentOS 7.x. We have dropped support for CentOS 6 (and other RHEL
        6 derivatives, like Scientific Linux 6).
    -   Debian Jessie 8.x. Debian Wheezy 7.x\'s g++ has incomplete
        support for C++11 (and no systemd).
    -   Ubuntu Xenial 16.04 and Trusty 14.04. Ubuntu Precise 12.04 is no
        longer supported.
    -   Fedora 22 or later.
-   aarch64 / arm64:
    -   Ubuntu Xenial 16.04.

### Upgrading from Infernalis or Hammer

-   We now recommend against using `ext4` as the underlying file system
    for Ceph OSDs, especially when RGW or other users of long RADOS
    object names are used. For more information about why, please see
    [Filesystem
    Recommendations](../configuration/filesystem-recommendations).

    If you have an existing cluster that uses ext4 for the OSDs but uses
    only RBD and/or CephFS, then the ext4 limitations will not affect
    you. Before upgrading, be sure add the following to `ceph.conf` to
    allow the OSDs to start:

        osd max object name len = 256
        osd max object namespace len = 64

    Keep in mind that if you set these lower object name limits and
    later decide to use RGW on this cluster, it will have problems
    storing S3/Swift objects with long names. This startup check can
    also be disabled via the below option, although this is not
    recommended:

        osd check max object name len on startup = false

-   There are no major compatibility changes since Infernalis. Simply
    upgrading the daemons on each host and restarting all daemons is
    sufficient.

-   The rbd CLI no longer accepts the deprecated \'\--image-features\'
    option during create, import, and clone operations. The
    \'\--image-feature\' option should be used instead.

-   The rbd legacy image format (version 1) is deprecated with the Jewel
    release. Attempting to create a new version 1 RBD image will result
    in a warning. Future releases of Ceph will remove support for
    version 1 RBD images.

-   The \'send_pg_creates\' and \'map_pg_creates\' mon CLI commands are
    obsolete and no longer supported.

-   A new configure option \'mon_election_timeout\' is added to
    specifically limit max waiting time of monitor election process,
    which was previously restricted by \'mon_lease\'.

-   CephFS filesystems created using versions older than Firefly (0.80)
    must use the new \'cephfs-data-scan tmap_upgrade\' command after
    upgrading to Jewel. See \'Upgrading\' in the CephFS documentation
    for more information.

-   The \'ceph mds setmap\' command has been removed.

-   The default RBD image features for new images have been updated to
    enable the following: exclusive lock, object map, fast-diff, and
    deep-flatten. These features are not currently supported by the RBD
    kernel driver nor older RBD clients. They can be disabled on a
    per-image basis via the RBD CLI, or the default features can be
    updated to the pre-Jewel setting by adding the following to the
    client section of the Ceph configuration file:

        rbd default features = 1

-   The rbd legacy image format (version 1) is deprecated with the Jewel
    release.

-   After upgrading, users should set the \'sortbitwise\' flag to enable
    the new internal object sort order:

        ceph osd set sortbitwise

    This flag is important for the new object enumeration API and for
    new backends like BlueStore.

-   The rbd CLI no longer permits creating images and snapshots with
    potentially ambiguous names (e.g. the \'/\' and \'@\' characters are
    disallowed). The validation can be temporarily disabled by adding
    \"\--rbd-validate-names=false\" to the rbd CLI when creating an
    image or snapshot. It can also be disabled by adding the following
    to the client section of the Ceph configuration file:

        rbd validate names = false

### Upgrading from Hammer

-   All cluster nodes must first upgrade to Hammer v0.94.4 or a later
    v0.94.z release; only then is it possible to upgrade to Jewel
    10.2.z.

-   For all distributions that support systemd (CentOS 7, Fedora, Debian
    Jessie 8.x, OpenSUSE), ceph daemons are now managed using native
    systemd files instead of the legacy sysvinit scripts. For example:

        systemctl start ceph.target       # start all daemons
        systemctl status ceph-osd@12      # check status of osd.12

    The main notable distro that is *not* yet using systemd is Ubuntu
    trusty 14.04. (The next Ubuntu LTS, 16.04, will use systemd instead
    of upstart.)

-   Ceph daemons now run as user and group `ceph` by default. The ceph
    user has a static UID assigned by Fedora and Debian (also used by
    derivative distributions like RHEL/CentOS and Ubuntu). On SUSE the
    same UID/GID as in Fedora and Debian will be used, *provided it is
    not already assigned*. In the unlikely event the preferred UID or
    GID is assigned to a different user/group, ceph will get a
    dynamically assigned UID/GID.

    If your systems already have a ceph user, upgrading the package will
    cause problems. We suggest you first remove or rename the existing
    \'ceph\' user and \'ceph\' group before upgrading.

    When upgrading, administrators have two options:

    > 1.  Add the following line to `ceph.conf` on all hosts:
    >
    >         setuser match path = /var/lib/ceph/$type/$cluster-$id
    >
    >     This will make the Ceph daemons run as root (i.e., not drop
    >     privileges and switch to user ceph) if the daemon\'s data
    >     directory is still owned by root. Newly deployed daemons will
    >     be created with data owned by user ceph and will run with
    >     reduced privileges, but upgraded daemons will continue to run
    >     as root.
    >
    > 2.  Fix the data ownership during the upgrade. This is the
    >     preferred option, but it is more work and can be very time
    >     consuming. The process for each host is to:
    >
    >     1.  Upgrade the ceph package. This creates the ceph user and
    >         group. For example:
    >
    >             ceph-deploy install --stable jewel HOST
    >
    >     2.  Stop the daemon(s):
    >
    >             service ceph stop           # fedora, centos, rhel, debian
    >             stop ceph-all               # ubuntu
    >
    >     3.  Fix the ownership:
    >
    >             chown -R ceph:ceph /var/lib/ceph
    >             chown -R ceph:ceph /var/log/ceph
    >
    >     4.  Restart the daemon(s):
    >
    >             start ceph-all                # ubuntu
    >             systemctl start ceph.target   # debian, centos, fedora, rhel
    >
    >     Alternatively, the same process can be done with a single
    >     daemon type, for example by stopping only monitors and
    >     chowning only `/var/lib/ceph/mon`.

-   The on-disk format for the experimental KeyValueStore OSD backend
    has changed. You will need to remove any OSDs using that backend
    before you upgrade any test clusters that use it.

-   When a pool quota is reached, librados operations now block
    indefinitely, the same way they do when the cluster fills up.
    (Previously they would return -ENOSPC.) By default, a full cluster
    or pool will now block. If your librados application can handle
    ENOSPC or EDQUOT errors gracefully, you can get error returns
    instead by using the new librados OPERATION_FULL_TRY flag.

-   The return code for librbd\'s rbd_aio_read and Image::aio_read API
    methods no longer returns the number of bytes read upon success.
    Instead, it returns 0 upon success and a negative value upon
    failure.

-   \'ceph scrub\', \'ceph compact\' and \'ceph sync force\' are now
    DEPRECATED. Users should instead use \'ceph mon scrub\', \'ceph mon
    compact\' and \'ceph mon sync force\'.

-   \'ceph mon_metadata\' should now be used as \'ceph mon metadata\'.
    There is no need to deprecate this command (same major release since
    it was first introduced).

-   The [\--dump-json]{.title-ref} option of \"osdmaptool\" is replaced
    by [\--dump json]{.title-ref}.

-   The commands of \"pg ls-by-{pool,primary,osd}\" and \"pg ls\" now
    take \"recovering\" instead of \"recovery\", to include the
    recovering pgs in the listed pgs.

### Upgrading from Firefly

Upgrading directly from Firefly v0.80.z is not recommended. It is
possible to do a direct upgrade, but not without downtime, as all OSDs
must be stopped, upgraded, and then restarted. We recommend that
clusters be first upgraded to Hammer v0.94.6 or a later v0.94.z release;
only then is it possible to upgrade to Jewel 10.2.z for an online
upgrade (see below).

To do an offline upgrade directly from Firefly, all Firefly OSDs must be
stopped and marked down before any Jewel OSDs will be allowed to start
up. This fencing is enforced by the Jewel monitor, so you should use an
upgrade procedure like:

> 1.  Upgrade Ceph on monitor hosts
>
> 2.  Restart all ceph-mon daemons
>
> 3.  
>
>     Set noout::
>
>     :   ceph osd set noout
>
> 4.  Upgrade Ceph on all OSD hosts
>
> 5.  Stop all ceph-osd daemons
>
> 6.  
>
>     Mark all OSDs down with something like::
>
>     :   ceph osd down [seq 0 1000]{.title-ref}
>
> 7.  Start all ceph-osd daemons
>
> 8.  
>
>     Let the cluster settle and then unset noout::
>
>     :   ceph osd unset noout
>
> 9.  Upgrade and restart any remaining daemons (ceph-mds, radosgw)

### Notable Changes since Infernalis

-   aarch64: add optimized version of crc32c (Yazen Ghannam, Steve
    Capper)
-   Adding documentation on how to use new dynamic throttle scheme
    ([pr#8069](http://github.com/ceph/ceph/pull/8069), Somnath Roy)
-   admin/build-doc: depend on zlib1g-dev and graphviz
    ([pr#7522](http://github.com/ceph/ceph/pull/7522), Ken Dreyer)
-   auth: cache/reuse crypto lib key objects, optimize msg signature
    check (Sage Weil)
-   auth: fail if rotating key is missing (do not spam log)
    ([pr#6473](http://github.com/ceph/ceph/pull/6473), Qiankun Zheng)
-   auth: fix crash when bad keyring is passed
    ([pr#6698](http://github.com/ceph/ceph/pull/6698), Dunrong Huang)
-   auth: make keyring without mon entity type return -EACCES
    ([pr#5734](http://github.com/ceph/ceph/pull/5734), Xiaowei Chen)
-   AUTHORS: update email
    ([pr#7854](http://github.com/ceph/ceph/pull/7854), Yehuda Sadeh)
-   auth: reinit NSS after fork() (#11128 Yan, Zheng)
-   authtool: update \--help and manpage to match code.
    ([pr#8456](http://github.com/ceph/ceph/pull/8456), Robin H. Johnson)
-   autotools: fix out of tree build (Krxysztof Kosinski)
-   autotools: improve make check output (Loic Dachary)
-   Be more careful about directory fragmentation and scrubbing
    ([issue#15167](http://tracker.ceph.com/issues/15167),
    [pr#8180](http://github.com/ceph/ceph/pull/8180), Yan, Zheng)
-   bluestore: latest and greatest
    ([issue#14210](http://tracker.ceph.com/issues/14210),
    [issue#13801](http://tracker.ceph.com/issues/13801),
    [pr#6896](http://github.com/ceph/ceph/pull/6896), xie.xingguo,
    Jianpeng Ma, YiQiang Chen, Sage Weil, Ning Yao)
-   buffer: add invalidate_crc() (Piotr Dalek)
-   buffer: add symmetry operator==() and operator!=()
    ([pr#7974](http://github.com/ceph/ceph/pull/7974), Kefu Chai)
-   buffer: fix internal iterator invalidation on rebuild,
    get_contiguous ([pr#6962](http://github.com/ceph/ceph/pull/6962),
    Sage Weil)
-   buffer: fix zero bug (#12252 Haomai Wang)
-   buffer: hide iterator_impl symbols
    ([issue#14788](http://tracker.ceph.com/issues/14788),
    [pr#7688](http://github.com/ceph/ceph/pull/7688), Kefu Chai)
-   buffer: increment history alloc as well in raw_combined
    ([issue#14955](http://tracker.ceph.com/issues/14955),
    [pr#7910](http://github.com/ceph/ceph/pull/7910), Samuel Just)
-   buffer: make usable outside of ceph source again
    ([pr#6863](http://github.com/ceph/ceph/pull/6863), Josh Durgin)
-   buffer: raw_combined allocations buffer and ref count together
    ([pr#7612](http://github.com/ceph/ceph/pull/7612), Sage Weil)
-   buffer: some cleanup (Michal Jarzabek)
-   buffer: use move construct to append/push_back/push_front
    ([pr#7455](http://github.com/ceph/ceph/pull/7455), Haomai Wang)
-   build: Adding build requires
    ([pr#7742](http://github.com/ceph/ceph/pull/7742), Erwan Velu)
-   build: a few armhf (32-bit build) fixes
    ([pr#7999](http://github.com/ceph/ceph/pull/7999), Eric Lee, Sage
    Weil)
-   build: allow jemalloc with rocksdb-static
    ([pr#7368](http://github.com/ceph/ceph/pull/7368), Somnath Roy)
-   build: allow tcmalloc-minimal (Thorsten Behrens)
-   build: build internal plugins and classes as modules
    ([pr#6462](http://github.com/ceph/ceph/pull/6462), James Page)
-   build: C++11 now supported
-   build: cmake check fixes
    ([pr#6787](http://github.com/ceph/ceph/pull/6787), Orit Wasserman)
-   build: cmake: fix nss linking (Danny Al-Gaaf)
-   build: cmake: misc fixes (Orit Wasserman, Casey Bodley)
-   build: cmake tweaks
    ([pr#6254](http://github.com/ceph/ceph/pull/6254), John Spray)
-   build: disable LTTNG by default (#11333 Josh Durgin)
-   build: do not build ceph-dencoder with tcmalloc (#10691 Boris Ranto)
-   build: fix a few warnings
    ([pr#6847](http://github.com/ceph/ceph/pull/6847), Orit Wasserman)
-   build: fix bz2-dev dependency
    ([pr#6948](http://github.com/ceph/ceph/pull/6948), Samuel Just)
-   build: fix compiling warnings
    ([pr#8366](http://github.com/ceph/ceph/pull/8366), Dongsheng Yang)
-   build: Fixing BTRFS issue at \'make check\'
    ([pr#7805](http://github.com/ceph/ceph/pull/7805), Erwan Velu)
-   build: fix Jenkins make check errors due to deep-scrub randomization
    ([pr#6671](http://github.com/ceph/ceph/pull/6671), David Zafman)
-   build: fix junit detection on Fedora 22 (Ira Cooper)
-   build: fix pg ref disabling (William A. Kennington III)
-   build: fix ppc build (James Page)
-   build: fix the autotools and cmake build (the new fusestore needs
    libfuse) ([pr#7393](http://github.com/ceph/ceph/pull/7393), Kefu
    Chai)
-   build: fix warnings
    ([pr#7197](http://github.com/ceph/ceph/pull/7197), Kefu Chai, xie
    xingguo)
-   build: fix warnings
    ([pr#7315](http://github.com/ceph/ceph/pull/7315), Kefu Chai)
-   build: FreeBSD related fixes
    ([pr#7170](http://github.com/ceph/ceph/pull/7170), Mykola Golub)
-   build: Gentoo: \_FORTIFY_SOURCE fix.
    ([issue#13920](http://tracker.ceph.com/issues/13920),
    [pr#6739](http://github.com/ceph/ceph/pull/6739), Robin H. Johnson)
-   build: install-deps: misc fixes (Loic Dachary)
-   build: install-deps.sh improvements (Loic Dachary)
-   build: install-deps: support OpenSUSE (Loic Dachary)
-   build: kill warnings
    ([pr#7397](http://github.com/ceph/ceph/pull/7397), Kefu Chai)
-   build: make_dist_tarball.sh (Sage Weil)
-   build: many cmake improvements
-   build: misc cmake fixes (Matt Benjamin)
-   build: misc fixes (Boris Ranto, Ken Dreyer, Owen Synge)
-   build: misc make check fixes
    ([pr#7153](http://github.com/ceph/ceph/pull/7153), Sage Weil)
-   build: more CMake package check fixes
    ([pr#6108](http://github.com/ceph/ceph/pull/6108), Daniel
    Gryniewicz)
-   build: move libexec scripts to standardize across distros
    ([issue#14687](http://tracker.ceph.com/issues/14687),
    [issue#14705](http://tracker.ceph.com/issues/14705),
    [issue#14723](http://tracker.ceph.com/issues/14723),
    [pr#7636](http://github.com/ceph/ceph/pull/7636), Nathan Cutler,
    Kefu Chai)
-   build/ops: enable CR in CentOS 7
    ([issue#13997](http://tracker.ceph.com/issues/13997),
    [pr#6844](http://github.com/ceph/ceph/pull/6844), Loic Dachary)
-   build/ops: rbd-replay moved from ceph-test-dbg to ceph-common-dbg
    ([issue#13785](http://tracker.ceph.com/issues/13785),
    [pr#6578](http://github.com/ceph/ceph/pull/6578), Loic Dachary)
-   build/ops: systemd ceph-disk unit must not assume /bin/flock
    ([issue#13975](http://tracker.ceph.com/issues/13975),
    [pr#6803](http://github.com/ceph/ceph/pull/6803), Loic Dachary)
-   build: OSX build fixes (Yan, Zheng)
-   build: Refrain from versioning and packaging EC testing plugins
    ([issue#14756](http://tracker.ceph.com/issues/14756),
    [issue#14723](http://tracker.ceph.com/issues/14723),
    [pr#7637](http://github.com/ceph/ceph/pull/7637), Nathan Cutler,
    Kefu Chai)
-   build: remove rest-bench
-   build: Respect TMPDIR for virtualenv.
    ([pr#8457](http://github.com/ceph/ceph/pull/8457), Robin H. Johnson)
-   build: spdk submodule; cmake
    ([pr#7503](http://github.com/ceph/ceph/pull/7503), Kefu Chai)
-   build: workaround an automake bug for \"make check\"
    ([issue#14723](http://tracker.ceph.com/issues/14723),
    [pr#7626](http://github.com/ceph/ceph/pull/7626), Kefu Chai)
-   ceph-authtool: fix return code on error (Gerhard Muntingh)
-   ceph: bash auto complete for CLI based on mon command descriptions
    ([pr#7693](http://github.com/ceph/ceph/pull/7693), Adam Kupczyk)
-   ceph_daemon.py: Resolved ImportError to work with python3
    ([pr#7937](http://github.com/ceph/ceph/pull/7937), Sarthak Munshi)
-   ceph-detect-init: add debian/jessie test
    ([pr#8074](http://github.com/ceph/ceph/pull/8074), Kefu Chai)
-   ceph-detect-init: added Linux Mint (Michal Jarzabek)
-   ceph-detect-init: add missing test case
    ([pr#8105](http://github.com/ceph/ceph/pull/8105), Nathan Cutler)
-   ceph-detect-init: fix py3 test
    ([pr#7025](http://github.com/ceph/ceph/pull/7025), Kefu Chai)
-   ceph-detect-init: fix py3 test
    ([pr#7243](http://github.com/ceph/ceph/pull/7243), Kefu Chai)
-   ceph_detect_init/\_\_init\_\_.py: remove shebang
    ([pr#7731](http://github.com/ceph/ceph/pull/7731), Nathan Cutler)
-   ceph-detect-init: return correct value on recent SUSE distros
    ([issue#14770](http://tracker.ceph.com/issues/14770),
    [pr#7909](http://github.com/ceph/ceph/pull/7909), Nathan Cutler)
-   ceph-detect-init: robust init system detection (Owen Synge)
-   ceph-detect-init/run-tox.sh: FreeBSD: No init detect
    ([pr#8373](http://github.com/ceph/ceph/pull/8373), Willem Jan
    Withagen)
-   ceph-detect-init: Ubuntu \>= 15.04 uses systemd
    ([pr#6873](http://github.com/ceph/ceph/pull/6873), James Page)
-   ceph-disk: Add destroy and deactivate option
    ([issue#7454](http://tracker.ceph.com/issues/7454),
    [pr#5867](http://github.com/ceph/ceph/pull/5867), Vicente Cheng)
-   ceph-disk: add -f flag for btrfs mkfs
    ([pr#7222](http://github.com/ceph/ceph/pull/7222), Darrell Enns)
-   ceph-disk: Add \--setuser and \--setgroup options for ceph-disk
    ([pr#7351](http://github.com/ceph/ceph/pull/7351), Mike Shuey)
-   ceph-disk: ceph-disk list fails on /dev/cciss!c0d0
    ([issue#13970](http://tracker.ceph.com/issues/13970),
    [issue#14233](http://tracker.ceph.com/issues/14233),
    [issue#14230](http://tracker.ceph.com/issues/14230),
    [pr#6879](http://github.com/ceph/ceph/pull/6879), Loic Dachary)
-   ceph-disk: compare parted output with the dereferenced path
    ([issue#13438](http://tracker.ceph.com/issues/13438),
    [pr#6219](http://github.com/ceph/ceph/pull/6219), Joe Julian)
-   ceph-disk: deactivate / destroy PATH arg are optional
    ([pr#7756](http://github.com/ceph/ceph/pull/7756), Loic Dachary)
-   ceph-disk: do not always fail when re-using a partition
    ([pr#8508](http://github.com/ceph/ceph/pull/8508), You Ji)
-   ceph-disk: ensure \'zap\' only operates on a full disk (#11272 Loic
    Dachary)
-   ceph-disk: fixes to respect init system (Loic Dachary, Owen Synge)
-   ceph-disk: fix failures when preparing disks with udev \> 214
    ([issue#14080](http://tracker.ceph.com/issues/14080),
    [issue#14094](http://tracker.ceph.com/issues/14094),
    [pr#6926](http://github.com/ceph/ceph/pull/6926), Loic Dachary, Ilya
    Dryomov)
-   ceph-disk: fix prepare \--help
    ([pr#7758](http://github.com/ceph/ceph/pull/7758), Loic Dachary)
-   ceph-disk: Fix trivial typo
    ([pr#7472](http://github.com/ceph/ceph/pull/7472), Brad Hubbard)
-   ceph-disk: fix zap sgdisk invocation (Owen Synge, Thorsten Behrens)
-   ceph-disk: flake8 fixes
    ([pr#7646](http://github.com/ceph/ceph/pull/7646), Loic Dachary)
-   ceph-disk: follow ceph-osd hints when creating journal (#9580 Sage
    Weil)
-   ceph-disk: get Nonetype when ceph-disk list with \--format plain on
    single device. ([pr#6410](http://github.com/ceph/ceph/pull/6410),
    Vicente Cheng)
-   ceph-disk: handle re-using existing partition (#10987 Loic Dachary)
-   ceph-disk: improve parted output parsing (#10983 Loic Dachary)
-   ceph-disk: Improving \'make check\' for ceph-disk
    ([pr#7762](http://github.com/ceph/ceph/pull/7762), Erwan Velu)
-   ceph-disk: install pip \> 6.1 (#11952 Loic Dachary)
-   ceph-disk: key management support
    ([issue#14669](http://tracker.ceph.com/issues/14669),
    [pr#7552](http://github.com/ceph/ceph/pull/7552), Loic Dachary)
-   ceph-disk: make some arguments as required if necessary
    ([pr#7687](http://github.com/ceph/ceph/pull/7687), Dongsheng Yang)
-   ceph-disk: make suppression work for activate-all and
    activate-journal (Dan van der Ster)
-   ceph-disk: many fixes (Loic Dachary, Alfredo Deza)
-   ceph-disk: pass \--cluster arg on prepare subcommand (Kefu Chai)
-   ceph-disk: s/dmcrpyt/dmcrypt/
    ([issue#14838](http://tracker.ceph.com/issues/14838),
    [pr#7744](http://github.com/ceph/ceph/pull/7744), Loic Dachary,
    Frode Sandholtbraaten)
-   ceph-disk: support bluestore
    ([issue#13422](http://tracker.ceph.com/issues/13422),
    [pr#7218](http://github.com/ceph/ceph/pull/7218), Loic Dachary, Sage
    Weil)
-   ceph-disk: support for multipath devices (Loic Dachary)
-   ceph-disk: support NVMe device partitions (#11612 Ilja Slepnev)
-   ceph-disk/test: fix test_prepare.py::TestPrepare tests
    ([pr#7549](http://github.com/ceph/ceph/pull/7549), Kefu Chai)
-   ceph-disk: warn for prepare partitions with bad GUIDs
    ([issue#13943](http://tracker.ceph.com/issues/13943),
    [pr#6760](http://github.com/ceph/ceph/pull/6760), David Disseldorp)
-   ceph: fix \'df\' units (Zhe Zhang)
-   ceph: fix parsing in interactive cli mode (#11279 Kefu Chai)
-   ceph: fix tell behavior
    ([pr#6329](http://github.com/ceph/ceph/pull/6329), David Zafman)
-   cephfs-data-scan: many additions, improvements (John Spray)
-   cephfs-data-scan: scan_frags
    ([pr#5941](http://github.com/ceph/ceph/pull/5941), John Spray)
-   cephfs-data-scan: scrub tag filtering (#12133 and #12145)
    ([issue#12133](http://tracker.ceph.com/issues/12133),
    [issue#12145](http://tracker.ceph.com/issues/12145),
    [pr#5685](http://github.com/ceph/ceph/pull/5685), John Spray)
-   ceph-fuse: add process to ceph-fuse \--help
    ([pr#6821](http://github.com/ceph/ceph/pull/6821), Wei Feng)
-   ceph-fuse: do not require successful remount when unmounting (#10982
    Greg Farnum)
-   ceph-fuse: fix double decreasing the count to trim caps
    ([issue#14319](http://tracker.ceph.com/issues/14319),
    [pr#7229](http://github.com/ceph/ceph/pull/7229), Zhi Zhang)
-   ceph-fuse: fix double free of args
    ([pr#7015](http://github.com/ceph/ceph/pull/7015), Ilya Shipitsin)
-   ceph-fuse: fix fsync()
    ([pr#6388](http://github.com/ceph/ceph/pull/6388), Yan, Zheng)
-   ceph-fuse: Fix potential filehandle ref leak at umount
    ([issue#14800](http://tracker.ceph.com/issues/14800),
    [pr#7686](http://github.com/ceph/ceph/pull/7686), Zhi Zhang)
-   ceph-fuse, libcephfs: don\'t clear COMPLETE when trimming null (Yan,
    Zheng)
-   ceph-fuse, libcephfs: drop inode when rmdir finishes (#11339 Yan,
    Zheng)
-   ceph-fuse,libcephfs: Fix client handling of \"lost\" open
    directories on shutdown
    ([issue#14996](http://tracker.ceph.com/issues/14996),
    [pr#7994](http://github.com/ceph/ceph/pull/7994), Yan, Zheng)
-   ceph-fuse,libcephfs: fix free fds being exhausted eventually because
    freed fds are never put back
    ([issue#14798](http://tracker.ceph.com/issues/14798),
    [pr#7685](http://github.com/ceph/ceph/pull/7685), Zhi Zhang)
-   ceph-fuse,libcephfs: fix uninline (#11356 Yan, Zheng)
-   ceph-fuse, libcephfs: hold exclusive caps on dirs we \"own\" (#11226
    Greg Farnum)
-   ceph-fuse: mostly behave on 32-bit hosts (Yan, Zheng)
-   ceph-fuse:print usage information when no parameter specified
    ([pr#6868](http://github.com/ceph/ceph/pull/6868), Bo Cai)
-   ceph-fuse: rotate log file
    ([pr#8485](http://github.com/ceph/ceph/pull/8485), Sage Weil)
-   ceph-fuse: While starting ceph-fuse, start the log thread first
    ([issue#13443](http://tracker.ceph.com/issues/13443),
    [pr#6224](http://github.com/ceph/ceph/pull/6224), Wenjun Huang)
-   ceph: improve error output for \'tell\' (#11101 Kefu Chai)
-   ceph: improve the error message
    ([issue#11101](http://tracker.ceph.com/issues/11101),
    [pr#7106](http://github.com/ceph/ceph/pull/7106), Kefu Chai)
-   ceph.in: avoid a broken pipe error when use ceph command
    ([issue#14354](http://tracker.ceph.com/issues/14354),
    [pr#7212](http://github.com/ceph/ceph/pull/7212), Bo Cai)
-   ceph.in: correct dev python path for automake builds
    ([pr#8360](http://github.com/ceph/ceph/pull/8360), Josh Durgin)
-   ceph.in: fix python libpath for automake as well
    ([pr#8362](http://github.com/ceph/ceph/pull/8362), Josh Durgin)
-   ceph.in: Minor python3 specific changes
    ([pr#7947](http://github.com/ceph/ceph/pull/7947), Sarthak Munshi)
-   ceph-kvstore-tool: handle bad out file on command line
    ([pr#6093](http://github.com/ceph/ceph/pull/6093), Kefu Chai)
-   ceph-mds:add \--help/-h
    ([pr#6850](http://github.com/ceph/ceph/pull/6850), Cilang Zhao)
-   ceph-monstore-tool: fix store-copy (Huangjun)
-   ceph: new \'ceph daemonperf\' command (John Spray, Mykola Golub)
-   ceph_objectstore_bench: fix race condition, bugs
    ([issue#13516](http://tracker.ceph.com/issues/13516),
    [pr#6681](http://github.com/ceph/ceph/pull/6681), Igor Fedotov)
-   ceph-objectstore-tool: fix \--dry-run for many ceph-objectstore-tool
    operations ([pr#6545](http://github.com/ceph/ceph/pull/6545), David
    Zafman)
-   ceph-objectstore-tool: many many improvements (David Zafman)
-   ceph-objectstore-tool: refactoring and cleanup (John Spray)
-   ceph-post-file: misc fixes (Joey McDonald, Sage Weil)
-   ceph-rest-api: fix fs/flag/set
    ([pr#8428](http://github.com/ceph/ceph/pull/8428), Sage Weil)
-   ceph.spec.in: add BuildRequires: systemd
    ([issue#13860](http://tracker.ceph.com/issues/13860),
    [pr#6692](http://github.com/ceph/ceph/pull/6692), Nathan Cutler)
-   ceph.spec.in: add copyright notice
    ([issue#14694](http://tracker.ceph.com/issues/14694),
    [pr#7569](http://github.com/ceph/ceph/pull/7569), Nathan Cutler)
-   ceph.spec.in: add license declaration
    ([pr#7574](http://github.com/ceph/ceph/pull/7574), Nathan Cutler)
-   ceph.spec.in: disable lttng and babeltrace explicitly
    ([issue#14844](http://tracker.ceph.com/issues/14844),
    [pr#7857](http://github.com/ceph/ceph/pull/7857), Kefu Chai)
-   ceph.spec.in: do not install Ceph RA on systemd platforms
    ([issue#14828](http://tracker.ceph.com/issues/14828),
    [pr#7894](http://github.com/ceph/ceph/pull/7894), Nathan Cutler)
-   ceph.spec.in: fix openldap and openssl build dependencies for SUSE
    ([issue#15138](http://tracker.ceph.com/issues/15138),
    [pr#8120](http://github.com/ceph/ceph/pull/8120), Nathan Cutler)
-   ceph.spec.in: limit \_smp_mflags when lowmem_builder is set in
    SUSE\'s OBS ([issue#13858](http://tracker.ceph.com/issues/13858),
    [pr#6691](http://github.com/ceph/ceph/pull/6691), Nathan Cutler)
-   ceph_test_libcephfs: tolerate duplicated entries in readdir
    ([issue#14377](http://tracker.ceph.com/issues/14377),
    [pr#7246](http://github.com/ceph/ceph/pull/7246), Yan, Zheng)
-   ceph_test_msgr: reduce test size to fix memory size
    ([pr#8127](http://github.com/ceph/ceph/pull/8127), Haomai Wang)
-   ceph_test_msgr: Use send_message instead of keepalive to wakeup
    connection ([pr#6605](http://github.com/ceph/ceph/pull/6605), Haomai
    Wang)
-   ceph_test_rados_misc: shorten mount timeout
    ([pr#8209](http://github.com/ceph/ceph/pull/8209), Sage Weil)
-   ceph_test_rados: test pipelined reads (Zhiqiang Wang)
-   check-generated.sh: can\'t source bash from sh
    ([pr#8521](http://github.com/ceph/ceph/pull/8521), Michal Jarzabek)
-   cleanup ([pr#8058](http://github.com/ceph/ceph/pull/8058), Yehuda
    Sadeh, Orit Wasserman)
-   cleanup: remove misc dead code
    ([pr#7201](http://github.com/ceph/ceph/pull/7201), Erwan Velu)
-   client: a better check for MDS availability
    ([pr#6253](http://github.com/ceph/ceph/pull/6253), John Spray)
-   client: add option to control how directory size is calculated
    ([pr#7323](http://github.com/ceph/ceph/pull/7323), Yan, Zheng)
-   client: avoid creating orphan object in Client::check_pool_perm()
    ([issue#13782](http://tracker.ceph.com/issues/13782),
    [pr#6603](http://github.com/ceph/ceph/pull/6603), Yan, Zheng)
-   client: avoid sending unnecessary FLUSHSNAP messages (Yan, Zheng)
-   client: check if Fh is readable when processing a read
    ([issue#11517](http://tracker.ceph.com/issues/11517),
    [pr#7209](http://github.com/ceph/ceph/pull/7209), Yan, Zheng)
-   client: close mds sessions in shutdown()
    ([pr#6269](http://github.com/ceph/ceph/pull/6269), John Spray)
-   client: don\'t invalidate page cache when inode is no longer used
    ([pr#6380](http://github.com/ceph/ceph/pull/6380), Yan, Zheng)
-   client: don\'t mark_down on command reply
    ([pr#6204](http://github.com/ceph/ceph/pull/6204), John Spray)
-   client: drop prefix from ints
    ([pr#6275](http://github.com/ceph/ceph/pull/6275), John Coyle)
-   client: exclude setfilelock when calculating oldest tid (Yan, Zheng)
-   client: fix error handling in check_pool_perm (John Spray)
-   client: flush kernel pagecache before creating snapshot
    ([issue#10436](http://tracker.ceph.com/issues/10436),
    [pr#7495](http://github.com/ceph/ceph/pull/7495), Yan, Zheng)
-   client: fsync waits only for inode\'s caps to flush (Yan, Zheng)
-   client: invalidate kernel dcache when cache size exceeds limits
    (Yan, Zheng)
-   client: make fsync wait for unsafe dir operations (Yan, Zheng)
-   client: modify a word in log
    ([pr#6906](http://github.com/ceph/ceph/pull/6906), YongQiang He)
-   client: pin lookup dentry to avoid inode being freed (Yan, Zheng)
-   client: properly trim unlinked inode
    ([issue#13903](http://tracker.ceph.com/issues/13903),
    [pr#7297](http://github.com/ceph/ceph/pull/7297), Yan, Zheng)
-   client: removed unused Mutex from MetaRequest
    ([pr#7655](http://github.com/ceph/ceph/pull/7655), Greg Farnum)
-   client: sys/file.h includes for flock operations
    ([pr#6282](http://github.com/ceph/ceph/pull/6282), John Coyle)
-   client: use null snapc to check pool permission
    ([issue#13714](http://tracker.ceph.com/issues/13714),
    [pr#6497](http://github.com/ceph/ceph/pull/6497), Yan, Zheng)
-   cls/cls_rbd.cc: fix misused metadata_name_from_key
    ([issue#13922](http://tracker.ceph.com/issues/13922),
    [pr#6661](http://github.com/ceph/ceph/pull/6661), Xiaoxi Chen)
-   cls/cls_rbd: pass string by reference
    ([pr#7232](http://github.com/ceph/ceph/pull/7232), Jeffrey Lu)
-   cls_hello: Fix grammatical error in description comment
    ([pr#7951](http://github.com/ceph/ceph/pull/7951), Brad Hubbard)
-   cls_journal: fix -EEXIST checking
    ([pr#8413](http://github.com/ceph/ceph/pull/8413), runsisi)
-   cls_rbd: add guards for error cases
    ([issue#14316](http://tracker.ceph.com/issues/14316),
    [issue#14317](http://tracker.ceph.com/issues/14317),
    [pr#7165](http://github.com/ceph/ceph/pull/7165), xie xingguo)
-   cls_rbd: change object_map_update to return 0 on success, add
    logging ([pr#6467](http://github.com/ceph/ceph/pull/6467), Douglas
    Fuller)
-   cls_rbd: enable object map checksums for object_map_save
    ([issue#14280](http://tracker.ceph.com/issues/14280),
    [pr#7149](http://github.com/ceph/ceph/pull/7149), Douglas Fuller)
-   cls_rbd: fix -EEXIST checking in cls::rbd::image_set
    ([pr#8371](http://github.com/ceph/ceph/pull/8371), runsisi)
-   cls_rbd: fix the test for ceph-dencoder
    ([pr#7793](http://github.com/ceph/ceph/pull/7793), Kefu Chai)
-   cls_rbd: mirror_image_list should return global image id
    ([pr#8297](http://github.com/ceph/ceph/pull/8297), Jason Dillaman)
-   cls_rbd: mirroring directory
    ([issue#14419](http://tracker.ceph.com/issues/14419),
    [pr#7620](http://github.com/ceph/ceph/pull/7620), Josh Durgin)
-   cls_rbd: pass WILLNEED fadvise flags during object map update
    ([issue#15332](http://tracker.ceph.com/issues/15332),
    [pr#8380](http://github.com/ceph/ceph/pull/8380), Jason Dillaman)
-   cls_rbd: protect against excessively large object maps
    ([issue#15121](http://tracker.ceph.com/issues/15121),
    [pr#8099](http://github.com/ceph/ceph/pull/8099), Jason Dillaman)
-   cls_rbd: read_peers: update last_read on next cls_cxx_map_get_vals
    ([pr#8374](http://github.com/ceph/ceph/pull/8374), Mykola Golub)
-   cls/rgw: fix FTBFS
    ([pr#8142](http://github.com/ceph/ceph/pull/8142), Kefu Chai)
-   cls/rgw: fix use of timespan
    ([issue#15181](http://tracker.ceph.com/issues/15181),
    [pr#8212](http://github.com/ceph/ceph/pull/8212), Yehuda Sadeh)
-   cmake: add common/fs_types.cc to libcommon
    ([pr#7898](http://github.com/ceph/ceph/pull/7898), Orit Wasserman)
-   cmake: Add common/PluginRegistry.cc to CMakeLists.txt
    ([pr#6805](http://github.com/ceph/ceph/pull/6805), Pete Zaitcev)
-   cmake: Added new unittests to make check
    ([pr#7572](http://github.com/ceph/ceph/pull/7572), Ali Maredia)
-   cmake: Add ENABLE_GIT_VERSION to avoid rebuilding
    ([pr#7171](http://github.com/ceph/ceph/pull/7171), Kefu Chai)
-   cmake: add ErasureCode.cc to jerasure plugins
    ([pr#7808](http://github.com/ceph/ceph/pull/7808), Casey Bodley)
-   cmake: add FindOpenSSL.cmake
    ([pr#8106](http://github.com/ceph/ceph/pull/8106), Marcus Watts,
    Matt Benjamin)
-   cmake: add KernelDevice.cc to libos_srcs
    ([pr#7507](http://github.com/ceph/ceph/pull/7507), Kefu Chai)
-   cmake: add missing check for HAVE_EXECINFO_H
    ([pr#7270](http://github.com/ceph/ceph/pull/7270), Casey Bodley)
-   cmake: add missing librbd image_watcher sources
    ([issue#14823](http://tracker.ceph.com/issues/14823),
    [pr#7717](http://github.com/ceph/ceph/pull/7717), Casey Bodley)
-   cmake: add missing librbd/MirrorWatcher.cc and
    librd/ObjectWatcher.cc
    ([pr#8399](http://github.com/ceph/ceph/pull/8399), Orit Wasserman)
-   cmake: add nss as a suffix for pk11pub.h
    ([pr#6556](http://github.com/ceph/ceph/pull/6556), Samuel Just)
-   cmake: add rgw_basic_types.cc to librgw.a
    ([pr#6786](http://github.com/ceph/ceph/pull/6786), Orit Wasserman)
-   cmake: add StandardPolicy.cc to librbd
    ([pr#8368](http://github.com/ceph/ceph/pull/8368), Kefu Chai)
-   cmake: add TracepointProvider.cc to libcommon
    ([pr#6823](http://github.com/ceph/ceph/pull/6823), Orit Wasserman)
-   cmake: avoid false-positive LDAP header detect
    ([pr#8100](http://github.com/ceph/ceph/pull/8100), Matt Benjamin)
-   cmake: Build cython modules and change paths to bin/, lib/
    ([pr#8351](http://github.com/ceph/ceph/pull/8351), John Spray, Ali
    Maredia)
-   cmake: check for libsnappy in default path also
    ([pr#7366](http://github.com/ceph/ceph/pull/7366), Kefu Chai)
-   cmake: cleanups and more features from automake
    ([pr#7103](http://github.com/ceph/ceph/pull/7103), Casey Bodley, Ali
    Maredia)
-   cmake: define STRERROR_R_CHAR_P for GNU-specific strerror_r
    ([pr#6751](http://github.com/ceph/ceph/pull/6751), Ilya Dryomov)
-   cmake: detect bzip2 and lz4
    ([pr#7126](http://github.com/ceph/ceph/pull/7126), Kefu Chai)
-   cmake: feb5 ([pr#7541](http://github.com/ceph/ceph/pull/7541), Matt
    Benjamin)
-   cmake: fix build with bluestore
    ([pr#7099](http://github.com/ceph/ceph/pull/7099), John Spray)
-   cmake: fix files list
    ([pr#6539](http://github.com/ceph/ceph/pull/6539), Yehuda Sadeh)
-   cmake: fix mrun to handle cmake build structure
    ([pr#8237](http://github.com/ceph/ceph/pull/8237), Orit Wasserman)
-   cmake: fix paths to various EC source files
    ([pr#7748](http://github.com/ceph/ceph/pull/7748), Ali Maredia, Matt
    Benjamin)
-   cmake: fix the build of test_rados_api_list
    ([pr#8438](http://github.com/ceph/ceph/pull/8438), Kefu Chai)
-   cmake: fix the build of tests
    ([pr#7523](http://github.com/ceph/ceph/pull/7523), Kefu Chai)
-   cmake: fix the build on trusty
    ([pr#7249](http://github.com/ceph/ceph/pull/7249), Kefu Chai)
-   cmake: For CMake version \<= 2.8.11, use LINK_PRIVATE and
    LINK_PUBLIC ([pr#7474](http://github.com/ceph/ceph/pull/7474), Tao
    Chang)
-   CMake: For CMake version \<= 2.8.11, use LINK_PRIVATE
    ([pr#8422](http://github.com/ceph/ceph/pull/8422), Haomai Wang)
-   cmake: let ceph-client-debug link with tcmalloc
    ([pr#7314](http://github.com/ceph/ceph/pull/7314), Kefu Chai)
-   cmake: librbd and libjournal build fixes
    ([pr#6557](http://github.com/ceph/ceph/pull/6557), Ilya Dryomov)
-   cmake: made rocksdb an imported library
    ([pr#7131](http://github.com/ceph/ceph/pull/7131), Ali Maredia)
-   cmake: no need to run configure from run-cmake-check.sh
    ([pr#6959](http://github.com/ceph/ceph/pull/6959), Orit Wasserman)
-   cmake ([pr#7849](http://github.com/ceph/ceph/pull/7849), Ali
    Maredia)
-   cmake: Remove duplicate find_package libcurl line.
    ([pr#7972](http://github.com/ceph/ceph/pull/7972), Brad Hubbard)
-   cmake: support ccache via a WITH_CCACHE build option
    ([pr#6875](http://github.com/ceph/ceph/pull/6875), John Coyle)
-   cmake: test_build_libcephfs needs \${ALLOC_LIBS}
    ([pr#7300](http://github.com/ceph/ceph/pull/7300), Ali Maredia)
-   cmake: update for recent librbd changes
    ([pr#6715](http://github.com/ceph/ceph/pull/6715), John Spray)
-   cmake: update for recent rbd changes
    ([pr#6818](http://github.com/ceph/ceph/pull/6818), Mykola Golub)
-   cmake: Use uname instead of arch.
    ([pr#6358](http://github.com/ceph/ceph/pull/6358), John Coyle)
-   coc: fix typo in the apt-get command
    ([pr#6659](http://github.com/ceph/ceph/pull/6659), Chris Holcombe)
-   common: add descriptions to perfcounters (Kiseleva Alyona)
-   common: add generic plugin infrastructure
    ([pr#6696](http://github.com/ceph/ceph/pull/6696), Sage Weil)
-   common: add latency perf counter for finisher
    ([pr#6175](http://github.com/ceph/ceph/pull/6175), Xinze Chi)
-   common: add perf counter descriptions (Alyona Kiseleva)
-   common/address_help.cc: fix the leak in entity_addr_from_url()
    ([issue#14132](http://tracker.ceph.com/issues/14132),
    [pr#6987](http://github.com/ceph/ceph/pull/6987), Qiankun Zheng)
-   common: add thread names
    ([pr#5882](http://github.com/ceph/ceph/pull/5882), Igor Podoski)
-   common: add zlib compression plugin
    ([pr#7437](http://github.com/ceph/ceph/pull/7437), Alyona Kiseleva,
    Kiseleva Alyona)
-   common: admin socket commands for tcmalloc heap get/set operations
    ([pr#7512](http://github.com/ceph/ceph/pull/7512), Samuel Just)
-   common: ake ceph_time clocks work under BSD
    ([pr#7340](http://github.com/ceph/ceph/pull/7340), Adam C. Emerson)
-   common: allow enable/disable of optracker at runtime
    ([pr#5168](http://github.com/ceph/ceph/pull/5168), Jianpeng Ma)
-   common: Allow OPT_INT settings with negative values
    ([issue#13829](http://tracker.ceph.com/issues/13829),
    [pr#7390](http://github.com/ceph/ceph/pull/7390), Brad Hubbard, Kefu
    Chai)
-   common: assert: abort() rather than throw
    ([pr#6804](http://github.com/ceph/ceph/pull/6804), Adam C. Emerson)
-   common: assert: \_\_STRING macro is not defined by musl libc.
    ([pr#6210](http://github.com/ceph/ceph/pull/6210), John Coyle)
-   common/bit_vector: use hard-coded value for block size
    ([issue#14747](http://tracker.ceph.com/issues/14747),
    [pr#7610](http://github.com/ceph/ceph/pull/7610), Jason Dillaman)
-   common: buffer: add cached_crc and cached_crc_adjust counts to perf
    dump ([pr#6535](http://github.com/ceph/ceph/pull/6535), Ning Yao)
-   common: buffer/assert minor fixes
    ([pr#6990](http://github.com/ceph/ceph/pull/6990), Matt Benjamin)
-   common: bufferlist performance tuning (Piotr Dalek, Sage Weil)
-   common: buffer: put a guard for stat() syscall during read_file
    ([pr#7956](http://github.com/ceph/ceph/pull/7956), xie xingguo)
-   common: buffer: remove unneeded list destructor
    ([pr#6456](http://github.com/ceph/ceph/pull/6456), Michal Jarzabek)
-   common/buffer: replace RWLock with spinlocks
    ([pr#7294](http://github.com/ceph/ceph/pull/7294), Piotr Dałek)
-   common/ceph_context.cc:fix order of initialisers
    ([pr#6838](http://github.com/ceph/ceph/pull/6838), Michal Jarzabek)
-   common: change the type of counter total/unhealthy_workers
    ([pr#7254](http://github.com/ceph/ceph/pull/7254), Guang Yang)
-   common: default cluster name to config file prefix
    ([pr#7364](http://github.com/ceph/ceph/pull/7364), Javen Wu)
-   common: Deprecate or free up a bunch of feature bits
    ([pr#8214](http://github.com/ceph/ceph/pull/8214), Samuel Just)
-   common: detect overflow of int config values (#11484 Kefu Chai)
-   common: Do not use non-portable constants in mutex_debug
    ([pr#7766](http://github.com/ceph/ceph/pull/7766), Adam C. Emerson)
-   common: don\'t reverse hobject_t hash bits when zero
    ([pr#6653](http://github.com/ceph/ceph/pull/6653), Piotr Dałek)
-   common: fix bit_vector extent calc (#12611 Jason Dillaman)
-   common: fix json parsing of utf8 (#7387 Tim Serong)
-   common: fix leak of pthread_mutexattr (#11762 Ketor Meng)
-   common: fix LTTNG vs fork issue (Josh Durgin)
-   common: fix OpTracker age histogram calculation
    ([pr#5065](http://github.com/ceph/ceph/pull/5065), Zhiqiang Wang)
-   common: fix race during optracker switches between enabled/disabled
    mode ([pr#8330](http://github.com/ceph/ceph/pull/8330), xie xingguo)
-   common: fix reset max in Throttle using perf reset command
    ([issue#13517](http://tracker.ceph.com/issues/13517),
    [pr#6300](http://github.com/ceph/ceph/pull/6300), Xinze Chi)
-   common: fix throttle max change (Henry Chang)
-   common: fix time_t cast in decode
    ([issue#15330](http://tracker.ceph.com/issues/15330),
    [pr#8419](http://github.com/ceph/ceph/pull/8419), Adam C. Emerson)
-   common/Formatter: avoid newline if there is no output
    ([pr#5351](http://github.com/ceph/ceph/pull/5351), Aran85)
-   common: improve shared_cache and simple_cache efficiency with hash
    table ([pr#6909](http://github.com/ceph/ceph/pull/6909), Ning Yao)
-   common/lockdep: increase max lock names
    ([pr#6961](http://github.com/ceph/ceph/pull/6961), Sage Weil)
-   common: log: Assign LOG_DEBUG priority to syslog calls
    ([issue#13993](http://tracker.ceph.com/issues/13993),
    [pr#6815](http://github.com/ceph/ceph/pull/6815), Brad Hubbard)
-   common: log: predict log message buffer allocation size
    ([pr#6641](http://github.com/ceph/ceph/pull/6641), Adam Kupczyk)
-   common: make mutex more efficient
-   common: make work queue addition/removal thread safe (#12662 Jason
    Dillaman)
-   common/MemoryModel: Added explicit feature check for mallinfo().
    ([pr#6252](http://github.com/ceph/ceph/pull/6252), John Coyle)
-   common: new timekeeping common code, and Objecter conversion
    ([pr#5782](http://github.com/ceph/ceph/pull/5782), Adam C. Emerson)
-   common/obj_bencher.cc: bump the precision of bandwidth field
    ([pr#8021](http://github.com/ceph/ceph/pull/8021), Piotr Dałek)
-   common/obj_bencher.cc: faster object name generation
    ([pr#7863](http://github.com/ceph/ceph/pull/7863), Piotr Dałek)
-   common/obj_bencher.cc: fix verification crashing when there\'s no
    objects ([pr#5853](http://github.com/ceph/ceph/pull/5853), Piotr
    Dałek)
-   common/obj_bencher.cc: make verify error fatal
    ([issue#14971](http://tracker.ceph.com/issues/14971),
    [pr#7897](http://github.com/ceph/ceph/pull/7897), Piotr Dałek)
-   common: optimize debug logging code
    ([pr#6441](http://github.com/ceph/ceph/pull/6441), Adam Kupczyk)
-   common: optimize debug logging
    ([pr#6307](http://github.com/ceph/ceph/pull/6307), Adam Kupczyk)
-   common: optracker improvements (Zhiqiang Wang, Jianpeng Ma)
-   common/page.cc: \_page_mask has too many bits
    ([pr#7588](http://github.com/ceph/ceph/pull/7588), Dan Mick)
-   common: perf counter for bufferlist history total alloc
    ([pr#6198](http://github.com/ceph/ceph/pull/6198), Xinze Chi)
-   common: PriorityQueue tests (Kefu Chai)
-   common: reduce CPU usage by making stringstream in stringify
    function thread local
    ([pr#6543](http://github.com/ceph/ceph/pull/6543), Evgeniy Firsov)
-   common: re-enable backtrace support
    ([pr#6771](http://github.com/ceph/ceph/pull/6771), Jason Dillaman)
-   common: set thread name from correct thread
    ([pr#7845](http://github.com/ceph/ceph/pull/7845), Igor Podoski)
-   common: signal_handler: added support for using reentrant
    strsignal() implementations vs. sys_siglist\[\]
    ([pr#6796](http://github.com/ceph/ceph/pull/6796), John Coyle)
-   common: snappy decompressor may assert when handling segmented input
    bufferlist ([issue#14400](http://tracker.ceph.com/issues/14400),
    [pr#7268](http://github.com/ceph/ceph/pull/7268), Igor Fedotov)
-   common: some async compression infrastructure (Haomai Wang)
-   common/str_map: cleanup: replaced get_str_map() function overloading
    by using default parameters for delimiters
    ([pr#7266](http://github.com/ceph/ceph/pull/7266), Sahithi R V)
-   common/strtol.cc: fix the coverity warnings
    ([pr#7967](http://github.com/ceph/ceph/pull/7967), Kefu Chai)
-   common: SubProcess: Avoid buffer corruption when calling err()
    ([issue#15011](http://tracker.ceph.com/issues/15011),
    [pr#8054](http://github.com/ceph/ceph/pull/8054), Erwan Velu)
-   common: SubProcess: fix multiple definition bug
    ([pr#6790](http://github.com/ceph/ceph/pull/6790), Yunchuan Wen)
-   common: Thread: move copy constructor and assignment op
    ([pr#5133](http://github.com/ceph/ceph/pull/5133), Michal Jarzabek)
-   common: time: have skewing-now call non-skewing now
    ([pr#7466](http://github.com/ceph/ceph/pull/7466), Adam C. Emerson)
-   common/TrackedOp: fix inaccurate counting for slow requests
    ([issue#14804](http://tracker.ceph.com/issues/14804),
    [pr#7690](http://github.com/ceph/ceph/pull/7690), xie xingguo)
-   common: unit test for interval_set implementations
    ([pr#6](http://github.com/ceph/ceph/pull/6), Igor Fedotov)
-   common: use namespace instead of subclasses for buffer
    ([pr#6686](http://github.com/ceph/ceph/pull/6686), Michal Jarzabek)
-   common: various fixes from SCA runs
    ([pr#7680](http://github.com/ceph/ceph/pull/7680), Danny Al-Gaaf)
-   common: WorkQueue: new PointerWQ base class for ContextWQ
    ([issue#13636](http://tracker.ceph.com/issues/13636),
    [pr#6525](http://github.com/ceph/ceph/pull/6525), Jason Dillaman)
-   compat: use prefixed typeof extension
    ([pr#6216](http://github.com/ceph/ceph/pull/6216), John Coyle)
-   config: add \$data_dir/config to config search path
    ([pr#7377](http://github.com/ceph/ceph/pull/7377), Sage Weil)
-   config: complains when a setting is not tracked
    ([issue#11692](http://tracker.ceph.com/issues/11692),
    [pr#7085](http://github.com/ceph/ceph/pull/7085), Kefu Chai)
-   config: fix osd_crush_initial_weight
    ([pr#7975](http://github.com/ceph/ceph/pull/7975), You Ji)
-   config: increase default async op threads
    ([pr#7802](http://github.com/ceph/ceph/pull/7802), Piotr Dałek)
-   config_opts: disable filestore throttle soft backoff by default
    ([pr#8265](http://github.com/ceph/ceph/pull/8265), Samuel Just)
-   configure.ac: boost_iostreams is required, not optional
    ([pr#7816](http://github.com/ceph/ceph/pull/7816), Hector Martin)
-   configure.ac: macro fix
    ([pr#6769](http://github.com/ceph/ceph/pull/6769), Igor Podoski)
-   configure.ac: make \"\--with-librocksdb-static\" default to
    \'check\' ([issue#14463](http://tracker.ceph.com/issues/14463),
    [pr#7317](http://github.com/ceph/ceph/pull/7317), Dan Mick)
-   configure.ac: update help strings for cython
    ([pr#7856](http://github.com/ceph/ceph/pull/7856), Josh Durgin)
-   configure: Add -D_LARGEFILE64_SOURCE to Linux build.
    ([pr#8402](http://github.com/ceph/ceph/pull/8402), Ira Cooper)
-   configure: detect bz2 and lz4
    ([issue#13850](http://tracker.ceph.com/issues/13850),
    [issue#13981](http://tracker.ceph.com/issues/13981),
    [pr#7030](http://github.com/ceph/ceph/pull/7030), Kefu Chai)
-   correct radosgw-admin command
    ([pr#7006](http://github.com/ceph/ceph/pull/7006), YankunLi)
-   crush: add \--check to validate dangling names, max osd id (Kefu
    Chai)
-   crush: add chooseleaf_stable tunable
    ([pr#6572](http://github.com/ceph/ceph/pull/6572), Sangdi Xu, Sage
    Weil)
-   crush: add safety assert
    ([issue#14496](http://tracker.ceph.com/issues/14496),
    [pr#7344](http://github.com/ceph/ceph/pull/7344), songbaisen)
-   crush: cleanup, sync with kernel (Ilya Dryomov)
-   crush: clean up whitespace removal
    ([issue#14302](http://tracker.ceph.com/issues/14302),
    [pr#7157](http://github.com/ceph/ceph/pull/7157), songbaisen)
-   crush/CrushTester: check for overlapped rules
    ([pr#7139](http://github.com/ceph/ceph/pull/7139), Kefu Chai)
-   crush/CrushTester: workaround a bug in boost::icl
    ([pr#7560](http://github.com/ceph/ceph/pull/7560), Kefu Chai)
-   crush: fix cli tests for new crush tunables
    ([pr#8107](http://github.com/ceph/ceph/pull/8107), Sage Weil)
-   crush: fix crash from invalid \'take\' argument (#11602 Shiva
    Rkreddy, Sage Weil)
-   crush: fix divide-by-2 in straw2 (#11357 Yann Dupont, Sage Weil)
-   crush: fix error log
    ([pr#8430](http://github.com/ceph/ceph/pull/8430), Wei Jin)
-   crush: fix has_v4_buckets (#11364 Sage Weil)
-   crush: fix subtree base weight on adjust_subtree_weight (#11855 Sage
    Weil)
-   crush: fix typo ([pr#8518](http://github.com/ceph/ceph/pull/8518),
    Wei Jin)
-   crush: reply quickly from get_immediate_parent
    ([issue#14334](http://tracker.ceph.com/issues/14334),
    [pr#7181](http://github.com/ceph/ceph/pull/7181), song baisen)
-   crush: respect default replicated ruleset config on map creation
    (Ilya Dryomov)
-   crushtool: Don\'t crash when called on a file that isn\'t a crushmap
    ([issue#8286](http://tracker.ceph.com/issues/8286),
    [pr#8038](http://github.com/ceph/ceph/pull/8038), Brad Hubbard)
-   crushtool: fix order of operations, usage (Sage Weil)
-   crushtool: improve usage/tip messages
    ([pr#7142](http://github.com/ceph/ceph/pull/7142), xie xingguo)
-   crushtool: set type 0 name \"device\" for \--build option
    ([pr#6824](http://github.com/ceph/ceph/pull/6824), Sangdi Xu)
-   crush: update tunable docs. change default profile to jewel
    ([pr#7964](http://github.com/ceph/ceph/pull/7964), Sage Weil)
-   crush: validate bucket id before indexing buckets array
    ([issue#13477](http://tracker.ceph.com/issues/13477),
    [pr#6246](http://github.com/ceph/ceph/pull/6246), Sage Weil)
-   crypto: fix NSS leak (Jason Dillaman)
-   crypto: fix unbalanced init/shutdown (#12598 Zheng Yan)
-   deb: fix rest-bench-dbg and ceph-test-dbg dependendies (Ken Dreyer)
-   debian/changelog: Remove stray \'v\' in version
    ([pr#7936](http://github.com/ceph/ceph/pull/7936), Dan Mick)
-   debian/changelog: Remove stray \'v\' in version
    ([pr#7938](http://github.com/ceph/ceph/pull/7938), Dan Mick)
-   debian: include cpio in build-requiers
    ([pr#7533](http://github.com/ceph/ceph/pull/7533), Rémi BUISSON)
-   debian: minor package reorg (Ken Dreyer)
-   debian: package librgw_file\* tests
    ([pr#7930](http://github.com/ceph/ceph/pull/7930), Ken Dreyer)
-   debian: packaging fixes for jewel
    ([pr#7807](http://github.com/ceph/ceph/pull/7807), Ken Dreyer, Ali
    Maredia)
-   debian/rpm split servers
    ([issue#10587](http://tracker.ceph.com/issues/10587),
    [pr#7746](http://github.com/ceph/ceph/pull/7746), Ken Dreyer)
-   debian/rules: put init-ceph in /etc/init.d/ceph, not ceph-base
    ([issue#15329](http://tracker.ceph.com/issues/15329),
    [pr#8406](http://github.com/ceph/ceph/pull/8406), Dan Mick)
-   deb, rpm: move ceph-objectstore-tool to ceph (Ken Dreyer)
-   doc: add ceph-detect-init(8) source to dist tarball
    ([pr#7933](http://github.com/ceph/ceph/pull/7933), Ken Dreyer)
-   doc: add cinder backend section to rbd-openstack.rst
    ([pr#7923](http://github.com/ceph/ceph/pull/7923), RustShen)
-   doc: adding \"\--allow-shrink\" in decreasing the size of the rbd
    block to distinguish from the increasing option
    ([pr#7020](http://github.com/ceph/ceph/pull/7020), Yehua)
-   doc: add orphans commands to radosgw-admin(8)
    ([issue#14637](http://tracker.ceph.com/issues/14637),
    [pr#7518](http://github.com/ceph/ceph/pull/7518), Ken Dreyer)
-   doc: add v0.80.11 to the release timeline
    ([pr#6658](http://github.com/ceph/ceph/pull/6658), Loic Dachary)
-   doc: admin/build-doc: add lxml dependencies on debian
    ([pr#6610](http://github.com/ceph/ceph/pull/6610), Ken Dreyer)
-   doc: admin/build-doc: make paths absolute
    ([pr#7119](http://github.com/ceph/ceph/pull/7119), Dan Mick)
-   doc: amend Fixes instructions in SubmittingPatches
    ([pr#8312](http://github.com/ceph/ceph/pull/8312), Nathan Cutler)
-   doc: amend the rados.8
    ([pr#7251](http://github.com/ceph/ceph/pull/7251), Kefu Chai)
-   doc/architecture.rst: remove redundant word \"across\"
    ([pr#8179](http://github.com/ceph/ceph/pull/8179), Zhao Junwang)
-   doc/cephfs/posix: update
    ([pr#6922](http://github.com/ceph/ceph/pull/6922), Sage Weil)
-   doc: Clarify usage on starting single osd/mds/mon.
    ([pr#7641](http://github.com/ceph/ceph/pull/7641), Patrick Donnelly)
-   doc: CodingStyle: fix broken URLs
    ([pr#6733](http://github.com/ceph/ceph/pull/6733), Kefu Chai)
-   doc: correct typo \'restared\' to \'restarted\'
    ([pr#6734](http://github.com/ceph/ceph/pull/6734), Yilong Zhao)
-   doc: detailed description of bugfixing workflow
    ([pr#7941](http://github.com/ceph/ceph/pull/7941), Nathan Cutler)
-   doc/dev: add \"Deploy a cluster for manual testing\" section
    ([issue#15218](http://tracker.ceph.com/issues/15218),
    [pr#8228](http://github.com/ceph/ceph/pull/8228), Nathan Cutler)
-   doc/dev: add section on interrupting a running suite
    ([pr#8116](http://github.com/ceph/ceph/pull/8116), Nathan Cutler)
-   doc/dev: continue writing Testing in the cloud chapter
    ([pr#7960](http://github.com/ceph/ceph/pull/7960), Nathan Cutler)
-   doc: dev: document ceph-qa-suite
    ([pr#6955](http://github.com/ceph/ceph/pull/6955), Loic Dachary)
-   doc/dev/index: refactor/reorg
    ([pr#6792](http://github.com/ceph/ceph/pull/6792), Nathan Cutler)
-   doc/dev/index.rst: begin writing Contributing to Ceph
    ([pr#6727](http://github.com/ceph/ceph/pull/6727), Nathan Cutler)
-   doc/dev/index.rst: fix headings
    ([pr#6780](http://github.com/ceph/ceph/pull/6780), Nathan Cutler)
-   doc/dev: integrate testing into the narrative
    ([pr#7946](http://github.com/ceph/ceph/pull/7946), Nathan Cutler)
-   doc: dev: introduction to tests
    ([pr#6910](http://github.com/ceph/ceph/pull/6910), Loic Dachary)
-   doc/dev: various refinements
    ([pr#7954](http://github.com/ceph/ceph/pull/7954), Nathan Cutler)
-   doc: docuemnt object corpus generation (#11099 Alexis Normand)
-   doc: document \"readforward\" and \"readproxy\" cache mode
    ([pr#7023](http://github.com/ceph/ceph/pull/7023), Kefu Chai)
-   doc: document region hostnames (Robin H. Johnson)
-   doc: download GPG key from download.ceph.com
    ([issue#13603](http://tracker.ceph.com/issues/13603),
    [pr#6384](http://github.com/ceph/ceph/pull/6384), Ken Dreyer)
-   doc: draft notes for jewel
    ([pr#8211](http://github.com/ceph/ceph/pull/8211), Loic Dachary,
    Sage Weil)
-   doc: file must be empty when writing layout fields of file use
    \"setfattr\" ([pr#6848](http://github.com/ceph/ceph/pull/6848),
    Cilang Zhao)
-   doc: fix 0.94.4 and 0.94.5 ordering
    ([pr#7763](http://github.com/ceph/ceph/pull/7763), Loic Dachary)
-   doc: Fixed incorrect name of a \"List Multipart Upload Parts\"
    Response Entity
    ([issue#14003](http://tracker.ceph.com/issues/14003),
    [pr#6829](http://github.com/ceph/ceph/pull/6829), Lenz Grimmer)
-   doc: Fixes a CRUSH map step take argument
    ([pr#7327](http://github.com/ceph/ceph/pull/7327), Ivan Grcic)
-   doc: Fixes a spelling error
    ([pr#6705](http://github.com/ceph/ceph/pull/6705), Jeremy Qian)
-   doc: Fixes headline different font size and type
    ([pr#8328](http://github.com/ceph/ceph/pull/8328), scienceluo)
-   doc: fix gender neutrality (Alexandre Maragone)
-   doc: fixing image in section ERASURE CODING
    ([pr#7298](http://github.com/ceph/ceph/pull/7298), Rachana Patel)
-   doc: fix install doc (#10957 Kefu Chai)
-   doc: fix misleading configuration guide on cache tiering
    ([pr#7000](http://github.com/ceph/ceph/pull/7000), Yuan Zhou)
-   doc: fix \"mon osd down out subtree limit\" option name
    ([pr#7164](http://github.com/ceph/ceph/pull/7164), François Lafont)
-   doc: fix outdated content in cache tier
    ([pr#6272](http://github.com/ceph/ceph/pull/6272), Yuan Zhou)
-   doc: fix S3 C# example
    ([pr#7027](http://github.com/ceph/ceph/pull/7027), Dunrong Huang)
-   doc: fix sphinx issues (Kefu Chai)
-   doc: fix typo, duplicated content etc. for Jewel release notes
    ([pr#8342](http://github.com/ceph/ceph/pull/8342), xie xingguo)
-   doc: fix typo in cephfs/quota
    ([pr#6745](http://github.com/ceph/ceph/pull/6745), Drunkard Zhang)
-   doc: fix typo, indention etc.
    ([pr#7829](http://github.com/ceph/ceph/pull/7829), xie xingguo)
-   doc: fix typo in developer guide
    ([pr#6943](http://github.com/ceph/ceph/pull/6943), Nathan Cutler)
-   doc: fix typo ([pr#7004](http://github.com/ceph/ceph/pull/7004),
    tianqing)
-   doc: fix wrong type of hyphen
    ([pr#8252](http://github.com/ceph/ceph/pull/8252), xie xingguo)
-   doc: initial draft of RBD mirroring admin documentation
    ([issue#15041](http://tracker.ceph.com/issues/15041),
    [pr#8169](http://github.com/ceph/ceph/pull/8169), Jason Dillaman)
-   doc: INSTALL redirect to online documentation
    ([pr#6749](http://github.com/ceph/ceph/pull/6749), Loic Dachary)
-   doc: little improvements for troubleshooting scrub issues
    ([pr#6827](http://github.com/ceph/ceph/pull/6827), Mykola Golub)
-   doc: man page updates (Kefu Chai)
-   doc: mds data structure docs (Yan, Zheng)
-   doc: misc updates (Francois Lafont, Ken Dreyer, Kefu Chai, Owen
    Synge, Gael Fenet-Garde, Loic Dachary, Yannick Atchy-Dalama, Jiaying
    Ren, Kevin Caradant, Robert Maxime, Nicolas Yong, Germain Chipaux,
    Arthur Gorjux, Gabriel Sentucq, Clement Lebrun, Jean-Remi Deveaux,
    Clair Massot, Robin Tang, Thomas Laumondais, Jordan Dorne, Yuan
    Zhou, Valentin Thomas, Pierre Chaumont, Benjamin Troquereau,
    Benjamin Sesia, Vikhyat Umrao, Nilamdyuti Goswami, Vartika Rai,
    Florian Haas, Loic Dachary, Simon Guinot, Andy Allan, Alistair
    Israel, Ken Dreyer, Robin Rehu, Lee Revell, Florian Marsylle, Thomas
    Johnson, Bosse Klykken, Travis Rhoden, Ian Kelling)
-   doc: Modified a note section in rbd-snapshot doc.
    ([pr#6908](http://github.com/ceph/ceph/pull/6908), Nilamdyuti
    Goswami)
-   doc: note that cephfs auth stuff is new in jewel
    ([pr#6858](http://github.com/ceph/ceph/pull/6858), John Spray)
-   doc: osd-config Add Configuration Options for op queue.
    ([pr#7837](http://github.com/ceph/ceph/pull/7837), Robert LeBlanc)
-   doc: osd: s/schedued/scheduled/
    ([pr#6872](http://github.com/ceph/ceph/pull/6872), Loic Dachary)
-   doc/rados/api/librados-intro.rst: fix typo
    ([pr#7879](http://github.com/ceph/ceph/pull/7879), xie xingguo)
-   doc/rados/operations/crush: fix the formatting
    ([pr#8306](http://github.com/ceph/ceph/pull/8306), Kefu Chai)
-   doc: release-notes: draft v0.80.11 release notes
    ([pr#6374](http://github.com/ceph/ceph/pull/6374), Loic Dachary)
-   doc: release-notes: draft v10.0.0 release notes
    ([pr#6666](http://github.com/ceph/ceph/pull/6666), Loic Dachary)
-   doc/release-notes: fix indents
    ([pr#8345](http://github.com/ceph/ceph/pull/8345), Kefu Chai)
-   doc/release-notes: v9.1.0
    ([pr#6281](http://github.com/ceph/ceph/pull/6281), Loic Dachary)
-   doc/releases-notes: fix build error
    ([pr#6483](http://github.com/ceph/ceph/pull/6483), Kefu Chai)
-   doc: Remove Ceph Monitors do lots of fsync()
    ([issue#15288](http://tracker.ceph.com/issues/15288),
    [pr#8327](http://github.com/ceph/ceph/pull/8327), Vikhyat Umrao)
-   doc: remove redundant space in ceph-authtool/monmaptool doc
    ([pr#7244](http://github.com/ceph/ceph/pull/7244), Jiaying Ren)
-   doc: remove toctree items under Create CephFS
    ([pr#6241](http://github.com/ceph/ceph/pull/6241), Jevon Qiao)
-   doc: remove unnecessary period in headline
    ([pr#6775](http://github.com/ceph/ceph/pull/6775), Marc Koderer)
-   doc: rename the \"Create a Ceph User\" section and add verbage
    about... ([issue#13502](http://tracker.ceph.com/issues/13502),
    [pr#6297](http://github.com/ceph/ceph/pull/6297), ritz303)
-   doc: revise SubmittingPatches
    ([pr#7292](http://github.com/ceph/ceph/pull/7292), Kefu Chai)
-   doc: rgw admin uses \"region list\" not \"regions list\"
    ([pr#8517](http://github.com/ceph/ceph/pull/8517), Kris Jurka)
-   doc: rgw explain keystone\'s verify ssl switch
    ([pr#7862](http://github.com/ceph/ceph/pull/7862), Abhishek
    Lekshmanan)
-   doc: rgw: port changes from downstream to upstream
    ([pr#7264](http://github.com/ceph/ceph/pull/7264), Bara Ancincova)
-   doc: rgw_region_root_pool option should be in \[global\]
    ([issue#15244](http://tracker.ceph.com/issues/15244),
    [pr#8271](http://github.com/ceph/ceph/pull/8271), Vikhyat Umrao)
-   doc: rst style fix for pools document
    ([pr#6816](http://github.com/ceph/ceph/pull/6816), Drunkard Zhang)
-   doc: script and guidelines for mirroring Ceph
    ([pr#7384](http://github.com/ceph/ceph/pull/7384), Wido den
    Hollander)
-   docs: Fix styling of newly added mirror docs
    ([pr#6127](http://github.com/ceph/ceph/pull/6127), Wido den
    Hollander)
-   doc: small fixes ([pr#7813](http://github.com/ceph/ceph/pull/7813),
    xiexingguo)
-   doc: standardize \@param (not \@parma, \@parmam, \@params)
    ([pr#7714](http://github.com/ceph/ceph/pull/7714), Nathan Cutler)
-   doc: SubmittingPatches: there is no next; only jewel
    ([pr#6811](http://github.com/ceph/ceph/pull/6811), Nathan Cutler)
-   doc: swift tempurls (#10184 Abhishek Lekshmanan)
-   doc: switch doxygen integration back to breathe (#6115 Kefu Chai)
-   doc, tests: update all <http://ceph.com/> to download.ceph.com
    ([pr#6435](http://github.com/ceph/ceph/pull/6435), Alfredo Deza)
-   doc: Update ceph-disk manual page with new feature
    deactivate/destroy.
    ([pr#6637](http://github.com/ceph/ceph/pull/6637), Vicente Cheng)
-   doc: Updated CloudStack RBD documentation
    ([pr#8308](http://github.com/ceph/ceph/pull/8308), Wido den
    Hollander)
-   doc: update doc for with new pool settings
    ([pr#5951](http://github.com/ceph/ceph/pull/5951), Guang Yang)
-   doc: Updated the rados command man page to include the \--run-name
    opt... ([issue#12899](http://tracker.ceph.com/issues/12899),
    [pr#5900](http://github.com/ceph/ceph/pull/5900), ritz303)
-   doc: update infernalis release notes
    ([pr#6575](http://github.com/ceph/ceph/pull/6575), vasukulkarni)
-   doc: Update list of admin/build-doc dependencies
    ([issue#14070](http://tracker.ceph.com/issues/14070),
    [pr#6934](http://github.com/ceph/ceph/pull/6934), Nathan Cutler)
-   doc: update radosgw-admin example
    ([pr#6256](http://github.com/ceph/ceph/pull/6256), YankunLi)
-   doc: update release schedule docs (Loic Dachary)
-   doc: update the OS recommendations for newer Ceph releases
    ([pr#6355](http://github.com/ceph/ceph/pull/6355), ritz303)
-   doc: use \'ceph auth get-or-create\' for creating RGW keyring
    ([pr#6930](http://github.com/ceph/ceph/pull/6930), Wido den
    Hollander)
-   doc: very basic doc on mstart
    ([pr#8207](http://github.com/ceph/ceph/pull/8207), Abhishek
    Lekshmanan)
-   drop envz.h includes
    ([pr#6285](http://github.com/ceph/ceph/pull/6285), John Coyle)
-   erasure-code: cleanup (Kefu Chai)
-   erasure-code: improve tests (Loic Dachary)
-   erasure-code: shec: fix recovery bugs (Takanori Nakao, Shotaro
    Kawaguchi)
-   erasure-code: update ISA-L to 2.13 (Yuan Zhou)
-   fix FTBFS introduced by d0af316
    ([pr#7792](http://github.com/ceph/ceph/pull/7792), Kefu Chai)
-   fix: use right init_flags to finish CephContext
    ([pr#6549](http://github.com/ceph/ceph/pull/6549), Yunchuan Wen)
-   fs: be more careful about the \"mds setmap\" command to prevent
    breakage ([issue#14380](http://tracker.ceph.com/issues/14380),
    [pr#7262](http://github.com/ceph/ceph/pull/7262), Yan, Zheng)
-   ghobject_t: use \# instead of ! as a separator
    ([pr#8055](http://github.com/ceph/ceph/pull/8055), Sage Weil)
-   global: do not start two daemons with a single pid-file
    ([issue#13422](http://tracker.ceph.com/issues/13422),
    [pr#7075](http://github.com/ceph/ceph/pull/7075), shun song)
-   global: do not start two daemons with a single pid-file (part 2)
    ([issue#13422](http://tracker.ceph.com/issues/13422),
    [pr#7463](http://github.com/ceph/ceph/pull/7463), Loic Dachary)
-   global/global_init: expand metavariables in setuser_match_path
    ([issue#15365](http://tracker.ceph.com/issues/15365),
    [pr#8433](http://github.com/ceph/ceph/pull/8433), Sage Weil)
-   global/signal_handler: print thread name in signal handler
    ([pr#8177](http://github.com/ceph/ceph/pull/8177), Jianpeng Ma)
-   gmock: switch to submodule (Danny Al-Gaaf, Loic Dachary)
-   hadoop: add terasort test (Noah Watkins)
-   helgrind: additional race conditionslibrbd: journal replay should
    honor inter-event dependencies
    ([pr#7274](http://github.com/ceph/ceph/pull/7274), Jason Dillaman)
-   helgrind: fix real (and imaginary) race conditions
    ([issue#14163](http://tracker.ceph.com/issues/14163),
    [pr#7208](http://github.com/ceph/ceph/pull/7208), Jason Dillaman)
-   include/encoding: do not try to be clever with list encoding
    ([pr#7913](http://github.com/ceph/ceph/pull/7913), Sage Weil)
-   init-ceph: do umount when the path exists.
    ([pr#6866](http://github.com/ceph/ceph/pull/6866), Xiaoxi Chen)
-   init-ceph.in: allow case-insensitive true in [osd crush update on
    start\' (\`pr#7943
    \<http://github.com/ceph/ceph/pull/7943\>]{.title-ref}\_, Eric Cook)
-   init-ceph.in: skip ceph-disk if it is not present
    ([issue#10587](http://tracker.ceph.com/issues/10587),
    [pr#7286](http://github.com/ceph/ceph/pull/7286), Ken Dreyer)
-   init-ceph: use getopt to make option processing more flexible
    ([issue#3015](http://tracker.ceph.com/issues/3015),
    [pr#6089](http://github.com/ceph/ceph/pull/6089), Nathan Cutler)
-   init-radosgw: merge with sysv version; fix enumeration (Sage Weil)
-   java: fix libcephfs bindings (Noah Watkins)
-   journal: async methods to (un)register and update client
    ([pr#7832](http://github.com/ceph/ceph/pull/7832), Mykola Golub)
-   journal: disconnect watch after watch error
    ([issue#14168](http://tracker.ceph.com/issues/14168),
    [pr#7113](http://github.com/ceph/ceph/pull/7113), Jason Dillaman)
-   journal: fire replay complete event after reading last object
    ([issue#13924](http://tracker.ceph.com/issues/13924),
    [pr#6762](http://github.com/ceph/ceph/pull/6762), Jason Dillaman)
-   journal: fix final result for JournalTrimmer::C_RemoveSet
    ([pr#8516](http://github.com/ceph/ceph/pull/8516), runsisi)
-   journal: fix race condition between Future and journal shutdown
    ([issue#15364](http://tracker.ceph.com/issues/15364),
    [pr#8477](http://github.com/ceph/ceph/pull/8477), Jason Dillaman)
-   journal: flush commit position on metadata shutdown
    ([pr#7385](http://github.com/ceph/ceph/pull/7385), Mykola Golub)
-   journal: improve commit position tracking
    ([pr#7776](http://github.com/ceph/ceph/pull/7776), Jason Dillaman)
-   journal: incremental improvements and fixes
    ([pr#6552](http://github.com/ceph/ceph/pull/6552), Mykola Golub)
-   journal: prevent race injecting new records into overflowed object
    ([issue#15202](http://tracker.ceph.com/issues/15202),
    [pr#8220](http://github.com/ceph/ceph/pull/8220), Jason Dillaman)
-   journal: reset commit_position_task_ctx pointer after task complete
    ([pr#7480](http://github.com/ceph/ceph/pull/7480), Mykola Golub)
-   journal: re-use common threads between journalers
    ([pr#7906](http://github.com/ceph/ceph/pull/7906), Jason Dillaman)
-   journal: support replaying beyond skipped splay objects
    ([pr#6687](http://github.com/ceph/ceph/pull/6687), Jason Dillaman)
-   krbd: remove deprecated \--quiet param from udevadm
    ([issue#13560](http://tracker.ceph.com/issues/13560),
    [pr#6394](http://github.com/ceph/ceph/pull/6394), Jason Dillaman)
-   kv: fix bug in kv key optimization
    ([pr#6511](http://github.com/ceph/ceph/pull/6511), Sage Weil)
-   kv: implement value_as_ptr() and use it in .get()
    ([pr#7052](http://github.com/ceph/ceph/pull/7052), Piotr Dałek)
-   kv/KineticStore: fix broken split_key
    ([pr#6574](http://github.com/ceph/ceph/pull/6574), Haomai Wang)
-   kv: optimize and clean up internal key/value interface
    ([pr#6312](http://github.com/ceph/ceph/pull/6312), Piotr Dałek, Sage
    Weil)
-   libcephfs: add pread, pwrite (Jevon Qiao)
-   libcephfs,ceph-fuse: cache cleanup (Zheng Yan)
-   libcephfs,ceph-fuse: fix request resend on cap reconnect (#10912
    Yan, Zheng)
-   libcephfs: fix python tests and fix getcwd on missing dir
    ([pr#7901](http://github.com/ceph/ceph/pull/7901), John Spray)
-   libcephfs: Improve portability by replacing loff_t type usage with
    off_t ([pr#6301](http://github.com/ceph/ceph/pull/6301), John Coyle)
-   libcephfs: only check file offset on glibc platforms
    ([pr#6288](http://github.com/ceph/ceph/pull/6288), John Coyle)
-   libcephfs: update LIBCEPHFS_VERSION to indicate the interface was
    changed ([pr#7551](http://github.com/ceph/ceph/pull/7551), Jevon
    Qiao)
-   librados: add config observer (Alistair Strachan)
-   librados: add c++ style osd/pg command interface
    ([pr#6893](http://github.com/ceph/ceph/pull/6893), Yunchuan Wen)
-   librados: add FULL_TRY and FULL_FORCE flags for dealing with full
    clusters or pools (Sage Weil)
-   librados: add src_fadvise_flags for copy-from (Jianpeng Ma)
-   librados: aix gcc librados port
    ([pr#6675](http://github.com/ceph/ceph/pull/6675), Rohan Mars)
-   librados: avoid malloc(0) (which can return NULL on some platforms)
    ([issue#13944](http://tracker.ceph.com/issues/13944),
    [pr#6779](http://github.com/ceph/ceph/pull/6779), Dan Mick)
-   librados: cancel aio notification linger op upon completion
    ([pr#8102](http://github.com/ceph/ceph/pull/8102), Jason Dillaman)
-   librados: check connection state in rados_monitor_log
    ([issue#14499](http://tracker.ceph.com/issues/14499),
    [pr#7350](http://github.com/ceph/ceph/pull/7350), David Disseldorp)
-   librados: clean up Objecter.h
    ([pr#6731](http://github.com/ceph/ceph/pull/6731), Jie Wang)
-   librados: define C++ flags from C constants (Josh Durgin)
-   librados: detect laggy ops with objecter_timeout, not osd_timeout
    ([pr#7629](http://github.com/ceph/ceph/pull/7629), Greg Farnum)
-   librados: do cleanup
    ([pr#6488](http://github.com/ceph/ceph/pull/6488), xie xingguo)
-   librados: do not clear handle for aio_watch()
    ([pr#7771](http://github.com/ceph/ceph/pull/7771), xie xingguo)
-   librados: fadvise flags per op (Jianpeng Ma)
-   librados: fix examples/librados/Makefile error.
    ([pr#6320](http://github.com/ceph/ceph/pull/6320), You Ji)
-   librados: fix last_force_resent handling (#11026 Jianpeng Ma)
-   librados: fix memory leak from C_TwoContexts (Xiong Yiliang)
-   librados: fix notify completion race (#13114 Sage Weil)
-   librados: fix pool alignment API overflow issue
    ([issue#13715](http://tracker.ceph.com/issues/13715),
    [pr#6489](http://github.com/ceph/ceph/pull/6489), xie xingguo)
-   librados: fix potential null pointer access when do pool_snap_list
    ([issue#13639](http://tracker.ceph.com/issues/13639),
    [pr#6422](http://github.com/ceph/ceph/pull/6422), xie xingguo)
-   librados: fix PromoteOn2ndRead test for EC
    ([pr#6373](http://github.com/ceph/ceph/pull/6373), Sage Weil)
-   librados: fix rare race where pool op callback may hang forever
    ([issue#13642](http://tracker.ceph.com/issues/13642),
    [pr#6426](http://github.com/ceph/ceph/pull/6426), xie xingguo)
-   librados: fix several flaws introduced by the enumeration_objects
    API ([issue#14299](http://tracker.ceph.com/issues/14299),
    [issue#14301](http://tracker.ceph.com/issues/14301),
    [issue#14300](http://tracker.ceph.com/issues/14300),
    [pr#7156](http://github.com/ceph/ceph/pull/7156), xie xingguo)
-   librados: fix striper when stripe_count = 1 and stripe_unit !=
    object_size (#11120 Yan, Zheng)
-   librados: fix test failure with new aio watch/unwatch API
    ([pr#7824](http://github.com/ceph/ceph/pull/7824), Jason Dillaman)
-   librados: implement async watch/unwatch
    ([pr#7649](http://github.com/ceph/ceph/pull/7649), Haomai Wang)
-   librados: include/rados/librados.h: fix typo
    ([pr#6741](http://github.com/ceph/ceph/pull/6741), Nathan Cutler)
-   librados: init crush_location from config file.
    ([issue#13473](http://tracker.ceph.com/issues/13473),
    [pr#6243](http://github.com/ceph/ceph/pull/6243), Wei Luo)
-   librados, libcephfs: randomize client nonces (Josh Durgin)
-   librados: mix lock cycle (un)registering asok commands
    ([pr#7581](http://github.com/ceph/ceph/pull/7581), John Spray)
-   librados: move to c++11 concurrency types
    ([pr#5931](http://github.com/ceph/ceph/pull/5931), Adam C. Emerson)
-   librados: new style (sharded) object listing
    ([pr#6405](http://github.com/ceph/ceph/pull/6405), John Spray, Sage
    Weil)
-   librados: op perf counters (John Spray)
-   librados: potential null pointer access in [list]()(n)objects
    ([issue#13822](http://tracker.ceph.com/issues/13822),
    [pr#6639](http://github.com/ceph/ceph/pull/6639), xie xingguo)
-   librados: pybind: fix binary omap values (Robin H. Johnson)
-   librados: pybind: fix write() method return code (Javier Guerra)
-   librados: race condition on aio_notify completion handling
    ([pr#7864](http://github.com/ceph/ceph/pull/7864), Jason Dillaman)
-   librados: remove duplicate definitions for rados pool_stat_t and
    cluster_stat_t ([pr#7330](http://github.com/ceph/ceph/pull/7330),
    Igor Fedotov)
-   librados: respect default_crush_ruleset on pool_create (#11640 Yuan
    Zhou)
-   librados: Revert \"rados: Add new field flags for
    ceph_osd_op.copy_get.\"
    ([pr#8486](http://github.com/ceph/ceph/pull/8486), Sage Weil)
-   librados: shutdown finisher in a more graceful way
    ([pr#7519](http://github.com/ceph/ceph/pull/7519), xie xingguo)
-   librados: Solaris port
    ([pr#6416](http://github.com/ceph/ceph/pull/6416), Rohan Mars)
-   librados: stat2 with higher time precision
    ([pr#7915](http://github.com/ceph/ceph/pull/7915), Yehuda Sadeh,
    Matt Benjamin)
-   librados: Striper: Fix incorrect push_front -\> append_zero change
    ([pr#7578](http://github.com/ceph/ceph/pull/7578), Haomai Wang)
-   libradosstriper: fix leak (Danny Al-Gaaf)
-   librados_test_stub: protect against notify/unwatch race
    ([pr#7540](http://github.com/ceph/ceph/pull/7540), Jason Dillaman)
-   librados: wrongly passed in argument for stat command
    ([issue#13703](http://tracker.ceph.com/issues/13703),
    [pr#6476](http://github.com/ceph/ceph/pull/6476), xie xingguo)
-   librbd: add const for single-client-only features (Josh Durgin)
-   librbd: add deep-flatten operation (Jason Dillaman)
-   librbd: add purge_on_error cache behavior (Jianpeng Ma)
-   librbd: allocate new journal tag after acquiring exclusive lock
    ([pr#7884](http://github.com/ceph/ceph/pull/7884), Jason Dillaman)
-   librbd: allow additional metadata to be stored with the image
    (Haomai Wang)
-   librbd: API: async open and close
    ([issue#14264](http://tracker.ceph.com/issues/14264),
    [pr#7259](http://github.com/ceph/ceph/pull/7259), Mykola Golub)
-   librbd: automatically flush IO after blocking write operations
    ([issue#13913](http://tracker.ceph.com/issues/13913),
    [pr#6742](http://github.com/ceph/ceph/pull/6742), Jason Dillaman)
-   librbd: avoid blocking aio API methods (#11056 Jason Dillaman)
-   librbd: Avoid create two threads per image
    ([pr#7400](http://github.com/ceph/ceph/pull/7400), Haomai Wang)
-   librbd: avoid throwing error if mirroring is unsupported
    ([pr#8417](http://github.com/ceph/ceph/pull/8417), Jason Dillaman)
-   librbd: better handling for dup flatten requests (#11370 Jason
    Dillaman)
-   librbd: better handling of exclusive lock transition period
    ([pr#7204](http://github.com/ceph/ceph/pull/7204), Jason Dillaman)
-   librbd: block maintenance ops until after journal is ready
    ([issue#14510](http://tracker.ceph.com/issues/14510),
    [pr#7382](http://github.com/ceph/ceph/pull/7382), Jason Dillaman)
-   librbd: block read requests until journal replayed
    ([pr#7627](http://github.com/ceph/ceph/pull/7627), Jason Dillaman)
-   librbd: cancel in-flight ops on watch error (#11363 Jason Dillaman)
-   librbd: check for presence of journal before attempting to remove
    ([issue#13912](http://tracker.ceph.com/issues/13912),
    [pr#6737](http://github.com/ceph/ceph/pull/6737), Jason Dillaman)
-   librbd: clear error when older OSD doesn\'t support image flags
    ([issue#14122](http://tracker.ceph.com/issues/14122),
    [pr#7035](http://github.com/ceph/ceph/pull/7035), Jason Dillaman)
-   librbd: correct include guard in RenameRequest.h
    ([pr#7143](http://github.com/ceph/ceph/pull/7143), Jason Dillaman)
-   librbd: correct issues discovered during teuthology testing
    ([issue#14108](http://tracker.ceph.com/issues/14108),
    [issue#14107](http://tracker.ceph.com/issues/14107),
    [pr#6974](http://github.com/ceph/ceph/pull/6974), Jason Dillaman)
-   librbd: correct issues discovered via valgrind memcheck
    ([pr#8132](http://github.com/ceph/ceph/pull/8132), Jason Dillaman)
-   librbd: correct issues discovered when cache is disabled
    ([issue#14123](http://tracker.ceph.com/issues/14123),
    [pr#6979](http://github.com/ceph/ceph/pull/6979), Jason Dillaman)
-   librbd: correct race conditions discovered during unit testing
    ([issue#14060](http://tracker.ceph.com/issues/14060),
    [pr#6923](http://github.com/ceph/ceph/pull/6923), Jason Dillaman)
-   librbd: deadlock while attempting to flush AIO requests
    ([issue#13726](http://tracker.ceph.com/issues/13726),
    [pr#6508](http://github.com/ceph/ceph/pull/6508), Jason Dillaman)
-   librbd: default new images to format 2 (#11348 Jason Dillaman)
-   librbd: differentiate journal replay flush vs shut down
    ([pr#7698](http://github.com/ceph/ceph/pull/7698), Jason Dillaman)
-   librbd: disable copy-on-read when not exclusive lock owner
    ([issue#14167](http://tracker.ceph.com/issues/14167),
    [pr#7129](http://github.com/ceph/ceph/pull/7129), Jason Dillaman)
-   librbd: disable image mirroring when image is removed
    ([issue#15265](http://tracker.ceph.com/issues/15265),
    [pr#8375](http://github.com/ceph/ceph/pull/8375), Ricardo Dias)
-   librbd: disallow unsafe rbd_op_threads values
    ([issue#15034](http://tracker.ceph.com/issues/15034),
    [pr#8459](http://github.com/ceph/ceph/pull/8459), Josh Durgin)
-   librbd: do not ignore self-managed snapshot release result
    ([issue#14170](http://tracker.ceph.com/issues/14170),
    [pr#7043](http://github.com/ceph/ceph/pull/7043), Jason Dillaman)
-   librbd: enable/disable image mirroring automatically for pool mode
    ([issue#15143](http://tracker.ceph.com/issues/15143),
    [pr#8204](http://github.com/ceph/ceph/pull/8204), Ricardo Dias)
-   librbd: ensure copy-on-read requests are complete prior to closing
    parent image ([pr#6740](http://github.com/ceph/ceph/pull/6740),
    Jason Dillaman)
-   librbd: ensure librados callbacks are flushed prior to destroying
    ([issue#14092](http://tracker.ceph.com/issues/14092),
    [pr#7040](http://github.com/ceph/ceph/pull/7040), Jason Dillaman)
-   librbd: exit if parent\'s snap is gone during clone
    ([issue#14118](http://tracker.ceph.com/issues/14118),
    [pr#6968](http://github.com/ceph/ceph/pull/6968), xie xingguo)
-   librbd: fadvise for copy, export, import (Jianpeng Ma)
-   librbd: fast diff implementation that leverages object map (Jason
    Dillaman)
-   librbd: fix enable objectmap feature issue
    ([issue#13558](http://tracker.ceph.com/issues/13558),
    [pr#6339](http://github.com/ceph/ceph/pull/6339), xinxin shu)
-   librbd: fix fast diff bugs (#11553 Jason Dillaman)
-   librbd: fix image format detection (Zhiqiang Wang)
-   librbd: fix internal handling of dynamic feature updates
    ([pr#7299](http://github.com/ceph/ceph/pull/7299), Jason Dillaman)
-   librbd: fix journal iohint
    ([pr#6917](http://github.com/ceph/ceph/pull/6917), Jianpeng Ma)
-   librbd: fix known test case race condition failures
    ([issue#13969](http://tracker.ceph.com/issues/13969),
    [pr#6800](http://github.com/ceph/ceph/pull/6800), Jason Dillaman)
-   librbd: fix lock ordering issue (#11577 Jason Dillaman)
-   librbd: fix merge-diff for \>2GB diff-files
    ([issue#14030](http://tracker.ceph.com/issues/14030),
    [pr#6889](http://github.com/ceph/ceph/pull/6889), Yunchuan Wen)
-   librbd: fix potential memory leak
    ([issue#14332](http://tracker.ceph.com/issues/14332),
    [issue#14333](http://tracker.ceph.com/issues/14333),
    [pr#7174](http://github.com/ceph/ceph/pull/7174), xie xingguo)
-   librbd: fix reads larger than the cache size (Lu Shi)
-   librbd: fix snap_exists API return code overflow
    ([issue#14129](http://tracker.ceph.com/issues/14129),
    [pr#6986](http://github.com/ceph/ceph/pull/6986), xie xingguo)
-   librbd: fix snapshot creation when other snap is active (#11475
    Jason Dillaman)
-   librbd: fix state machine race conditions during shut down
    ([pr#7761](http://github.com/ceph/ceph/pull/7761), Jason Dillaman)
-   librbd: fix test case race condition for journaling ops
    ([pr#6877](http://github.com/ceph/ceph/pull/6877), Jason Dillaman)
-   librbd: fix tracepoint parameter in diff_iterate
    ([pr#6892](http://github.com/ceph/ceph/pull/6892), Yunchuan Wen)
-   librbd: flatten/copyup fixes (Jason Dillaman)
-   librbd: flush and invalidate cache via admin socket
    ([issue#2468](http://tracker.ceph.com/issues/2468),
    [pr#6453](http://github.com/ceph/ceph/pull/6453), Mykola Golub)
-   librbd: handle NOCACHE fadvise flag (Jinapeng Ma)
-   librbd: handle unregistering the image watcher when disconnected
    ([pr#8094](http://github.com/ceph/ceph/pull/8094), Jason Dillaman)
-   librbd: image refresh code paths converted to async state machines
    ([pr#6859](http://github.com/ceph/ceph/pull/6859), Jason Dillaman)
-   librbd: include missing header for bool type
    ([pr#6798](http://github.com/ceph/ceph/pull/6798), Mykola Golub)
-   librbd: initial collection of state machine unit tests
    ([pr#6703](http://github.com/ceph/ceph/pull/6703), Jason Dillaman)
-   librbd: integrate journaling for maintenance operations
    ([pr#6625](http://github.com/ceph/ceph/pull/6625), Jason Dillaman)
-   librbd: integrate journaling support for IO operations
    ([pr#6541](http://github.com/ceph/ceph/pull/6541), Jason Dillaman)
-   librbd: integrate journal replay with fsx testing
    ([pr#7583](http://github.com/ceph/ceph/pull/7583), Jason Dillaman)
-   librbd: journal framework for tracking exclusive lock transitions
    ([issue#13298](http://tracker.ceph.com/issues/13298),
    [pr#7529](http://github.com/ceph/ceph/pull/7529), Jason Dillaman)
-   librbd: journaling-related lock dependency cleanup
    ([pr#6777](http://github.com/ceph/ceph/pull/6777), Jason Dillaman)
-   librbd: journal replay needs to support re-executing maintenance ops
    ([issue#14822](http://tracker.ceph.com/issues/14822),
    [pr#7785](http://github.com/ceph/ceph/pull/7785), Jason Dillaman)
-   librbd: journal replay should honor inter-event dependencies
    ([pr#7019](http://github.com/ceph/ceph/pull/7019), Jason Dillaman)
-   librbd: journal shut down flush race condition
    ([issue#14434](http://tracker.ceph.com/issues/14434),
    [pr#7302](http://github.com/ceph/ceph/pull/7302), Jason Dillaman)
-   librbd: lockdep, helgrind validation (Jason Dillaman, Josh Durgin)
-   librbd: metadata filter fixes (Haomai Wang)
-   librbd: misc aio fixes (#5488 Jason Dillaman)
-   librbd: misc rbd fixes (#11478 #11113 #11342 #11380 Jason Dillaman,
    Zhiqiang Wang)
-   librbd: new diff_iterate2 API (Jason Dillaman)
-   librbd: not necessary to hold owner_lock while releasing snap id
    ([issue#13914](http://tracker.ceph.com/issues/13914),
    [pr#6736](http://github.com/ceph/ceph/pull/6736), Jason Dillaman)
-   librbd: object map rebuild support (Jason Dillaman)
-   librbd: only send signal when AIO completions queue empty
    ([pr#6729](http://github.com/ceph/ceph/pull/6729), Jianpeng Ma)
-   librbd: only update image flags while hold exclusive lock (#11791
    Jason Dillaman)
-   librbd: optionally disable allocation hint (Haomai Wang)
-   librbd: optionally validate new RBD pools for snapshot support
    ([issue#13633](http://tracker.ceph.com/issues/13633),
    [pr#6925](http://github.com/ceph/ceph/pull/6925), Jason Dillaman)
-   librbd: partial revert of commit 9b0e359
    ([issue#13969](http://tracker.ceph.com/issues/13969),
    [pr#6789](http://github.com/ceph/ceph/pull/6789), Jason Dillaman)
-   librbd: perf counters might not be initialized on error
    ([issue#13740](http://tracker.ceph.com/issues/13740),
    [pr#6523](http://github.com/ceph/ceph/pull/6523), Jason Dillaman)
-   librbd: perf section name: use hyphen to separate components
    ([issue#13719](http://tracker.ceph.com/issues/13719),
    [pr#6516](http://github.com/ceph/ceph/pull/6516), Mykola Golub)
-   librbd: prevent race between resize requests (#12664 Jason Dillaman)
-   librbd: properly handle replay of snap remove RPC message
    ([issue#14164](http://tracker.ceph.com/issues/14164),
    [pr#7042](http://github.com/ceph/ceph/pull/7042), Jason Dillaman)
-   librbd: readahead fixes (Zhiqiang Wang)
-   librbd: reduce mem copies to user-buffer during read
    ([pr#7548](http://github.com/ceph/ceph/pull/7548), Jianpeng Ma)
-   librbd: reduce verbosity of common error condition logging
    ([issue#14234](http://tracker.ceph.com/issues/14234),
    [pr#7114](http://github.com/ceph/ceph/pull/7114), Jason Dillaman)
-   librbd: refresh image if required before replaying journal ops
    ([issue#14908](http://tracker.ceph.com/issues/14908),
    [pr#7978](http://github.com/ceph/ceph/pull/7978), Jason Dillaman)
-   librbd: remove canceled tasks from timer thread
    ([issue#14476](http://tracker.ceph.com/issues/14476),
    [pr#7329](http://github.com/ceph/ceph/pull/7329), Douglas Fuller)
-   librbd: remove duplicate read_only test in librbd::async_flatten
    ([pr#5856](http://github.com/ceph/ceph/pull/5856), runsisi)
-   librbd: remove last synchronous librados calls from open/close state
    machine ([pr#7839](http://github.com/ceph/ceph/pull/7839), Jason
    Dillaman)
-   librbd: replaying a journal op post-refresh requires locking
    ([pr#8028](http://github.com/ceph/ceph/pull/8028), Jason Dillaman)
-   librbd: resize should only update image size within header
    ([issue#13674](http://tracker.ceph.com/issues/13674),
    [pr#6447](http://github.com/ceph/ceph/pull/6447), Jason Dillaman)
-   librbd: retrieve image name when opening by id
    ([pr#7736](http://github.com/ceph/ceph/pull/7736), Mykola Golub)
-   librbd: return error if we fail to delete object_map head object
    ([issue#14098](http://tracker.ceph.com/issues/14098),
    [pr#6958](http://github.com/ceph/ceph/pull/6958), xie xingguo)
-   librbd: return result code from close (#12069 Jason Dillaman)
-   librbd: Revert \"librbd: use task finisher per CephContext\"
    ([issue#14780](http://tracker.ceph.com/issues/14780),
    [pr#7667](http://github.com/ceph/ceph/pull/7667), Josh Durgin)
-   librbd: send notifications for mirroring status updates
    ([pr#8355](http://github.com/ceph/ceph/pull/8355), Jason Dillaman)
-   librbd: several race conditions discovered under single CPU
    environment ([pr#7653](http://github.com/ceph/ceph/pull/7653), Jason
    Dillaman)
-   librbd: simplify IO method signatures for 32bit environments
    ([pr#6700](http://github.com/ceph/ceph/pull/6700), Jason Dillaman)
-   librbd: small fixes for error messages and readahead counter
    ([issue#14127](http://tracker.ceph.com/issues/14127),
    [pr#6983](http://github.com/ceph/ceph/pull/6983), xie xingguo)
-   librbd: start perf counters after id is initialized
    ([issue#13720](http://tracker.ceph.com/issues/13720),
    [pr#6494](http://github.com/ceph/ceph/pull/6494), Mykola Golub)
-   librbd: store metadata, including config options, in image (Haomai
    Wang)
-   librbd: support eventfd for AIO completion notifications
    ([pr#5465](http://github.com/ceph/ceph/pull/5465), Haomai Wang)
-   librbd: tolerate old osds when getting image metadata (#11549 Jason
    Dillaman)
-   librbd: truncate does not need to mark the object as existing in the
    object map ([issue#14789](http://tracker.ceph.com/issues/14789),
    [pr#7772](http://github.com/ceph/ceph/pull/7772), xinxin shu)
-   librbd: uninitialized state in snap remove state machine
    ([pr#6982](http://github.com/ceph/ceph/pull/6982), Jason Dillaman)
-   librbd: update of mirror pool mode and mirror peer handling
    ([pr#7718](http://github.com/ceph/ceph/pull/7718), Jason Dillaman)
-   librbd: use async librados notifications
    ([pr#7668](http://github.com/ceph/ceph/pull/7668), Jason Dillaman)
-   librbd: use write_full when possible (Zhiqiang Wang)
-   log: do not repeat errors to stderr
    ([issue#14616](http://tracker.ceph.com/issues/14616),
    [pr#7983](http://github.com/ceph/ceph/pull/7983), Sage Weil)
-   log: fix data corruption race resulting from log rotation (#12465
    Samuel Just)
-   log: fix stack overflow when flushing large log lines
    ([issue#14707](http://tracker.ceph.com/issues/14707),
    [pr#7599](http://github.com/ceph/ceph/pull/7599), Igor Fedotov)
-   logrotate.d: prefer service over invoke-rc.d (#11330 Win Hierman,
    Sage Weil)
-   log: segv in a portable way
    ([issue#14856](http://tracker.ceph.com/issues/14856),
    [pr#7790](http://github.com/ceph/ceph/pull/7790), Kefu Chai)
-   log: use delete\[\]
    ([pr#7904](http://github.com/ceph/ceph/pull/7904), Sage Weil)
-   mailmap: add UMCloud affiliation
    ([pr#6820](http://github.com/ceph/ceph/pull/6820), Jiaying Ren)
-   mailmap for 10.0.4
    ([pr#7932](http://github.com/ceph/ceph/pull/7932), Abhishek
    Lekshmanan)
-   mailmap: hange organization for Dongmao Zhang
    ([pr#7173](http://github.com/ceph/ceph/pull/7173), Dongmao Zhang)
-   mailmap: Igor Podoski affiliation
    ([pr#7219](http://github.com/ceph/ceph/pull/7219), Igor Podoski)
-   mailmap: Jewel updates
    ([pr#6750](http://github.com/ceph/ceph/pull/6750), Abhishek
    Lekshmanan)
-   mailmap: modify member info
    ([pr#6468](http://github.com/ceph/ceph/pull/6468), Xiaowei Chen)
-   mailmap: revise organization
    ([pr#6519](http://github.com/ceph/ceph/pull/6519), Li Wang)
-   mailmap: Ubuntu Kylin name changed to Kylin Cloud
    ([pr#6532](http://github.com/ceph/ceph/pull/6532), Loic Dachary)
-   mailmap: update .organizationmap
    ([pr#6565](http://github.com/ceph/ceph/pull/6565), chenji-kael)
-   mailmap update ([pr#7210](http://github.com/ceph/ceph/pull/7210), M
    Ranga Swami Reddy)
-   mailmap update ([pr#8522](http://github.com/ceph/ceph/pull/8522), M
    Ranga Swami Reddy)
-   mailmap: updates for infernalis.
    ([pr#6495](http://github.com/ceph/ceph/pull/6495), Yann Dupont)
-   mailmap: updates ([pr#6258](http://github.com/ceph/ceph/pull/6258),
    M Ranga Swami Reddy)
-   mailmap: updates ([pr#6594](http://github.com/ceph/ceph/pull/6594),
    chenji-kael)
-   mailmap updates ([pr#6992](http://github.com/ceph/ceph/pull/6992),
    Loic Dachary)
-   mailmap updates ([pr#7189](http://github.com/ceph/ceph/pull/7189),
    Loic Dachary)
-   mailmap updates ([pr#7528](http://github.com/ceph/ceph/pull/7528),
    Yann Dupont)
-   mailmap updates ([pr#8256](http://github.com/ceph/ceph/pull/8256),
    Loic Dachary)
-   mailmap: Xie Xingguo affiliation
    ([pr#6409](http://github.com/ceph/ceph/pull/6409), Loic Dachary)
-   Makefile-env.am: set a default for CEPH_BUILD_VIRTUALENV (part 2)
    ([pr#8320](http://github.com/ceph/ceph/pull/8320), Loic Dachary)
-   makefile: fix rbdmap manpage
    ([pr#8310](http://github.com/ceph/ceph/pull/8310), Kefu Chai)
-   makefile: remove libedit from libclient.la
    ([pr#7284](http://github.com/ceph/ceph/pull/7284), Kefu Chai)
-   makefiles: remove bz2-dev from dependencies
    ([issue#13981](http://tracker.ceph.com/issues/13981),
    [pr#6939](http://github.com/ceph/ceph/pull/6939), Piotr Dałek)
-   man/8/ceph-disk: fix formatting issue
    ([pr#8003](http://github.com/ceph/ceph/pull/8003), Sage Weil)
-   man/8/ceph-disk: fix formatting issue
    ([pr#8012](http://github.com/ceph/ceph/pull/8012), Sage Weil)
-   man: document listwatchers cmd in \"rados\" manpage
    ([pr#7021](http://github.com/ceph/ceph/pull/7021), Kefu Chai)
-   mdsa: A few more snapshot fixes, mostly around snapshotted
    inode/dentry tracking
    ([pr#7798](http://github.com/ceph/ceph/pull/7798), Yan, Zheng)
-   mds: Add cmapv to ESessions default constructor initializer list
    ([pr#8403](http://github.com/ceph/ceph/pull/8403), John Coyle)
-   mds: add \'damaged\' state to MDSMap (John Spray)
-   mds: add nicknames for perfcounters (John Spray)
-   mds: add \'p\' flag in auth caps to control setting pool in layout
    ([pr#6567](http://github.com/ceph/ceph/pull/6567), John Spray)
-   mds: advance clientreplay when replying
    ([issue#14357](http://tracker.ceph.com/issues/14357),
    [pr#7216](http://github.com/ceph/ceph/pull/7216), John Spray)
-   mds: allow client to request caps when opening file
    ([issue#14360](http://tracker.ceph.com/issues/14360),
    [pr#7952](http://github.com/ceph/ceph/pull/7952), Yan, Zheng)
-   mds: avoid emitting cap warnigns before evicting session (John
    Spray)
-   mds: avoid getting stuck in XLOCKDONE (#11254 Yan, Zheng)
-   mds, client: add namespace to file_layout_t (previously
    ceph_file_layout) ([pr#7098](http://github.com/ceph/ceph/pull/7098),
    Yan, Zheng, Sage Weil)
-   mds, client: fix locking around handle_conf_change
    ([issue#14365](http://tracker.ceph.com/issues/14365),
    [issue#14374](http://tracker.ceph.com/issues/14374),
    [pr#7312](http://github.com/ceph/ceph/pull/7312), John Spray)
-   mds: disable problematic rstat propagation into snap parents (Yan,
    Zheng)
-   mds: do not add snapped items to bloom filter (Yan, Zheng)
-   mds: don\'t double-shutdown the timer when suiciding
    ([issue#14697](http://tracker.ceph.com/issues/14697),
    [pr#7616](http://github.com/ceph/ceph/pull/7616), Greg Farnum)
-   mds: expose frags via asok (John Spray)
-   mds: expose state of recovery to status ASOK command
    ([issue#14146](http://tracker.ceph.com/issues/14146),
    [pr#7068](http://github.com/ceph/ceph/pull/7068), Yan, Zheng)
-   mds: Extend the existing pool access checking to include specific
    RADOS namespacse.
    ([pr#8444](https://github.com/ceph/ceph/pull/8444), Yan, Zheng)
-   mds: filelock deadlock
    ([pr#7713](http://github.com/ceph/ceph/pull/7713), Yan, Zheng)
-   mds: fix client capabilities during reconnect (client.XXXX isn\'t
    responding to mclientcaps(revoke))
    ([issue#11482](http://tracker.ceph.com/issues/11482),
    [pr#6432](http://github.com/ceph/ceph/pull/6432), Yan, Zheng)
-   mds: fix client cap/message replay order on restart
    ([issue#14254](http://tracker.ceph.com/issues/14254),
    [issue#13546](http://tracker.ceph.com/issues/13546),
    [pr#7199](http://github.com/ceph/ceph/pull/7199), Yan, Zheng)
-   mds: fix expected holes in journal objects (#13167 Yan, Zheng)
-   mds: fix file_layout_t legacy encoding snafu
    ([pr#8455](http://github.com/ceph/ceph/pull/8455), Sage Weil)
-   mds: fix fsmap decode
    ([pr#8063](http://github.com/ceph/ceph/pull/8063), Greg Farnum)
-   mds: fix FSMap upgrade with daemons in the map
    ([pr#8073](http://github.com/ceph/ceph/pull/8073), John Spray, Greg
    Farnum)
-   mds: fix handling for missing mydir dirfrag (#11641 John Spray)
-   mds: fix inode_t::compare()
    ([issue#15038](http://tracker.ceph.com/issues/15038),
    [pr#8014](http://github.com/ceph/ceph/pull/8014), Yan, Zheng)
-   mds: fix integer truncateion on large client ids (Henry Chang)
-   mds: fix mydir replica issue with shutdown (#10743 John Spray)
-   mds: fix out-of-order messages (#11258 Yan, Zheng)
-   mds: fix rejoin (Yan, Zheng)
-   mds: fix scrub_path
    ([pr#6684](http://github.com/ceph/ceph/pull/6684), John Spray)
-   mds: fix setting entire file layout in one setxattr (John Spray)
-   mds: fix setvxattr (broken in a536d114)
    ([issue#14029](http://tracker.ceph.com/issues/14029),
    [pr#6941](http://github.com/ceph/ceph/pull/6941), John Spray)
-   mds: fix shutdown (John Spray)
-   mds: fix shutdown with strays (#10744 John Spray)
-   mds: fix SnapServer crash on deleted pool (John Spray)
-   mds: fix snapshot bugs (Yan, Zheng)
-   mds: fix standby replay thread creation
    ([issue#14144](http://tracker.ceph.com/issues/14144),
    [pr#7132](http://github.com/ceph/ceph/pull/7132), John Spray)
-   mds: fix stray handling (John Spray)
-   mds: fix stray purging in \'stripe_count \> 1\' case
    ([issue#15050](http://tracker.ceph.com/issues/15050),
    [pr#8040](http://github.com/ceph/ceph/pull/8040), Yan, Zheng)
-   mds: fix stray reintegration (Yan, Zheng)
-   mds: fix suicide beacon (John Spray)
-   mds: flush immediately in do_open_truncate (#11011 John Spray)
-   mds: function parameter \'df\' should be passed by reference
    ([pr#7490](http://github.com/ceph/ceph/pull/7490), Na Xie)
-   mds: handle misc corruption issues (John Spray)
-   mds: implement snapshot rename
    ([pr#5645](http://github.com/ceph/ceph/pull/5645), xinxin shu)
-   mds: improve dump methods (John Spray)
-   mds: judgment added to avoid the risk of visiting the NULL pointer
    ([pr#7358](http://github.com/ceph/ceph/pull/7358), Kongming Wu)
-   mds: many fixes (Yan, Zheng, John Spray, Greg Farnum)
-   mds: many snapshot and stray fixes (Yan, Zheng)
-   mds: messages/MOSDOp: cast in assert to eliminate warnings
    ([issue#13625](http://tracker.ceph.com/issues/13625),
    [pr#6414](http://github.com/ceph/ceph/pull/6414), David Zafman)
-   mds: misc fixes (Jianpeng Ma, Dan van der Ster, Zhang Zhi)
-   mds: misc journal cleanups and fixes (#10368 John Spray)
-   mds: misc repair improvements (John Spray)
-   mds: misc snap fixes (Zheng Yan)
-   mds: misc snapshot fixes (Yan, Zheng)
-   mds: Multi-filesystem support
    ([issue#14952](http://tracker.ceph.com/issues/14952),
    [pr#6953](http://github.com/ceph/ceph/pull/6953), John Spray, Sage
    Weil)
-   mds: new filtered MDS tell commands for sessions
    ([pr#6180](http://github.com/ceph/ceph/pull/6180), John Spray)
-   mds: new SessionMap storage using omap (#10649 John Spray)
-   mds: persist completed_requests reliably (#11048 John Spray)
-   mds: properly set STATE_STRAY/STATE_ORPHAN for stray dentry/inode
    ([issue#13777](http://tracker.ceph.com/issues/13777),
    [pr#6553](http://github.com/ceph/ceph/pull/6553), Yan, Zheng)
-   mds: Protect a number of unstable/experimental features behind
    durable flags ([pr#8383](https://github.com/ceph/ceph/pull/8383),
    Greg Farnum)
-   mds: reduce memory consumption (Yan, Zheng)
-   mds: repair the command option \"\--hot-standby\"
    ([pr#6454](http://github.com/ceph/ceph/pull/6454), Wei Feng)
-   mds: respawn instead of suicide on blacklist (John Spray)
-   mds: ScrubStack and \"tag path\" command
    ([pr#5662](http://github.com/ceph/ceph/pull/5662), Yan, Zheng, John
    Spray, Greg Farnum)
-   mds: separate safe_pos in Journaler (#10368 John Spray)
-   mds/Session: use projected parent for auth path check
    ([issue#13364](http://tracker.ceph.com/issues/13364),
    [pr#6200](http://github.com/ceph/ceph/pull/6200), Sage Weil)
-   mds: snapshot rename support (#3645 Yan, Zheng)
-   mds: store layout on header object (#4161 John Spray)
-   mds: tear down connections from [tell]{.title-ref} commands
    ([issue#14048](http://tracker.ceph.com/issues/14048),
    [pr#6933](http://github.com/ceph/ceph/pull/6933), John Spray)
-   mds: throttle purge stray operations (#10390 John Spray)
-   mds: tolerate clock jumping backwards (#11053 Yan, Zheng)
-   mds: warn when clients fail to advance oldest_client_tid (#10657
    Yan, Zheng)
-   mds: we should wait messenger when MDSDaemon suicide
    ([pr#6996](http://github.com/ceph/ceph/pull/6996), Wei Feng)
-   messages/MOSDOp: clear reqid inc for v6 encoding
    ([issue#15230](http://tracker.ceph.com/issues/15230),
    [pr#8299](http://github.com/ceph/ceph/pull/8299), Sage Weil)
-   Minor fixes around data scan in some scenarios
    ([pr#8115](http://github.com/ceph/ceph/pull/8115), Yan, Zheng)
-   mirrors: Change contact e-mail address for se.ceph.com
    ([pr#8007](http://github.com/ceph/ceph/pull/8007), Wido den
    Hollander)
-   mirrors: Updated scripts and documentation for mirrors
    ([pr#7847](http://github.com/ceph/ceph/pull/7847), Wido den
    Hollander)
-   misc cleanups and fixes (Danny Al-Gaaf)
-   misc coverity fixes (Danny Al-Gaaf)
-   misc performance and cleanup (Nathan Cutler, Xinxin Shu)
-   misc: use make_shared while creating shared_ptr
    ([pr#7769](http://github.com/ceph/ceph/pull/7769), Somnath Roy)
-   mon: add an independent option for max election time
    ([pr#7245](http://github.com/ceph/ceph/pull/7245), Sangdi Xu)
-   mon: add cache over MonitorDBStore (Kefu Chai)
-   mon: add \'mon_metadata \<id\>\' command (Kefu Chai)
-   mon: add \'node ls \...\' command (Kefu Chai)
-   mon: add NOFORWARD, OBSOLETE, DEPRECATE flags for mon commands (Joao
    Eduardo Luis)
-   mon: add [osd blacklist clear]{.title-ref}
    ([pr#6945](http://github.com/ceph/ceph/pull/6945), John Spray)
-   mon: add PG count to \'ceph osd df\' output (Michal Jarzabek)
-   mon: add RAW USED column to ceph df detail
    ([pr#7087](http://github.com/ceph/ceph/pull/7087), Ruifeng Yang)
-   mon: block \'ceph osd pg-temp \...\' if pg_temp update is already
    pending ([pr#6704](http://github.com/ceph/ceph/pull/6704), Sage
    Weil)
-   mon: \'ceph osd metadata\' can dump all osds (Haomai Wang)
-   mon: clean up, reorg some mon commands (Joao Eduardo Luis)
-   mon: cleanup set-quota error msg
    ([pr#7371](http://github.com/ceph/ceph/pull/7371), Abhishek
    Lekshmanan)
-   monclient: avoid key renew storm on clock skew
    ([issue#12065](http://tracker.ceph.com/issues/12065),
    [pr#8258](http://github.com/ceph/ceph/pull/8258), Alexey Sheplyakov)
-   monclient: flush_log (John Spray)
-   mon: compact full epochs also
    ([issue#14537](http://tracker.ceph.com/issues/14537),
    [pr#7396](http://github.com/ceph/ceph/pull/7396), Kefu Chai)
-   mon: consider pool size when creating pool
    ([issue#14509](http://tracker.ceph.com/issues/14509),
    [pr#7359](http://github.com/ceph/ceph/pull/7359), songbaisen)
-   mon: consider the pool size when setting pool crush rule
    ([issue#14495](http://tracker.ceph.com/issues/14495),
    [pr#7341](http://github.com/ceph/ceph/pull/7341), song baisen)
-   mon: degrade a log message to level 2
    ([pr#6929](http://github.com/ceph/ceph/pull/6929), Kongming Wu)
-   mon: detect kv backend failures (Sage Weil)
-   mon: disallow \>2 tiers (#11840 Kefu Chai)
-   mon: disallow ec pools as tiers (#11650 Samuel Just)
-   mon: do not deactivate last mds (#10862 John Spray)
-   mon: do not send useless pg_create messages for split pgs
    ([pr#8247](http://github.com/ceph/ceph/pull/8247), Sage Weil)
-   mon: don\'t require OSD W for MRemoveSnaps
    ([issue#13777](http://tracker.ceph.com/issues/13777),
    [pr#6601](http://github.com/ceph/ceph/pull/6601), John Spray)
-   mon: drop useless rank init assignment
    ([issue#14508](http://tracker.ceph.com/issues/14508),
    [pr#7321](http://github.com/ceph/ceph/pull/7321), huanwen ren)
-   mon: enable \'mon osd prime pg temp\' by default
    ([pr#7838](http://github.com/ceph/ceph/pull/7838), Robert LeBlanc)
-   mon: fix average utilization calc for \'osd df\' (Mykola Golub)
-   mon: fix calculation of %USED
    ([pr#7881](http://github.com/ceph/ceph/pull/7881), Adam Kupczyk)
-   mon: fix ceph df pool available calculation for 0-weighted OSDs
    ([pr#6660](http://github.com/ceph/ceph/pull/6660), Chengyuan Li)
-   mon: fix coding-style on PG related Monitor files
    ([pr#6881](http://github.com/ceph/ceph/pull/6881), Wido den
    Hollander)
-   mon: fix CRUSH map test for new pools (Sage Weil)
-   mon: fixes related to mondbstore-\>get() changes
    ([pr#6564](http://github.com/ceph/ceph/pull/6564), Piotr Dałek)
-   mon: fix keyring permissions
    ([issue#14950](http://tracker.ceph.com/issues/14950),
    [pr#7880](http://github.com/ceph/ceph/pull/7880), Owen Synge)
-   mon: fix locking in preinit error paths
    ([issue#14473](http://tracker.ceph.com/issues/14473),
    [pr#7353](http://github.com/ceph/ceph/pull/7353), huanwen ren)
-   mon: fix log dump crash when debugging (Mykola Golub)
-   mon: fix mds beacon replies (#11590 Kefu Chai)
-   mon: fix metadata update race (Mykola Golub)
-   mon: fix min_last_epoch_clean tracking (Kefu Chai)
-   mon: fix monmap creation stamp
    ([pr#7459](http://github.com/ceph/ceph/pull/7459), duanweijun)
-   mon: fix \'pg ls\' sort order, state names (#11569 Kefu Chai)
-   mon: fix refresh (#11470 Joao Eduardo Luis)
-   mon: fix reuse of osd ids (clear osd info on osd deletion)
    ([issue#13988](http://tracker.ceph.com/issues/13988),
    [pr#6900](http://github.com/ceph/ceph/pull/6900), Loic Dachary, Sage
    Weil)
-   mon: fix routed_request_tids leak
    ([pr#6102](http://github.com/ceph/ceph/pull/6102), Ning Yao)
-   mon: fix sync of config-key data
    ([pr#7363](http://github.com/ceph/ceph/pull/7363), Xiaowei Chen)
-   mon: fix the can\'t change subscribe level bug in monitoring log
    ([pr#7031](http://github.com/ceph/ceph/pull/7031), Zhiqiang Wang)
-   mon: fix variance calc in \'osd df\' (Sage Weil)
-   mon: go into ERR state if multiple PGs are stuck inactive
    ([issue#13923](http://tracker.ceph.com/issues/13923),
    [pr#7253](http://github.com/ceph/ceph/pull/7253), Wido den
    Hollander)
-   mon: improve callout to crushtool (Mykola Golub)
-   mon: initialize [last]()\* timestamps on new pgs to creation time
    ([issue#14952](http://tracker.ceph.com/issues/14952),
    [pr#7980](http://github.com/ceph/ceph/pull/7980), Sage Weil)
-   mon: initialize recorded election epoch properly even when
    standalone ([issue#13627](http://tracker.ceph.com/issues/13627),
    [pr#6407](http://github.com/ceph/ceph/pull/6407), huanwen ren)
-   mon: make blocked op messages more readable (Jianpeng Ma)
-   mon: make clock skew checks sane
    ([issue#14175](http://tracker.ceph.com/issues/14175),
    [pr#7141](http://github.com/ceph/ceph/pull/7141), Joao Eduardo Luis)
-   mon: make osd get pool \'all\' only return applicable fields (#10891
    Michal Jarzabek)
-   mon: mark_down_pgs in lockstep with pg_map\'s osdmap epoch
    ([pr#8208](http://github.com/ceph/ceph/pull/8208), Sage Weil)
-   mon/MDSMonitor: add confirmation to \"ceph mds rmfailed\"
    ([issue#14379](http://tracker.ceph.com/issues/14379),
    [pr#7248](http://github.com/ceph/ceph/pull/7248), Yan, Zheng)
-   mon/MDSMonitor.cc: properly note beacon when health metrics changes
    ([issue#14684](http://tracker.ceph.com/issues/14684),
    [pr#7757](http://github.com/ceph/ceph/pull/7757), Yan, Zheng)
-   mon: misc scaling fixes (Sage Weil)
-   mon: modify a dout level in OSDMonitor.cc
    ([pr#6928](http://github.com/ceph/ceph/pull/6928), Yongqiang He)
-   mon/MonClient: avoid null pointer error when configured incorrectly
    ([issue#14405](http://tracker.ceph.com/issues/14405),
    [pr#7276](http://github.com/ceph/ceph/pull/7276), Bo Cai)
-   mon/MonClient: fix shutdown race
    ([issue#13992](http://tracker.ceph.com/issues/13992),
    [pr#8335](http://github.com/ceph/ceph/pull/8335), Sage Weil)
-   mon/monitor: some clean up
    ([pr#7520](http://github.com/ceph/ceph/pull/7520), huanwen ren)
-   mon: MonmapMonitor: don\'t expose uncommitted state to client
    ([pr#6854](http://github.com/ceph/ceph/pull/6854), Joao Eduardo
    Luis)
-   mon: normalize erasure-code profile for storage and comparison (Loic
    Dachary)
-   mon: only send mon metadata to supporting peers (Sage Weil)
-   mon: optionally specify osd id on \'osd create\' (Mykola Golub)
-   mon/OSDMonitor: osdmap laggy set a maximum limit for interval
    ([pr#7109](http://github.com/ceph/ceph/pull/7109), Zengran Zhang)
-   mon: osd \[test-\]reweight-by-{pg,utilization} command updates
    ([pr#7890](http://github.com/ceph/ceph/pull/7890), Dan van der Ster,
    Sage Weil)
-   mon: \'osd tree\' fixes (Kefu Chai)
-   mon: paxos is_recovering calc error
    ([pr#7227](http://github.com/ceph/ceph/pull/7227), Weijun Duan)
-   mon: periodic background scrub (Joao Eduardo Luis)
-   mon/PGMap: show rd/wr iops separately in status reports
    ([pr#7072](http://github.com/ceph/ceph/pull/7072), Cilang Zhao)
-   mon: PGMonitor: acting primary diff with cur_stat, should not set pg
    to stale ([pr#7083](http://github.com/ceph/ceph/pull/7083), Xiaowei
    Chen)
-   mon/PGMonitor: reliably mark PGs state
    ([pr#8089](http://github.com/ceph/ceph/pull/8089), Sage Weil)
-   mon: PG Monitor should report waiting for backfill
    ([issue#12744](http://tracker.ceph.com/issues/12744),
    [pr#7398](http://github.com/ceph/ceph/pull/7398), Abhishek
    Lekshmanan)
-   mon/pgmonitor: use appropriate forced conversions in get_rule_avail
    ([pr#7705](http://github.com/ceph/ceph/pull/7705), huanwen ren)
-   mon: prevent bucket deletion when referenced by a crush rule (#11602
    Sage Weil)
-   mon: prevent pgp_num \> pg_num (#12025 Xinxin Shu)
-   mon: prevent pool with snapshot state from being used as a tier
    (#11493 Sage Weil)
-   mon: prime pg_temp when CRUSH map changes (Sage Weil)
-   mon: reduce CPU and memory manager pressure of pg health check
    ([pr#7482](http://github.com/ceph/ceph/pull/7482), Piotr Dałek)
-   mon: refine check_remove_tier checks (#11504 John Spray)
-   mon: reject large max_mds values (#12222 John Spray)
-   mon: remove \'mds setmap\'
    ([issue#15136](http://tracker.ceph.com/issues/15136),
    [pr#8121](http://github.com/ceph/ceph/pull/8121), Sage Weil)
-   mon: remove remove_legacy_versions()
    ([pr#8324](http://github.com/ceph/ceph/pull/8324), Kefu Chai)
-   mon: remove spurious who arg from \'mds rm \...\' (John Spray)
-   mon: remove unnecessary comment for update_from_paxos
    ([pr#8400](http://github.com/ceph/ceph/pull/8400), Qinghua Jin)
-   mon: remove unused variable
    ([issue#15292](http://tracker.ceph.com/issues/15292),
    [pr#8337](http://github.com/ceph/ceph/pull/8337), Javier M. Mellid)
-   mon: revert MonitorDBStore\'s WholeStoreIteratorImpl::get
    ([issue#13742](http://tracker.ceph.com/issues/13742),
    [pr#6522](http://github.com/ceph/ceph/pull/6522), Piotr Dałek)
-   mon: should not set isvalid = true when cephx_verify_authorizer
    return false ([issue#13525](http://tracker.ceph.com/issues/13525),
    [pr#6306](http://github.com/ceph/ceph/pull/6306), Ruifeng Yang)
-   mon: show the pool quota info on ceph df detail command
    ([issue#14216](http://tracker.ceph.com/issues/14216),
    [pr#7094](http://github.com/ceph/ceph/pull/7094), song baisen)
-   mon: some cleanup in MonmapMonitor.cc
    ([pr#7418](http://github.com/ceph/ceph/pull/7418), huanwen ren)
-   mon: standardize Ceph removal commands
    ([pr#7939](http://github.com/ceph/ceph/pull/7939), Dongsheng Yang)
-   mon: streamline session handling, fix memory leaks (Sage Weil)
-   mon: support min_down_reporter by subtree level (default by host)
    ([pr#6709](http://github.com/ceph/ceph/pull/6709), Xiaoxi Chen)
-   mon: unconfuse object count skew message
    ([pr#7882](http://github.com/ceph/ceph/pull/7882), Piotr Dałek)
-   mon: unregister command on shutdown
    ([pr#7504](http://github.com/ceph/ceph/pull/7504), huanwen ren)
-   mon: upgrades must pass through hammer (Sage Weil)
-   mon: warn if pg(s) not scrubbed
    ([issue#13142](http://tracker.ceph.com/issues/13142),
    [pr#6440](http://github.com/ceph/ceph/pull/6440), Michal Jarzabek)
-   mon: warn on bogus cache tier config (Jianpeng Ma)
-   mount.ceph: memory leaks
    ([pr#6905](http://github.com/ceph/ceph/pull/6905), Qiankun Zheng)
-   mount.fuse.ceph: better parsing of arguments passed to
    mount.fuse.ceph by mount command
    ([issue#14735](http://tracker.ceph.com/issues/14735),
    [pr#7607](http://github.com/ceph/ceph/pull/7607), Florent Bautista)
-   mrun: update path to cmake binaries
    ([pr#8447](http://github.com/ceph/ceph/pull/8447), Casey Bodley)
-   msg: add override to virutal methods
    ([pr#6977](http://github.com/ceph/ceph/pull/6977), Michal Jarzabek)
-   msg: add thread safety for \"random\" Messenger + fix wrong usage of
    random functions ([pr#7650](http://github.com/ceph/ceph/pull/7650),
    Avner BenHanoch)
-   msg/async: AsyncConnection: avoid debug log in cleanup_handler
    ([pr#7547](http://github.com/ceph/ceph/pull/7547), Haomai Wang)
-   msg/async: AsyncMessenger: fix several bugs
    ([pr#7831](http://github.com/ceph/ceph/pull/7831), Haomai Wang)
-   msg/async: AsyncMessenger: fix valgrind leak
    ([pr#7725](http://github.com/ceph/ceph/pull/7725), Haomai Wang)
-   msg/async: avoid log spam on throttle
    ([issue#15031](http://tracker.ceph.com/issues/15031),
    [pr#8263](http://github.com/ceph/ceph/pull/8263), Kefu Chai)
-   msg/async: bunch of fixes
    ([pr#7379](http://github.com/ceph/ceph/pull/7379), Piotr Dałek)
-   msg/async: cleanup dead connection and misc things
    ([pr#7158](http://github.com/ceph/ceph/pull/7158), Haomai Wang)
-   msg/async: don\'t calculate msg header crc when not needed
    ([pr#7815](http://github.com/ceph/ceph/pull/7815), Piotr Dałek)
-   msg/async: don\'t use shared_ptr to manage EventCallback
    ([pr#7028](http://github.com/ceph/ceph/pull/7028), Haomai Wang)
-   msg/async: Event: fix clock skew problem
    ([pr#7949](http://github.com/ceph/ceph/pull/7949), Wei Jin)
-   msg/async: fix array boundary
    ([pr#7451](http://github.com/ceph/ceph/pull/7451), Wei Jin)
-   msg: async: fix perf counter description and simplify
    \_send_keepalive_or_ack
    ([pr#8046](http://github.com/ceph/ceph/pull/8046), xie xingguo)
-   msg/async: fix potential race condition
    ([pr#7453](http://github.com/ceph/ceph/pull/7453), Haomai Wang)
-   msg/async: fix send closed local_connection message problem
    ([pr#7255](http://github.com/ceph/ceph/pull/7255), Haomai Wang)
-   msg/async: let receiver ack message ASAP
    ([pr#6478](http://github.com/ceph/ceph/pull/6478), Haomai Wang)
-   msg/async: reduce extra tcp packet for message ack
    ([pr#7380](http://github.com/ceph/ceph/pull/7380), Haomai Wang)
-   msg/async: remove experiment feature
    ([pr#7820](http://github.com/ceph/ceph/pull/7820), Haomai Wang)
-   msg: async: small cleanups
    ([pr#7871](http://github.com/ceph/ceph/pull/7871), xie xingguo)
-   msg/async: smarter MSG_MORE
    ([pr#7625](http://github.com/ceph/ceph/pull/7625), Piotr Dałek)
-   msg: async: start over after failing to bind a port in specified
    range ([issue#14928](http://tracker.ceph.com/issues/14928),
    [issue#13002](http://tracker.ceph.com/issues/13002),
    [pr#7852](http://github.com/ceph/ceph/pull/7852), xie xingguo)
-   msg/async: support of non-block connect in async messenger
    ([issue#12802](http://tracker.ceph.com/issues/12802),
    [pr#5848](http://github.com/ceph/ceph/pull/5848), Jianhui Yuan)
-   msg/async: \_try_send trim already sent for outcoming_bl more
    efficient ([pr#7970](http://github.com/ceph/ceph/pull/7970), Yan
    Jun)
-   msg/async: will crash if enabling async msg because of an assertion
    ([pr#6640](http://github.com/ceph/ceph/pull/6640), Zhi Zhang)
-   msg: filter out lo addr when bind osd addr
    ([pr#7012](http://github.com/ceph/ceph/pull/7012), Ji Chen)
-   msgr: add ceph_perf_msgr tool (Hoamai Wang)
-   msgr: async: fix seq handling (Haomai Wang)
-   msgr: async: many many fixes (Haomai Wang)
-   msg: removed unneeded includes from Dispatcher
    ([pr#6814](http://github.com/ceph/ceph/pull/6814), Michal Jarzabek)
-   msg: remove duplicated code - local_delivery will now call
    \'enqueue\' ([pr#7948](http://github.com/ceph/ceph/pull/7948), Avner
    BenHanoch)
-   msg: remove unneeded inline
    ([pr#6989](http://github.com/ceph/ceph/pull/6989), Michal Jarzabek)
-   msgr: fix large message data content length causing overflow
    ([pr#6809](http://github.com/ceph/ceph/pull/6809), Jun Huang, Haomai
    Wang)
-   msgr: simple: fix clear_pipe (#11381 Haomai Wang)
-   msgr: simple: fix connect_seq assert (Haomai Wang)
-   msgr: xio: fastpath improvements (Raju Kurunkad)
-   msgr: xio: fix ip and nonce (Raju Kurunkad)
-   msgr: xio: improve lane assignment (Vu Pham)
-   msgr: xio: misc fixes (#10735 Matt Benjamin, Kefu Chai, Danny
    Al-Gaaf, Raju Kurunkad, Vu Pham, Casey Bodley)
-   msgr: xio: sync with accellio v1.4 (Vu Pham)
-   msg: significantly reduce minimal memory usage of connections
    ([pr#7567](http://github.com/ceph/ceph/pull/7567), Piotr Dałek)
-   msg/simple: pipe: memory leak when signature check failed
    ([pr#7096](http://github.com/ceph/ceph/pull/7096), Ruifeng Yang)
-   msg/simple: remove unneeded friend declarations
    ([pr#6924](http://github.com/ceph/ceph/pull/6924), Michal Jarzabek)
-   msg: unit tests (Haomai Wang)
-   msg/xio: fix compilation
    ([pr#7479](http://github.com/ceph/ceph/pull/7479), Roi Dayan)
-   msg/xio: fixes ([pr#7603](http://github.com/ceph/ceph/pull/7603),
    Roi Dayan)
-   mstart: start rgw on different ports as well
    ([pr#8167](http://github.com/ceph/ceph/pull/8167), Abhishek
    Lekshmanan)
-   nfs for rgw (Matt Benjamin, Orit Wasserman)
    ([pr#7634](http://github.com/ceph/ceph/pull/7634), Yehuda Sadeh,
    Matt Benjamin)
-   objectcacher: misc bug fixes (Jianpeng Ma)
-   objecter: avoid recursive lock of Objecter::rwlock
    ([pr#7343](http://github.com/ceph/ceph/pull/7343), Yan, Zheng)
-   organizationmap: modify org mail info.
    ([pr#7240](http://github.com/ceph/ceph/pull/7240), Xiaowei Chen)
-   os/bluestore: a few fixes
    ([pr#8193](http://github.com/ceph/ceph/pull/8193), Sage Weil)
-   os/bluestore/BlueFS: Before reap ioct, it should wait io complete
    ([pr#8178](http://github.com/ceph/ceph/pull/8178), Jianpeng Ma)
-   os/bluestore/BlueStore: Don\'t leak trim overlay data before write.
    ([pr#7895](http://github.com/ceph/ceph/pull/7895), Jianpeng Ma)
-   os/bluestore: ceph-bluefs-tool fixes
    ([issue#15261](http://tracker.ceph.com/issues/15261),
    [pr#8292](http://github.com/ceph/ceph/pull/8292), Venky Shankar)
-   os/bluestore: clone overlay data
    ([pr#7860](http://github.com/ceph/ceph/pull/7860), Jianpeng Ma)
-   os/bluestore: fix assert
    ([issue#14436](http://tracker.ceph.com/issues/14436),
    [pr#7293](http://github.com/ceph/ceph/pull/7293), xie xingguo)
-   os/bluestore: fix a typo in SPDK path parsing
    ([pr#7601](http://github.com/ceph/ceph/pull/7601), Jianjian Huo)
-   os/bluestore: fix bluestore_wal_transaction_t encoding test
    ([pr#7342](http://github.com/ceph/ceph/pull/7342), Kefu Chai)
-   os/bluestore: fix bluestore_wal_transaction_t encoding test
    ([pr#7419](http://github.com/ceph/ceph/pull/7419), Kefu Chai, Brad
    Hubbard)
-   os/bluestore: insert new onode to the front position of onode LRU
    ([pr#7492](http://github.com/ceph/ceph/pull/7492), Jianjian Huo)
-   os/bluestore/KernelDevice: force block size
    ([pr#8006](http://github.com/ceph/ceph/pull/8006), Sage Weil)
-   os/bluestore: make bluestore_sync_transaction = true can work.
    ([pr#7674](http://github.com/ceph/ceph/pull/7674), Jianpeng Ma)
-   os/bluestore/NVMEDevice: make IO thread using dpdk launch
    ([pr#8160](http://github.com/ceph/ceph/pull/8160), Haomai Wang)
-   os/bluestore/NVMEDevice: refactor probe/attach codes and support
    zero command ([pr#7647](http://github.com/ceph/ceph/pull/7647),
    Haomai Wang)
-   os/bluestore: revamp BlueFS bdev management and add perfcounters
    ([issue#15376](http://tracker.ceph.com/issues/15376),
    [pr#8431](http://github.com/ceph/ceph/pull/8431), Sage Weil)
-   os/bluestore: small fixes in bluestore StupidAllocator
    ([pr#8101](http://github.com/ceph/ceph/pull/8101), Jianjian Huo)
-   os/bluestore: use intrusive_ptr for Dir
    ([pr#7247](http://github.com/ceph/ceph/pull/7247), Igor Fedotov)
-   osd: add cache hint when pushing raw clone during recovery
    ([pr#7069](http://github.com/ceph/ceph/pull/7069), Zhiqiang Wang)
-   osd: Add config option osd_read_ec_check_for_errors for testing
    ([pr#5865](http://github.com/ceph/ceph/pull/5865), David Zafman)
-   osd: add latency perf counters for tier operations (Xinze Chi)
-   osd: add misc perfcounters (Xinze Chi)
-   osd: add missing newline to usage message
    ([pr#7613](http://github.com/ceph/ceph/pull/7613), Willem Jan
    Withagen)
-   osd: add osd op queue latency perfcounter
    ([pr#5793](http://github.com/ceph/ceph/pull/5793), Haomai Wang)
-   osd: add pin/unpin support to cache tier (11066)
    ([pr#6326](http://github.com/ceph/ceph/pull/6326), Zhiqiang Wang)
-   osd: add \'proxy\' cache mode
    ([issue#12814](http://tracker.ceph.com/issues/12814),
    [pr#8210](http://github.com/ceph/ceph/pull/8210), Sage Weil)
-   osd: add scrub persist/query API
    ([issue#13505](http://tracker.ceph.com/issues/13505),
    [pr#6898](http://github.com/ceph/ceph/pull/6898), Kefu Chai, Samuel
    Just)
-   osd: add simple sleep injection in recovery (Sage Weil)
-   osd: add the support of per pool scrub priority
    ([pr#7062](http://github.com/ceph/ceph/pull/7062), Zhiqiang Wang)
-   osd: a fix for HeartbeatDispatcher and cleanups
    ([pr#7550](http://github.com/ceph/ceph/pull/7550), Kefu Chai)
-   osd: Allow repair of history.last_epoch_started using config
    ([pr#6793](http://github.com/ceph/ceph/pull/6793), David Zafman)
-   osd: allow SEEK_HOLE/SEEK_DATA for sparse read (Zhiqiang Wang)
-   osd: auto repair EC pool
    ([issue#12754](http://tracker.ceph.com/issues/12754),
    [pr#6196](http://github.com/ceph/ceph/pull/6196), Guang Yang)
-   osd: avoid calculating crush mapping for most ops
    ([pr#6371](http://github.com/ceph/ceph/pull/6371), Sage Weil)
-   osd: avoid debug std::string initialization in PG::get/put
    ([pr#7117](http://github.com/ceph/ceph/pull/7117), Evgeniy Firsov)
-   osd: avoid double-check for replaying and can_checkpoint() in
    FileStore::\_check_replay_guard
    ([pr#6471](http://github.com/ceph/ceph/pull/6471), Ning Yao)
-   osd: avoid duplicate op-\>mark_started in ReplicatedBackend
    ([pr#6689](http://github.com/ceph/ceph/pull/6689), Jacek J. Łakis)
-   osd: avoid dup omap sets for in pg metadata (Sage Weil)
-   osd: avoid FORCE updating digest been overwritten by MAYBE when
    comparing scrub map
    ([pr#7051](http://github.com/ceph/ceph/pull/7051), Zhiqiang Wang)
-   osd: avoid multiple hit set insertions (Zhiqiang Wang)
-   osd: avoid osd_op_thread suicide because osd_scrub_sleep
    ([pr#7009](http://github.com/ceph/ceph/pull/7009), Jianpeng Ma)
-   osd: avoid transaction append in some cases (Sage Weil)
-   osd: bail out of \_committed_osd_maps if we are shutting down
    ([pr#8267](http://github.com/ceph/ceph/pull/8267), Samuel Just)
-   osd: blockdevice: avoid implicit cast and add guard
    ([pr#7460](http://github.com/ceph/ceph/pull/7460), xie xingguo)
-   osd: bluefs: fix alignment for odd page sizes
    ([pr#7900](http://github.com/ceph/ceph/pull/7900), Dan Mick)
-   osd: bluestore: add \'override\' to virtual functions
    ([pr#7886](http://github.com/ceph/ceph/pull/7886), Michal Jarzabek)
-   osd: bluestore: allow \_dump_onode dynamic accept log level
    ([pr#7995](http://github.com/ceph/ceph/pull/7995), Jianpeng Ma)
-   osd: bluestore/blockdevice: use std::mutex et al
    ([pr#7568](http://github.com/ceph/ceph/pull/7568), Sage Weil)
-   osd: bluestore: bluefs: fix several small bugs
    ([issue#14344](http://tracker.ceph.com/issues/14344),
    [issue#14343](http://tracker.ceph.com/issues/14343),
    [pr#7200](http://github.com/ceph/ceph/pull/7200), xie xingguo)
-   osd: bluestore/BlueFS: initialize super block_size earlier in mkfs
    ([pr#7535](http://github.com/ceph/ceph/pull/7535), Sage Weil)
-   osd: bluestore: don\'t include when building without libaio
    ([issue#14207](http://tracker.ceph.com/issues/14207),
    [pr#7169](http://github.com/ceph/ceph/pull/7169), Mykola Golub)
-   osd: bluestore: fix bluestore onode_t attr leak
    ([pr#7125](http://github.com/ceph/ceph/pull/7125), Ning Yao)
-   osd: bluestore: fix bluestore_wal_transaction_t encoding test
    ([pr#7168](http://github.com/ceph/ceph/pull/7168), Kefu Chai)
-   osd: bluestore: fix check for write falling within the same extent
    ([issue#14954](http://tracker.ceph.com/issues/14954),
    [pr#7892](http://github.com/ceph/ceph/pull/7892), Jianpeng Ma)
-   osd: BlueStore: fix fsck and blockdevice read-relevant issue
    ([pr#7362](http://github.com/ceph/ceph/pull/7362), xie xingguo)
-   osd: BlueStore: fix null pointer access
    ([issue#14561](http://tracker.ceph.com/issues/14561),
    [pr#7435](http://github.com/ceph/ceph/pull/7435), xie xingguo)
-   osd: bluestore: fix several bugs
    ([issue#14259](http://tracker.ceph.com/issues/14259),
    [issue#14353](http://tracker.ceph.com/issues/14353),
    [issue#14260](http://tracker.ceph.com/issues/14260),
    [issue#14261](http://tracker.ceph.com/issues/14261),
    [pr#7122](http://github.com/ceph/ceph/pull/7122), xie xingguo)
-   osd: bluestore: fix space rebalancing, collection split, buffered
    reads ([pr#7196](http://github.com/ceph/ceph/pull/7196), Sage Weil)
-   osd: bluestore: for overwrite a extent, allocate new extent on
    min_alloc_size write
    ([pr#7996](http://github.com/ceph/ceph/pull/7996), Jianpeng Ma)
-   osd: bluestore: improve fs-type verification and tidy up
    ([pr#7651](http://github.com/ceph/ceph/pull/7651), xie xingguo)
-   osd: bluestore, kstore: fix nid overwritten logic
    ([issue#14407](http://tracker.ceph.com/issues/14407),
    [issue#14433](http://tracker.ceph.com/issues/14433),
    [pr#7283](http://github.com/ceph/ceph/pull/7283), xie xingguo)
-   osd: bluestore: misc fixes
    ([pr#7658](http://github.com/ceph/ceph/pull/7658), Jianpeng Ma)
-   osd: bluestore: more fixes
    ([pr#7130](http://github.com/ceph/ceph/pull/7130), Sage Weil)
-   osd: BlueStore/NVMEDevice: fix compiling and fd leak
    ([pr#7496](http://github.com/ceph/ceph/pull/7496), xie xingguo)
-   osd: bluestore: NVMEDevice: fix error handling
    ([pr#7799](http://github.com/ceph/ceph/pull/7799), xie xingguo)
-   osd: bluestore: remove unneeded includes
    ([pr#7870](http://github.com/ceph/ceph/pull/7870), Michal Jarzabek)
-   osd: bluestore: Revert NVMEDevice task cstor and refresh interface
    changes ([pr#7729](http://github.com/ceph/ceph/pull/7729), Haomai
    Wang)
-   osd: bluestore updates, scrub fixes
    ([pr#8035](http://github.com/ceph/ceph/pull/8035), Sage Weil)
-   osd: bluestore: use btree_map for allocator
    ([pr#7269](http://github.com/ceph/ceph/pull/7269), Igor Fedotov,
    Sage Weil)
-   osd: break PG removal into multiple iterations (#10198 Guang Yang)
-   osd: cache proxy-write support (Zhiqiang Wang, Samuel Just)
-   osd: cache tier: add config option for eviction check list size
    ([pr#6997](http://github.com/ceph/ceph/pull/6997), Yuan Zhou)
-   osd: call on_new_interval on newly split child PG
    ([issue#13962](http://tracker.ceph.com/issues/13962),
    [pr#6778](http://github.com/ceph/ceph/pull/6778), Sage Weil)
-   osd: cancel failure reports if we fail to rebind network
    ([pr#6278](http://github.com/ceph/ceph/pull/6278), Xinze Chi)
-   osdc: Fix race condition with tick_event and shutdown
    ([issue#14256](http://tracker.ceph.com/issues/14256),
    [pr#7151](http://github.com/ceph/ceph/pull/7151), Adam C. Emerson)
-   osd: change mutex to spinlock to optimize thread context switch.
    ([pr#6492](http://github.com/ceph/ceph/pull/6492), Xiaowei Chen)
-   osd: check do_shutdown before do_restart
    ([pr#6547](http://github.com/ceph/ceph/pull/6547), Xiaoxi Chen)
-   osd: check health state before pre_booting
    ([issue#14181](http://tracker.ceph.com/issues/14181),
    [pr#7053](http://github.com/ceph/ceph/pull/7053), Xiaoxi Chen)
-   osd: check scrub state when handling map (Jianpeng Ma)
-   osd: clarify the scrub result report
    ([pr#6534](http://github.com/ceph/ceph/pull/6534), Li Wang)
-   osd/ClassHandler: only dlclose() the classes not missing
    ([pr#8354](http://github.com/ceph/ceph/pull/8354), Kefu Chai)
-   osd: clean up CMPXATTR checks
    ([pr#5961](http://github.com/ceph/ceph/pull/5961), Jianpeng Ma)
-   osd: clean up some constness, privateness (Kefu Chai)
-   osd: clean up temp object if copy-from fails
    ([pr#8487](http://github.com/ceph/ceph/pull/8487), Sage Weil)
-   osd: clean up temp object if promotion fails (Jianpeng Ma)
-   osd: clear pg_stat_queue after stopping pgs
    ([issue#14212](http://tracker.ceph.com/issues/14212),
    [pr#7091](http://github.com/ceph/ceph/pull/7091), Sage Weil)
-   osdc/Objecter: allow per-pool calls to op_cancel_writes (John Spray)
-   osdc/Objecter: dout log after assign tid
    ([pr#8202](http://github.com/ceph/ceph/pull/8202), Xinze Chi)
-   osdc/Objecter: fix narrow race with tid assignment
    ([issue#14364](http://tracker.ceph.com/issues/14364),
    [pr#7981](http://github.com/ceph/ceph/pull/7981), Sage Weil)
-   osdc/Objecter: use full pgid hash in PGNLS ops
    ([pr#8378](http://github.com/ceph/ceph/pull/8378), Sage Weil)
-   osd: configure promotion based on write recency (Zhiqiang Wang)
-   osd: consider high/low mode when putting agent to sleep
    ([issue#14752](http://tracker.ceph.com/issues/14752),
    [pr#7631](http://github.com/ceph/ceph/pull/7631), Sage Weil)
-   osd: constrain collections to meta and PGs (normal and temp) (Sage
    Weil)
-   osd: correctly handle small osd_scrub_interval_randomize_ratio
    ([pr#7147](http://github.com/ceph/ceph/pull/7147), Samuel Just)
-   osd: defer decoding of MOSDRepOp/MOSDRepOpReply
    ([pr#6503](http://github.com/ceph/ceph/pull/6503), Xinze Chi)
-   osd: delay populating in-memory PG log hashmaps
    ([pr#6425](http://github.com/ceph/ceph/pull/6425), Piotr Dałek)
-   osd: disable filestore_xfs_extsize by default
    ([issue#14397](http://tracker.ceph.com/issues/14397),
    [pr#7265](http://github.com/ceph/ceph/pull/7265), Ken Dreyer)
-   osd: do not keep ref of old osdmap in pg
    ([issue#13990](http://tracker.ceph.com/issues/13990),
    [pr#7007](http://github.com/ceph/ceph/pull/7007), Kefu Chai)
-   osd: don\'t do random deep scrubs for user initiated scrubs
    ([pr#6673](http://github.com/ceph/ceph/pull/6673), David Zafman)
-   osd: don\'t send dup MMonGetOSDMap requests (Sage Weil, Kefu Chai)
-   osd: don\'t update epoch and rollback_info objects attrs if there is
    no need ([pr#6555](http://github.com/ceph/ceph/pull/6555), Ning Yao)
-   osd: drop deprecated removal pg type
    ([pr#6970](http://github.com/ceph/ceph/pull/6970), Igor Podoski)
-   osd: drop fiemap len=0 logic
    ([pr#7267](http://github.com/ceph/ceph/pull/7267), Sage Weil)
-   osd: drop the interim set from load_pgs()
    ([pr#6277](http://github.com/ceph/ceph/pull/6277), Piotr Dałek)
-   osd: dump number of missing objects for each peer with pg query
    ([pr#6058](http://github.com/ceph/ceph/pull/6058), Guang Yang)
-   osd: duplicated clear for peer_missing
    ([pr#8315](http://github.com/ceph/ceph/pull/8315), Ning Yao)
-   osd: EIO injection (David Zhang)
-   osd: elminiate txn apend, ECSubWrite copy (Samuel Just)
-   osd: enable perfcounters on sharded work queue mutexes
    ([pr#6455](http://github.com/ceph/ceph/pull/6455), Jacek J. Łakis)
-   osd: ensure new osdmaps commit before publishing them to pgs
    ([issue#15073](http://tracker.ceph.com/issues/15073),
    [pr#8096](http://github.com/ceph/ceph/pull/8096), Sage Weil)
-   osd: erasure-code: drop entries according to LRU (Andreas-Joachim
    Peters)
-   osd: erasure-code: fix SHEC floating point bug (#12936 Loic Dachary)
-   osd: erasure-code: update to ISA-L 2.14 (Yuan Zhou)
-   osd: filejournal: cleanup (David Zafman)
-   osd: FileJournal: \_fdump wrongly returns if journal is currently
    unreadable. ([issue#13626](http://tracker.ceph.com/issues/13626),
    [pr#6406](http://github.com/ceph/ceph/pull/6406), xie xingguo)
-   osd: FileJournal: fix return code of create method
    ([issue#14134](http://tracker.ceph.com/issues/14134),
    [pr#6988](http://github.com/ceph/ceph/pull/6988), xie xingguo)
-   osd: FileJournal: reduce locking scope in write_aio_bl
    ([issue#12789](http://tracker.ceph.com/issues/12789),
    [pr#5670](http://github.com/ceph/ceph/pull/5670), Zhi Zhang)
-   osd: filejournal: report journal entry count
    ([pr#7643](http://github.com/ceph/ceph/pull/7643), tianqing)
-   osd: FileJournal: support batch peak and pop from writeq
    ([pr#6701](http://github.com/ceph/ceph/pull/6701), Xinze Chi)
-   osd: FileStore: add a field indicate xattr only one chunk for set
    xattr. ([pr#6244](http://github.com/ceph/ceph/pull/6244), Jianpeng
    Ma)
-   osd: FileStore: Added O_DSYNC write scheme
    ([pr#7752](http://github.com/ceph/ceph/pull/7752), Somnath Roy)
-   osd: FileStore: add error check for object_map-\>sync()
    ([pr#7281](http://github.com/ceph/ceph/pull/7281), Chendi Xue)
-   osd: FileStore: cleanup: remove obsolete option
    \"filestore_xattr_use_omap\"
    ([issue#14356](http://tracker.ceph.com/issues/14356),
    [pr#7217](http://github.com/ceph/ceph/pull/7217), Vikhyat Umrao)
-   osd: filestore: clone using splice (Jianpeng Ma)
-   osd: FileStore: conditional collection of drive metadata
    ([pr#6956](http://github.com/ceph/ceph/pull/6956), Somnath Roy)
-   osd: filestore: FALLOC_FL_PUNCH_HOLE must be used with
    FALLOC_FL_KEEP_SIZE
    ([pr#7768](http://github.com/ceph/ceph/pull/7768), xinxin shu)
-   osd: filestore: fast abort if statfs encounters ENOENT
    ([pr#7703](http://github.com/ceph/ceph/pull/7703), xie xingguo)
-   osd: FileStore: fix initialization order for m_disable_wbthrottle
    ([pr#8067](http://github.com/ceph/ceph/pull/8067), Samuel Just)
-   osd: filestore: fix race condition with split vs
    collection_move_rename and long object names
    ([issue#14766](http://tracker.ceph.com/issues/14766),
    [pr#8136](http://github.com/ceph/ceph/pull/8136), Samuel Just)
-   osd: filestore: fix recursive lock (Xinxin Shu)
-   osd: filestore: fix result code overwritten for clone
    ([issue#14817](http://tracker.ceph.com/issues/14817),
    [issue#14827](http://tracker.ceph.com/issues/14827),
    [pr#7711](http://github.com/ceph/ceph/pull/7711), xie xingguo)
-   osd: filestore: fix wrong scope of result code for error cases
    during mkfs ([issue#14814](http://tracker.ceph.com/issues/14814),
    [pr#7704](http://github.com/ceph/ceph/pull/7704), xie xingguo)
-   osd: filestore: fix wrong scope of result code for error cases
    during mount ([issue#14815](http://tracker.ceph.com/issues/14815),
    [pr#7707](http://github.com/ceph/ceph/pull/7707), xie xingguo)
-   osd: FileStore: LFNIndex: remove redundant local variable \'obj\'.
    ([issue#13552](http://tracker.ceph.com/issues/13552),
    [pr#6333](http://github.com/ceph/ceph/pull/6333), xiexingguo)
-   osd: FileStore: modify the format of colon
    ([pr#7333](http://github.com/ceph/ceph/pull/7333), Donghai Xu)
-   osd: FileStore:: optimize lfn_unlink
    ([pr#6649](http://github.com/ceph/ceph/pull/6649), Jianpeng Ma)
-   osd: FileStore: potential memory leak if \_fgetattrs fails
    ([issue#13597](http://tracker.ceph.com/issues/13597),
    [pr#6377](http://github.com/ceph/ceph/pull/6377), xie xingguo)
-   osd: FileStore: print file name before osd assert if read file
    failed ([pr#7111](http://github.com/ceph/ceph/pull/7111), Ji Chen)
-   osd: FileStore: remove \_\_SWORD_TYPE dependency
    ([pr#6263](http://github.com/ceph/ceph/pull/6263), John Coyle)
-   osd: FileStore: remove unused local variable \'handle\'
    ([pr#6381](http://github.com/ceph/ceph/pull/6381), xie xingguo)
-   osd: filestore: restructure journal and op queue throttling
    ([pr#7767](http://github.com/ceph/ceph/pull/7767), Samuel Just)
-   osd: FileStore: support multiple ondisk finish and apply finishers
    ([pr#6486](http://github.com/ceph/ceph/pull/6486), Xinze Chi, Haomai
    Wang)
-   osd: FileStore: use pwritev instead of lseek+writev
    ([pr#7349](http://github.com/ceph/ceph/pull/7349), Haomai Wang, Tao
    Chang)
-   osd: fix bogus scrub results when missing a clone
    ([issue#12738](http://tracker.ceph.com/issues/12738),
    [issue#12740](http://tracker.ceph.com/issues/12740),
    [pr#5783](http://github.com/ceph/ceph/pull/5783), David Zafman)
-   osd: fix broken balance / localized read handling
    ([issue#13491](http://tracker.ceph.com/issues/13491),
    [pr#6364](http://github.com/ceph/ceph/pull/6364), Jason Dillaman)
-   osd: fix bug in [last]()\* PG state timestamps
    ([pr#6517](http://github.com/ceph/ceph/pull/6517), Li Wang)
-   osd: fix bugs for omap ops
    ([pr#8230](http://github.com/ceph/ceph/pull/8230), Jianpeng Ma)
-   osd: fix check_for_full (Henry Chang)
-   osd: fix ClassHandler::ClassData::get_filter()
    ([pr#6747](http://github.com/ceph/ceph/pull/6747), Yan, Zheng)
-   osd: fix/clean up full map request handling
    ([pr#8446](http://github.com/ceph/ceph/pull/8446), Sage Weil)
-   osd: fix debug message in OSD::is_healthy
    ([pr#6226](http://github.com/ceph/ceph/pull/6226), Xiaoxi Chen)
-   osd: fix dirty accounting in make_writeable (Zhiqiang Wang)
-   osd: fix dirtying info without correctly setting drity_info field
    ([pr#8275](http://github.com/ceph/ceph/pull/8275), xie xingguo)
-   osd: fix dump_ops_in_flight races
    ([issue#8885](http://tracker.ceph.com/issues/8885),
    [pr#8044](http://github.com/ceph/ceph/pull/8044), David Zafman)
-   osd: fix dup promotion lost op bug (Zhiqiang Wang)
-   osd: fix endless repair when object is unrecoverable (Jianpeng Ma,
    Kefu Chai)
-   osd: fix epoch check in handle_pg_create
    ([pr#8382](http://github.com/ceph/ceph/pull/8382), Samuel Just)
-   osd: fixes for several cases where op result code was not checked or
    set ([issue#13566](http://tracker.ceph.com/issues/13566),
    [pr#6347](http://github.com/ceph/ceph/pull/6347), xie xingguo)
-   osd: fix failure report handling during ms_handle_connect()
    ([pr#8348](http://github.com/ceph/ceph/pull/8348), xie xingguo)
-   osd: fix FileStore::\_destroy_collection error return code
    ([pr#6612](http://github.com/ceph/ceph/pull/6612), Ruifeng Yang)
-   osd: fix forced prmootion for CALL ops
    ([issue#14745](http://tracker.ceph.com/issues/14745),
    [pr#7617](http://github.com/ceph/ceph/pull/7617), Sage Weil)
-   osd: fix fusestore hanging during stop/quit
    ([issue#14786](http://tracker.ceph.com/issues/14786),
    [pr#7677](http://github.com/ceph/ceph/pull/7677), xie xingguo)
-   osd: fix hitset object naming to use GMT (Kefu Chai)
-   osd: fix inaccurate counter and skip over queueing an empty
    transaction ([pr#7754](http://github.com/ceph/ceph/pull/7754), xie
    xingguo)
-   osd: fix incorrect throttle in WBThrottle
    ([pr#6713](http://github.com/ceph/ceph/pull/6713), Zhang Huan)
-   osd: fix invalid list traversal in process_copy_chunk
    ([pr#7511](http://github.com/ceph/ceph/pull/7511), Samuel Just)
-   osd: fix lack of object unblock when flush fails
    ([issue#14511](http://tracker.ceph.com/issues/14511),
    [pr#7584](http://github.com/ceph/ceph/pull/7584), Igor Fedotov)
-   osd: fix log info ([pr#8273](http://github.com/ceph/ceph/pull/8273),
    Wei Jin)
-   osd: fix misc memory leaks (Sage Weil)
-   osd: fix MOSDOp encoding
    ([pr#6174](http://github.com/ceph/ceph/pull/6174), Sage Weil)
-   osd: fix MOSDRepScrub reference counter in replica_scrub
    ([pr#6730](http://github.com/ceph/ceph/pull/6730), Jie Wang)
-   osd: fix negative degraded stats during backfill (Guang Yang)
-   osd: fix null pointer access and race condition
    ([issue#14072](http://tracker.ceph.com/issues/14072),
    [pr#6916](http://github.com/ceph/ceph/pull/6916), xie xingguo)
-   osd: fix osdmap dump of blacklist items (John Spray)
-   osd: fix overload of \'==\' operator for pg_stat_t
    ([issue#14921](http://tracker.ceph.com/issues/14921),
    [pr#7842](http://github.com/ceph/ceph/pull/7842), xie xingguo)
-   osd: fix peek_queue locking in FileStore (Xinze Chi)
-   osd: fix pg resurrection (#11429 Samuel Just)
-   osd: fix promotion vs full cache tier (Samuel Just)
-   osd: fix race condition for heartbeat_need_update
    ([issue#14387](http://tracker.ceph.com/issues/14387),
    [pr#7739](http://github.com/ceph/ceph/pull/7739), xie xingguo)
-   osd: fix reactivate (check OSDSuperblock in mkfs() when we already
    have the superblock)
    ([issue#13586](http://tracker.ceph.com/issues/13586),
    [pr#6385](http://github.com/ceph/ceph/pull/6385), Vicente Cheng)
-   osd: fix reference count, rare race condition etc.
    ([pr#8254](http://github.com/ceph/ceph/pull/8254), xie xingguo)
-   osd: fix replay requeue when pg is still activating (#13116 Samuel
    Just)
-   osd: fix return value from maybe_handle_cache_detail()
    ([pr#7593](http://github.com/ceph/ceph/pull/7593), Igor Fedotov)
-   osd: fix rollback_info_trimmed_to before index()
    ([issue#13965](http://tracker.ceph.com/issues/13965),
    [pr#6801](http://github.com/ceph/ceph/pull/6801), Samuel Just)
-   osd: fix scrub start hobject
    ([pr#7467](http://github.com/ceph/ceph/pull/7467), Sage Weil)
-   osd: fix scrub stat bugs (Sage Weil, Samuel Just)
-   osd: fix snap flushing from cache tier (again) (#11787 Samuel Just)
-   osd: fix snap handling on promotion (#11296 Sam Just)
-   osd: fix sparse-read result code checking logic
    ([issue#14151](http://tracker.ceph.com/issues/14151),
    [pr#7016](http://github.com/ceph/ceph/pull/7016), xie xingguo)
-   osd: fix temp-clearing (David Zafman)
-   osd: fix temp object removal after upgrade
    ([issue#13862](http://tracker.ceph.com/issues/13862),
    [pr#6976](http://github.com/ceph/ceph/pull/6976), David Zafman)
-   osd: fix tick relevant issues
    ([pr#8369](http://github.com/ceph/ceph/pull/8369), xie xingguo)
-   osd: fix trivial scrub bug
    ([pr#6533](http://github.com/ceph/ceph/pull/6533), Li Wang)
-   osd: fix two scrub relevant issues
    ([pr#8462](http://github.com/ceph/ceph/pull/8462), xie xingguo)
-   osd: fix unnecessary object promotion when deleting from cache pool
    ([issue#13894](http://tracker.ceph.com/issues/13894),
    [pr#7537](http://github.com/ceph/ceph/pull/7537), Igor Fedotov)
-   osd: fix wip (l_osd_op_wip) perf counter and remove repop_map
    ([pr#7077](http://github.com/ceph/ceph/pull/7077), Xinze Chi)
-   osd: fix wrongly placed assert and some cleanups
    ([pr#6766](http://github.com/ceph/ceph/pull/6766), xiexingguo, xie
    xingguo)
-   osd: fix wrong return type of find_osd_on_ip()
    ([issue#14872](http://tracker.ceph.com/issues/14872),
    [pr#7812](http://github.com/ceph/ceph/pull/7812), xie xingguo)
-   osd: fix wrong use of right parenthesis in localized read logic
    ([pr#6566](http://github.com/ceph/ceph/pull/6566), Jie Wang)
-   osd: force promotion for ops EC can\'t handle (Zhiqiang Wang)
-   osd: ghobject_t: use ! instead of @ as a separator
    ([pr#7595](http://github.com/ceph/ceph/pull/7595), Sage Weil)
-   osd: handle dup pg_create that races with pg deletion
    ([pr#8033](http://github.com/ceph/ceph/pull/8033), Sage Weil)
-   osd: handle log split with overlapping entries (#11358 Samuel Just)
-   osd: ignore non-existent osds in unfound calc (#10976 Mykola Golub)
-   osd: improve behavior on machines with large memory pages (Steve
    Capper)
-   osd: improve temperature calculation for cache tier agent
    ([pr#4737](http://github.com/ceph/ceph/pull/4737), MingXin Liu)
-   osd: include a temp namespace within each collection/pgid (Sage
    Weil)
-   osd: increase default max open files (Owen Synge)
-   osd: initialize last_recalibrate field at construction
    ([pr#8071](http://github.com/ceph/ceph/pull/8071), xie xingguo)
-   osd: init started to 0
    ([issue#13206](http://tracker.ceph.com/issues/13206),
    [pr#6107](http://github.com/ceph/ceph/pull/6107), Sage Weil)
-   osd: KeyValueStore: don\'t queue NULL context
    ([pr#6783](http://github.com/ceph/ceph/pull/6783), Haomai Wang)
-   osd: KeyValueStore: fix return code of mkfs
    ([pr#7036](http://github.com/ceph/ceph/pull/7036), xie xingguo)
-   osd: KeyValueStore: fix the name\'s typo of
    keyvaluestore_default_strip_size
    ([pr#6375](http://github.com/ceph/ceph/pull/6375), Zhi Zhang)
-   osd: KeyValueStore: fix wrongly placed assert
    ([issue#14176](http://tracker.ceph.com/issues/14176),
    [issue#14178](http://tracker.ceph.com/issues/14178),
    [pr#7047](http://github.com/ceph/ceph/pull/7047), xie xingguo)
-   osd: keyvaluestore: misc fixes (Varada Kari)
-   osd: kstore: fix a race condition in \_txc_finish()
    ([pr#7804](http://github.com/ceph/ceph/pull/7804), Jianjian Huo)
-   osd: kstore: latency breakdown
    ([pr#7850](http://github.com/ceph/ceph/pull/7850), James Liu)
-   osd: kstore: several small fixes
    ([issue#14351](http://tracker.ceph.com/issues/14351),
    [issue#14352](http://tracker.ceph.com/issues/14352),
    [pr#7213](http://github.com/ceph/ceph/pull/7213), xie xingguo)
-   osd: kstore: small fixes to kstore
    ([issue#14204](http://tracker.ceph.com/issues/14204),
    [pr#7095](http://github.com/ceph/ceph/pull/7095), xie xingguo)
-   osd: kstore: sync up kstore with recent bluestore updates
    ([pr#7681](http://github.com/ceph/ceph/pull/7681), Jianjian Huo)
-   osd: low and high speed flush modes (Mingxin Liu)
-   osd: make backend and block device code a bit more generic
    ([pr#6759](http://github.com/ceph/ceph/pull/6759), Sage Weil)
-   osd: make list_missing query missing_loc.needs_recovery_map
    ([pr#6298](http://github.com/ceph/ceph/pull/6298), Guang Yang)
-   osd: make suicide timeouts individually configurable (Samuel Just)
-   osdmap: remove unused local variables
    ([pr#6864](http://github.com/ceph/ceph/pull/6864), luo kexue)
-   osdmap: rm nonused variable
    ([pr#8423](http://github.com/ceph/ceph/pull/8423), Wei Jin)
-   osd: memstore: fix alignment of Page for test_pageset
    ([pr#7587](http://github.com/ceph/ceph/pull/7587), Casey Bodley)
-   osd: memstore: fix two bugs
    ([pr#6963](http://github.com/ceph/ceph/pull/6963), Casey Bodley,
    Sage Weil)
-   osd: merge local_t and op_t txn to single one
    ([pr#6439](http://github.com/ceph/ceph/pull/6439), Xinze Chi)
-   osd: merge multiple setattr calls into a setattrs call (Xinxin Shu)
-   osd: min_write_recency_for_promote & min_read_recency_for_promote
    are tiering only ([pr#8081](http://github.com/ceph/ceph/pull/8081),
    huanwen ren)
-   osd: misc FileStore fixes
    ([issue#14192](http://tracker.ceph.com/issues/14192),
    [issue#14188](http://tracker.ceph.com/issues/14188),
    [issue#14194](http://tracker.ceph.com/issues/14194),
    [issue#14187](http://tracker.ceph.com/issues/14187),
    [issue#14186](http://tracker.ceph.com/issues/14186),
    [pr#7059](http://github.com/ceph/ceph/pull/7059), xie xingguo)
-   osd: misc fixes (Ning Yao, Kefu Chai, Xinze Chi, Zhiqiang Wang,
    Jianpeng Ma)
-   osd: misc optimization for map utilization
    ([pr#6950](http://github.com/ceph/ceph/pull/6950), Ning Yao)
-   osd, mon: fix exit issue
    ([pr#7420](http://github.com/ceph/ceph/pull/7420), Jiaying Ren)
-   osd,mon: log leveldb and rocksdb to ceph log
    ([pr#6921](http://github.com/ceph/ceph/pull/6921), Sage Weil)
-   osd: more fixes for incorrectly dirtying info; resend reply for
    duplicated scrub-reserve req
    ([pr#8291](http://github.com/ceph/ceph/pull/8291), xie xingguo)
-   osd: move newest decode version of MOSDOp and MOSDOpReply to the
    front ([pr#6642](http://github.com/ceph/ceph/pull/6642), Jacek J.
    Łakis)
-   osd: move scrub in OpWQ (Samuel Just)
-   osd: new and delete ObjectStore::Transaction in a function is not
    necessary ([pr#6299](http://github.com/ceph/ceph/pull/6299), Ruifeng
    Yang)
-   osd: newstore: misc updates (including kv and os/fs stuff)
    ([pr#6609](http://github.com/ceph/ceph/pull/6609), Sage Weil)
-   osd: newstore prototype (Sage Weil)
-   osd: note down the number of missing clones
    ([pr#6654](http://github.com/ceph/ceph/pull/6654), Kefu Chai)
-   osd: ObjectStore internal API refactor (Sage Weil)
-   osd: Omap small bugs adapted
    ([pr#6669](http://github.com/ceph/ceph/pull/6669), Jianpeng Ma,
    David Zafman)
-   osd: optimize clone write path if object-map is enabled
    ([pr#6403](http://github.com/ceph/ceph/pull/6403), xinxin shu)
-   osd: optimize get_object_context
    ([pr#6305](http://github.com/ceph/ceph/pull/6305), Jianpeng Ma)
-   osd: optimize MOSDOp/do_op/handle_op
    ([pr#5211](http://github.com/ceph/ceph/pull/5211), Jacek J. Lakis)
-   osd: optimize scrub subset_last_update calculation
    ([pr#6518](http://github.com/ceph/ceph/pull/6518), Li Wang)
-   osd: optimize the session_handle_reset function
    ([issue#14182](http://tracker.ceph.com/issues/14182),
    [pr#7054](http://github.com/ceph/ceph/pull/7054), songbaisen)
-   osd: os/chain_xattr: On linux use linux/limits.h for XATTR_NAME_MAX.
    ([pr#6343](http://github.com/ceph/ceph/pull/6343), John Coyle)
-   osd/OSD.cc: finish full_map_request every MOSDMap message.
    ([issue#15130](http://tracker.ceph.com/issues/15130),
    [pr#8147](http://github.com/ceph/ceph/pull/8147), Xiaoxi Chen)
-   osd/OSD: fix build_past_intervals_parallel
    ([pr#8215](http://github.com/ceph/ceph/pull/8215), David Zafman)
-   osd/OSDMap: fix typo in summarize_mapping_stats
    ([pr#8088](http://github.com/ceph/ceph/pull/8088), Sage Weil)
-   osd: OSDMap: reset osd_primary_affinity shared_ptr when
    deepish_copy_from
    ([issue#14686](http://tracker.ceph.com/issues/14686),
    [pr#7553](http://github.com/ceph/ceph/pull/7553), Xinze Chi)
-   osd: OSDService: Fix typo in osdmap comment
    ([pr#7275](http://github.com/ceph/ceph/pull/7275), Brad Hubbard)
-   osd: os: skip checking pg_meta object existance in FileStore
    ([pr#6870](http://github.com/ceph/ceph/pull/6870), Ning Yao)
-   osd: partial revert of \"ReplicatedPG: result code not correctly set
    in some cases.\"
    ([issue#13796](http://tracker.ceph.com/issues/13796),
    [pr#6622](http://github.com/ceph/ceph/pull/6622), Sage Weil)
-   osd: peer_features includes self (David Zafman)
-   osd: PG::activate(): handle unexpected cached_removed_snaps more
    gracefully ([issue#14428](http://tracker.ceph.com/issues/14428),
    [pr#7309](http://github.com/ceph/ceph/pull/7309), Alexey Sheplyakov)
-   osd/PG: indicate in pg query output whether ignore_history_les would
    help ([pr#8156](http://github.com/ceph/ceph/pull/8156), Sage Weil)
-   osd: PGLog: clean up read_log
    ([pr#7092](http://github.com/ceph/ceph/pull/7092), Jie Wang)
-   osd/PGLog: fix warning
    ([pr#8057](http://github.com/ceph/ceph/pull/8057), Sage Weil)
-   osd: pg_pool_t: add dictionary for pool options
    ([issue#13077](http://tracker.ceph.com/issues/13077),
    [pr#6081](http://github.com/ceph/ceph/pull/6081), Mykola Golub)
-   osd/PG: set epoch_created and parent_split_bits for child pg
    ([issue#15426](http://tracker.ceph.com/issues/15426),
    [pr#8552](http://github.com/ceph/ceph/pull/8552), Kefu Chai)
-   osd: pool size change triggers new interval (#11771 Samuel Just)
-   osd: prepopulate needs_recovery_map when only one peer has missing
    (#9558 Guang Yang)
-   osd: prevent osd_recovery_sleep from causing recovery-thread suicide
    ([pr#7065](http://github.com/ceph/ceph/pull/7065), Jianpeng Ma)
-   osd: probabilistic cache tier promotion throttling
    ([pr#7465](http://github.com/ceph/ceph/pull/7465), Sage Weil)
-   osd: randomize deep scrubbing
    ([pr#6550](http://github.com/ceph/ceph/pull/6550), Dan van der Ster,
    Herve Rousseau)
-   osd: randomize scrub times (#10973 Kefu Chai)
-   osd: recovery, peering fixes (#11687 Samuel Just)
-   osd: reduce memory consumption of some structs
    ([pr#6475](http://github.com/ceph/ceph/pull/6475), Piotr Dałek)
-   osd: reduce string use in coll_t::calc_str()
    ([pr#6505](http://github.com/ceph/ceph/pull/6505), Igor Podoski)
-   osd: refactor scrub and digest recording (Sage Weil)
-   osd: refuse first write to EC object at non-zero offset (Jianpeng
    Ma)
-   osd: relax reply order on proxy read (#11211 Zhiqiang Wang)
-   osd: release related sources when scrub is interrupted
    ([pr#6744](http://github.com/ceph/ceph/pull/6744), Jianpeng Ma)
-   osd: release the message throttle when OpRequest unregistered
    ([issue#14248](http://tracker.ceph.com/issues/14248),
    [pr#7148](http://github.com/ceph/ceph/pull/7148), Samuel Just)
-   osd: remove \_\_SWORD_TYPE dependency
    ([pr#6262](http://github.com/ceph/ceph/pull/6262), John Coyle)
-   osd: remove unused OSDMap::set_weightf()
    ([issue#14369](http://tracker.ceph.com/issues/14369),
    [pr#7231](http://github.com/ceph/ceph/pull/7231), huanwen ren)
-   osd: remove up_thru_pending field, which is never used
    ([pr#7991](http://github.com/ceph/ceph/pull/7991), xie xingguo)
-   osd: reorder bool fields in PGLog struct
    ([pr#6279](http://github.com/ceph/ceph/pull/6279), Piotr Dałek)
-   osd: Replace snprintf with faster implementation in
    eversion_t::get_key_name
    ([pr#7121](http://github.com/ceph/ceph/pull/7121), Evgeniy Firsov)
-   osd/ReplicatedPG: be more careful about calling
    publish_stats_to_osd()
    ([issue#14962](http://tracker.ceph.com/issues/14962),
    [pr#8039](http://github.com/ceph/ceph/pull/8039), Greg Farnum)
-   osd: replicatedpg: break out loop if we encounter fatal error during
    do_pg_op() ([issue#14922](http://tracker.ceph.com/issues/14922),
    [pr#7844](http://github.com/ceph/ceph/pull/7844), xie xingguo)
-   osd: ReplicatedPG: clean up unused function
    ([pr#7211](http://github.com/ceph/ceph/pull/7211), Xiaowei Chen)
-   osd/ReplicatedPG: clear watches on change after applying repops
    ([issue#15151](http://tracker.ceph.com/issues/15151),
    [pr#8163](http://github.com/ceph/ceph/pull/8163), Sage Weil)
-   osd/ReplicatedPG: fix promotion recency logic
    ([issue#14320](http://tracker.ceph.com/issues/14320),
    [pr#6702](http://github.com/ceph/ceph/pull/6702), Sage Weil)
-   osd: ReplicatedPG: remove unused local variables
    ([issue#13575](http://tracker.ceph.com/issues/13575),
    [pr#6360](http://github.com/ceph/ceph/pull/6360), xiexingguo)
-   osd/ReplicatedPG::\_rollback_to: update the OMAP flag
    ([issue#14777](http://tracker.ceph.com/issues/14777),
    [pr#8495](http://github.com/ceph/ceph/pull/8495), Samuel Just)
-   osd: repop and lost-unfound overhaul
    ([pr#7765](http://github.com/ceph/ceph/pull/7765), Samuel Just)
-   osd: require firefly features (David Zafman)
-   osd: reset primary and up_primary when building a new past_interval.
    ([issue#13471](http://tracker.ceph.com/issues/13471),
    [pr#6240](http://github.com/ceph/ceph/pull/6240), xiexingguo)
-   osd: resolve boot vs NOUP set + clear race
    ([pr#7483](http://github.com/ceph/ceph/pull/7483), Sage Weil)
-   osd: scrub: do not assign value if read error
    ([pr#6568](http://github.com/ceph/ceph/pull/6568), Li Wang)
-   osd/ScrubStore: remove unused function
    ([pr#8045](http://github.com/ceph/ceph/pull/8045), Kefu Chai)
-   osd: set initial crush weight with more precision (Sage Weil)
-   osd: several small cleanups
    ([pr#7055](http://github.com/ceph/ceph/pull/7055), xie xingguo)
-   osd: SHEC no longer experimental
-   osd: shut down if we flap too many times in a short period
    ([pr#6708](http://github.com/ceph/ceph/pull/6708), Xiaoxi Chen)
-   osd: skip promote for writefull w/ FADVISE_DONTNEED/NOCACHE
    ([pr#7010](http://github.com/ceph/ceph/pull/7010), Jianpeng Ma)
-   osd: skip promotion for flush/evict op (Zhiqiang Wang)
-   osd: slightly reduce actual size of pg_log_entry_t
    ([pr#6690](http://github.com/ceph/ceph/pull/6690), Piotr Dałek)
-   osd: small fixes to memstore
    ([issue#14228](http://tracker.ceph.com/issues/14228),
    [issue#14229](http://tracker.ceph.com/issues/14229),
    [issue#14227](http://tracker.ceph.com/issues/14227),
    [pr#7107](http://github.com/ceph/ceph/pull/7107), xie xingguo)
-   osd: stripe over small xattrs to fit in XFS\'s 255 byte inline limit
    (Sage Weil, Ning Yao)
-   osd: support pool level recovery_priority and recovery_op_priority
    ([pr#5953](http://github.com/ceph/ceph/pull/5953), Guang Yang)
-   osd: sync object_map on syncfs (Samuel Just)
-   osd: take excl lock of op is rw (Samuel Just)
-   osd: throttle evict ops (Yunchuan Wen)
-   osd: try evicting after flushing is done
    ([pr#5630](http://github.com/ceph/ceph/pull/5630), Zhiqiang Wang)
-   osd: upgrades must pass through hammer (Sage Weil)
-   osd: use a temp object for recovery (Sage Weil)
-   osd: use atomic to generate ceph_tid
    ([pr#7017](http://github.com/ceph/ceph/pull/7017), Evgeniy Firsov)
-   osd: use blkid to collection partition information (Joseph Handzik)
-   osd: use optimized is_zero in object_stat_sum_t.is_zero()
    ([pr#7203](http://github.com/ceph/ceph/pull/7203), Piotr Dałek)
-   osd: use pg id (without shard) when referring the PG
    ([pr#6236](http://github.com/ceph/ceph/pull/6236), Guang Yang)
-   osd: use SEEK_HOLE / SEEK_DATA for sparse copy (Xinxin Shu)
-   osd: utime_t, eversion_t, osd_stat_sum_t encoding optimization
    ([pr#6902](http://github.com/ceph/ceph/pull/6902), Xinze Chi)
-   osd: WBThrottle cleanups (Jianpeng Ma)
-   osd: WeightedPriorityQueue: move to intrusive containers
    ([pr#7654](http://github.com/ceph/ceph/pull/7654), Robert LeBlanc)
-   osd: write file journal optimization
    ([pr#6484](http://github.com/ceph/ceph/pull/6484), Xinze Chi)
-   osd: write journal header on clean shutdown (Xinze Chi)
-   os/filestore: enlarge getxattr buffer size (Jianpeng Ma)
-   os/filestore/FileJournal: set block size via config option
    ([pr#7628](http://github.com/ceph/ceph/pull/7628), Sage Weil)
-   os/filestore: fix punch hole usage in \_zero
    ([pr#8050](http://github.com/ceph/ceph/pull/8050), Sage Weil)
-   os/filestore: fix result handling logic of destroy_collection
    ([pr#7721](http://github.com/ceph/ceph/pull/7721), xie xingguo)
-   os/filestore: force lfn attrs to be written atomically, restructure
    name length limits
    ([pr#8496](http://github.com/ceph/ceph/pull/8496), Samuel Just)
-   os/filestore: require offset == length == 0 for full object read;
    add test ([pr#7957](http://github.com/ceph/ceph/pull/7957), Jianpeng
    Ma)
-   os/fs: fix io_getevents argument
    ([pr#7355](http://github.com/ceph/ceph/pull/7355), Jingkai Yuan)
-   os/fusestore: add error handling
    ([pr#7395](http://github.com/ceph/ceph/pull/7395), xie xingguo)
-   os/keyvaluestore: kill KeyValueStore
    ([pr#7320](http://github.com/ceph/ceph/pull/7320), Haomai Wang)
-   os/kstore: insert new onode to the front position of onode LRU
    ([pr#7505](http://github.com/ceph/ceph/pull/7505), xie xingguo)
-   os/ObjectStore: add custom move operations for
    ObjectStore::Transaction
    ([pr#7303](http://github.com/ceph/ceph/pull/7303), Casey Bodley)
-   os/ObjectStore: add noexcept to ensure move ctor is used
    ([pr#8421](http://github.com/ceph/ceph/pull/8421), Kefu Chai)
-   os/ObjectStore: fix \_update_op for split dest_cid
    ([pr#8364](http://github.com/ceph/ceph/pull/8364), Sage Weil)
-   os/ObjectStore: implement more efficient get_encoded_bytes()
    ([pr#7775](http://github.com/ceph/ceph/pull/7775), Piotr Dałek)
-   os/ObjectStore: make device uuid probe output something friendly
    ([pr#8418](http://github.com/ceph/ceph/pull/8418), Sage Weil)
-   os/ObjectStore: try_move_rename in transaction append and add
    coverage to store_test
    ([issue#15205](http://tracker.ceph.com/issues/15205),
    [pr#8359](http://github.com/ceph/ceph/pull/8359), Samuel Just)
-   packaging: add build dependency on python devel package
    ([pr#7205](http://github.com/ceph/ceph/pull/7205), Josh Durgin)
-   packaging: make infernalis -\> jewel upgrade work
    ([issue#15047](http://tracker.ceph.com/issues/15047),
    [pr#8034](http://github.com/ceph/ceph/pull/8034), Nathan Cutler)
-   packaging: move cephfs repair tools to ceph-common
    ([issue#15145](http://tracker.ceph.com/issues/15145),
    [pr#8133](http://github.com/ceph/ceph/pull/8133), Boris Ranto, Ken
    Dreyer)
-   PG: pg down state blocked by osd.x, lost osd.x cannot solve peering
    stuck ([issue#13531](http://tracker.ceph.com/issues/13531),
    [pr#6317](http://github.com/ceph/ceph/pull/6317), Xiaowei Chen)
-   pybind: add ceph_volume_client interface for Manila and similar
    frameworks ([pr#6205](http://github.com/ceph/ceph/pull/6205), John
    Spray)
-   pybind: add flock to libcephfs python bindings
    ([pr#7902](http://github.com/ceph/ceph/pull/7902), John Spray)
-   pybind/cephfs: add symlink and its unit test
    ([pr#6323](http://github.com/ceph/ceph/pull/6323), Shang Ding)
-   pybind: decode empty string in conf_parse_argv() correctly
    ([pr#6711](http://github.com/ceph/ceph/pull/6711), Josh Durgin)
-   pybind: Ensure correct python flags are passed
    ([pr#7663](http://github.com/ceph/ceph/pull/7663), James Page)
-   pybind: fix build failure, remove extraneous semicolon in method
    ([issue#14371](http://tracker.ceph.com/issues/14371),
    [pr#7235](http://github.com/ceph/ceph/pull/7235), Abhishek
    Lekshmanan)
-   pybind: flag an RBD image as closed regardless of result code
    ([pr#8005](http://github.com/ceph/ceph/pull/8005), Jason Dillaman)
-   pybind: Implementation of rados_ioctx_snapshot_rollback
    ([pr#6878](http://github.com/ceph/ceph/pull/6878), Florent Manens)
-   pybind/Makefile.am: Prevent race creating CYTHON_BUILD_DIR
    ([issue#15276](http://tracker.ceph.com/issues/15276),
    [pr#8356](http://github.com/ceph/ceph/pull/8356), Dan Mick)
-   pybind: move cephfs to Cython
    ([pr#7745](http://github.com/ceph/ceph/pull/7745), John Spray, Mehdi
    Abaakouk)
-   pybind: pep8 cleanups (Danny Al-Gaaf)
-   pybind: port the rbd bindings to Cython
    ([issue#13115](http://tracker.ceph.com/issues/13115),
    [pr#6768](http://github.com/ceph/ceph/pull/6768), Hector Martin)
-   pybind/rados: fix object lifetime issues and other bugs in aio
    ([pr#7778](http://github.com/ceph/ceph/pull/7778), Hector Martin)
-   pybind/rados: python3 fix
    ([pr#8331](http://github.com/ceph/ceph/pull/8331), Mehdi Abaakouk)
-   pybind/rados: use \_\_dealloc\_\_ since \_\_del\_\_ is ignored by
    cython ([pr#7692](http://github.com/ceph/ceph/pull/7692), Mehdi
    Abaakouk)
-   pybind: remove next() on iterators
    ([pr#7706](http://github.com/ceph/ceph/pull/7706), Mehdi Abaakouk)
-   pybind: replace \_\_del\_\_ with \_\_dealloc\_\_ for rbd
    ([pr#7708](http://github.com/ceph/ceph/pull/7708), Josh Durgin)
-   pybind: support ioctx:exec
    ([pr#6795](http://github.com/ceph/ceph/pull/6795), Noah Watkins)
-   pybind/test_rbd: fix test_create_defaults
    ([issue#14279](http://tracker.ceph.com/issues/14279),
    [pr#7155](http://github.com/ceph/ceph/pull/7155), Josh Durgin)
-   pybind: use correct subdir for rados install-exec rule
    ([pr#7684](http://github.com/ceph/ceph/pull/7684), Josh Durgin)
-   pycephfs: many fixes for bindings (Haomai Wang)
-   python binding of librados with cython
    ([pr#7621](http://github.com/ceph/ceph/pull/7621), Mehdi Abaakouk)
-   python: use pip instead of python setup.py
    ([pr#7605](http://github.com/ceph/ceph/pull/7605), Loic Dachary)
-   qa: add workunit to run ceph_test_rbd_mirror
    ([pr#8221](http://github.com/ceph/ceph/pull/8221), Josh Durgin)
-   qa: disable rbd/qemu-iotests test case 055 on RHEL/CentOSlibrbd:
    journal replay should honor inter-event dependencies
    ([issue#14385](http://tracker.ceph.com/issues/14385),
    [pr#7272](http://github.com/ceph/ceph/pull/7272), Jason Dillaman)
-   qa: erasure-code benchmark plugin selection
    ([pr#6685](http://github.com/ceph/ceph/pull/6685), Loic Dachary)
-   qa: fix filelock_interrupt.py test (Yan, Zheng)
-   qa: improve ceph-disk tests (Loic Dachary)
-   qa: improve docker build layers (Loic Dachary)
-   qa/krbd: Expunge generic/247
    ([pr#6831](http://github.com/ceph/ceph/pull/6831), Douglas Fuller)
-   qa: run-make-check.sh script (Loic Dachary)
-   qa: update rest test cephfs calls
    ([issue#15309](http://tracker.ceph.com/issues/15309),
    [pr#8372](http://github.com/ceph/ceph/pull/8372), John Spray)
-   qa: update rest test cephfs calls (part 2)
    ([issue#15309](http://tracker.ceph.com/issues/15309),
    [pr#8393](http://github.com/ceph/ceph/pull/8393), John Spray)
-   qa/workunits/cephtool/test.sh: false positive fail on /tmp/obj1.
    ([pr#6837](http://github.com/ceph/ceph/pull/6837), Robin H. Johnson)
-   qa/workunits/cephtool/test.sh: no ./
    ([pr#6748](http://github.com/ceph/ceph/pull/6748), Sage Weil)
-   qa/workunits/cephtool/test.sh: wait longer in ceph_watch_start()
    ([issue#14910](http://tracker.ceph.com/issues/14910),
    [pr#7861](http://github.com/ceph/ceph/pull/7861), Kefu Chai)
-   qa/workunits: merge_diff shouldn\'t attempt to use striping
    ([issue#14165](http://tracker.ceph.com/issues/14165),
    [pr#7041](http://github.com/ceph/ceph/pull/7041), Jason Dillaman)
-   qa/workunits/rados/test.sh: capture stderr too
    ([pr#8004](http://github.com/ceph/ceph/pull/8004), Sage Weil)
-   qa/workunits/rados/test.sh: test tmap_migrate
    ([pr#8114](http://github.com/ceph/ceph/pull/8114), Sage Weil)
-   qa/workunits/rbd: do not use object map during read flag testing
    ([pr#8104](http://github.com/ceph/ceph/pull/8104), Jason Dillaman)
-   qa/workunits/rbd: new online maintenance op tests
    ([pr#8216](http://github.com/ceph/ceph/pull/8216), Jason Dillaman)
-   qa/workunits/rbd: rbd-nbd test should use sudo for map/unmap ops
    ([issue#14221](http://tracker.ceph.com/issues/14221),
    [pr#7101](http://github.com/ceph/ceph/pull/7101), Jason Dillaman)
-   qa/workunits/rbd: use POSIX function definition
    ([issue#15104](http://tracker.ceph.com/issues/15104),
    [pr#8068](http://github.com/ceph/ceph/pull/8068), Nathan Cutler)
-   qa/workunits/rest/test.py: add confirmation to \'mds setmap\'
    ([issue#14606](http://tracker.ceph.com/issues/14606),
    [pr#7982](http://github.com/ceph/ceph/pull/7982), Sage Weil)
-   qa/workunits/rest/test.py: don\'t use newfs
    ([pr#8191](http://github.com/ceph/ceph/pull/8191), Sage Weil)
-   qa/workunits/snaps: move snap tests into fs sub-directory
    ([pr#6496](http://github.com/ceph/ceph/pull/6496), Yan, Zheng)
-   rados: add ceph:: namespace to bufferlist type
    ([pr#8059](http://github.com/ceph/ceph/pull/8059), Noah Watkins)
-   rados: add \--striper option to use libradosstriper (#10759
    Sebastien Ponce)
-   rados: bench: add \--no-verify option to improve performance (Piotr
    Dalek)
-   rados: bench: fix off-by-one to avoid writing past object_size
    ([pr#6677](http://github.com/ceph/ceph/pull/6677), Tao Chang)
-   rados bench: misc fixes (Dmitry Yatsushkevich)
-   rados: fix bug for write bench
    ([pr#7851](http://github.com/ceph/ceph/pull/7851), James Liu)
-   rados: fix error message on failed pool removal (Wido den Hollander)
-   radosgw-admin: add \'bucket check\' function to repair bucket index
    (Yehuda Sadeh)
-   radosgw-admin: allow
    ([pr#8529](http://github.com/ceph/ceph/pull/8529), Orit Wasserman)
-   radosgw-admin: Checking the legality of the parameters
    ([issue#13018](http://tracker.ceph.com/issues/13018),
    [pr#5879](http://github.com/ceph/ceph/pull/5879), Qiankun Zheng)
-   radosgw-admin: Create \--secret-key alias for \--secret
    ([issue#5821](http://tracker.ceph.com/issues/5821),
    [pr#5335](http://github.com/ceph/ceph/pull/5335), Yuan Zhou)
-   radosgw-admin: fix for \'realm pull\'
    ([pr#8404](http://github.com/ceph/ceph/pull/8404), Casey Bodley)
-   radosgw-admin: fix subuser modify output (#12286 Guce)
-   radosgw-admin: metadata list user should return an empty list when
    user pool is empty
    ([issue#13596](http://tracker.ceph.com/issues/13596),
    [pr#6465](http://github.com/ceph/ceph/pull/6465), Orit Wasserman)
-   radosgw-admin: \'period commit\' supplies user-readable error
    messages ([pr#8264](http://github.com/ceph/ceph/pull/8264), Casey
    Bodley)
-   rados: handle \--snapid arg properly (Abhishek Lekshmanan)
-   rados: implement rm \--force option to force remove when full
    ([pr#6202](http://github.com/ceph/ceph/pull/6202), Xiaowei Chen)
-   rados: improve bench buffer handling, performance (Piotr Dalek)
-   rados: misc bench fixes (Dmitry Yatsushkevich)
-   rados: new options for write benchmark
    ([pr#6340](http://github.com/ceph/ceph/pull/6340), Joaquim Rocha)
-   rados: new pool import implementation (John Spray)
-   rados: translate errno to string in CLI (#10877 Kefu Chai)
-   rbd: accept map options config option (Ilya Dryomov)
-   rbd: accept \--user, refuse -i command-line optionals
    ([pr#6590](http://github.com/ceph/ceph/pull/6590), Ilya Dryomov)
-   rbd: add disk usage tool (#7746 Jason Dillaman)
-   rbd: additional validation for striping parameters
    ([pr#6914](http://github.com/ceph/ceph/pull/6914), Na Xie)
-   rbd: add missing command aliases to refactored CLI
    ([issue#13806](http://tracker.ceph.com/issues/13806),
    [pr#6606](http://github.com/ceph/ceph/pull/6606), Jason Dillaman)
-   rbd: add \--object-size option, deprecate \--order
    ([issue#12112](http://tracker.ceph.com/issues/12112),
    [pr#6830](http://github.com/ceph/ceph/pull/6830), Vikhyat Umrao)
-   rbd: add pool name to disambiguate rbd admin socket commands
    ([pr#6904](http://github.com/ceph/ceph/pull/6904), wuxiangwei)
-   rbd: add RBD pool mirroring configuration API + CLI
    ([pr#6129](http://github.com/ceph/ceph/pull/6129), Jason Dillaman)
-   rbd: add support for mirror image promotion/demotion/resync
    ([pr#8138](http://github.com/ceph/ceph/pull/8138), Jason Dillaman)
-   rbd: allow librados to prune the command-line for config overrides
    ([issue#15250](http://tracker.ceph.com/issues/15250),
    [pr#8282](http://github.com/ceph/ceph/pull/8282), Jason Dillaman)
-   rbd: allow unmapping by spec (Ilya Dryomov)
-   rbd: cli: fix arg parsing with \--io-pattern (Dmitry Yatsushkevich)
-   rbd: clone operation should default to image format 2
    ([pr#8119](http://github.com/ceph/ceph/pull/8119), Jason Dillaman)
-   rbd: correct an output string for merge-diff
    ([pr#7046](http://github.com/ceph/ceph/pull/7046), Kongming Wu)
-   rbd: deprecate image format 1
    ([pr#7841](http://github.com/ceph/ceph/pull/7841), Jason Dillaman)
-   rbd: deprecate \--new-format option (Jason Dillman)
-   rbd: dynamically generated bash completion
    ([issue#13494](http://tracker.ceph.com/issues/13494),
    [pr#6316](http://github.com/ceph/ceph/pull/6316), Jason Dillaman)
-   rbd: fix build with \"\--without-rbd\"
    ([issue#14058](http://tracker.ceph.com/issues/14058),
    [pr#6899](http://github.com/ceph/ceph/pull/6899), Piotr Dałek)
-   rbd: fix clone isssue
    ([issue#13553](http://tracker.ceph.com/issues/13553),
    [pr#6334](http://github.com/ceph/ceph/pull/6334), xinxin shu)
-   rbd: fix error messages (#2862 Rajesh Nambiar)
-   rbd: fixes for refactored CLI and related tests
    ([pr#6738](http://github.com/ceph/ceph/pull/6738), Ilya Dryomov)
-   rbd: fix init-rbdmap CMDPARAMS
    ([issue#13214](http://tracker.ceph.com/issues/13214),
    [pr#6109](http://github.com/ceph/ceph/pull/6109), Sage Weil)
-   rbd: fix link issues (Jason Dillaman)
-   rbd: fix static initialization ordering issues
    ([pr#6978](http://github.com/ceph/ceph/pull/6978), Mykola Golub)
-   rbd-fuse: image name can not include snap name
    ([pr#7044](http://github.com/ceph/ceph/pull/7044), Yongqiang He)
-   rbd-fuse: implement mv operation
    ([pr#6938](http://github.com/ceph/ceph/pull/6938), wuxiangwei)
-   rbd: improve CLI arg parsing, usage (Ilya Dryomov)
-   rbd: journal: configuration via conf, cli, api and some fixes
    ([pr#6665](http://github.com/ceph/ceph/pull/6665), Mykola Golub)
-   rbd: journal reset should disable/re-enable journaling feature
    ([issue#15097](http://tracker.ceph.com/issues/15097),
    [pr#8490](http://github.com/ceph/ceph/pull/8490), Jason Dillaman)
-   rbd: make config changes actually apply
    ([pr#6520](http://github.com/ceph/ceph/pull/6520), Mykola Golub)
-   rbdmap: add manpage
    ([issue#15212](http://tracker.ceph.com/issues/15212),
    [pr#8224](http://github.com/ceph/ceph/pull/8224), Nathan Cutler)
-   rbdmap: systemd support
    ([issue#13374](http://tracker.ceph.com/issues/13374),
    [pr#6479](http://github.com/ceph/ceph/pull/6479), Boris Ranto)
-   rbd: merge_diff test should use new \--object-size parameter instead
    of \--order ([issue#14106](http://tracker.ceph.com/issues/14106),
    [pr#6972](http://github.com/ceph/ceph/pull/6972), Na Xie, Jason
    Dillaman)
-   rbd-mirror: asok commands to get status and flush on Mirror and
    Replayer level ([pr#8235](http://github.com/ceph/ceph/pull/8235),
    Mykola Golub)
-   rbd-mirror: enabling/disabling pool mirroring should update the
    mirroring directory
    ([issue#15217](http://tracker.ceph.com/issues/15217),
    [pr#8261](http://github.com/ceph/ceph/pull/8261), Ricardo Dias)
-   rbd-mirror: fix image replay test failures
    ([pr#8158](http://github.com/ceph/ceph/pull/8158), Jason Dillaman)
-   rbd-mirror: fix long termination due to 30sec wait in main loop
    ([pr#8185](http://github.com/ceph/ceph/pull/8185), Mykola Golub)
-   rbd-mirror: fix missing increment for iterators
    ([pr#8352](http://github.com/ceph/ceph/pull/8352), runsisi)
-   rbd-mirror: ImageReplayer async start/stop
    ([pr#7944](http://github.com/ceph/ceph/pull/7944), Mykola Golub)
-   rbd-mirror: ImageReplayer improvements
    ([pr#7759](http://github.com/ceph/ceph/pull/7759), Mykola Golub)
-   rbd-mirror: implement ImageReplayer
    ([pr#7614](http://github.com/ceph/ceph/pull/7614), Mykola Golub)
-   rbd-mirror: initial failover / failback support
    ([pr#8287](http://github.com/ceph/ceph/pull/8287), Jason Dillaman)
-   rbd-mirror: integrate with image sync state machine
    ([pr#8079](http://github.com/ceph/ceph/pull/8079), Jason Dillaman)
-   rbd-mirror: make remote context respect env and argv config params
    ([pr#8182](http://github.com/ceph/ceph/pull/8182), Mykola Golub)
-   rbd-mirror: minor fix-ups for initial skeleton implementation
    ([pr#7958](http://github.com/ceph/ceph/pull/7958), Mykola Golub)
-   rbd-mirror: prevent enabling/disabling an image\'s mirroring when
    not in image mode
    ([issue#15267](http://tracker.ceph.com/issues/15267),
    [pr#8332](http://github.com/ceph/ceph/pull/8332), Ricardo Dias)
-   rbd-mirror: remote to local cluster image sync
    ([pr#7979](http://github.com/ceph/ceph/pull/7979), Jason Dillaman)
-   rbd-mirror: switch fsid over to mirror uuid
    ([issue#15238](http://tracker.ceph.com/issues/15238),
    [pr#8280](http://github.com/ceph/ceph/pull/8280), Ricardo Dias)
-   rbd-mirror: use pool/image names in asok commands
    ([pr#8159](http://github.com/ceph/ceph/pull/8159), Mykola Golub)
-   rbd-mirror: use the mirroring directory to detect candidate images
    ([issue#15142](http://tracker.ceph.com/issues/15142),
    [pr#8162](http://github.com/ceph/ceph/pull/8162), Ricardo Dias)
-   rbd-mirror: workaround for intermingled lockdep singletons
    ([pr#8476](http://github.com/ceph/ceph/pull/8476), Jason Dillaman)
-   rbd: must specify both of stripe-unit and stripe-count when
    specifying stripingv2 feature
    ([pr#7026](http://github.com/ceph/ceph/pull/7026), Donghai Xu)
-   rbd-nbd: add copyright
    ([pr#7166](http://github.com/ceph/ceph/pull/7166), Li Wang)
-   rbd-nbd: fix up return code handling
    ([pr#7215](http://github.com/ceph/ceph/pull/7215), Mykola Golub)
-   rbd-nbd: network block device (NBD) support for RBD
    ([pr#6657](http://github.com/ceph/ceph/pull/6657), Yunchuan Wen, Li
    Wang)
-   rbd-nbd: small improvements in logging and forking
    ([pr#7127](http://github.com/ceph/ceph/pull/7127), Mykola Golub)
-   rbd: output formatter may not be closed upon error
    ([issue#13711](http://tracker.ceph.com/issues/13711),
    [pr#6706](http://github.com/ceph/ceph/pull/6706), xie xingguo)
-   rbd: rbdmap improvements
    ([pr#6445](http://github.com/ceph/ceph/pull/6445), Boris Ranto)
-   rbd: rbd order will be place in 22, when set to 0 in the config_opt
    ([issue#14139](http://tracker.ceph.com/issues/14139),
    [issue#14047](http://tracker.ceph.com/issues/14047),
    [pr#6886](http://github.com/ceph/ceph/pull/6886), huanwen ren)
-   rbd: rbd-replay-prep and rbd-replay improvements (Jason Dillaman)
-   rbd: recognize queue_depth kernel option (Ilya Dryomov)
-   rbd: refactor cli command handling
    ([pr#5987](http://github.com/ceph/ceph/pull/5987), Jason Dillaman)
-   rbd/run_cli_tests.sh: Reflect test failures
    ([issue#14825](http://tracker.ceph.com/issues/14825),
    [pr#7781](http://github.com/ceph/ceph/pull/7781), Zack Cerza)
-   rbd: stripe unit/count set incorrectly from config
    ([pr#6593](http://github.com/ceph/ceph/pull/6593), Mykola Golub)
-   rbd: striping parameters should support 64bit integers
    ([pr#6942](http://github.com/ceph/ceph/pull/6942), Na Xie)
-   rbd: support for enabling/disabling mirroring on specific images
    ([issue#13296](http://tracker.ceph.com/issues/13296),
    [pr#8056](http://github.com/ceph/ceph/pull/8056), Ricardo Dias)
-   rbd: support G and T units for CLI (Abhishek Lekshmanan)
-   rbd: support negative boolean command-line optionals
    ([issue#13784](http://tracker.ceph.com/issues/13784),
    [pr#6607](http://github.com/ceph/ceph/pull/6607), Jason Dillaman)
-   rbd: unbreak rbd map + cephx_sign_messages option
    ([pr#6583](http://github.com/ceph/ceph/pull/6583), Ilya Dryomov)
-   rbd: update default image features
    ([pr#7846](http://github.com/ceph/ceph/pull/7846), Jason Dillaman)
-   rbd: update rbd man page (Ilya Dryomov)
-   rbd: update xfstests tests (Douglas Fuller)
-   rbd: use default order from configuration when not specified
    ([pr#6965](http://github.com/ceph/ceph/pull/6965), Yunchuan Wen)
-   rbd: use image-spec and snap-spec in help (Vikhyat Umrao, Ilya
    Dryomov)
-   release-notes: draft v0.94.4 release notes
    ([pr#5907](http://github.com/ceph/ceph/pull/5907), Loic Dachary)
-   release-notes: draft v0.94.4 release notes
    ([pr#6195](http://github.com/ceph/ceph/pull/6195), Loic Dachary)
-   release-notes: draft v0.94.4 release notes
    ([pr#6238](http://github.com/ceph/ceph/pull/6238), Loic Dachary)
-   release-notes: draft v0.94.6 release notes
    ([issue#13356](http://tracker.ceph.com/issues/13356),
    [pr#7689](http://github.com/ceph/ceph/pull/7689), Abhishek Varshney,
    Loic Dachary)
-   release-notes: draft v10.0.3 release notes
    ([pr#7592](http://github.com/ceph/ceph/pull/7592), Loic Dachary)
-   release-notes: draft v10.0.4 release notes
    ([pr#7966](http://github.com/ceph/ceph/pull/7966), Loic Dachary)
-   release-notes: draft v9.2.1 release notes
    ([issue#13750](http://tracker.ceph.com/issues/13750),
    [pr#7694](http://github.com/ceph/ceph/pull/7694), Abhishek Varshney)
-   releases: what is merged where and when ?
    ([pr#8358](http://github.com/ceph/ceph/pull/8358), Loic Dachary)
-   rest-bench: misc fixes (Shawn Chen)
-   rest-bench: support https (#3968 Yuan Zhou)
-   rgw: accept data only at the first time in response to a request
    ([pr#8084](http://github.com/ceph/ceph/pull/8084), sunspot)
-   rgw: add a few more help options in admin interface
    ([pr#8410](http://github.com/ceph/ceph/pull/8410), Abhishek
    Lekshmanan)
-   rgw: add a method to purge all associate keys when removing a
    subuser ([issue#12890](http://tracker.ceph.com/issues/12890),
    [pr#6002](http://github.com/ceph/ceph/pull/6002), Sangdi Xu)
-   rgw: add a missing cap type
    ([pr#6774](http://github.com/ceph/ceph/pull/6774), Yehuda Sadeh)
-   rgw: add an inspection to the field of type when assigning user caps
    ([pr#6051](http://github.com/ceph/ceph/pull/6051), Kongming Wu)
-   rgw: add bucket request payment feature usage statistics integration
    ([issue#13834](http://tracker.ceph.com/issues/13834),
    [pr#6656](http://github.com/ceph/ceph/pull/6656), Javier M. Mellid)
-   rgw: add compat header for TEMP_FAILURE_RETRY
    ([pr#6294](http://github.com/ceph/ceph/pull/6294), John Coyle)
-   rgw: add default quota config
    ([pr#6400](http://github.com/ceph/ceph/pull/6400), Daniel
    Gryniewicz)
-   rgw: add LifeCycle feature
    ([pr#6331](http://github.com/ceph/ceph/pull/6331), Ji Chen)
-   rgw: add max multipart upload parts (#12146 Abshishek Dixit)
-   rgw: add missing error code for admin op API
    ([pr#7037](http://github.com/ceph/ceph/pull/7037), Dunrong Huang)
-   rgw: add missing headers to Swift container details (#10666 Ahmad
    Faheem, Dmytro Iurchenko)
-   rgw: add stats to headers for account GET (#10684 Yuan Zhou)
-   rgw: adds the radosgw-admin sync status command that gives a human
    readable status of the sync process at a specific zone
    ([pr#8030](http://github.com/ceph/ceph/pull/8030), Yehuda Sadeh)
-   rgw: add support for caching of Keystone admin token.
    ([pr#7630](http://github.com/ceph/ceph/pull/7630), Radoslaw
    Zarzynski)
-   rgw: add support for \"end_marker\" parameter for GET on Swift
    account. ([issue#10682](http://tracker.ceph.com/issues/10682),
    [pr#4216](http://github.com/ceph/ceph/pull/4216), Radoslaw
    Zarzynski)
-   rgw: add support for getting Swift\'s DLO without manifest handling
    ([pr#6206](http://github.com/ceph/ceph/pull/6206), Radoslaw
    Zarzynski)
-   rgw: add support for metadata upload during PUT on Swift container.
    ([pr#8002](http://github.com/ceph/ceph/pull/8002), Radoslaw
    Zarzynski)
-   rgw: add support for Static Large Objects of Swift API
    ([issue#12886](http://tracker.ceph.com/issues/12886),
    [issue#13452](http://tracker.ceph.com/issues/13452),
    [pr#6643](http://github.com/ceph/ceph/pull/6643), Yehuda Sadeh,
    Radoslaw Zarzynski)
-   rgw: add support for system requests over Swift API
    ([pr#7666](http://github.com/ceph/ceph/pull/7666), Radoslaw
    Zarzynski)
-   rgw: add Trasnaction-Id to response (Abhishek Dixit)
-   rgw: add X-Timestamp for Swift containers (#10938 Radoslaw
    Zarzynski)
-   rgw: add zone delete to rgw-admin help
    ([pr#8184](http://github.com/ceph/ceph/pull/8184), Abhishek
    Lekshmanan)
-   rgw: adjust error code when bucket does not exist in copy operation
    ([issue#14975](http://tracker.ceph.com/issues/14975),
    [pr#7916](http://github.com/ceph/ceph/pull/7916), Yehuda Sadeh)
-   rgw: adjust the request_uri to support absoluteURI of http request
    ([issue#12917](http://tracker.ceph.com/issues/12917),
    [pr#7675](http://github.com/ceph/ceph/pull/7675), Wenjun Huang)
-   rgw: admin api for retrieving usage info (Ji Chen)
    ([pr#8031](http://github.com/ceph/ceph/pull/8031), Yehuda Sadeh, Ji
    Chen)
-   rgw_admin: orphans finish segfaults
    ([pr#6652](http://github.com/ceph/ceph/pull/6652), Igor Fedotov)
-   rgw-admin: remove unused iterator and fix error message
    ([pr#8507](http://github.com/ceph/ceph/pull/8507), Karol Mroz)
-   rgw_admin: remove unused parent_period arg
    ([pr#8411](http://github.com/ceph/ceph/pull/8411), Abhishek
    Lekshmanan)
-   rgw: Allow an implicit tenant in case of Keystone
    ([pr#8139](http://github.com/ceph/ceph/pull/8139), Pete Zaitcev)
-   rgw: allow authentication keystone with self signed certs
    ([issue#14853](http://tracker.ceph.com/issues/14853),
    [issue#13422](http://tracker.ceph.com/issues/13422),
    [pr#7777](http://github.com/ceph/ceph/pull/7777), Abhishek
    Lekshmanan)
-   rgw: always check if token is expired (#11367 Anton Aksola, Riku
    Lehto)
-   rgw: approximate AmazonS3 HostId error field.
    ([pr#7444](http://github.com/ceph/ceph/pull/7444), Robin H. Johnson)
-   rgw: aws4 subdomain calling bugfix
    ([issue#15369](http://tracker.ceph.com/issues/15369),
    [pr#8472](http://github.com/ceph/ceph/pull/8472), Javier M. Mellid)
-   rgw:bucket link now set the bucket.instance acl (bug fix)
    ([issue#11076](http://tracker.ceph.com/issues/11076),
    [pr#8037](http://github.com/ceph/ceph/pull/8037), Zengran Zhang)
-   rgw: bucket request payment support
    ([issue#13427](http://tracker.ceph.com/issues/13427),
    [pr#6214](http://github.com/ceph/ceph/pull/6214), Javier M. Mellid)
-   rgw: Bug fix for mtime anomalies in RadosGW and other places
    ([pr#7328](http://github.com/ceph/ceph/pull/7328), Adam C. Emerson,
    Casey Bodley)
-   rgw: build-related fixes
    ([pr#8076](http://github.com/ceph/ceph/pull/8076), Yehuda Sadeh,
    Matt Benjamin)
-   rgw: calculate payload hash in RGWPutObj_ObjStore only when
    necessary. ([pr#7869](http://github.com/ceph/ceph/pull/7869),
    Radoslaw Zarzynski)
-   \[rgw\] Check return code in RGWFileHandle::write
    ([pr#7875](http://github.com/ceph/ceph/pull/7875), Brad Hubbard)
-   rgw: check the return value when call fe-\>run()
    ([issue#14585](http://tracker.ceph.com/issues/14585),
    [pr#7457](http://github.com/ceph/ceph/pull/7457), wei qiaomiao)
-   rgw: clarify the error message when trying to create an existed user
    ([pr#5938](http://github.com/ceph/ceph/pull/5938), Zeqiang Zhuang)
-   rgw: cleanups to comments and messages
    ([pr#7633](http://github.com/ceph/ceph/pull/7633), Pete Zaitcev)
-   rgw: content length
    ([issue#13582](http://tracker.ceph.com/issues/13582),
    [pr#6975](http://github.com/ceph/ceph/pull/6975), Yehuda Sadeh)
-   rgw: conversion tool to repair broken multipart objects (#12079
    Yehuda Sadeh)
-   rgw: convert plain object to versioned (with null version) when
    removing ([issue#15243](http://tracker.ceph.com/issues/15243),
    [pr#8268](http://github.com/ceph/ceph/pull/8268), Yehuda Sadeh)
-   rgw: delete default zone
    ([pr#7005](http://github.com/ceph/ceph/pull/7005), YankunLi)
-   rgw: document layout of pools and objects (Pete Zaitcev)
-   rgw: do not abort radowgw server when using admin op API with bad
    parameters ([issue#14190](http://tracker.ceph.com/issues/14190),
    [issue#14191](http://tracker.ceph.com/issues/14191),
    [pr#7063](http://github.com/ceph/ceph/pull/7063), Dunrong Huang)
-   rgw: do not enclose bucket header in quotes (#11860 Wido den
    Hollander)
-   rgw: do not prefetch data for HEAD requests (Guang Yang)
-   rgw: do not preserve ACLs when copying object (#12370 Yehuda Sadeh)
-   rgw: Do not send a Content-Type on a \'304 Not Modified\' response
    ([issue#15119](http://tracker.ceph.com/issues/15119),
    [pr#8253](http://github.com/ceph/ceph/pull/8253), Wido den
    Hollander)
-   rgw: do not set content-type if length is 0 (#11091 Orit Wasserman)
-   rgw: don\'t clobber bucket/object owner when setting ACLs (#10978
    Yehuda Sadeh)
-   rgw: don\'t use end_marker for namespaced object listing (#11437
    Yehuda Sadeh)
-   rgw: don\'t use rgw_socket_path if frontend is configured (#11160
    Yehuda Sadeh)
-   rgw: don\'t use s-\>bucket for metadata api path entry
    ([issue#14549](http://tracker.ceph.com/issues/14549),
    [pr#7408](http://github.com/ceph/ceph/pull/7408), Yehuda Sadeh)
-   rgw: Drop a debugging message
    ([pr#7280](http://github.com/ceph/ceph/pull/7280), Pete Zaitcev)
-   rgw: drop permissions of rgw/civetweb after startup
    ([issue#13600](http://tracker.ceph.com/issues/13600),
    [pr#8019](http://github.com/ceph/ceph/pull/8019), Karol Mroz)
-   rgw: Drop unused usage_exit from rgw_admin.cc
    ([pr#7632](http://github.com/ceph/ceph/pull/7632), Pete Zaitcev)
-   rgw: enforce Content-Length for POST on Swift cont/obj (#10661
    Radoslaw Zarzynski)
-   rgw: error out if frontend did not send all data (#11851 Yehuda
    Sadeh)
-   rgw: expose the number of unhealthy workers through admin socket
    (Guang Yang)
-   rgw: extend rgw_extended_http_attrs to affect Swift accounts and
    containers as well
    ([pr#5969](http://github.com/ceph/ceph/pull/5969), Radoslaw
    Zarzynski)
-   rgw: fail if parts not specified on multipart upload (#11435 Yehuda
    Sadeh)
-   rgw: fcgi should include acconfig
    ([pr#7760](http://github.com/ceph/ceph/pull/7760), Abhishek
    Lekshmanan)
-   rgw_file: set owner uid, gid, and Unix mode on new objects
    ([pr#8321](http://github.com/ceph/ceph/pull/8321), Matt Benjamin)
-   rgw: fix a glaring syntax error
    ([pr#6888](http://github.com/ceph/ceph/pull/6888), Pavan
    Rallabhandi)
-   rgw: fix assignment of copy obj attributes (#11563 Yehuda Sadeh)
-   rgw: fix a typo in error message
    ([pr#8434](http://github.com/ceph/ceph/pull/8434), Abhishek
    Lekshmanan)
-   rgw: fix a typo in init-radosgw
    ([pr#6817](http://github.com/ceph/ceph/pull/6817), Zhi Zhang)
-   rgw: fix broken stats in container listing (#11285 Radoslaw
    Zarzynski)
-   rgw: fix bug in domain/subdomain splitting (Robin H. Johnson)
-   rgw: fix casing of Content-Type header (Robin H. Johnson)
-   rgw: fix civetweb max threads (#10243 Yehuda Sadeh)
-   rgw: fix compilation warning
    ([pr#7160](http://github.com/ceph/ceph/pull/7160), Yehuda Sadeh)
-   rgw: fix compiling error
    ([pr#8394](http://github.com/ceph/ceph/pull/8394), xie xingguo)
-   rgw: fix Connection: header handling (#12298 Wido den Hollander)
-   rgw: fix copy metadata, support X-Copied-From for swift (#10663
    Radoslaw Zarzynski)
-   rgw: fix data corruptions race condition (#11749 Wuxingyi)
-   rgw: fix decoding of X-Object-Manifest from GET on Swift DLO
    (Radslow Rzarzynski)
-   rgw: fixes for per-period metadata logs
    ([pr#7827](http://github.com/ceph/ceph/pull/7827), Casey Bodley)
-   rgw: fix GET on swift account when limit == 0 (#10683 Radoslaw
    Zarzynski)
-   rgw: fix handling empty metadata items on Swift container (#11088
    Radoslaw Zarzynski)
-   rgw: fix JSON response when getting user quota (#12117 Wuxingyi)
-   rgw: fix locator for objects starting with \_ (#11442 Yehuda Sadeh)
-   rgw: fix lockdep false positive
    ([pr#8284](http://github.com/ceph/ceph/pull/8284), Yehuda Sadeh)
-   rgw: fix log rotation (Wuxingyi)
-   rgw: fix mdlog ([pr#8183](http://github.com/ceph/ceph/pull/8183),
    Orit Wasserman)
-   rgw: fix mulitipart upload in retry path (#11604 Yehuda Sadeh)
-   rgw: fix objects can not be displayed which object name does not
    cont... ([issue#12963](http://tracker.ceph.com/issues/12963),
    [pr#5738](http://github.com/ceph/ceph/pull/5738), Weijun Duan)
-   rgw: fix openssl linkage
    ([pr#6513](http://github.com/ceph/ceph/pull/6513), Yehuda Sadeh)
-   rgw: fix partial read issue in rgw_admin and rgw_tools
    ([pr#6761](http://github.com/ceph/ceph/pull/6761), Jiaying Ren)
-   rgw: fix problem deleting objects begining with double underscores
    ([issue#15318](http://tracker.ceph.com/issues/15318),
    [pr#8488](http://github.com/ceph/ceph/pull/8488), Orit Wasserman)
-   rgw: fix quota enforcement on POST (#11323 Sergey Arkhipov)
-   rgw: fix reload on non Debian systems.
    ([pr#6482](http://github.com/ceph/ceph/pull/6482), Hervé Rousseau)
-   rgw: fix reset_loc (#11974 Yehuda Sadeh)
-   rgw: fix response of delete expired objects
    ([issue#13469](http://tracker.ceph.com/issues/13469),
    [pr#6228](http://github.com/ceph/ceph/pull/6228), Yuan Zhou)
-   rgw: fix return code on missing upload (#11436 Yehuda Sadeh)
-   rgw: Fix subuser harder with tenants
    ([pr#7618](http://github.com/ceph/ceph/pull/7618), Pete Zaitcev)
-   rgw: fix swift API returning incorrect account metadata
    ([issue#13140](http://tracker.ceph.com/issues/13140),
    [pr#6047](http://github.com/ceph/ceph/pull/6047), Sangdi Xu)
-   rgw: fix sysvinit script
-   rgw: fix sysvinit script w/ multiple instances (Sage Weil, Pavan
    Rallabhandi)
-   rgw: fix the build failure
    ([pr#6927](http://github.com/ceph/ceph/pull/6927), Kefu Chai)
-   rgw: fix typo in RGWHTTPClient::process error message
    ([pr#6424](http://github.com/ceph/ceph/pull/6424), Brad Hubbard)
-   rgw: fix wrong check for parse() return
    ([pr#6797](http://github.com/ceph/ceph/pull/6797), Dunrong Huang)
-   rgw: fix wrong etag calculation during POST on S3 bucket.
    ([issue#11241](http://tracker.ceph.com/issues/11241),
    [pr#6030](http://github.com/ceph/ceph/pull/6030), Radoslaw
    Zarzynski)
-   rgw: fix wrong handling of limit=0 during listing of Swift account.
    ([issue#14903](http://tracker.ceph.com/issues/14903),
    [pr#7821](http://github.com/ceph/ceph/pull/7821), Radoslaw
    Zarzynski)
-   rgw: force content_type for swift bucket stats requests (#12095 Orit
    Wasserman)
-   rgw: force content type header on responses with no body (#11438
    Orit Wasserman)
-   rgw: generate Date header for civetweb (#10873 Radoslaw Zarzynski)
-   rgw: generate new object tag when setting attrs (#11256 Yehuda
    Sadeh)
-   rgw: highres time stamps
    ([pr#8108](http://github.com/ceph/ceph/pull/8108), Yehuda Sadeh,
    Adam C. Emerson, Matt Benjamin)
-   rgw: improve content-length env var handling (#11419 Robin H.
    Johnson)
-   rgw: improved support for swift account metadata (Radoslaw
    Zarzynski)
-   rgw: improve error handling in S3/Keystone integration
    ([pr#7597](http://github.com/ceph/ceph/pull/7597), Radoslaw
    Zarzynski)
-   rgw: improve handling of already removed buckets in expirer
    (Radoslaw Rzarzynski)
-   rgw: increase verbosity level on RGWObjManifest line
    ([pr#7285](http://github.com/ceph/ceph/pull/7285), magicrobotmonkey)
-   rgw: indexless ([pr#7786](http://github.com/ceph/ceph/pull/7786),
    Yehuda Sadeh)
-   rgw: issue aio for first chunk before flush cached data (#11322
    Guang Yang)
-   rgw: Jewel nfs fixes 3
    ([pr#8460](http://github.com/ceph/ceph/pull/8460), Matt Benjamin)
-   rgw: keystone v3 ([pr#7719](http://github.com/ceph/ceph/pull/7719),
    Mark Barnes, Radoslaw Zarzynski)
-   rgw: ldap fixes ([pr#8168](http://github.com/ceph/ceph/pull/8168),
    Matt Benjamin)
-   rgw_ldap: make ldap.h inclusion conditional
    ([pr#8500](http://github.com/ceph/ceph/pull/8500), Matt Benjamin)
-   rgw: ldap (Matt Benjamin)
    ([pr#7985](http://github.com/ceph/ceph/pull/7985), Matt Benjamin)
-   rgw: let radosgw-admin bucket stats return a standard josn
    ([pr#7029](http://github.com/ceph/ceph/pull/7029), Ruifeng Yang)
-   rgw: link against system openssl (instead of dlopen at runtime)
    ([pr#6419](http://github.com/ceph/ceph/pull/6419), Sage Weil)
-   rgw: link civetweb with openssl (Sage, Marcus Watts)
    ([pr#7825](http://github.com/ceph/ceph/pull/7825), Marcus Watts,
    Sage Weil)
-   rgw: link payer info to usage logging
    ([pr#7918](http://github.com/ceph/ceph/pull/7918), Yehuda Sadeh,
    Javier M. Mellid)
-   rgw: log to /var/log/ceph instead of /var/log/radosgw
-   rgw: make init script wait for radosgw to stop (#11140 Dmitry
    Yatsushkevich)
-   rgw: make max put size configurable (#6999 Yuan Zhou)
-   rgw: make quota/gc threads configurable (#11047 Guang Yang)
-   rgw: make read user buckets backward compat (#10683 Radoslaw
    Zarzynski)
-   rgw: mdlog trim add usage prompt
    ([pr#6059](http://github.com/ceph/ceph/pull/6059), Weijun Duan)
-   rgw: merge manifests properly with prefix override (#11622 Yehuda
    Sadeh)
-   rgw: modify command stucking when operating radosgw-admin metadata
    list user ([pr#7032](http://github.com/ceph/ceph/pull/7032), Peiyang
    Liu)
-   rgw: modify documents and help infos\' descriptions to the usage of
    option date when executing command \"log show\"
    ([pr#6080](http://github.com/ceph/ceph/pull/6080), Kongming Wu)
-   rgw: modify the conditional statement in parse_metadata_key method.
    ([pr#5875](http://github.com/ceph/ceph/pull/5875), Zengran Zhang)
-   rgw: move signal.h dependency from rgw_front.h
    ([pr#7678](http://github.com/ceph/ceph/pull/7678), Matt Benjamin)
-   rgw: Multipart ListPartsResult ETag quotes
    ([issue#15334](http://tracker.ceph.com/issues/15334),
    [pr#8387](http://github.com/ceph/ceph/pull/8387), Robin H. Johnson)
-   rgw: multiple improvements regarding etag calculation for SLO/DLO of
    Swift API. ([pr#7764](http://github.com/ceph/ceph/pull/7764),
    Radoslaw Zarzynski)
-   rgw: multiple Swift API compliance improvements for TempURL
    (Radoslaw Zarzynsk)
    ([issue#14806](http://tracker.ceph.com/issues/14806),
    [issue#11163](http://tracker.ceph.com/issues/11163),
    [pr#7891](http://github.com/ceph/ceph/pull/7891), Radoslaw
    Zarzynski)
-   rgw: multisite fixes
    ([pr#8013](http://github.com/ceph/ceph/pull/8013), Yehuda Sadeh)
-   rgw: multitenancy support
    ([pr#6784](http://github.com/ceph/ceph/pull/6784), Yehuda Sadeh,
    Pete Zaitcev)
-   rgw: new multisite merge
    ([issue#14549](http://tracker.ceph.com/issues/14549),
    [pr#7709](http://github.com/ceph/ceph/pull/7709), Yehuda Sadeh, Orit
    Wasserman, Casey Bodley, Daniel Gryniewicz)
-   rgw: only scan for objects not in a namespace (#11984 Yehuda Sadeh)
-   rgw: orphan detection tool (Yehuda Sadeh)
-   rgw: Parse \--subuser better
    ([pr#7279](http://github.com/ceph/ceph/pull/7279), Pete Zaitcev)
-   rgw: pass in civetweb configurables (#10907 Yehuda Sadeh)
-   rgw: prevent anonymous user from reading bucket with authenticated
    read ACL ([issue#13207](http://tracker.ceph.com/issues/13207),
    [pr#6057](http://github.com/ceph/ceph/pull/6057), root)
-   rgw: radosgw-admin bucket check \--fix not work
    ([pr#7093](http://github.com/ceph/ceph/pull/7093), Weijun Duan)
-   rgw: rectify 202 Accepted in PUT response (#11148 Radoslaw
    Zarzynski)
-   rgw: refuse to calculate digest when the s3 secret key is empty
    ([issue#13133](http://tracker.ceph.com/issues/13133),
    [pr#6045](http://github.com/ceph/ceph/pull/6045), Sangdi Xu)
-   rgw: remove duplicated code in RGWRados::get_bucket_info()
    ([pr#7413](http://github.com/ceph/ceph/pull/7413), liyankun)
-   rgw: remove extra check in RGWGetObj::execute
    ([issue#12352](http://tracker.ceph.com/issues/12352),
    [pr#5262](http://github.com/ceph/ceph/pull/5262), Javier M. Mellid)
-   rgw: remove meta file after deleting bucket (#11149 Orit Wasserman)
-   rgw: remove trailing :port from HTTP_HOST header (Sage Weil)
-   rgw: Remove unused code in PutMetadataAccount:execute
    ([pr#6668](http://github.com/ceph/ceph/pull/6668), Pete Zaitcev)
-   rgw: remove unused variable in RGWPutMetadataBucket::execute
    ([pr#6735](http://github.com/ceph/ceph/pull/6735), Radoslaw
    Zarzynski)
-   rgw: remove unused vector
    ([pr#7990](http://github.com/ceph/ceph/pull/7990), Na Xie)
-   rgw: reset return code in when iterating over the bucket the objects
    ([issue#14826](http://tracker.ceph.com/issues/14826),
    [pr#7803](http://github.com/ceph/ceph/pull/7803), Orit Wasserman)
-   rgw: retry RGWRemoteMetaLog::read_log_info() while master is down
    ([pr#8453](http://github.com/ceph/ceph/pull/8453), Casey Bodley)
-   rgw: return 412 on bad limit when listing buckets (#11613 Yehuda
    Sadeh)
-   rgw: Revert \"rgw ldap\"
    ([pr#8075](http://github.com/ceph/ceph/pull/8075), Yehuda Sadeh)
-   rgw: rework X-Trans-Id header to conform with Swift API (Radoslaw
    Rzarzynski)
-   rgw/rgw_admin:fix bug about list and stats command
    ([pr#8200](http://github.com/ceph/ceph/pull/8200), Qiankun Zheng)
-   rgw/rgw_common.h: fix the RGWBucketInfo decoding
    ([pr#8154](http://github.com/ceph/ceph/pull/8154), Kefu Chai)
-   rgw/rgw_common.h: fix the RGWBucketInfo decoding
    ([pr#8165](http://github.com/ceph/ceph/pull/8165), Kefu Chai)
-   rgw: RGWLib::env is not used so remove it
    ([pr#7874](http://github.com/ceph/ceph/pull/7874), Brad Hubbard)
-   rgw/rgw_orphan: check the return value of save_state
    ([pr#7544](http://github.com/ceph/ceph/pull/7544), Boris Ranto)
-   rgw/rgw_resolve: fallback to res_query when res_nquery not
    implemented ([pr#6292](http://github.com/ceph/ceph/pull/6292), John
    Coyle)
-   rgw: RGWZoneParams::create should not handle -EEXIST error
    ([pr#7927](http://github.com/ceph/ceph/pull/7927), Orit Wasserman)
-   rgw: s3 encoding-type for get bucket (Jeff Weber)
-   rgw: S3: set EncodingType in ListBucketResult
    ([pr#7712](http://github.com/ceph/ceph/pull/7712), Victor Makarov)
-   rgw: send ETag, Last-Modified for swift (#11087 Radoslaw Zarzynski)
-   rgw: set content length on container GET, PUT, DELETE, HEAD (#10971,
    #11036 Radoslaw Zarzynski)
-   rgw: set max buckets per user in ceph.conf (Vikhyat Umrao)
-   rgw: shard work over multiple librados instances (Pavan Rallabhandi)
-   rgw: signature mismatch with escaped characters in url query portion
    ([issue#15358](http://tracker.ceph.com/issues/15358),
    [pr#8445](http://github.com/ceph/ceph/pull/8445), Javier M. Mellid)
-   rgw: static large objects (Radoslaw Zarzynski, Yehuda Sadeh)
-   rgw: store system object meta in cache when creating it
    ([issue#14678](http://tracker.ceph.com/issues/14678),
    [pr#7615](http://github.com/ceph/ceph/pull/7615), Yehuda Sadeh)
-   rgw: support core file limit for radosgw daemon
    ([pr#6346](http://github.com/ceph/ceph/pull/6346), Guang Yang)
-   rgw: support end marker on swift container GET (#10682 Radoslaw
    Zarzynski)
-   rgw: support for aws authentication v4 (Javier M. Mellid)
    ([issue#10333](http://tracker.ceph.com/issues/10333),
    [pr#7720](http://github.com/ceph/ceph/pull/7720), Yehuda Sadeh,
    Javier M. Mellid)
-   rgw: support for Swift expiration API (Radoslaw Rzarzynski, Yehuda
    Sadeh)
-   rgw: support json format for admin policy API (Dunrong Huang)
    ([issue#14090](http://tracker.ceph.com/issues/14090),
    [pr#8036](http://github.com/ceph/ceph/pull/8036), Yehuda Sadeh,
    Dunrong Huang)
-   rgw: swift: allow setting attributes with COPY (#10662 Ahmad Faheem,
    Dmytro Iurchenko)
-   rgw: swift bulk delete (Radoslaw Zarzynski)
-   rgw: swift: do not override sent content type (#12363 Orit
    Wasserman)
-   rgw: swift: enforce Content-Type in response (#12157 Radoslaw
    Zarzynski)
-   rgw: swift: fix account listing (#11501 Radoslaw Zarzynski)
-   rgw: swift: fix metadata handling on copy (#10645 Radoslaw
    Zarzynski)
-   rgw: swift: send Last-Modified header (#10650 Radoslaw Zarzynski)
-   rgw: swift: set Content-Length for account GET (#12158 Radoslav
    Zarzynski)
-   rgw: swift: set content-length on keystone tokens (#11473 Herv
    Rousseau)
-   rgw: swift use Civetweb ssl can not get right url
    ([issue#13628](http://tracker.ceph.com/issues/13628),
    [pr#6408](http://github.com/ceph/ceph/pull/6408), Weijun Duan)
-   rgw: swift versioning disabled
    ([pr#8066](http://github.com/ceph/ceph/pull/8066), Yehuda Sadeh,
    Radoslaw Zarzynski)
-   rgw: sync fixes 3 ([pr#8170](http://github.com/ceph/ceph/pull/8170),
    Yehuda Sadeh)
-   rgw: sync fixes 4 ([pr#8190](http://github.com/ceph/ceph/pull/8190),
    Yehuda Sadeh)
-   rgw sync fixes ([pr#8095](http://github.com/ceph/ceph/pull/8095),
    Yehuda Sadeh)
-   rgw: the map \'headers\' is assigned a wrong value
    ([pr#8481](http://github.com/ceph/ceph/pull/8481), weiqiaomiao)
-   rgw: try to parse Keystone token in order appropriate to
    configuration. ([pr#7822](http://github.com/ceph/ceph/pull/7822),
    Radoslaw Zarzynski)
-   rgw: update keystone cache with token info (#11125 Yehuda Sadeh)
-   rgw: update to latest civetweb, enable config for IPv6 (#10965
    Yehuda Sadeh)
-   rgw: use attrs from source bucket on copy (#11639 Javier M. Mellid)
-   rgw: use correct oid for gc chains (#11447 Yehuda Sadeh)
-   rgw:Use count fn in RGWUserBuckets for quota check
    ([pr#8294](http://github.com/ceph/ceph/pull/8294), Abhishek
    Lekshmanan)
-   rgw: use pimpl pattern for RGWPeriodHistory
    ([pr#7809](http://github.com/ceph/ceph/pull/7809), Casey Bodley)
-   rgw: user quota may not adjust on bucket removal
    ([issue#14507](http://tracker.ceph.com/issues/14507),
    [pr#7586](http://github.com/ceph/ceph/pull/7586), root)
-   rgw: user rm is idempotent (Orit Wasserman)
-   rgw: use smart pointer for C_Reinitwatch
    ([pr#6767](http://github.com/ceph/ceph/pull/6767), Orit Wasserman)
-   rgw: use unique request id for civetweb (#10295 Orit Wasserman)
-   rgw: warn on suspicious civetweb frontend parameters
    ([pr#6944](http://github.com/ceph/ceph/pull/6944), Matt Benjamin)
-   rocksdb: add perf counters for get/put latency (Xinxin Shu)
-   rocksdb: build with PORTABLE=1
    ([pr#6311](http://github.com/ceph/ceph/pull/6311), Sage Weil)
-   rocksdb, leveldb: fix compact_on_mount (Xiaoxi Chen)
-   rocksdb: pass options as single string (Xiaoxi Chen)
-   rocksdb: remove rdb source files from dist tarball
    ([issue#13554](http://tracker.ceph.com/issues/13554),
    [pr#6379](http://github.com/ceph/ceph/pull/6379), Kefu Chai)
-   rocksdb: remove rdb sources from dist tarball
    ([issue#13554](http://tracker.ceph.com/issues/13554),
    [pr#7105](http://github.com/ceph/ceph/pull/7105), Venky Shankar)
-   rocksdb: update to latest (Xiaoxi Chen)
-   rocksdb: use native rocksdb makefile (and our autotools)
    ([pr#6290](http://github.com/ceph/ceph/pull/6290), Sage Weil)
-   rpm: add suse firewall files (Tim Serong)
-   rpm: always rebuild and install man pages for rpm (Owen Synge)
-   rpm: ceph.spec.in: correctly declare systemd dependency for
    SLE/openSUSE ([pr#6114](http://github.com/ceph/ceph/pull/6114),
    Nathan Cutler)
-   rpm: ceph.spec.in: fix libs-compat / devel-compat conditional
    ([issue#12315](http://tracker.ceph.com/issues/12315),
    [pr#5219](http://github.com/ceph/ceph/pull/5219), Ken Dreyer)
-   rpm,deb: remove conditional BuildRequires for btrfs-progs
    ([issue#15042](http://tracker.ceph.com/issues/15042),
    [pr#8016](http://github.com/ceph/ceph/pull/8016), Erwan Velu)
-   rpm: loosen ceph-test dependencies (Ken Dreyer)
-   rpm: many spec file fixes (Owen Synge, Ken Dreyer)
-   rpm: misc fixes (Boris Ranto, Owen Synge, Ken Dreyer, Ira Cooper)
-   rpm: misc systemd and SUSE fixes (Owen Synge, Nathan Cutler)
-   rpm: move %post(un) ldconfig calls to ceph-base
    ([issue#14940](http://tracker.ceph.com/issues/14940),
    [pr#7867](http://github.com/ceph/ceph/pull/7867), Nathan Cutler)
-   rpm: move runtime dependencies to ceph-base and fix other packaging
    issues ([issue#14864](http://tracker.ceph.com/issues/14864),
    [pr#7826](http://github.com/ceph/ceph/pull/7826), Nathan Cutler)
-   rpm: prefer UID/GID 167 when creating ceph user/group
    ([issue#15246](http://tracker.ceph.com/issues/15246),
    [pr#8277](http://github.com/ceph/ceph/pull/8277), Nathan Cutler)
-   rpm: remove sub-package dependencies on \"ceph\"
    ([issue#15146](http://tracker.ceph.com/issues/15146),
    [pr#8137](http://github.com/ceph/ceph/pull/8137), Ken Dreyer)
-   rpm: rhel 5.9 librados compile fix, moved blkid to RBD
    check/compilation
    ([issue#13177](http://tracker.ceph.com/issues/13177),
    [pr#5954](http://github.com/ceph/ceph/pull/5954), Rohan Mars)
-   script: add missing stop_rgw variable to stop.sh script
    ([pr#7959](http://github.com/ceph/ceph/pull/7959), Karol Mroz)
-   scripts: adjust mstart and mstop script to run with cmake build
    ([pr#6920](http://github.com/ceph/ceph/pull/6920), Orit Wasserman)
-   scripts: release_notes can track original issue
    ([pr#6009](http://github.com/ceph/ceph/pull/6009), Abhishek
    Lekshmanan)
-   script: subscription-manager support
    ([issue#14972](http://tracker.ceph.com/issues/14972),
    [pr#7907](http://github.com/ceph/ceph/pull/7907), Loic Dachary)
-   selinux: allow log files to be located in /var/log/radosgw
    ([pr#7604](http://github.com/ceph/ceph/pull/7604), Boris Ranto)
-   selinux policy (Boris Ranto, Milan Broz)
-   selinux: Update policy to grant additional access
    ([issue#14870](http://tracker.ceph.com/issues/14870),
    [pr#7971](http://github.com/ceph/ceph/pull/7971), Boris Ranto)
-   set 128MB tcmalloc cache size by bytes
    ([pr#8427](http://github.com/ceph/ceph/pull/8427), Star Guo)
-   sstring.hh: return type from str_len(\...) need not be const
    ([pr#7679](http://github.com/ceph/ceph/pull/7679), Matt Benjamin)
-   stringify outputted error code and fix unmatched parentheses.
    ([pr#6998](http://github.com/ceph/ceph/pull/6998), xie.xingguo, xie
    xingguo)
-   Striper: reduce assemble_result log level
    ([pr#8426](http://github.com/ceph/ceph/pull/8426), Jason Dillaman)
-   submodules: revert an accidental change
    ([pr#7929](http://github.com/ceph/ceph/pull/7929), Yehuda Sadeh)
-   systemd: correctly escape block device paths
    ([issue#14706](http://tracker.ceph.com/issues/14706),
    [pr#7579](http://github.com/ceph/ceph/pull/7579), James Page)
-   systemd: drop any systemd imposed process/thread limits
    ([pr#8450](http://github.com/ceph/ceph/pull/8450), James Page)
-   systemd: fix typos
    ([pr#6679](http://github.com/ceph/ceph/pull/6679), Tobias Suckow)
-   systemd: logrotate fixes (Tim Serong, Lars Marowsky-Bree, Nathan
    Cutler)
-   systemd: many fixes (Sage Weil, Owen Synge, Boris Ranto, Dan van der
    Ster)
-   systemd: run daemons as user ceph
-   systemd: set up environment in rbdmap unit file
    ([issue#14984](http://tracker.ceph.com/issues/14984),
    [pr#8222](http://github.com/ceph/ceph/pull/8222), Nathan Cutler)
-   systemd: start/stop/restart ceph services by daemon type
    ([issue#13497](http://tracker.ceph.com/issues/13497),
    [pr#6276](http://github.com/ceph/ceph/pull/6276), Zhi Zhang)
-   sysvinit: allow custom cluster names
    ([pr#6732](http://github.com/ceph/ceph/pull/6732), Richard Chan)
-   sysvinit compat: misc fixes (Owen Synge)
-   test: add missing shut_down mock method
    ([pr#8125](http://github.com/ceph/ceph/pull/8125), Jason Dillaman)
-   test/bufferlist: Avoid false-positive tests
    ([pr#7955](http://github.com/ceph/ceph/pull/7955), Erwan Velu)
-   test: ceph_test_rados: use less CPU
    ([pr#7513](http://github.com/ceph/ceph/pull/7513), Samuel Just)
-   test/cli-integration/rbd: disable progress output
    ([issue#14931](http://tracker.ceph.com/issues/14931),
    [pr#7858](http://github.com/ceph/ceph/pull/7858), Josh Durgin)
-   test: correct librbd errors discovered with unoptimized cmake build
    ([pr#7914](http://github.com/ceph/ceph/pull/7914), Jason Dillaman)
-   test: create pools for rbd tests with different prefix
    ([pr#7738](http://github.com/ceph/ceph/pull/7738), Mykola Golub)
-   test: enable test for bug #2339 which has been resolved.
    ([pr#7743](http://github.com/ceph/ceph/pull/7743), You Ji)
-   test/encoding/readable.sh fix
    ([pr#6714](http://github.com/ceph/ceph/pull/6714), Igor Podoski)
-   Test exit values on test.sh, fix tier.cc
    ([issue#15165](http://tracker.ceph.com/issues/15165),
    [pr#8266](http://github.com/ceph/ceph/pull/8266), Samuel Just)
-   test: fix issues discovered via the rbd permissions test case
    ([pr#8129](http://github.com/ceph/ceph/pull/8129), Jason Dillaman)
-   test: fix osd-scrub-snaps.sh
    ([pr#6697](http://github.com/ceph/ceph/pull/6697), Xinze Chi)
-   test: Fix test to run with btrfs which has [snap]()\### dirs
    ([issue#15347](http://tracker.ceph.com/issues/15347),
    [pr#8420](http://github.com/ceph/ceph/pull/8420), David Zafman)
-   test: fixup and improvements for rbd-mirror test
    ([pr#8090](http://github.com/ceph/ceph/pull/8090), Mykola Golub)
-   test: fix ut test failure caused by lfn change
    ([issue#15464](http://tracker.ceph.com/issues/15464),
    [pr#8544](http://github.com/ceph/ceph/pull/8544), xie xingguo)
-   test: fix valgrind memcheck issues for rbd-mirror test cases
    ([issue#15354](http://tracker.ceph.com/issues/15354),
    [pr#8493](http://github.com/ceph/ceph/pull/8493), Jason Dillaman)
-   test: handle exception thrown from close during rbd lock test
    ([pr#8124](http://github.com/ceph/ceph/pull/8124), Jason Dillaman)
-   test/libcephfs/flock: add sys/file.h include for flock operations
    ([pr#6310](http://github.com/ceph/ceph/pull/6310), John Coyle)
-   test/librados/test.cc: clean up EC pools\' crush rules too
    ([issue#13878](http://tracker.ceph.com/issues/13878),
    [pr#6788](http://github.com/ceph/ceph/pull/6788), Loic Dachary, Dan
    Mick)
-   test/librbd/fsx: Use c++11 std::mt19937 generator instead of
    random_r() ([pr#6332](http://github.com/ceph/ceph/pull/6332), John
    Coyle)
-   test: misc fs test improvements (John Spray, Loic Dachary)
-   test/mon/osd-erasure-code-profile: pick new mon port
    ([pr#7161](http://github.com/ceph/ceph/pull/7161), Sage Weil)
-   test: more debug logging for TestWatchNotify
    ([pr#7737](http://github.com/ceph/ceph/pull/7737), Mykola Golub)
-   test: new librbd flatten test case
    ([pr#7609](http://github.com/ceph/ceph/pull/7609), Jason Dillaman)
-   test/osd: Relax the timing intervals in osd-markdown.sh
    ([pr#7899](http://github.com/ceph/ceph/pull/7899), Dan Mick)
-   test_pool_create.sh: put test files in the test dir so they are
    cleaned up ([pr#8219](http://github.com/ceph/ceph/pull/8219), Josh
    Durgin)
-   test/pybind/test_ceph_argparse: fix reweight-by-utilization tests
    ([pr#8027](http://github.com/ceph/ceph/pull/8027), Kefu Chai, Sage
    Weil)
-   test: python tests, linter cleanup (Alfredo Deza)
-   test/radosgw-admin: update the expected usage outputs
    ([pr#7723](http://github.com/ceph/ceph/pull/7723), Kefu Chai)
-   test: rbd-mirror: add \"switch to the next tag\" test
    ([pr#8149](http://github.com/ceph/ceph/pull/8149), Mykola Golub)
-   test: rbd-mirror: compare positions using all fields
    ([pr#8172](http://github.com/ceph/ceph/pull/8172), Mykola Golub)
-   test: rbd-mirror: script improvements for manual testing
    ([pr#8325](http://github.com/ceph/ceph/pull/8325), Mykola Golub)
-   test: reproducer for writeback CoW deadlock
    ([pr#8009](http://github.com/ceph/ceph/pull/8009), Jason Dillaman)
-   test/rgw: add multisite test for meta sync across periods
    ([pr#7887](http://github.com/ceph/ceph/pull/7887), Casey Bodley)
-   test_rgw_admin: use freopen for output redirection.
    ([pr#6303](http://github.com/ceph/ceph/pull/6303), John Coyle)
-   tests: add const for ec test
    ([pr#6911](http://github.com/ceph/ceph/pull/6911), Michal Jarzabek)
-   tests: add Ubuntu 16.04 xenial dockerfile
    ([pr#8519](http://github.com/ceph/ceph/pull/8519), Loic Dachary)
-   tests: allow docker-test.sh to run under root
    ([issue#13355](http://tracker.ceph.com/issues/13355),
    [pr#6173](http://github.com/ceph/ceph/pull/6173), Loic Dachary)
-   tests: allow object corpus readable test to skip specific incompat
    instances ([pr#6932](http://github.com/ceph/ceph/pull/6932), Igor
    Podoski)
-   tests: centos7 needs the Continuous Release (CR) Repository enabled
    for ([issue#13997](http://tracker.ceph.com/issues/13997),
    [pr#6842](http://github.com/ceph/ceph/pull/6842), Brad Hubbard)
-   tests: ceph-disk.sh: should use \"readlink -f\" instead
    ([pr#7594](http://github.com/ceph/ceph/pull/7594), Kefu Chai)
-   tests: ceph-disk.sh: use \"readlink -f\" instead for fullpath
    ([pr#7606](http://github.com/ceph/ceph/pull/7606), Kefu Chai)
-   tests: ceph-disk workunit uses configobj
    ([pr#6342](http://github.com/ceph/ceph/pull/6342), Loic Dachary)
-   tests: ceph-helpers assert success getting backfills
    ([pr#6699](http://github.com/ceph/ceph/pull/6699), Loic Dachary)
-   tests: ceph_test_keyvaluedb_iterators: fix broken test
    ([pr#6597](http://github.com/ceph/ceph/pull/6597), Haomai Wang)
-   tests: concatenate test_rados_test_tool from src and qa
    ([issue#13691](http://tracker.ceph.com/issues/13691),
    [pr#6464](http://github.com/ceph/ceph/pull/6464), Loic Dachary)
-   tests: configure with rocksdb by default
    ([issue#14220](http://tracker.ceph.com/issues/14220),
    [pr#7100](http://github.com/ceph/ceph/pull/7100), Loic Dachary)
-   tests: destroy testprofile before creating one
    ([issue#13664](http://tracker.ceph.com/issues/13664),
    [pr#6446](http://github.com/ceph/ceph/pull/6446), Loic Dachary)
-   tests: fix a few build warnings
    ([pr#7608](http://github.com/ceph/ceph/pull/7608), Sage Weil)
-   tests: fixes for rbd xstests (Douglas Fuller)
-   tests: fix failure for osd-scrub-snap.sh
    ([issue#13986](http://tracker.ceph.com/issues/13986),
    [pr#6890](http://github.com/ceph/ceph/pull/6890), Loic Dachary, Ning
    Yao)
-   tests: Fix for make check.
    ([pr#7102](http://github.com/ceph/ceph/pull/7102), David Zafman)
-   tests: Fixing broken test/cephtool-test-mon.sh test
    ([pr#8429](http://github.com/ceph/ceph/pull/8429), Erwan Velu)
-   tests: fix race condition testing auto scrub
    ([issue#13592](http://tracker.ceph.com/issues/13592),
    [pr#6724](http://github.com/ceph/ceph/pull/6724), Xinze Chi, Loic
    Dachary)
-   tests: fix test_rados_tools.sh rados lookup
    ([issue#13691](http://tracker.ceph.com/issues/13691),
    [pr#6502](http://github.com/ceph/ceph/pull/6502), Loic Dachary)
-   tests: fix tiering health checks (Loic Dachary)
-   tests: fix typo in TestClsRbd.snapshots test case
    ([issue#13727](http://tracker.ceph.com/issues/13727),
    [pr#6504](http://github.com/ceph/ceph/pull/6504), Jason Dillaman)
-   tests: flush op work queue prior to destroying MockImageCtx
    ([issue#14092](http://tracker.ceph.com/issues/14092),
    [pr#7002](http://github.com/ceph/ceph/pull/7002), Jason Dillaman)
-   tests for low-level performance (Haomai Wang)
-   tests: ignore test-suite.log
    ([pr#6584](http://github.com/ceph/ceph/pull/6584), Loic Dachary)
-   tests: Improving \'make check\' execution time
    ([pr#8131](http://github.com/ceph/ceph/pull/8131), Erwan Velu)
-   tests: many ec non-regression improvements (Loic Dachary)
-   tests: many many ec test improvements (Loic Dachary)
-   tests: notification slave needs to wait for master
    ([issue#13810](http://tracker.ceph.com/issues/13810),
    [pr#7220](http://github.com/ceph/ceph/pull/7220), Jason Dillaman)
-   tests: \--osd-scrub-load-threshold=2000 for more consistency
    ([issue#14027](http://tracker.ceph.com/issues/14027),
    [pr#6871](http://github.com/ceph/ceph/pull/6871), Loic Dachary)
-   tests: osd-scrub-snaps.sh to display full osd logs on error
    ([issue#13986](http://tracker.ceph.com/issues/13986),
    [pr#6857](http://github.com/ceph/ceph/pull/6857), Loic Dachary)
-   tests: port uniqueness reminder
    ([pr#6387](http://github.com/ceph/ceph/pull/6387), Loic Dachary)
-   tests: restore run-cli-tests
    ([pr#6571](http://github.com/ceph/ceph/pull/6571), Loic Dachary,
    Sage Weil, Jason Dillaman)
-   tests: snap rename and rebuild object map in client update test
    ([pr#7224](http://github.com/ceph/ceph/pull/7224), Jason Dillaman)
-   tests: sync ceph-erasure-code-corpus for mktemp -d
    ([pr#7596](http://github.com/ceph/ceph/pull/7596), Loic Dachary)
-   tests: test/librados/test.cc must create profile
    ([issue#13664](http://tracker.ceph.com/issues/13664),
    [pr#6452](http://github.com/ceph/ceph/pull/6452), Loic Dachary)
-   tests: test_pidfile.sh lingering processes
    ([issue#14834](http://tracker.ceph.com/issues/14834),
    [pr#7734](http://github.com/ceph/ceph/pull/7734), Loic Dachary)
-   tests: unittest_bufferlist: fix hexdump test
    ([pr#7152](http://github.com/ceph/ceph/pull/7152), Sage Weil)
-   tests: unittest_ipaddr: fix segv
    ([pr#7154](http://github.com/ceph/ceph/pull/7154), Sage Weil)
-   test/system/rados_list_parallel: print oid if rados_write fails
    ([issue#15240](http://tracker.ceph.com/issues/15240),
    [pr#8309](http://github.com/ceph/ceph/pull/8309), Kefu Chai)
-   test/system/\*: use dynamically generated pool name
    ([issue#15240](http://tracker.ceph.com/issues/15240),
    [pr#8318](http://github.com/ceph/ceph/pull/8318), Kefu Chai)
-   test/test-erasure-code.sh: disable pg_temp priming
    ([issue#15211](http://tracker.ceph.com/issues/15211),
    [pr#8260](http://github.com/ceph/ceph/pull/8260), Sage Weil)
-   test: TestMirroringWatcher test cases were not closing images
    ([pr#8435](http://github.com/ceph/ceph/pull/8435), Jason Dillaman)
-   test/TestPGLog: fix the FTBFS
    ([issue#14930](http://tracker.ceph.com/issues/14930),
    [pr#7855](http://github.com/ceph/ceph/pull/7855), Kefu Chai)
-   test/test_pool_create.sh: fix port
    ([pr#8361](http://github.com/ceph/ceph/pull/8361), Sage Weil)
-   test/time: no need to abs(uint64_t) for comparing
    ([pr#7726](http://github.com/ceph/ceph/pull/7726), Kefu Chai)
-   test: update rbd integration cram tests for new default features
    ([pr#8001](http://github.com/ceph/ceph/pull/8001), Jason Dillaman)
-   test: use sequential journal_tid for object cacher test
    ([issue#13877](http://tracker.ceph.com/issues/13877),
    [pr#6710](http://github.com/ceph/ceph/pull/6710), Josh Durgin)
-   tools: add cephfs-table-tool \'take_inos\'
    ([pr#6655](http://github.com/ceph/ceph/pull/6655), John Spray)
-   tools/cephfs: add tmap_upgrade
    ([pr#7003](http://github.com/ceph/ceph/pull/7003), John Spray)
-   tools/cephfs: fix overflow writing header to fixed size buffer
    (#13816) ([pr#6617](http://github.com/ceph/ceph/pull/6617), John
    Spray)
-   tools/cephfs: fix tmap_upgrade
    ([issue#15135](http://tracker.ceph.com/issues/15135),
    [pr#8128](http://github.com/ceph/ceph/pull/8128), John Spray)
-   tools: ceph_monstore_tool: add inflate-pgmap command
    ([issue#14217](http://tracker.ceph.com/issues/14217),
    [pr#7097](http://github.com/ceph/ceph/pull/7097), Kefu Chai)
-   tools: ceph-monstore-update-crush: add \"\--test\" when testing
    crushmap ([pr#6418](http://github.com/ceph/ceph/pull/6418), Kefu
    Chai)
-   tools: Fix layout handing in cephfs-data-scan (#13898)
    ([pr#6719](http://github.com/ceph/ceph/pull/6719), John Spray)
-   tools: monstore: add \'show-versions\' command.
    ([pr#7073](http://github.com/ceph/ceph/pull/7073), Cilang Zhao)
-   tools/rados: reduce \"rados put\" memory usage by op_size
    ([pr#7928](http://github.com/ceph/ceph/pull/7928), Piotr Dałek)
-   tools:remove duplicate references
    ([pr#5917](http://github.com/ceph/ceph/pull/5917), Bo Cai)
-   tools: support printing part cluster map in readable fashion
    ([issue#13079](http://tracker.ceph.com/issues/13079),
    [pr#5921](http://github.com/ceph/ceph/pull/5921), Bo Cai)
-   unittest_compression_zlib: do not assume buffer will be null
    terminated ([pr#8064](http://github.com/ceph/ceph/pull/8064), Sage
    Weil)
-   unittest_erasure_code_plugin: fix deadlock (Alpine)
    ([pr#8314](http://github.com/ceph/ceph/pull/8314), John Coyle)
-   unittest_osdmap: default crush tunables now firefly
    ([pr#8098](http://github.com/ceph/ceph/pull/8098), Sage Weil)
-   upstart: throttle restarts (#11798 Sage Weil, Greg Farnum)
-   vstart: fix up cmake paths when VSTART_DEST is given
    ([pr#8363](http://github.com/ceph/ceph/pull/8363), Casey Bodley)
-   vstart: grant full access to Swift testing account
    ([pr#6239](http://github.com/ceph/ceph/pull/6239), Yuan Zhou)
-   vstart: make -k with optional mon_num.
    ([pr#8251](http://github.com/ceph/ceph/pull/8251), Jianpeng Ma)
-   vstart: set cephfs root uid/gid to caller
    ([pr#6255](http://github.com/ceph/ceph/pull/6255), John Spray)
-   vstart.sh: add mstart, mstop, mrun wrappers for running multiple
    vstart-style test clusters out of src tree
    ([pr#6901](http://github.com/ceph/ceph/pull/6901), Yehuda Sadeh)
-   vstart.sh: avoid race condition starting rgw via vstart.sh
    ([issue#14829](http://tracker.ceph.com/issues/14829),
    [pr#7727](http://github.com/ceph/ceph/pull/7727), Javier M. Mellid)
-   vstart.sh: silence a harmless msg where btrfs is not found
    ([pr#7640](http://github.com/ceph/ceph/pull/7640), Patrick Donnelly)
-   xio: add prefix to xio msgr logs
    ([pr#8148](http://github.com/ceph/ceph/pull/8148), Roi Dayan)
-   xio: fix compilation against latest accelio
    ([pr#8022](http://github.com/ceph/ceph/pull/8022), Roi Dayan)
-   xio: fix incorrect ip being assigned in case of multiple RDMA ports
    ([pr#7747](http://github.com/ceph/ceph/pull/7747), Subramanyam
    Varanasi)
-   xio: remove duplicate assignment of peer addr
    ([pr#8025](http://github.com/ceph/ceph/pull/8025), Roi Dayan)
-   xio: remove redundant magic methods
    ([pr#7773](http://github.com/ceph/ceph/pull/7773), Roi Dayan)
-   xio: remove unused variable
    ([pr#8023](http://github.com/ceph/ceph/pull/8023), Roi Dayan)
-   xio: xio_init needs to be called before any other xio function
    ([pr#8227](http://github.com/ceph/ceph/pull/8227), Roi Dayan)
-   xxhash: use clone of xxhash.git; add .gitignore
    ([pr#7986](http://github.com/ceph/ceph/pull/7986), Sage Weil)
