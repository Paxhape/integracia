---
heat_template_version: 2016-04-08

description: testing

parameters:
  Cvicenie:
    description: Cislo cvicenia
    type: string
    default: cv3

AvailabilityZone:
    description: Availability zone
    type: string
    default: any

Flavor:
    description: flavor
    type: string
    default: Linux

Image:
    description: Image
    type: string
    default: cirros

Network:
    description: Network
    type: string
    default: ext-net

resources:
  Instance:
    type: OS::Nova::Server
    properties:
      #name: insta
      name: { list_join:[ '-', [ { get_param: "Cvicenie" }, 'instance' ] ] }
      availability_zone: { get_param: 'AvailabilityZone'}
      flavor: { get_param: 'Flavor' }
      image:  { get_param: 'Image' }
      network: { get_param: 'Network' }
      user_data: |
       #!/bin/bash
       apt-get update -y
      user_data_format: RAW
