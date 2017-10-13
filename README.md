# libcouch

## Replication

### Protocol

First of all the CouchDB Replicator verifies, if source and target exist. If the source does not exist an error is reported. 
The resulting action concerning the target check depends on the parameter <code>creating_target</code>. If the parameter is set to 
*true*, the target is created, otherwise an error is reported.

The method <code>HEAD /{db}</code> is used for the query.

### Clustering

In a cluster, replication jobs are balanced evenly among all the nodes nodes such that a replication job runs on only one node at a time.

Every time there is a cluster membership change, that is when nodes are added or removed, as it happens in a rolling reboot, replicator application will notice the change, rescan all the document and running replication, and re-evaluate their cluster placement in light of the new set of live nodes. This mechanism also provides replication fail-over in case a node fails. Replication jobs started from replication documents (but not those started from _replicate HTTP endpoint) will automatically migrate one of the live nodes.
