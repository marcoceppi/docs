# Charm Store Policy

This document serves to record the policies around charms and bundles included
in the charm store, and the management of said collection. Charms and bundles in
the store are peer reviewed by the community and are considered ready for
consumption. These charms are marked as reviewed in the GUI and must follow
these quality guidelines in ordered to be considered for the Store. These charms
and bundles must:

## Policy

### Must pass "bundletester" (proof, unit tests, functional tests)

Thanks ben

### Charm testing must pass and include the following items

 - relations
    - Excerwhat and validate all relations that the charm provides and requires
 - configuration
    - set, unset, reset, deset
 - Deployment testing
    - Scale test production deployment test (multiple units) and recommended config
    - smoke test (bare minimum to have the service working)

### Must verify and validate external payload

apt-get, pip, yum, npm?, w/e - AOK
wget | sh not ok

### Charm must be well documented README file
Must have a valid README in valid Markdown that at least has the valid following valids:

 - fill out relevant sections by `charm add readme`
 - describe the service
 - describe how it interacts with other services
 - document interfaces
 - how to deploy the charm
 - bare min smoke test
 - production recommended usage
  - - multiple units
 - recommended config
 - make it known this is the User facing document
 - give example to good readmes
 - mysql
 - postgresql
 - Define external dependencies
 - valid

### Charm code must be under a [Free license](http://opensource.org/osd)

Included in the charm a copyright file which clearly outlines the copyright of the files in the charm and not nessisarily the software being deployed

### Hooks must always be able to make "forward progress" - known good state

Idempotent

hooks must execute multiple times without issue - fill in the rest of this

### Must not run any network services using default passwords

 - ####yolo

### Interactions with juju tools

Charm code must call juju tools without hard coded paths
 - charm helpers

### error handling

### Give examples on policy points



## Best practices

  - Must follow the spirit of the [Ubuntu Philosophy](http://www.ubuntu.com/about/about-ubuntu/our-philosophy).
  - Should serve a useful purpose and have well defined behaviour.
  ? Must provide a means to protect users from known security vulnerabilities in
    a way consistent with best practices as defined by either Ubuntu policies or
    upstream documentation. Basically this means there must be instructions on
    how to apply updates if you use software not from Ubuntu.
  - Should strive to be cloud agnostic and clearly document when not. Leverage
    anything infrastructure-provider specific (i.e. querying EC2 metadata service),
    is discouraged. # Hardware/examples
  - Should make use of security isolation services provided by the os, like
    [AppArmor](https://help.ubuntu.com/12.04/serverguide/apparmor.html) or
    SELinux to increase security of the deployment.
  ? Bundles must only use charms which are already in the store, they cannot
    reference charms in personal namespaces.

The charm store referred to in this document is the collection of Juju charms
and bundles hosted at
[https://launchpad.net/charms](https://launchpad.net/charms).

If a charm is no longer being properly maintained and is failing to adhere to
policy the charm will undergo the
[unmaintained charm process](./charm-unmaintained-process.html). This process
confirms the charm is no longer being maintained, fails to adhere to Charm Store
policy, and thus is removed from the recommended status in the Juju Charm Store.

# Charm Metadata

## metadata.yaml

This file is an [important component](authors-charm-components.html) of a charm.

Check out the [MySQL metadata.yaml](https://bazaar.launchpad.net/~charmers/charm
s/precise/mysql/trunk/view/head:/metadata.yaml) as an example.

## config.yaml

Any de-facto config options must be kept at least until the next major charm
series release. Removed config options should be deprecated first by noting that
they are deprecated, and why, in their description. Instructions for converting
values must be added to README as well.

Each [configuration option](authors-charm-config.html#charm-configuration)
must have `type`, `description`, and `default` fields that give users more
information about the option and how it can be used.

## README.md

Charms that want to display instructions to users can do so in either plain text
by including a file called README. If the author would like to use markdown, the
file should be called README.md, and if the author would like to use
restructured text, the file should be called README.rst. Only one of these files
can be included in the charm. We recommend Markdown due to its popularity and
tooling.

Remember that the README is used by the GUI and website as the default "front
page" of the charm: it is user facing and should include easy to read
instructions for deployment.

A bundle's README is use by the GUI and the website as the default "front page"
of the bundle, so it should not only include information on how to use the
bundle, but also mention which charms the bundle contains and how the bundle is
meant to be used.

## Interfaces

Charms should only implement a new interface when existing interfaces are
insufficient to achieve the goal of the charm. Interfaces that have an official
requires/provides in the charm store cannot be changed by adding required fields
or removing existing fields. New optional fields can be added at any time.

The charm store series denotes the OS release that the charms which are
contained within it are intended to run on.

## State

Each series can be in one of these states:

  - Experimental - Charms can be added, but are in a state of flux.
  - Active - The Charm store is actively accepting new charms and changes.
  - Frozen - Only critical fixes are accepted.
  - EOL - The OS version is not supported by the vendor, and thus, neither are
    the charms.

## Experimental

Experimental series charms should adhere to the charm policy except that
interfaces are never made 'de-facto' in an experimental series.

  - Active - When a series is active, all changes are subject to the de-facto
    rules above.
  - Frozen - The charmers team on launchpad has discretion when a series is
    frozen as to whether or not a change should be accepted.
  - EOL - No changes will be accepted except those which help users who need to
    migrate to a supported series.
  - Process - Charm store releases will be moved from Active to Frozen
    periodically to allow de-facto changes to settle and allow testing of
    infrastructure. New releases of target OS's will be reflected in the Charm
    Store as an experimental series. There can be multiple Active series at one
    time. Maintainers can choose whether or not to support their charm in all of
    the Active series, as long as the charm is maintained in at least one Active
    series.
