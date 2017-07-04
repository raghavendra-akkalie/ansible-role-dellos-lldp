LLDP Role for Dell EMC Networking OS
====================================

This role facilitates the configuration of Link Layer Discovery Protocol(LLDP) attributes at global and interface level. It supports the configuration of hello, mode, multiplier, advertise tlvs, management interface, fcoe, iscsi at global and interface level.
This role is abstracted for dellos9.

Installation
------------

```
ansible-galaxy install Dell-Networking.dellos-lldp
```

Requirements
------------

This role requires an SSH connection for connectivity to your Dell EMC Networking device. You can use any of the built-in Dell EMC Networking OS connection variables, or the ``provider`` dictionary.

Role Variables
--------------

This role is abstracted using the variable ``ansible_net_os_name`` that can take the following values: dellos9 and dellos10.

Any role variable with a corresponding state variable setting to absent negates the configuration of that variable.
For variables with no state variable, setting an empty value for the variable negates the corresponding configuration.
The variables and its values are case-sensitive.

``dellos_lldp`` holds the following keys:

|        Key | Type                      | Notes                                                                                                                                                                                     |
|-----------:|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| global_lldp_state | string, choices: absent, present   | Removes protocol lldp at global level, if set to absent.|
| enable  | boolean         | Enables or Disables the protocol lldp at global level. |
| hello | integer | Configures global lldp hello interval. The value can be in range 5-180. |
| mode  | string, choices: rx,tx   | Configures global lldp mode configuration. |
| multiplier | integer | Configures global lldp multiplier. The value can be in range 2-10. |
| fcoe_priority_bits | integer | Configures priority bits for FCoE traffic. The value can be in range 1-FF. |
| iscsi_priority_bits | integer | Configures priority bits for ISCSI traffic. The value can be in range 1-FF. |
| dcbx | dictionary  | Configures DCBx parameters at global level. See the following dcbx.* for each item.     |
| dcbx.version | string     | Configures DCBx version.  |
| advertise | dictionary     | Configures tlv advertisement at global level. See the following advertise.* for each item.     |
| advertise.dcbx_tlv | string     | Configures DCBx TLVs advertisement. |
| advertise.dcbx_tlv_state | string, choices: present, absent     | Removes DCBx TLVs advertisement if set to absent. |
| advertise.dcbx_appln_tlv | string     | Configures DCBx Application priority TLVs advertisement. |
| advertise.dcbx_appln_tlv_state | string, choices: present, absent     | Removes DCBx application priority TLVs advertisement if set to absent. |
| advertise.dot1_tlv | dictionary     | Configures 802.1 TLVs advertisement. See the following dot1_tlv.* for each item. |
| dot1_tlv.port_tlv | dictionary     | Configures 802.1 port TLVs advertisement. See the following port_tlv.* for each item. |
| port_tlv.protocol_vlan_id | boolean     | Configures 802.1 port protocol vlan id TLVs advertisement. |
| port_tlv.port_vlan_id | boolean     | Configures 802.1 port vlan id TLVs advertisement. |
| dot1_tlv.vlan_tlv | dictionary     | Configures 802.1 VLAN TLVs advertisement. See the following vlan_tlv.* for each item. |
| vlan_tlv.vlan_range | string     | Configures 802.1 vlan name TLVs advertisement. |
| advertise.dot3_tlv | dictionary     | Configures 802.3 TLVs advertisement. See the following dot3_tlv.* for each item. |
| dot3_tlv.max_frame_size | boolean     | Configures 802.3 maximum frame size TLVs advertisement. |
| advertise.port_descriptor| boolean     | Configures global port descriptor advertisement. |
| advertise.management_tlv | string     | Configures global management TLVs advertisement. |
| advertise.management_tlv_state | string, choices; absent, present     | Removes global TLVs advertisement,if set to absent. |
| advertise.med | dictionary     | Configures med TLVs advertisement. See the following med_tlv.* for each item. |
| med.global_med | boolean     | Configures global med TLVs advertisement. |
| med.application | list     | Configures global med TLVs advertisement for the application. See the following application.* for each item. |
| application.name | string     | Configures the name of the application for med TLVs advertisement. |
| application.vlan_id | integer     | Configures the vlan id for the application med TLVs advertisement. The value can be in range 1-4094.|
| application.priority_tagged | boolean     | Configures priority tagged for the application med TLVs advertisement. This variale is mutually exclusive with application.vlan_id |
| application.l2_priority | integer     | Configures the L2 priority for the application med TLVs advertisement. The value can be in range 0-7.|
| application.code_point_value | integer     | Configures Differentiated services code point value for med TLVs advertisement. The value can be in range 0-63.|
| med.location_identification | list     | Configures med location identification TLVs advertisement. See the following location_identification.* for each item. |
| location_identification.loc_info | string     | Configures location information for med TLVs advertisement. |
| location_identification.value | string     | Configures the value of location information.|
| location_identification.state | string, choices: absent, present   | Removes the location information, if set to absent.|
| management_interface | dictionary     | Configures LLDP on management interface. See the following management_interface.* for each item.     |
| management_interface.enable  | boolean         | Enables or Disables the protocol lldp on management interface. |
| management_interface.hello | integer | Configures lldp hello interval on managementinterface. The value can be in range
5-180. |
| management_interface.mode  | string, choices: rx,tx   | Configures lldp mode on management interface. |
| management_interface.multiplier | integer | Configures lldp multiplier on management interface. The value can be in range
 2-10. |
| management_interface.advertise | dictionary     | Configures tlv advertisement on management interface. See the following advertise.* for each item.     |
| advertise.port_descriptor| boolean     | Configures port descriptor advertisement on management interface. |
| advertise.management_tlv | string     | Configures management TLVs advertisement. |
| advertise.management_tlv_state | string, choices; absent, present     | Removes management TLVs advertisement,if set to absent. |
| local_interface | dictionary     | Configures lldp at interface level. See the following local_interface.* for each item.     |
| local_interface.&lt;interface name&gt; | dictionary     | Configures lldp at interface level. See the following &lt;interface name&gt;.* for each item.     |
| &lt;interface name&gt;.state | string, choices: absent, present   | Removes protocol lldp at interface level, if set to absent.|
|  &lt;interface name&gt;.enable  | boolean         | Enables or Disables the protocol lldp at interface level. |
| &lt;interface name&gt;.hello | integer | Configures interface level lldp hello interval. The value can be in range 5-180. |
| &lt;interface name&gt;.mode  | string, choices: rx,tx   | Configures interface level lldp mode configuration. |
| &lt;interface name&gt;.multiplier | integer | Configures interface level lldp multiplier. The value can be in range 2-10. |
| &lt;interface name&gt;.dcbx | dictionary  | Configures DCBx parameters at interface level. See the following dcbx.* for each item.     |
| dcbx.version | string     | Configures DCBx version at interface level.  |
| dcbx.port_role | string     | Configures DCBx port role at interface level.  |
| &lt;interface name&gt;.advertise | dictionary     | Configures tlv advertisement at interface level. See the following advertise.* for each item.     |
| advertise.dcbx_tlv | string     | Configures DCBx TLVs advertisement at interface level. |
| advertise.dcbx_tlv_state | string, choices: present, absent     | Removes interface level DCBx TLVs advertisement if set to absent. |
| advertise.dcbx_appln_tlv | string     | Configures DCBx Application priority TLVs advertisement at interface level. |
| advertise.dcbx_appln_tlv_state | string, choices: present, absent     | Removes interface level DCBx application priority TLVs advertisement if set to absent. |
| advertise.dot1_tlv | dictionary     | Configures 802.1 TLVs advertisement at interface level. See the following dot1_tlv.* for each item. |
| dot1_tlv.port_tlv | dictionary     | Configures 802.1 port TLVs advertisement at interface level. See the following port_tlv.* for each item. |
| port_tlv.protocol_vlan_id | boolean     | Configures 802.1 port protocol vlan id TLVs advertisement at interface level. |
| port_tlv.port_vlan_id | boolean     | Configures 802.1 port vlan id TLVs advertisement at interface level. |
| dot1_tlv.vlan_tlv | dictionary     | Configures 802.1 VLAN TLVs advertisement at interface level. See the following vlan_tlv.* for each item. |
| vlan_tlv.vlan_range | string     | Configures 802.1 vlan name TLVs advertisement at interface level. |
| advertise.dot3_tlv | dictionary     | Configures 802.3 TLVs advertisement at interface level. See the following dot3_tlv.* for each item. |
| dot3_tlv.max_frame_size | boolean   | Configures 802.3 maximum frame size TLVs advertisement at interface level. |
| advertise.port_descriptor| boolean     | Configures interface level port descriptor advertisement. |
| advertise.management_tlv | string     | Configures interface level TLVs advertisement. |
| advertise.management_tlv_state | string, choices; absent, present     | Removes interface level TLVs advertisement,if set to absent. |
| advertise.med | dictionary     | Configures interface level med TLVs advertisement. See the following med_tlv.* for each item. |
| med.global_med | boolean     | Configures interface level med TLVs advertisement. |
| med.application | list     | Configures interface level med TLVs advertisement for the application. See the following application.* for each item. |
| application.name | string     | Configures the name of the application for med TLVs advertisement. |
| application.vlan_id | integer     | Configures the vlan id for the application med TLVs advertisement at interface level. The value can be in range 1-4094.|
| application.priority_tagged | boolean     | Configures priority tagged for the application med TLVs advertisement at interface level. This variale is mutually exclusive with application.vlan_id |
| application.l2_priority | integer     | Configures the L2 priority for the application med TLVs advertisement at interface level. The value can be in range 0-7.|
| application.code_point_value | integer     | Configures Differentiated services code point value for med TLVs advertisement at interface level. The value can be in range 0-63.|
| med.location_identification | list     | Configures med location identification TLVs advertisement at interface level. See the following location_identification.* for each item. |
| location_identification.loc_info | string     | Configures location information for med TLVs advertisement at inteface level. |
| location_identification.value | string     | Configures the value of location information for med TLVs advertisement at interface level.|
| location_identification.state | string, choices: absent, present   | Removes the interface level med location information, if set to absent.|

```
Note: Asterisk (*) denotes the default value if none is specified.
```
Connection Variables
--------------------

Ansible Dell EMC Networking roles require the following connection information to establish communication with the no
des in your inventory. This information can exist in the Ansible group_vars or host_vars directories, or in the playb
ook itself.

|         Key | Required | Choices    | Description                              |
| ----------: | -------- | ---------- | ---------------------------------------- |
|        host | yes      |            | Hostname or address for connecting to the remote device over the specified ``transport`` variable. The value of this key is the destination address for the transport. |
|        port | no       |            | Port used to build the connection to the remote device. If the value of this key is unspecified, the value defaults to 22. |
|    username | no       |            | Configures the username that authenticates the connection to the remote device. The value of this key authenticates the CLI login. If this key does not specify a value, the value of environment variable ANSIBLE_NET_USERNAME is used instead. |
|    password | no       |            | Specifies the password that authenticates the connection to the remote device. If this key does not specify a value, the value of environment variable ANSIBLE_NET_PASSWORD is used instead. |
|   authorize | no       | yes, no*   | Instructs the module to enter privileged mode on the remote device before sending any commands. If this key does not specify a value, the value of environment variable ANSIBLE_NET_AUTHORIZE is used instead. If not specified, the device attempts to execute all commands in non-privileged mode.|
|   auth_pass | no       |            | Specifies the password to use if required to enter privileged mode on the remote device. If ``authorize`` is set to no, then this key is not applicable. If this key does not specify a value, the value of environment variable ANSIBLE_NET_AUTH_PASS is used instead. |
|   transport | yes      | cli*       | Configures the transport connection to use when connecting to the remote device. This key supports connectivity to the device over CLI (SSH).  |
|    provider | no       |            | Convenient method that passes all of the above connection arguments as a dictionary object. All constraints (such as required or choices) must be met either by individual arguments or values in this dictionary. |


```
Note: Asterisk (*) denotes the default value if none is specified.
```

Dependencies
------------

The dellos-lldp role is built on modules included in the core Ansible code. These modules were added in Ansible version 2.2.0.


Example Playbook
----------------

The following example uses the dellos-lldp role to configure protocol lldp. The example creates a ``hosts`` file with the switch details and corresponding variables. The hosts file should define the variable `` ansible_net_os_name `` with corresponding Dell EMC networking OS name. It writes a simple playbook that only references the dellos-lldp role.

Sample ``hosts`` file:

    leaf1 ansible_host= <ip_address> ansible_net_os_name= <OS name(dellos9)>

Sample ``host_vars/leaf1``:

    hostname: leaf1
    provider:
      host: "{{ hostname }}"
      username: XXXX
      password: XXXX
      authorize: yes
      auth_pass: XXXX
      transport: cli
    dellos_lldp:
       global_lldp_state: present
       enable: false
        mode: rx
       multiplier: 3
       fcoe_priority_bits: 3
       iscsi_priority_bits: 3
       hello: 6
       dcbx:
         version: auto
       management_interface:
         hello: 7
         multiplier: 3
         mode: tx
         enable: true
         advertise:
           port_descriptor: false
           management_tlv: management-address system-capabilities
           management_tlv_state: absent
       advertise:
         dcbx_tlv: pfc
         dcbx_tlv_state: absent
         dcbx_appln_tlv: fcoe
         dcbx_appln_tlv_state:
         dot1_tlv:
           port_tlv:
              protocol_vlan_id: true
              port_vlan_id: true
           vlan_tlv:
              vlan_range: 2-4
         dot3_tlv:
           max_frame_size: false
         port_descriptor: false
         management_tlv: management-address system-capabilities
         management_tlv_state: absent
         med:
           global_med: true
           application:
             - name: "guest-voice"
               vlan_id: 2
               l2_priority: 3
               code_point_value: 4
             - name: voice
               priority_tagged: true
               l2_priority: 3
               code_point_value: 4
           location_identification:
             - loc_info: ecs-elin
               value: 12345678911
               state: present
       local_interface:
         fortyGigE 1/3:
           lldp_state: present
           enable: false
           mode: rx
           multiplier: 3
           hello: 8
           dcbx:
             version: auto
             port_role: auto-upstream
           advertise:
             dcbx_tlv: pfc
             dcbx_tlv_state: present
             dcbx_appln_tlv: fcoe
             dcbx_appln_tlv_state: absent
             dot1_tlv:
               port_tlv:
                 protocol_vlan_id: true
                 port_vlan_id: true
               vlan_tlv:
                 vlan_range: 2-4
                 state: present
             dot3_tlv:
               max_frame_size: true
             port_descriptor: true
             management_tlv: management-address system-capabilities
             management_tlv_state: absent
             med:
               application:
                 - name: guest-voice
                   vlan_id: 2
                   l2_priority: 3
                   code_point_value: 4
                 - name: voice
                   priority_tagged: true
                   l2_priority: 3
                   code_point_value: 4
               location_identification:
                 - loc_info: ecs-elin
                   value: 12345678911

A simple playbook to setup system, ``leaf.yaml``:

    - hosts: leaf1
      roles:
         - Dell-Networking.dellos-lldp

Then run with:

    ansible-playbook -i hosts leaf.yaml

License
-------

Copyright (c) 2017, Dell Inc. All rights reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

