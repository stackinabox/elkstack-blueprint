#
**This Heat template installs Elasticsearch, Logstash and Kibana (ELK) on a single node.**
#
===============================================================================

########
**Overview**
########

This template will launch an instance with Elasticsearch, Logstash and Kibana by taking the following as parameters.

**keyname, security group, image, flavor, internal network and public network**


Resources used in the HOT template are **port** and **floating ip**.

For the server that we are launching (OS::Nova::Server), we link it to a neutron port resource (type OS::Neutron::Port) and to a floating ip resource (type OS::Neutron::FloatingIP).


The port assigned to the server represents a logical switch port and is linked to the default security group to ensure secure access to the instance. The floating ip resources provide external access to the instance.


Detailed information on parameters and resource types are available on

http://docs.openstack.org/developer/heat/template_guide/hot_spec.html  
http://docs.openstack.org/developer/heat/template_guide/openstack.html

==========================================================================
########
**Launching the ELK Stack**
########

We can obtain the parameter values via the following commands:

public_net = nova net-list | awk '/ ext-net / { print $2 }'

internal_net = nova net-list | awk '/ int-net / { print $2 }'

internal_subnet = neutron subnet-list | awk '/internal-network1/ { print $2}'

securitygroup_id = nova secgroup-list | awk '/ default / { print $2 }'

key_name = nova keypair-list | awk '/ ELKkey / { print $2 }'

image_id = Ubuntu-14.04


Finally,

heat stack-create -f elkstack.yml -P "key_name=;securitygroup_id=;image_id=;public_net=;internal_net=;internal_subnet=;" Stackname

==========================================================================
########
**Verify Stack Creation**
#########

Verify if the stack was created successfully using:

heat stack-list


