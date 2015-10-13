# Postfix Role for Ansible

This role configures [Postfix](http://www.postfix.org/) which is a free and open-source mail transfer agent (MTA) that routes and delivers electronic mail, intended as an alternative to the widely used Sendmail MTA.

## Requirements

This role requires [Ansible](http://www.ansibleworks.com/) version 1.4 or higher and the Debian/Ubuntu platform.

## Role Variables

The variables that can be passed to this role and a brief description about
them are as follows:

```yaml
# The FQDN for the Postfix email server
postfix_domain: ''

# The receiving email address where root email is forwarded
postfix_notify_email: false

# The next-hop destination of non-local mail, for SMTP define a FQDN or hostname
postfix_relayhost: ''

# The default flag for whether to enable SMTP sending
postfix_use_smtp: false

# The username for SMTP authentication
postfix_relayhost_user: false

# The password for SMTP authentication
postfix_relayhost_pass: false

# The interfaces for Postfix to listen on
postfix_inet_interfaces: 'loopback-only'

# The protocols Postfix will use when it makes or accepts network connections, and also controls what DNS lookups Postfix will use when it makes network connections.
postfix_inet_protocols: 'all'

# The address type ("ipv6", "ipv4" or "any") that the Postfix SMTP client will try first, when a destination has IPv6 and IPv4 addresses with equal MX preference.
postfix_smtp_address_preference: 'all'
```

## Examples

1. Install Postfix with the default settings

    ```yaml
    ---
    # This playbook installs Postfix email server

    - name: Apply Postfix to mail nodes
      hosts: all
      roles:
        - { role: postfix, 
            postfix_domain: 'example.com',
            postfix_notify_email: 'janedoe@example.com'
          }
    ```

2. Install Postfix and configure to use SMTP relay (Mandrill, MailGun, SendGrid, etc.)

    ```yaml
    ---
    # This playbook installs Postfix email server

    - name: Apply Postfix to mail nodes
      hosts: all
      roles:
        - { role: postfix, 
            postfix_domain: 'example.com',
            postfix_notify_email: 'janedoe@example.com',
            postfix_use_smtp: true,
            postfix_relayhost: '[smtp.mandrill.com]',
            postfix_relayhost_user: 'mandrill_username',
            postfix_relayhost_user: 'mandrill_apikey'
          }
    ```

## Dependencies

None.

## License

MIT.
