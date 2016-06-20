#
**Install Elasticsearch,Logstash,Kibana on a single node using Heat template**
#
===============================================================================

########
**Overview**
########

This template will help us in launching an instance with Elasticsearch,logstash and Kibana by specifying the parameters listed below as parameters.

**keyname,security group,image,flavor,internal network and public network** have been specified as parameters so that we can choose type of **instance** and also **key pair,security group** and onto which **internal subnet** the instance is to be launched.


Resources used in the HOT template are **port** and **floating ip**

For the server that we are launching (OS::Nova::Server), we link it to a neutron port resource (type OS::Neutron::Port) and to a floating ip resource (type OS::Neutron::FloatingIP).


Port assigned to the server represents a logical switch port and is linked to the default security group to ensure secure access to the instances. The floating ip resources provide external access to instances.


Detailed information on parameters and resource types are available on

http://docs.openstack.org/developer/heat/template_guide/hot_spec.html  
http://docs.openstack.org/developer/heat/template_guide/openstack.html

==========================================================================
########
**Creating a Stack**
########

public_net = nova net-list | awk '/ ext-net / { print $2 }'

internal_net = nova net-list | awk '/ int-net / { print $2 }'

internal_subnet = neutron subnet-list | awk '/internal-network1/ { print $2}'

securitygroup_id = nova secgroup-list | awk '/ default / { print $2 }'

key_name = nova keypair-list | awk '/ ELKkey / { print $2 }'

image_id = Ubuntu-14.04



heat stack-create -f elkinstall.yml -P "key_name=;securitygroup_id=;image_id=;public_net=;internal_net=;internal_subnet=;" Stackname

==========================================================================
########
**Verify Stack creation**
#########

Verify if the stack was created successfully using:

heat stack-list


