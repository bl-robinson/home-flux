# Vaultwarden

Self-hosted Bitwarden-compatible password manager using the [guerzon/vaultwarden](https://github.com/guerzon/vaultwarden) Helm chart.

## Prerequisites

### 1. Create NFS directory

On `10.0.0.3`:

```bash
mkdir -p /data/vaultwarden
```

### 2. Generate admin token

Generate an Argon2id hash for the admin panel password:

```bash
docker run --rm -it vaultwarden/server /vaultwarden hash
```

This will prompt you for a password and output a PHC string like:

```
$argon2id$v=19$m=19456,t=2,p=1$<salt>$<hash>
```

The PHC string is what gets stored in the secret. You log in to the admin panel with the original password.

### 3. Add to Terraform

Add the token to `~/workspace/terraform-k8s-cluster-bootstrap/secrets.auto.tfvars`:

```
vaultwarden_admin_token = "$argon2id$v=19$m=19456,t=2,p=1$..."
```

Then apply:

```bash
cd ~/workspace/terraform-k8s-cluster-bootstrap
terraform apply
```

This creates the `vaultwarden` namespace and `vaultwarden-admin-token` secret.

### 4. DNS

Ensure `vaultwarden.k8s.home.blrobinson.uk` resolves to `10.0.3.101` (gateway-ingress LB IP).

## Deployment

Push this branch to trigger Flux reconciliation. Flux will deploy the HelmRelease, PV/PVC, and HTTPRoute.

## Access

- **Web vault:** https://vaultwarden.k8s.home.blrobinson.uk
- **Admin panel:** https://vaultwarden.k8s.home.blrobinson.uk/admin
