## Profiles

Configuration profiles allow to tweak configuration quickly. Profiles can be
applied with the `--profile` flag to `ipfs init` or with the `ipfs config profile
apply` command. When a profile is applied a backup of the configuration file
will be created in `$IPFS_PATH`.

The available configuration profiles are listed below. You can also find them
documented in `ipfs config profile --help`.

- `server`

  Disables local host discovery, recommended when
  running IPFS on machines with public IPv4 addresses.

- `randomports`

  Use a random port number for the incoming swarm connections.

- `default-datastore`

  Configures the node to use the default datastore (flatfs).

  Read the "flatfs" profile description for more information on this datastore.

  This profile may only be applied when first initializing the node.

- `local-discovery`

  Enables local discovery (enabled by default). Useful to re-enable local discovery after it's
  disabled by another profile (e.g., the server profile).

- `test`

  Reduces external interference of IPFS daemon, this
  is useful when using the daemon in test environments.

- `default-networking`

  Restores default network settings.
  Inverse profile of the test profile.

- `flatfs`

  Configures the node to use the flatfs datastore. Flatfs is the default datastore.

  This is the most battle-tested and reliable datastore.
  You should use this datastore if:

  - You need a very simple and very reliable datastore, and you trust your
    filesystem. This datastore stores each block as a separate file in the
    underlying filesystem so it's unlikely to lose data unless there's an issue
    with the underlying file system.
  - You need to run garbage collection in a way that reclaims free space as soon as possible.
  - You want to minimize memory usage.
  - You are ok with the default speed of data import, or prefer to use `--nocopy`.

  This profile may only be applied when first initializing the node.


- `badgerds`

  Configures the node to use the experimental badger datastore. Keep in mind that this **uses an outdated badger 1.x**.

  Use this datastore if some aspects of performance,
  especially the speed of adding many gigabytes of files, are critical. However, be aware that:

  - This datastore will not properly reclaim space when your datastore is
    smaller than several gigabytes. If you run IPFS with `--enable-gc`, you plan on storing very little data in
    your IPFS node, and disk usage is more critical than performance, consider using
    `flatfs`.
  - This datastore uses up to several gigabytes of memory.  
  - Good for medium-size datastores, but may run into performance issues if your dataset is bigger than a terabyte.
  - The current implementation is based on old badger 1.x which is no longer supported by the upstream team.

  This profile may only be applied when first initializing the node.

- `lowpower`

  Reduces daemon overhead on the system. Affects node
  functionality - performance of content discovery and data
  fetching may be degraded. Local data won't be announced on routing systems like DHT.

  - `Swarm.ConnMgr` set to maintain minimum number of p2p connections at a time.
  - Disables [`Reprovider`](#reprovider) service → no CID will be announced on DHT and other routing systems(!)
  - Disables AutoNAT.

  Use this profile with caution.
