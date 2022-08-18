Opendkim
=========

This role installs and configures opendkim. The role also creates the keys for the different domains.

Requirements
------------

None

Role Variables
--------------

| name                         | type            | default                 | description                                                                                                       |
|------------------------------|-----------------|-------------------------|-------------------------------------------------------------------------------------------------------------------|
| opendkim_autorestart         | boolean         | true                    | Whether or not the filter should arrange to restart automatically if it crashes.                                  ||
| opendkim_autorestart_rate    | string          | 10/h                    | Maximum automatic restart rate.                                                                                   ||
| opendkim_umask               | string          | 007                     | Process umask for file creation                                                                                   ||
| opendkim_syslog              | boolean         | true                    | Log to syslog                                                                                                     ||
| opendkim_syslog_success      | boolean         | true                    | Whether to log activity success to syslog                                                                         ||
| opendkim_log_why             | boolean         | true                    | issues very detailed logging about the logic behind the filter's decision to either sign a message  or verify it. ||
| opendkim_canonicalization    | string          | relaxed/simple          | The canonicalizations to use when signing. Can be "simple" or "relaxed"                                           ||
| opendkim_mode                | string          | sv                      | Modes of operation to provide. "s" means "sign", "v" means "verify"                                               ||
| opendkim_user                | string          | opendkim                | The user of opendkim                                                                                              ||
| opendkim_group               | string          | opendkim                | The group of the opendkim user                                                                                    ||
| opendkim_trust_anchor_file   | string          | /usr/share/dns/root.key | Specifies a file from which trust anchor data should be read when doing DNS queries.                              ||
| opendkim_socket              | string          | inet:8891@localhost     | Names the socket where this filter should listen for milter connections from the MTA.                             ||
| opendkim_domains             | Array of object | []                      | Domains to sign the emails. This variable is an array of object with keys: `domain`, `subdomain`.                 ||
| opendkim_signature_algorithm | string          | rsa-sha256              | The algorithm to use when generating signatures. Either `rsa-sha1` or `rsa-sha256`.                               ||

More details regarding opendkim parameters are available on [opendkim website](http://www.postfix.org/postconf.5.html)

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role:

````yaml
- hosts: servers
  become: true
  tasks:
    
    - name: Run opendkim role
      ansible.builtin.import_role:
        name: mivek.opendkim
      vars:
        opendkim_domains:
          - subdomain: '*'
            domain: example.com
          - subdomain: 'test'
            domain: example2.com
        opendkim_canonicalization: "simple/simple"
````

License
-------

BSD
