Role Name
=========

This Ansible role automates the process of requesting and retrieving a signed SSL/TLS certificate from an Active Directory Certificate Authority (AD CA) and manages the renewal of the certificate if it's expired or about to expire.

Requirements
------------

- A target system running RHEL or a RHEL-compatible OS.
- Access to an Active Directory Certificate Authority (AD CA) server.

Role Variables
--------------

## Role Variables

| Variable                    | Default       | Description                                                                                                                                                           |
|-----------------------------|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ca_server`                 | (required)    | The URL of the Active Directory Certificate Authority server.                                                                                                         |
| `csr_path`                  | (required)    | The path where the Certificate Signing Request (CSR) should be stored.                                                                                                |
| `ad_username`               | (optional)    | The Active Directory username for authentication.                                                                                                                     |
| `ad_password`               | (optional)    | The Active Directory password for authentication.                                                                                                                     |
| `private_key_path`          | (required)    | The path where the private key should be stored.                                                                                                                      |
| `request_id_path`           | (required)    | The path where the request ID should be stored.                                                                                                                       |
| `certificate_path`          | (required)    | The path where the signed certificate should be stored.                                                                                                               |
| `validate_certs`            | `yes`         | Whether or not to validate the CA server's SSL certificate. Set to `no` if using a self-signed certificate.                                                          |
| `force_renewal`             | `no`          | Whether to force renewal of the certificate, regardless of its expiration status.                                                                                     |
| `days_remaining`            | `30`          | The number of days remaining before the certificate expires. If the remaining days are less than or equal to this value, the certificate will be considered as expiring. |
| `certificate_template`      | `WebServer`    | The certificate template to be used when requesting the certificate.                                                                                                  |
| `cert_common_name`          | (required)    | The common name for the certificate.                                                                                                                                  |
| `cert_organization_name`    | (required)    | The organization name for the certificate.                                                                                                                            |
| `cert_locality_name`        | (required)    | The locality name for the certificate.                                                                                                                                |
| `cert_province_name`        | (required)    | The province name for the certificate.                                                                                                                                |
| `cert_country_name`         | (required)    | The country name for the certificate.                                                                                                                                  |
| `cert_email_address`        | (required)    | The email address for the certificate.                                                                                                                                |
| `cert_dns_names`            | (required)    | A list of DNS names for the Subject Alternative Name (SAN) field.                                                                                                    |
| `cert_ip_addresses`         | (required)    | A list of IP addresses for the Subject Alternative Name (SAN) field.                                                                                                 |


Dependencies
------------

None

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
    - role: ansible-role-ad-cert
      vars:
        ca_server: "https://ca.example.com"
        ad_username: "user@example.com"
        ad_password: "password"
        certificate_template: "WebServer"
        private_key_path: "/etc/pki/tls/private/example.com.key"
        csr_path: "/etc/pki/tls/certs/example.com.csr"
        request_id_path: "/etc/pki/tls/certs/example.com.reqid"
        certificate_path: "/etc/pki/tls/certs/example.com.crt"
        validate_certs: yes
        force_renewal: no
        days_remaining: 30
        common_name: "example.com"
        organization_name: "Example Inc."
        locality_name: "New York"
        province_name: "New York"
        country_name: "US"
        email_address: "admin@example.com"
        dns_names:
          - "example.com"
          - "www.example
          - "www.example.com"
        ip_addresses:
          - "192.168.1.1"

```

License
-------

BSD

Author Information
------------------

This role was created in 2023 by Ajin.
