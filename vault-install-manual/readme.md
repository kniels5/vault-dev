### Create ACL for vault

```bash
curl -X PUT -d @policy.json http://localhost:8500/v1/acl/create?token=<management-token>
```


### Consul Agent Client Config

```json
{
  "acl_datacenter":"dc1",
  "acl_default_policy":"allow",
  "acl_down_policy":"allow",
  "datacenter": "dc1",
  "acl_master_token":"398073a8-5091-4d9c-871a-bbbeb030d1f6",
  "skip_leave_on_interrupt": true,
  "encrypt": "Nwgk7kfcZcNRymDU+eNvkA==",
  "addresses": {
    "http": "unix:///tmp/consul-http.sock",
    "rpc": "unix:///tmp/consul-rpc.sock",
    "https": "0.0.0.0"
  },
  "unix_sockets": {
    "group": "501",
    "mode": "760"
  },
  "ports": {
      "https": 8501
  },
  "verify_incoming": true,
  "verify_outgoing": true,
  "ca_file": "/app_vg/hashicorp/certs/ca.pem",
  "key_file": "/app_vg/hashicorp/certs/key.pem",
  "cert_file": "/app_vg/hashicorp/certs/cert.pem",
  "retry_join": ["10.0.0.240", "10.0.0.46", "10.0.0.135"]
}
```

### Vault Config

```json
{
    "backend": {
        "consul": {
            "address": "unix:///tmp/consul-http.sock",
            "scheme": "http",
            "redirect_addr": "https://10.0.0.158:8200",
            "token": "c16c1564-9c95-8e6f-88f3-d07e95c9e5ac"
        }
    },
    "listener": {
        "tcp": {
            "address": "0.0.0.0:8200",
            "tls_disable": "0",
            "tls_key_file": "/app_vg/hashicorp/certs/key.pem",
            "tls_cert_file": "/app_vg/hashicorp/certs/cert.pem",
        }
    }
}
```

