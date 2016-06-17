#**Install Elasticsearch,Logstash,Kibana on a single node using Heat template**

===============================================================================

########
**Overview**
########

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

heat stack-create -f elkinstall.yml -P "key_name=;securitygroup_id=;image_id=;public_net=;internal_net=;internal_subnet=;" Stackname

==========================================================================
########
**Verify Stack creation**
#########

Verify if the stack was created successfully using:

heat stack-list





