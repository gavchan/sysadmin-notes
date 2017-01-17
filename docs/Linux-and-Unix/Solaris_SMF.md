[Basics of Service Management Facility (SMF) on Oracle Solaris 11](http://www.oracle.com/technetwork/articles/servers-storage-admin/intro-smf-basics-s11-1729181.html)

- A software framework that manages the services on a system.
- Each service has a well-defined state and a relationship to other dependent services.
- Ability to run multiple instanes of a given service and share common configuration.
- Configuration repository managed by `svc.configd`
- Each service described using a Fault Management Reousrce Indicator (FMRI)
- SMF framework always active on Oracle Solaris 11 - started and restarted through the default init process.

Command line:
```
svcadm
svcs
svcs -a    # Lists additional new service instances.
```
