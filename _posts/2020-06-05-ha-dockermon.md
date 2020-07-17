---

layout: post
title: HA-Dockermon
tags: [Smarthome, Docker]
comments: true
published: true
---

[HA-Dockermon](https://github.com/philhawthorne/ha-dockermon) is a great tool to connect Home Assistant to your docker containers, it can be used to `start`, `stop`, `restart` any container or also check they're status.

The installation is very straight forward unless I'm testing or experimenting I like to use docker-compose files and Portainer to manage them via webinterface.
That said to install HA-Dockermon I create docker-compose.yml file on the root of my docker folder or I edit the already existing one.

{% highlight yaml %}
version: "3.7"

networks:
  HTPC:
    external:
      name: HTPC
  default:
    driver: bridge

services:
  docker_mon:
    image: philhawthorne/ha-dockermon:latest
    container_name: ha_dockermon
    hostname: ha_dockermon
    networks:
      - HTPC
    restart: always
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - ${DOCKERDIR}/ha_dockermon:/config
    ports:
      - "${SERVERIP}:8126:8126"
{% endhighlight %}

Then on my Home Assistant configuration I like to use [Packages](https://www.home-assistant.io/docs/configuration/packages/) which I create a folder for my docker and inside a package file for each docker instance eg: `/config/Package_Configs/docker/octoprint_farm.yaml` which contains for example:

{% highlight yaml %}
homeassistant:

  customize_glob:
    "switch.docker_octoprint_*":
      icon: mdi:printer-3d-nozzle

  customize:
    switch.docker_portainer_octoprint:
      friendly_name: Portainer - OctoprintFarm
      icon: mdi:lifebuoy

    switch.docker_octoprint_ender3_1:
      friendly_name: "Ender3 n1"

    switch.docker_octoprint_ender3_2:
      friendly_name: "Ender3 n2"

    switch.docker_octoprint_geeetech_a10:
      friendly_name: "Geeetech A10"

    switch.docker_octoprint_biqu_legend:
      friendly_name: "BIQU Legend"

    switch.docker_octoprint_am8:
      friendly_name: "AM8"

    switch.docker_octoprint_hypercube300:
      friendly_name: "Hypercube300"

    switch.docker_octoprint_hypercube800:
      friendly_name: "Hypercube800"

    switch.docker_octoprint_bear_mk2:
      friendly_name: "Prusa Bear MK2"

    switch.docker_octoprint_bear_mk3_1:
      friendly_name: "Prusa Bear MK3 n1"

    switch.docker_octoprint_bear_mk3_2:
      friendly_name: "Prusa Bear MK3 n2"

    switch.docker_octoprint_prusa_mini:
      friendly_name: "Prusa Mini"

    switch.docker_octoprint_hopeless_automations:
      friendly_name: "Hopeless Automations"

switch:
####### OctoprintFarm

############# Portainer
  - platform: rest
    resource: http://{HA-Dockermon_IP:PORT}/container/portainer
    name: Docker Portainer Octoprint
    body_on: '{"state": "start"}'
    body_off: '{"state": "stop"}'
    is_on_template: '{{ value_json is not none and value_json.state == "running" }}'
############# Ourobos
  - platform: rest
    resource: http://{HA-Dockermon_IP:PORT}/container/ourobos
    name: Docker Ourobos Octoprint
    body_on: '{"state": "start"}'
    body_off: '{"state": "stop"}'
    is_on_template: '{{ value_json is not none and value_json.state == "running" }}'

############# Ender3_1
  - platform: rest
    resource: http://{HA-Dockermon_IP:PORT}/container/ender3_1
    name: Docker Octoprint Ender3_1
    body_on: '{"state": "start"}'
    body_off: '{"state": "stop"}'
    is_on_template: '{{ value_json is not none and value_json.state == "running" }}'

############# Ender3_2
  - platform: rest
    resource: http://{HA-Dockermon_IP:PORT}/container/ender3_2
    name: Docker Octoprint Ender3_2
    body_on: '{"state": "start"}'
    body_off: '{"state": "stop"}'
    is_on_template: '{{ value_json is not none and value_json.state == "running" }}'

############# Geeetech A10
  - platform: rest
    resource: http://{HA-Dockermon_IP:PORT}/container/geeetech_a10
    name: Docker Octoprint Geeetech A10
    body_on: '{"state": "start"}'
    body_off: '{"state": "stop"}'
    is_on_template: '{{ value_json is not none and value_json.state == "running" }}'

############# Biqu Legend
  - platform: rest
    resource: http://{HA-Dockermon_IP:PORT}/container/biqu_legend
    name: Docker Octoprint Biqu Legend
    body_on: '{"state": "start"}'
    body_off: '{"state": "stop"}'
    is_on_template: '{{ value_json is not none and value_json.state == "running" }}'

############# AM8
  - platform: rest
    resource: http://{HA-Dockermon_IP:PORT}/container/am8
    name: Docker Octoprint AM8
    body_on: '{"state": "start"}'
    body_off: '{"state": "stop"}'
    is_on_template: '{{ value_json is not none and value_json.state == "running" }}'

############# Hypercube300
  - platform: rest
    resource: http://{HA-Dockermon_IP:PORT}/container/hypercube300
    name: Docker Octoprint Hypercube300
    body_on: '{"state": "start"}'
    body_off: '{"state": "stop"}'
    is_on_template: '{{ value_json is not none and value_json.state == "running" }}'

############# Hypercube800
  - platform: rest
    resource: http://{HA-Dockermon_IP:PORT}/container/hypercube800
    name: Docker Octoprint Hypercube800
    body_on: '{"state": "start"}'
    body_off: '{"state": "stop"}'
    is_on_template: '{{ value_json is not none and value_json.state == "running" }}'

############# Prusa Bear MK2
  - platform: rest
    resource: http://{HA-Dockermon_IP:PORT}/container/bear_mk2
    name: Docker Octoprint Prusa Bear MK2
    body_on: '{"state": "start"}'
    body_off: '{"state": "stop"}'
    is_on_template: '{{ value_json is not none and value_json.state == "running" }}'

############# Prusa Bear MK3_1
  - platform: rest
    resource: http://{HA-Dockermon_IP:PORT}/container/bear_mk3_1
    name: Docker Octoprint Prusa Bear MK3_1
    body_on: '{"state": "start"}'
    body_off: '{"state": "stop"}'
    is_on_template: '{{ value_json is not none and value_json.state == "running" }}'

############# Prusa Bear MK3_2
  - platform: rest
    resource: http://{HA-Dockermon_IP:PORT}/container/bear_mk3_2
    name: Docker Octoprint Prusa Bear MK3_2
    body_on: '{"state": "start"}'
    body_off: '{"state": "stop"}'
    is_on_template: '{{ value_json is not none and value_json.state == "running" }}'

############# Prusa Mini
  - platform: rest
    resource: http://{HA-Dockermon_IP:PORT}/container/prusa_mini
    name: Docker Octoprint Prusa Mini
    body_on: '{"state": "start"}'
    body_off: '{"state": "stop"}'
    is_on_template: '{{ value_json is not none and value_json.state == "running" }}'

############# Hopeless Automations
  - platform: rest
    resource: http://{HA-Dockermon_IP:PORT}/container/hopeless_automations
    name: Docker Octoprint Hopeless Automations
    body_on: '{"state": "start"}'
    body_off: '{"state": "stop"}'
    is_on_template: '{{ value_json is not none and value_json.state == "running" }}'
{% endhighlight %}

If I have another instance of Docker running on another Device I will create similar file for that device.
