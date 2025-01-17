APPUiO Public Platform Specifics
================================

APPUiO is based on OpenShift Container Platform. This page describes APPUiO
specific OpenShift configuration settings as well as features which
were added to APPUiO that are not present in OpenShift.

Versions
--------

- Operating System: Red Hat Enterprise Linux (RHEL) 7
- OpenShift Container Platform: 3.9
- Docker: 1.13.1

You can download matching clients directly from APPUiO: :doc:`getting-started`.

URLs and Domains
----------------

- Master URL: https://console.appuio.ch/
- Metrics URL: https://metrics.appuio.ch/
- Logging URL: https://logging.appuio.ch/
- Application Domain: ``appuioapp.ch``

Persistent Storage
------------------

APPUiO currently uses GlusterFS based persistent storage. For now
volumes with the following sizes are available out of the box:

* 1 GiB
* 5 GiB

However you can contact us to get larger volumes: `Contact <http://appuio.ch/#contact>`__.
All volumes can be accessed with ReadWriteOnce (RWO) and ReadWriteMany (RWX)
access modes. Please see `Persistent Volumes 
<https://docs.openshift.com/container-platform/3.9/dev_guide/persistent_volumes.html>`__
for more information.

Quotas and Limits
-----------------

The quotas are defined in the project size you ordered. The exact numbers can be found
on the product site `APPUiO Public Platform <https://appuio.ch/public.html>`__

Secure Docker Builds
--------------------

Usually Docker builds from ``Dockerfile`` have to be disabled on multi-tenant platforms for
security reasons. However, APPUiO uses it's own implementation to securely run Docker builds
in dedicated VMs: :ref:`appuio_docker_builder`

Let's Encrypt Integration
-------------------------

Let's Encrypt is a certificate authority that provides free SSL/TLS certificates which are accepted by most of todays browser via an automated process. APPUiO provides integration with Let's Encrypt to automatically create, sign, install and renew certificates for your Domains running on APPUiO: :doc:`letsencrypt-integration`

Email Gateway
-------------

To send emails to external entities, you should SMTP relay via the email gateway at ``mxout.appuio.ch``.

To include the APPUiO email gateway in your existing SPF policy, you can include or redirect to ``spf.appuio.ch``.

Example DNS record::

    @ IN TXT "v=spf1 ... include:spf.appuio.ch ~all"

Or if you send emails for your domain exclusivly from appuio::

    @ IN TXT "v=spf1 redirect=spf.appuio.ch"
