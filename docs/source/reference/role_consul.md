
```{include} ../../../roles/consul/README.md
```

## Defaults

* Consul version to install (Debian package name referring )
```
hs_consul_version: "1.13.7-1"
```
### Local paths

* Path to local directory containing secrets to be uploaded to nodes

```
hs_consul_local_secrets_dir: >-
  {{
    hs_workspace_secrets_dir
    | default(inventory_dir + 'group_vars/hashistack/secrets')
  }}
```
* Path to local node certificate.
```
hs_consul_node_cert: "{{ hs_consul_local_secrets_dir }}/self.cert.pem"
```
* Path to local node fullchain certificate.
```
hs_consul_node_cert_fullchain: "{{ hs_consul_local_secrets_dir }}/self.fullchain.cert.pem"
```
* Path to local node certificate private key.
```
hs_consul_node_cert_private_key: "{{ hs_consul_local_secrets_dir }}/self.cert.key"

hs_consul_ca_certificate_dir: "/usr/local/share/ca-certificates"
hs_consul_ca_certificate: "/etc/ssl/certs/ca-certificates.crt"

tf_module_name: "consul_config"
hs_tf_action: apply

hs_consul_datacenter_name: >-
  {{
    hs_workspace
    | default('datacenter1')
  }}
hs_consul_node_name: "{{ inventory_hostname | regex_replace('_', '-') }}"
hs_consul_connect_token: ~

hs_consul_prometheus_enabled: true
hs_consul_connect_root_pki_path: "consul_connect_pki_root"
hs_consul_connect_intermediate_pki_path: "consul_connect_pki_inter"
```
* API address of the vault service
```
hs_consul_vault_address: "https://vault.{{ hs_consul_domain }}:8200"
hs_consul_api_port: "8501"
hs_consul_grpc_port: "8502"
hs_consul_grpc_tls_port: "8503"

hs_consul_domain: "{{ public_domain }}"
hs_consul_node_fqdn: "{{ hs_consul_node_name }}.{{ hs_consul_domain }}"

hs_consul_external_url: https://consul.{{ hs_consul_domain }}

hs_consul_bootstrap_expect: "{{ groups[__hs_consul_inventory_masters_group] | length }}"
hs_consul_advertise_addr: "{{ ansible_default_ipv4.address }}"

hs_consul_use_custom_ca: false
hs_consul_local_ca_cert: "{{ hs_workspace_secrets_dir }}/ca.cert.pem"

hs_consul_acl_default_policy: deny
hs_consul_acl_auto_encrypt_token: ~

hs_consul_packages_list:
  - "consul={{ hs_consul_version }}"

