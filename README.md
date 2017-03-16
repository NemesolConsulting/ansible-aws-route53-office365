AWS Route53 for Office365 Email
===============================

A simple role to create DNS zone and required entries for Office365 under Amazon Web Service Route53 DNS service. 


Requirements
------------

Requires boto.

Please configure your ~/.aws/credentials with your AWS key id and secret. Use the aws_profile variable to choose the profile you want to use. The credentials need to have access to configure Route53 for the account. 


...
[nemesol-consulting-aws-dns]
aws_access_key_id = XXXXXXXXXXXXXXXXXX
aws_secret_access_key = XXXXXXXXXXXXXXXXXXXXXXX
...

Role Variables
--------------

Required: 
aws_profile - the name of the profile as defined in ~/.aws/credentials
route53_domain - the root domain to configure for Office365 use.

Optional: 
SPF_APPEND - any additional email sending servers needed for the SPF record in this domain. 

Dependencies
------------

N/A

Example Playbook
----------------

### Simple run without inventory 


...

- hosts: localhost
  - roles: 
       - role { role: NemesolConsulting.aws-route53-office365, aws_profile: nemesol-consulting-aws-dns, route53_domain: nemesol.com }

...

### More fun with pseudo-host per domain in inventory

...

- hosts: nemesol-email-domains
  - roles: 
	- NemesolConsulting.aws-route53-office365

...
 
# Production inventory file then includes:

...
 
nemesol-com-route53 ansible_host=localhost ansible_connection=local
nemesol-fi-route53 ansible_host=localhost ansible_connection=local
nemesol-net-route53 ansible_host=localhost ansible_connection=local

[nemesol-email-domains]
nemesol-com-route53
nemesol-fi-route53
nemesol-net-route53

...

# And finally we define the params in hosts_var files


host_vars/nemesol-fi-route53
...
route53_domain: nemesol.com
aws_profile: nemesol-consulting-aws-dns
...

License
-------

BSD

Author Information
------------------

Markus Vilhelm Seppälä, Nemesol Oy  / Nemesol Consulting ( http://consulting.nemesol.fi )
