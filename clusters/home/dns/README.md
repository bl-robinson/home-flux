# Run bind9 DNS server.

This is probably/possible a bad way of doing this. IT may be possible just to use kubernetes for this natively but for now as its a migration.

Just spins up a DNS server and exposes it with TCP LoadBalancer.

Notes:
  - Deployed version of the [docker-dns](https://github.com/bl-robinson/docker-dns) repo.
  - It'd be good here to look at changing the deployment to be handled by GHA updating the container version...
  - This'd let me do that rather than just kubectl rolling restart.