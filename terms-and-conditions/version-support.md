---

copyright:

  years: 2015, 2019

lastupdated: "2019-11-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Update Policy and Supported Versions in {{site.data.keyword.cfee_full_notm}}
{: #update-policy-supported-versions}

This document describes the update policy and supported versions for the {{site.data.keyword.cfee_full}} service.

We recommend that users keep their {{site.data.keyword.cfee_full_notm}} service instances updated to the latest version to receive the latest capabilities and fixes.  For detailed instructions on how to update your instance, please see the instructions [here](cloud-foundry?topic=cloud-foundry-update-scale).

During an update, some metrics normally shown in the _Overview_, _Resource Usage_, and _Update and Scaling_ pages may not be available.
{: note}

## Version Support Policy
{: #version-support-policy}

### Definitions of Terms
{: #definitions-of-terms}
This document refers to certain terms with specific meanings.  We define those terms here:

A **release** refers to a specific build of the {{site.data.keyword.cfee_short}} service as delivered to customers.  Releases are made available as content changes dictate.  Every release has a specific _version_ as defined in the next paragraph.

A **version** can mean two things.  It most commonly refers to the [semver](https://semver.org) tag specific to each release.  The format of these tags is described in the [section on Versioning](cloud-foundry?topic=cloud-foundry-update-policy-supported-versions#versioning).  No two releases share the same version tag.

A **version** can also refer to a specific element of the overall version tag, be it the major, minor, or patch version level.  These terms are also defined in the [section on Versioning](cloud-foundry?topic=cloud-foundry-update-policy-supported-versions#versioning).

### {{site.data.keyword.cfee_short}} Versioning
{: #versioning}
New releases of the {{site.data.keyword.cfee_full_notm}} service are delivered on an ongoing basis.  The service follows [standard semantic versioning](https://semver.org) with the format _**Major.Minor.Patch**_.

The _major_ version is incremented only when CFEE adopts a new release of Cloud Foundry itself.  The [release notes](cloud-foundry?topic=cloud-foundry-what-s-new-in-ibm-cloud-foundry-enterprise-environment) for each new major version list the packaged Cloud Foundry release and contain a link to the Cloud Foundry-specific release notes.  While these updates do not follow a fixed or regular schedule (the service adopts new versions of Cloud Foundry as appopriate or required to pick up important new capabilities or fixes), the service releases a new major version approximately quarterly.

Within a given major version, all subsequent minor and patch versions can be assumed to have the same level of packaged Cloud Foundry and can also be assumed to be compatible with the same level of the Cloud Foundry CLI.

The _minor_ version is incremented when CFEE releases important capabilities which do not require updating the packaged Cloud Foundry release.  As with updates to the major version, the service publishes release notes for each new minor version.  These release notes will include descriptions of any new capabilities and/or limitations, as well as of any issues resolved by the new release.

The _patch_ version is incremented when the only change to the release is for bug or security fixes.  As with updates to the major and minor versions, the service publishes release notes for each new patch release describing the issue(s) resolved and any important considerations for adopters.

### {{site.data.keyword.cfee_short}} Provisioning
{: provisioning}
The {{site.data.keyword.cfee_full_notm}} service only supports provisioning new instances of the latest released version.  An easy way to see what the current version used for provisioning is to execute:

```
curl https://releases.cfaas.cloud.ibm.com/v1/releases/current
```
{: codeblock}

This is a public API which always returns the current version and includes the bill of materials for the included packages.

### {{site.data.keyword.cfee_short}} Updates and Support
{: #update-support}
{{site.data.keyword.cfee_full_notm}} supports releases on an _N-2_ basis.  This means that we support the latest release within the current, _N-1_, and _N-2_ major versions.  Patches and updates are only released for those releases.

For example, if the current release is _6.2_, and a security fix is required, it will only be published as a _6.2.1_ release.  There would no patch release for _6.0_ or _6.1_.

The update policy works similarly.  If the current release is _6.2_, and the latest 4.x release is _4.3_, users at _4.2.x_ or earlier would not be eligible to update to _6.2_.  Those users must attempt to update to _4.3_ first in order to stay within the supported update window.  

For this reason, it is _critical_ that users update their instances to stay within the _N-2_ support window.  We cannot commit to supporting attempts to update older releases, unfortunately, and users electing not to update do so at their own risk.
{: important}

### {{site.data.keyword.cfee_short}} Dependencies
{: #dependencies}
{{site.data.keyword.cfee_full_notm}} releases include specific versions of vendored dependencies, notably the IBM Kubernetes Service.  This means that your CFEE instance is provisioned using a specific kubernetes version, and CFEE updates will, from time to time, result in an update to the kubernetes version of the underlying cluster as well.

Performing manual kubernetes updates on the underlying kubernetes cluster is specifically not supported and may result in the CFEE instance being rendered non-functional due to incompatibilities with kubernetes versions not supported by CFEE.  As there is no way to revert a kubernetes update, users are warned in the strongest possible terms _not to update the kubernetes cluster directly unless specifically advised to do so by CFEE product support_.  We cannot provide support for instances on which the customer has performed a manual kubernetes update.
{: important}
