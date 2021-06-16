ASBRL-SPILO
=========

Deploy SPILO

Requirements
------------

Need to have Docker engine installed.

Role Variables
--------------

- ETCD_URL: "http//your-etcd-server"
- PGUSER_STANDBY: "replication-user"
- PGPASSWORD_STANDBY: password for replication user
- PGUSER_ADMIN: "admin"
- PGPASSWORD_ADMIN: password for admin user
- PGUSER_SUPERUSER: pg user, default: postgres
- PGPASSWORD_SUPERUSER: password for pg user
- PGDATA: path where to store the data
- PGPORT: container port of postgres "5432"  
- HOST_PGPORT: port where the host will listen

Dependencies
------------

None

Example command
----------------

ansiple-playbook playbook.yml -c local -e ETCD_URL="http//your-etcd-server"\
-e PGUSER_STANDBY="replication-user"\
-e PGPASSWORD_STANDBY="password123-replication-user"\
-e PGUSER_ADMIN="admin"\
-e PGPASSWORD_ADMIN="password123-admin"\
-e PGUSER_SUPERUSER="postgres"\
-e PGPASSWORD_SUPERUSER="password123-postgres"\
-e PGDATA="/etc/data/postgres"\
-e PGPORT="5432" 
-t "asbrl-spilo"

Example Playbook
----------------

    - name: Run etcd1
      include_role:
        name: asbrl-etcd
      vars:
        ETCD_INITIAL_CLUSTER: etcd1=http://3.80.73.102:2380,etcd2=http://34.228.9.16:2380,etcd3=http://34.228.77.225:2380
        ETCD_URL: http://3.80.73.102
        ETCD_TOKEN: pgEtcdCluster1
        ETCD_NAME: etcd1

    - name: Run etcd2
      include_role:
        name: asbrl-etcd
      vars:
        ETCD_INITIAL_CLUSTER: etcd1=http://3.80.73.102:2380,etcd2=http://34.228.9.16:2380,etcd3=http://34.228.77.225:2380
        ETCD_URL: http://34.228.9.16
        ETCD_TOKEN: pgEtcdCluster1
        ETCD_NAME: etcd2

    - name: Run etcd3
      include_role:
        name: asbrl-etcd
      vars:
        ETCD_INITIAL_CLUSTER: etcd1=http://3.80.73.102:2380,etcd2=http://34.228.9.16:2380,etcd3=http://34.228.77.225:2380
        ETCD_URL: http://34.228.77.225
        ETCD_TOKEN: pgEtcdCluster1
        ETCD_NAME: etcd3

License
-------

BSD

Author Information
------------------

Moegui.com