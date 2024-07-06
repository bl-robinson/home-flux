# github-arc

This uses https://github.com/actions/actions-runner-controller to register github runner sets for my docker repos.

As I am not an org... as far as I can tell I have to use repository runners, which means I need to register a RunnerSet per repo.
Hence the deploy- files.

These are combined with the deploy-access files in specific namespaces to grant cross namespace access to the deployments. (To allow for action runners to restart deployments)


