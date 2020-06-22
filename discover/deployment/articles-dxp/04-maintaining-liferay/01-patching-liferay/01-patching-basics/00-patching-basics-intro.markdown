---
header-id: patching-basics
---

# Patching Basics

[TOC levels=1-4]

<aside class="alert alert-info">
  <span class="wysiwyg-color-blue120">This document has been updated and ported to <a href="https://learn.liferay.com/dxp/7.x/en/installation-and-upgrades/maintaining-a-liferay-dxp-installation/patching-liferay/understanding-patch-types.html">Liferay Learn</a> and is no longer maintained here.</span>
</aside>

Liferay ships @product-ver@ fixes through three different channels: 

- Fix packs 
- Hotfixes 
- Service Packs 

## Fix Packs

On a regular schedule, the latest fixes that patch the core are bundled together
into fix packs that are provided to all of Liferay's customers. Fix packs
include fixes for both the core and the application suites that ship with the
product. Each fix pack contains all previous fix packs since the last
service pack. 

[Security Fix Packs](https://help.liferay.com/hc/en-us/articles/360035038331) 
are a special fix pack type for deploying critical security fixes quickly
without changing fix pack levels. 

## Hotfixes

A hotfix is provided to customers when they contact Liferay about an emergency
situation, and Liferay's support team--working with the customer-- determines
that the problem is an issue with the product that needs to be fixed very
quickly. Support fixes the bug and provides a hotfix to the customer
immediately. This is a short-term fix Hotfixes can patch both the core and the
application suites.

## Service Packs

Service packs are built on the top of the original @product@ release and
repackaged with the latest fix pack, Patching Tool and modules. Since a service
pack contains the latest fix pack, it contains all previous fix packs since the
last service pack. If starting a new project, always start with the latest
service pack. 

Rather than use the service packs to keep existing systems updated, existing
customers should

1. Keep their systems up-to-date with fix packs (according to their own
   deployment schedules).

2. Install the latest Marketplace updates frequently.

3. Update the Patching Tool when necessary.

This method updates the installation to the service pack levels, while allowing
scheduled deployments and preventing full environment rebuilds. 

## How Patches are Tested

Liferay extensively tests all three types of fix packs to ensure high quality.
For each issue fixed, fix packs go through both automated regression
testing and manual testing. Hotfixes receive similar automated testing, and the
fix for the reported issue is tested by the support engineer who fixed it.

Before releasing a service pack, test suites run on the packaged releases to
ensure the quality of the packaging.
