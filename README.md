# Postfix Email Server

This role configures Postfix which is a free and open-source mail transfer agent (MTA) that routes and delivers electronic mail, intended as an alternative to the widely used Sendmail MTA.

## Requirements

This role requires [Ansible](http://www.ansibleworks.com/) version 1.4 or higher and the Debian/Ubuntu platform.

## Role Variables

Certain variables can be passed into this role to adjust the default behavior. The common ones are mentioned below:

    postfix_notify_email:
    postfix_use_smtp: false
    postfix_relayhost:
    postfix_relayhost_user:
    postfix_relayhost_pass:

## Examples

1) Install with the defaults

    ---
    - hosts: all
      roles:
        - { role: postfix, postfix_notify_email: "janedoe@example.com" }

2) Install and configure to use SMTP relay (Mandrill, MailGun, SendGrid, etc.)

    ---
    - hosts: all
      roles:
        - { role: postfix,
            postfix_notify_email: "janedoe@example.com",
            postfix_use_smtp: true,
            postfix_relayhost: '[smtp.mandrill.com]',
            postfix_relayhost_user: 'mandrill_username',
            postfix_relayhost_user: 'mandrill_apikey'
          }

## Dependencies

None.

## License

MIT.
