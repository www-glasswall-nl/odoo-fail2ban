# odoo-fail2ban
# 15 apr 2019 - initial config done by Jan van de Rijt.

[Fail2Ban Odoo ruleset]
In order to use fail2ban to protect Odoo Glasswall has provided some rules to achieve that purpose.
There are 4 files included with the defined regex to provide the fail2ban jail the rules.

2 files are included for the default odoo log and 2 files if you chose to log odoo to syslog (preferred).
The add_to_jail.local are the actual rule settings.

[Installation]
Install fail2ban.
enable "syslog = true" in the odoo-server.conf and restart odoo (preferred but not necessary).
copy the odoo*.conf files to the /etc/fail2ban/filter.d/ directory.
append the rules add_to_jail.local to the /etc/fail2ban/jail.local file, if there is no jail.local file you can append them to the jail.conf.
restart fail2ban and the rules are aplied.

[Note]
The default Odoo installation logs to odoo-server.log, the time standard used in this log is UTC the time fail2ban uses is the system time (in my case CET).
To overcome this time issue i added 7200 secconds (2+hours included daylight saving) to the bantime in the rules file.
Changing the Odoo setting to use the syslog as logging file then the actual systemtime is used and you can use fail2ban without additional timecorrection.
Chose your preferred setting and be sure you have enabled the setting in the jail.local file (if you enable syslog, disable the odoo log and visaversa)

The fail2ban odoo filters contain 2 regularexpressions:
- one to check for faild logins (odoo.conf and odoo-syslog.conf)
- seccond to check for 404's (odoo-404.conf and odoo-404-syslog.conf)

Probably the regularexpressions can more efficient but as they are now they do the job.
Glasswall hopes these files will improve your Odoo security.
