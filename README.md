# minio

# install velero and restric

velero install \
--provider aws \
--plugins velero/velero-plugin-for-aws:v1.0.0 \
--bucket backup \
--secret-file ./credentials-minio \
--use-volume-snapshots=false \
--use-restic \
--backup-location-config \
region=minio,s3ForcePathStyle="true",s3Url=http://localhost:9000,publicUrl=http://localhost:9000


# velero backup
velero backup create harbor-bak --include-namespaces harbor
velero backup get
velero backup logs harbor-bak


# uninstall velero
kubectl delete namespace/velero clusterrolebinding/velero
kubectl delete crds -l component=velero
