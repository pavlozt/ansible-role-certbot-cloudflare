# Certbot Cloudflare

Use Cloudflare DNS for wildcard Certbot generation

## Requirements

- Cloudflare DNS setup
- Cloudflare token or Cloudflare API Key
- Wildcard domain setup (for wildcard certs) [*.domain.com or *.subdomain.domain.com]

## Role Variables

    certbot_cloudflare_email: "{{ certbot_email }}"

Your Cloudflare email address. This address is not necessarily the same as the address that appears on the certificates.

    certbot_cloudflare_api_token: ''

 Cloudflare API Token, optionally encrypted `ansible-vault encrypt_string 'CLOUDFLARE_API_TOKEN' --name 'certbot_cloudflare_api_token'`

    certbot_cloudflare_api_key: ''

**Alternatively** your Cloudflare Global API Key, optionally encrypted `ansible-vault encrypt_string 'CLOUDFLARE_API_KEY' --name 'certbot_cloudflare_api_key'`

You need to clearly separate API Key and API Token. Use the Token API in new code, it's more secure due to its limited impact.
You cannot set both variables `certbot_cloudflare_api_key` and `certbot_cloudflare_token`.
However, the email variable is needed to be passed to Certbot.

    certbot_cloudflare_propagation_seconds: 10

The number of seconds to wait for DNS to propagate before asking the ACME server to verify the DNS record. (Default: 10)


    certbot_certs:
      - email: "ssladmin@example.com"
      - domains:
          - "*.example.com"

The wildcard domain to create the cert for. For non-wildcard domains, I recommend using [geerlingguy.certbot](https://github.com/geerlingguy/ansible-role-certbot):

    certbot_cloudflare_acme_server: "{{ certbot_cloudflare_acme_test }}"

or:

    certbot_cloudflare_acme_server: "{{ certbot_cloudflare_acme_live }}"

Let's Encrypt server to use, defaults to test.

## Dependencies

- geerlingguy.pip
- geerlingguy.certbot

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers

      vars:
	certbot_create_if_missing: true
	certbot_cloudflare_api_key: 'CLOUDFLARE_API_TOKEN'
        certbot_certs:
          - email: "ssladmin@example.com"
          - domains:
              - "*.example.com"

      roles:
         - pavlozt.certbot_cloudflare

## License

MIT / BSD

## Author Information

This role was created in 2018 by [Michael Porter](https://www.michaelpporter.com/), in 2022 by [Nikolay Kolev](https://nikolay.com) and continued in 2023 by [Pavlozt](https://github.com/pavlozt)
