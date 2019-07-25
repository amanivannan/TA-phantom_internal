Requires NGINX TA for Web Parsing: https://splunkbase.splunk.com/app/3258/
Requires AuditD TA for Audit Parsing: https://splunkbase.splunk.com/app/4232/

Rename inputs.conf.template to inputs.conf and place into local folder. Add an index to each monitor stanza unless you want your data in main index.

This app collects logs documented here and provides basic parsing: https://my.phantom.us/kb/69/

# Phantom Daemon Logs

[monitor:///var/log/phantom/actiond.log]
sourcetype = phantom:daemon
disabled = true

[monitor:///var/log/phantom/decided.log]
sourcetype = phantom:daemon
disabled = true

[monitor:///var/log/phantom/ingestd.log]
sourcetype = phantom:daemon
disabled = true

[monitor:///var/log/phantom/watchdogd.log]
sourcetype = phantom:daemon
disabled = true

[monitor:///var/log/phantom/workflowd.log]
sourcetype = phantom:daemon
disabled = true
supervisord has different format then other logs

[monitor:///var/log/phantom/supervisord.log]
sourcetype = phantom:supervisord
disabled = true

[monitor:///var/log/phantom/wsgi.log]
sourcetype = phantom:wsgi
disabled = true
Other Phantom Logs

[monitor:///var/log/phantom/*.log]
sourcetype = phantom:logs
blacklist = (actiond.log|decided.log|ingestd.log|watchdogd.log|workflowd.log|supervisord.log|wsgi.log)
disabled = true


#nginx web server - use nginx app on splunkbase for parsing https://splunkbase.splunk.com/app/3258/

[monitor:///var/log/nginx/access.log]
sourcetype = nginx:plus:access
disabled = true

[monitor:///var/log/nginx/error.log]
sourcetype = nginx:plus:error
disabled = true
Postgress

[monitor:///opt/phantom/data/db/pg_log/*]
sourcetype = postgress
disabled = true


#Auditd - use TA-auditd for parsing https://splunkbase.splunk.com/app/4232/

[monitor:///var/log/audit/audit.log]
sourcetype = linux:audit
disabled = true
