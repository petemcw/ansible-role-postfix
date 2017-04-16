# Postfix Role for Ansible

This role configures [Postfix](http://www.postfix.org/) which is a free and
open-source mail transfer agent (MTA) that routes and delivers electronic mail,
intended as an alternative to the widely used Sendmail MTA.

## Requirements

This role requires [Ansible](http://www.ansibleworks.com/) version 1.4 or higher
and the Debian/Ubuntu platform.

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

# Don't use mechanisms that permit anonymous authentication.
postfix_smtp_sasl_security_options: 'noanonymous'

# Enable client-side authentication
# postfix_smtp_sasl_auth_enable: 'yes'

# SMTP user:pass
# postfix_smtp_sasl_password_maps: 'static:SMTP_Injection:APIKEY'

# Ensures that the connection to the remote smtp server will be encrypted
# postfix_smtp_tls_security_level: 'encrypt'

# Header size limitation
# postfix_header_size_limit: '4096000'
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
            postfix_relayhost_pass: 'mandrill_apikey'
          }
    ```
3. Install Postfix and configure to use SMTP relay (Sparkpost)

    ```yaml
    ---
    # This playbook installs Postfix email server

    - name: Apply Postfix to mail nodes
      hosts: all
      roles:
        - { role: postfix,
            postfix_domain: 'example.com',
            postfix_notify_email: 'mbr@example.com',
            postfix_use_smtp: true,
            postfix_relayhost: '[smtp.sparkpostmail.com]:587',
            postfix_smtp_sasl_auth_enable: 'yes',
            postfix_smtp_sasl_password_maps: 'static:SMTP_Injection:APIKEY',
            postfix_smtp_sasl_security_options: 'noanonymous',
            postfix_smtp_tls_security_level: 'encrypt',
            postfix_header_size_limit: '4096000'
          }
    ```

## Dependencies

None.

## License

MIT.
