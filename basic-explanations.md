# Secret-owner - what is meant by secret sharing?

Your key will be divided in to a number of parts in such a way that it can be fully recovered when a specific number of parts are recombined. These are then sent to trusted friends of your choice. For example if you choose a threshold of 3 and to generate 5 shards, any three of your five friends can recover your key.  But two of them alone will not be able to derive any information whatsoever. This also means there is a tolerance to two of the five friends being unavailable.

This works using Shamir's secret sharing.  Here is a [simple explanation of secret sharing](./shamirs-secret-sharing.md)

# Custodian - what does it mean to look after a shard for someone.

*Name* would like you to look after a shard of their private key, and keep it safe. If something happens to their key (for example they loose their device), they may ask you to return this shard. It is important that you look after it, however, you are not the only person who has one, and if you do loose it, others may be able to help.

This works using Shamir's secret sharing.  Here is a [simple explanation of secret sharing](./shamirs-secret-sharing.md)
