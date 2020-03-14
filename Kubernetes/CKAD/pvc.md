### Access Modes
PersistentVolumes support the following access modes:

1. ReadWriteOnce: The Volume can be mounted as read-write by a single node.
2. ReadOnlyMany: The Volume can be mounted read-only by many nodes.
3. ReadWriteMany: The Volume can be mounted as read-write by many nodes.PersistentVolumes that are backed by Compute Engine persistent disks don't support this access mode.