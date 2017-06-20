## Tomcat failover with Memcached + Memcached Session Manager + Haproxy (load blancer)

- Tested on Ansible 2.3.0.0 for OSX
- Expects hosts: Centos 6.x
- Use Vagrant + Virtual Box to create running environment

This playbook deploys a failover solution for clustered Tomcat using Haproxy as load balancer and Memcached + MSM as session manager.

- Haproxy: balances the requests by round robin.
- Memcached: stores `sessionid` of tomcat.
- MSM: manages tomcat session.

For more detail about session management, see https://github.com/magro/memcached-session-manager

This playbook also deploys a demo web app (https://github.com/magro/msm-sample-webapp) to test the session management.

You can change webapp in roles/webapp/files.


## Initial setup of inventory file

```
[lb_servers]
192.168.82.2

[backend_servers]
192.168.82.3
192.168.82.4
192.168.82.5

[memcached_servers]
192.168.82.6
192.168.82.7
```

Edit inventory file `hosts` to suit your requirements and run playbook:

```
    $ cd vagrant
    $ vagrant up
    $ vagrant provision
```

When finished, open web browser and access to http://192.168.82.2/ to start testing.And access to http://192.168.82.2/petclinic/ to use a webapp. 

## Ideas and improvements

- Setup SSL for load balancer.
- Hardening iptables rules.

Pull requests are welcome.

## License

This work is licensed under MIT license.
