# Release checklists

## Dev Kickoff

These steps should be taken when starting a new major release, just
after the previous release has been tagged (vX.2.0) and that tag has
been merged back into master.

X is the release we are just starting development on. X-1 is the one
that was just released (X-1).2.0.

### Versions and tags

-   \[x\] Update CMakeLists.txt VERSION (right at the top to X.0.0)

-   \[x\] Update src/librbd/CMakeLists.txt VERSION (librbd target at the
    bottom to 1.X.0)

-   \[x\] Update src/ceph_release with the new release name, number, and
    type (\'dev\')

-   

    \[ \] Initial tag vX.0.0 (so that we can distinguish from (and sort

    :   after) the backported (X-1).2.Z versions.

\### Notes on tagging \* Tags must be annonated as CMake determines
[CEPH_GIT_NICE_VER]{.title-ref} by calling [git describe
\--always]{.title-ref}. \* vX.0.0 are special ones in the sense they are
pushed manually (unlike v.X.2.n which are handled by Jenkins). \* vX.0.0
should point to a commit before the first one in a kickoff branch.

### Define release names and constants

Make sure X (and, ideally, X+1) is defined:

-   \[x\] src/common/ceph_releases.h ([ceph_release_t]{.title-ref})
-   \[x\] src/common/ceph_strings.cc ([ceph_release_name()]{.title-ref})
-   \[x\] src/include/rados.h ([CEPH_RELEASE\_\*]{.title-ref} and
    [MAX]{.title-ref})
-   \[x\] src/include/rbd/librbd.h ([LIBRBD_VER_MINOR]{.title-ref} to X)
-   \[x\] src/mon/mon_types.h
    ([ceph::features::mon::FEATURE\_\*]{.title-ref} and related structs
    and helpers; note that monmaptool CLI test output will need
    adjustment)
-   \[x\] src/mds/cephfs_features.h
    ([CEPHFS_CURRENT_RELEASE]{.title-ref})

#### Scripts

-   \[x\] src/script/backport-resolve-issue ([releases()]{.title-ref},
    [ver_to_release()]{.title-ref}\... but for X-1)
-   \[x\] src/script/ceph-release-notes (X-1)
-   \[ \] ceph-build.git scripts/build_utils.sh
    [release_from_version()]{.title-ref}

#### Misc

-   \[x\] update src/ceph-volume/ceph_volume/\_\_init\_\_.py
    ([\_\_release\_\_]{.title-ref})
-   \[x\] update src/tools/monmaptool.cc ([min_mon_release]{.title-ref}
    and corresponding output in [src/test/cli/monmaptool]{.title-ref})
-   \[x\] update src/cephadm/cephadmlib/constants.py
    ([DEFAULT_IMAGE_RELEASE]{.title-ref} to X)

### Feature bits

-   \[x\] ensure that [SERVER_X]{.title-ref} is defined
-   \[x\] change any features [DEPRECATED]{.title-ref} in release X-3
    are now marked [RETIRED]{.title-ref}.
-   \[ \] look for features that (1) were present in X-2 and (2) have no
    client dependency and mark them [DEPRECATED]{.title-ref} as of X.

### Compatsets

-   \[x\] mon/Monitor.h ([CEPH_MON_FEATURE_INCOMPAT_X]{.title-ref})
-   \[x\] mon/Monitor.cc (include in
    [get_supported_features()]{.title-ref})
-   \[x\] mon/Monitor.cc
    ([apply_monmap_to_compatset_features()]{.title-ref})
-   \[x\] mon/Monitor.cc ([calc_quorum_requirements()]{.title-ref})
-   \[x\] test/cli/monmaptool/feature-set-unset-list.t
    ([supported]{.title-ref}, [persistent]{.title-ref})

### Mon

-   \[x\] qa/standalone/mon/misc adjust [TEST_mon_features]{.title-ref}
    (add X cases and adjust [\--mon-debug-no-require-X]{.title-ref})
-   \[x\] qa/standalone/mon/misc bump up
    [jqfilter=\'.monmap.features.persistent \| length ==
    N\']{.title-ref} to [N+1]{.title-ref}
-   \[x\] mon/MgrMonitor.cc adjust [always_on_modules]{.title-ref}
-   \[x\] common/options/global.yaml.in define
    [mon_debug_no_require_X]{.title-ref}
-   \[x\] common/options/global.yaml.in remove
    [mon_debug_no_require_X-2]{.title-ref}
-   \[x\] mon/OSDMonitor.cc \`create_initial\`: adjust new
    [require_osd_release]{.title-ref}, and add associated
    [mon_debug_no_require_X]{.title-ref}
-   \[x\] mon/OSDMonitor.cc \`preprocess_boot\`: adjust \"disallow boot
    of \" condition to disallow X if [require_osd_release]{.title-ref}
    \< X-2.
-   \[x\] mon/OSDMonitor.cc: adjust \"osd require-osd-release\" to (1)
    allow setting X, and (2) check that all mons *and* OSDs have X
-   \[x\] mon/MonCommands.h: adjust \"osd require-osd-release\" allows
    options to include X
-   \[x\] qa/workunits/cephtool/test.sh: adjust
    [require-osd-release]{.title-ref} test

### OSDMap

-   \[x\] src/osd/OSDMap.cc add release name mapping for
    [SERVER_X]{.title-ref} in
    [pending_require_osd_release()]{.title-ref}

### Code cleanup

-   \[ \] search code for \"after X-1\" or \"X\" for conditional checks
-   \[ \] search code for X-2 and X-3
    ([CEPH_FEATURE_SERVER\_\*]{.title-ref} and
    [ceph_release_t::\*]{.title-ref})
-   \[ \] search code for [require_osd_release]{.title-ref}
-   \[ \] search code for [min_mon_release]{.title-ref}
-   \[ \] check include/denc.h if DENC_START macro still needs reference
    to squid

### QA suite

-   \[x\] create qa/workunits/[test_telemetry]()(X-1).sh
-   \[x\] create qa/workunits/[test_telemetry]()(X-1)\_x.sh
-   \[x\] create qa/suites/upgrade/(X-1)-x
-   \[x\] remove qa/suites/upgrade/(X-3)-x-\*
-   \[x\] create qa/releases/X.yaml
-   \[x\] create qa/suites/rados/thrash-old-clients/1-install/(X-1).yaml

### ceph-build

In the [ceph/ceph-build.git]{.title-ref} repo:

-   \[x\] add the version -\> X mapping
    ([release_from_version()]{.title-ref} in
    [scripts/build_utils.sh]{.title-ref})
-   \[x\] add the option for X ([case \$RELEASE_BRANCH]{.title-ref} in
    [ceph-dev-build/build/build_osc]{.title-ref})
-   \[x\] add the option for X ([case \$RELEASE_BRANCH]{.title-ref} in
    [ceph-dev-build/build/setup_osc]{.title-ref})
-   \[x\] grep for previous release and add relevant build targets (e.g.
    for reef <https://github.com/ceph/ceph-build/pull/2076> and
    <https://github.com/ceph/ceph-build/pull/2119>)

### ceph-container

In the [ceph/ceph-container.git]{.title-ref} repo:

-   \[x\] Add the release name to [Makefile]{.title-ref}
-   \[x\] Update
    [ceph-releases/ALL/centos/daemon-base/\_\_DOCKERFILE_INSTALL\_\_]{.title-ref}
    with the with the supported nfs-ganesha version
-   \[x\] Update [contrib/build-push-ceph-container-imgs.sh]{.title-ref}
    with the new release
-   \[x\] Update [contrib/ceph-build-config.sh]{.title-ref} with the
    release name
-   \[x\] Update [contrib/common.sh]{.title-ref} with supported version
    numbers
-   \[x\] Update [maint-lib/ceph_version.sh]{.title-ref} with the
    release name

See <https://github.com/ceph/ceph-container/pull/2109> as an example for
what to do.

## After dev freeze

-   \[ \] create branch for new release
-   \[ \] remove `doc/releases/*.rst`. This should leave behind
    `doc/releases/releases.yml` which is used for doc building purposes.
    See also commit 33d63c3 (\"doc: remove release notes for release
    branch\") for details.
-   \[ \] cherry-pick 8cf9ad62949516666ad0f2c0bb7726ef68e4d666 (\"doc:
    add releases links to toc\"). There will be trivial conflicts.
-   \[ \] add redirect for new major release at
    [RTD](https://readthedocs.org/dashboard/ceph/redirects/).
-   \[ \] add release name to redmine (using
    <https://tracker.ceph.com/custom_fields/16/edit>)
-   \[ \] add release name to .github/milestone.yml for github actions
    to automatically add milestone to backports (this commit must be
    backported to the release branch)

## First release candidate

-   \[ \] src/ceph_release: change type to [rc]{.title-ref}
-   \[ \] opt-in to all telemetry channels, generate telemetry reports,
    and verify no sensitive details (like pools names) are collected
-   \[ \] check if new pool flags exist in pg_pool_t (osd/osd_types.h),
    and add them to telemetry\'s basic_pool_flags collection, in case
    they are not sensitive

## First stable release

-   \[ \] src/ceph_release: change type [stable]{.title-ref}
-   \[ \] generate new object corpus for encoding/decoding tests - see
    `corpus`{.interpreted-text role="doc"}
-   \[ \] src/cephadm/cephadmlib/constants.py: update
    [LATEST_STABLE_RELEASE]{.title-ref}
