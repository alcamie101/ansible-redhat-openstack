ansible-redhat-openstack
========================
ggillies Openstack ansible build

1. deploy.openstack.yml         -    default playbook for the install of controller, network and compute nodes
2. deploy-storage.yml             -    playbook to setup gluster storage nodes. This going to be rewritten for Ceph
3. openstack-instance.yml       -    playbook to create extra compute nodes ontop of existing openstack installation

.
├── ansible.cfg
├── inventory
│   ├── group_vars
│   │   ├── all                (The redhat_username details can be removed for this setup)
│   │   └── openstack-instance-example
│   ├── host_vars
│   │   ├── openstack-compute-01.example.com.yml       (These will be renamed with your machines details) - These are setup as a cluster
│   │   ├── openstack-compute-02.example.com.yml       (These will be renamed with your machines details) - These are setup as a cluster
│   │   ├── openstack-controller-01.example.com.yml    (These will be renamed with your machines details)
│   │   ├── openstack-controller-02.example.com.yml    (These will be renamed with your machines details)
│   │   ├── openstack-network-01.example.com.yml       (These will be renamed with your machines details) - These are setup as a cluster
│   │   ├── openstack-network-02.example.com.yml       (These will be renamed with your machines details) - These are setup as a cluster
│   │   ├── openstack-storage-01.example.com.yml       (These will be renamed with your machines details) - These are not used for the initial openstack rollout
│   │   └── openstack-storage-02.example.com.yml       (These will be renamed with your machines details) - These are not used for the initial openstack rollout
│   ├── nova-example.ini                    (can ignore these for the install)
│   └── nova.py                                  (can ignore these for the install)
├── openstack-ansible-modules
│   ├── cinder_manage
│   ├── glance
│   ├── glance_manage
│   ├── keystone_manage
│   ├── keystone_service
│   ├── LICENSE
│   ├── Makefile
│   ├── neutron_floating_ip
│   ├── neutron_network
│   ├── neutron_router
│   ├── neutron_router_gateway
│   ├── neutron_router_interface
│   ├── neutron_sec_group
│   ├── neutron_subnet
│   ├── nova_flavor
│   ├── nova_manage
│   ├── README.md
│   └── tests
│       ├── keystone_service.py -> ../keystone_service
│       └── test_keystone_service.py
├── playbooks
│   ├── deploy-openstack.yml          -    default playbook for the install of controller, network and compute nodes
│   ├── deploy-storage.yml              -    playbook to setup gluster storage nodes. This going to be rewritten for Ceph
│   └── openstack-instance.yml        -    playbook to create extra compute nodes ontop of existing openstack installation
└── roles
    ├── cinder-server
    │   ├── defaults
    │   │   └── main.yml
    │   ├── tasks
    │   │   └── main.yml
    │   └── templates
    │       ├── cinder.conf.j2
    │       └── glusterfs_shares.j2
    ├── common
    │   └── tasks
    │       └── main.yml
    ├── glance-server
    │   ├── defaults
    │   │   └── main.yml
    │   ├── tasks
    │   │   └── main.yml
    │   └── templates
    │       ├── glance-api.conf.j2
    │       └── glance-registry.conf.j2
    ├── glusterfs-server
    │   ├── defaults
    │   │   └── main.yml
    │   └── tasks
    │       └── main.yml
    ├── haproxy-server
    │   ├── tasks
    │   │   └── main.yml
    │   └── templates
    │       └── haproxy.cfg.j2
    ├── heat-server
    │   ├── defaults
    │   │   └── main.yml
    │   ├── tasks
    │   │   └── main.yml
    │   └── templates
    │       └── heat.conf.j2
    ├── horizon-server
    │   ├── tasks
    │   │   └── main.yml
    │   └── templates
    │       └── local_settings.j2
    ├── keystone-server
    │   ├── defaults
    │   │   └── main.yml
    │   ├── tasks
    │   │   ├── main.yml
    │   │   └── users-and-endpoints.yml
    │   └── templates
    │       ├── keystone.conf.j2
    │       └── keystonerc.j2
    ├── mariadb-galera-server
    │   ├── defaults
    │   │   └── main.yml
    │   ├── files
    │   │   └── galera-monitor
    │   ├── handlers
    │   │   └── main.yml
    │   ├── tasks
    │   │   └── main.yml
    │   └── templates
    │       ├── clustercheck.j2
    │       ├── galera.cnf.j2
    │       ├── limits.conf.j2
    │       └── openstack.cnf.j2
    ├── memcached-server
    │   └── tasks
    │       └── main.yml
    ├── neutron-server
    │   ├── common
    │   │   ├── defaults
    │   │   │   └── main.yml
    │   │   ├── tasks
    │   │   │   └── main.yml
    │   │   └── templates
    │   │       ├── dhcp_agent.ini.j2
    │   │       ├── ifcfg.j2
    │   │       ├── l3_agent.ini.j2
    │   │       ├── lbaas_agent.ini.j2
    │   │       ├── metadata_agent.ini.j2
    │   │       ├── ml2_conf.ini.j2
    │   │       ├── neutron.conf.j2
    │   │       └── ovs_neutron_plugin.ini.j2
    │   ├── compute
    │   │   ├── meta
    │   │   │   └── main.yml
    │   │   └── tasks
    │   │       └── main.yml
    │   ├── controller
    │   │   ├── handlers
    │   │   │   └── main.yml
    │   │   ├── meta
    │   │   │   └── main.yml
    │   │   └── tasks
    │   │       └── main.yml
    │   └── network
    │       ├── meta
    │       │   └── main.yml
    │       └── tasks
    │           └── main.yml
    ├── nova-server
    │   ├── common
    │   │   ├── defaults
    │   │   │   └── main.yml
    │   │   ├── tasks
    │   │   │   └── main.yml
    │   │   └── templates
    │   │       └── nova.conf.j2
    │   ├── compute
    │   │   ├── meta
    │   │   │   └── main.yml
    │   │   └── tasks
    │   │       └── main.yml
    │   └── controller
    │       ├── handlers
    │       │   └── main.yml
    │       ├── meta
    │       │   └── main.yml
    │       └── tasks
    │           └── main.yml
    ├── openstack
    │   ├── compute
    │   │   └── meta
    │   │       └── main.yml
    │   ├── controller
    │   │   ├── defaults
    │   │   │   └── main.yml
    │   │   └── meta
    │   │       └── main.yml
    │   └── network
    │       └── meta
    │           └── main.yml
    ├── openstack-instance
    │   └── tasks
    │       └── main.yml
    ├── pacemaker-cluster
    │   ├── defaults
    │   │   └── main.yml
    │   ├── library
    │   │   ├── pcs_property
    │   │   └── pcs_resource
    │   └── tasks
    │       └── main.yml
    ├── rabbitmq-server
    │   ├── defaults
    │   │   └── main.yml
    │   ├── tasks
    │   │   └── main.yml
    │   └── templates
    │       ├── rabbitmq.config.j2
    │       └── rabbitmq-env.conf.j2
    └── trove-server
        ├── defaults
        │   └── main.yml
        ├── tasks
        │   └── main.yml
        └── templates
            ├── trove-conductor.conf.j2
            ├── trove.conf.j2
            └── trove-taskmanager.conf.j2
