# Sirepo Health Check

This is Sirepo health check utility. It checks the availability of the light page of the specified servers (currently 2 local NSLS-II servers and RadiaSoft's alpha/beta servers. It creates a `.json` status file (stored in `/tmp`, via a crontab job, see the [crontab](crontab) file for details). On the first start the utility checks the current statuses of the machines and sends a notification to the specified addresses like:

```
On 9/6/2017 17:15, Sirepo Health Check wrote:
Monitoring started for:
- https://expdev.nsls2.bnl.gov/light (up)
- http://nsls2expdev1.bnl.gov:8000/light (up)
- https://alpha.sirepo.com/light (up)
- https://beta.sirepo.com/light (up)
```

If any status changes, it sends the corresponding notification like:
```
http://nsls2expdev1.bnl.gov:8000/light: status changed: up -> down (2017-09-06 17:30:02)
```

When the server is back, it sends the confirmation:
```
http://nsls2expdev1.bnl.gov:8000/light: status changed: down -> up (2017-09-06 17:35:02)
```

The crontab job runs every 5 minutes on weekdays from 8 am to 7:55 pm. If the machine is not restored, a reminder email will be sent in 2 hours after the last notification.
