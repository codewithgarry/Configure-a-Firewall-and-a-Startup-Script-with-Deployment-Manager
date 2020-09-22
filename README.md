# Configure-a-Firewall-and-a-Startup-Script-with-Deployment-Manager

###################################################################################################################
Google cloud deployment-manager documentation - https://cloud.google.com/
deployment-manager/docs/quickstart

################################################################################################################### 
****************qwiklabs.jinja***************

resources:
- type: compute.v1.firewall
  name: tcp-firewall-rule
  properties:
    network: https://www.googleapis.com/compute/v1/
projects/{{ env["project"] }}/global/networks/default
    sourceRanges: ["0.0.0.0/0"]
    targetTags: ['http']
    allowed:
     - IPProtocol: TCP
       ports: ["80"]
- type: compute.v1.instance
  name: vm-test
  properties:
    zone: {{ properties['zone'] }}
    machineType: https://www.googleapis.com/compute/v1/
projects/{{ env['project'] }}/zones/{{ properties['zone'] }}
/machineTypes/f1-micro
    tags:
     items: ['http']
    metadata:
      items:
      # For more ways to use startup scripts on an instance, see:
      #   https://cloud.google.com/compute/docs...
      - key: startup-script
        value: |
          #!/bin/bash
          apt-get update
          apt-get install -y apache2
    disks:
    - deviceName: boot
      type: PERSISTENT
      boot: true
      autoDelete: true
      initializeParams:
        diskName: disk-{{ env["deployment"] }}
        sourceImage: https://www.googleapis.com/compute/v1/
projects/debian-cloud/global/images/family/debian-9
    networkInterfaces:
    - network: https://www.googleapis.com/compute/v1/
projects/{{ env["project"] }}/global/networks/default
      # Access Config required to give the instance a public IP address
      accessConfigs:
      - name: External NAT
        type: ONE_TO_ONE_NAT


###############################################################################################################################
qwiklabs.yaml - No Change
qwiklabs.jinja.scheme- No Change
