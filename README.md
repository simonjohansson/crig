# Intro
Want to try collectd -> Riemann -> InfluxDB <- Grafana ?

Yeah, me too!

	docker-compose up

Wiiiieee!

# Note

Due to some ehm, shortcomings[1] in docker-compose and collectd there is
some static config that needs to be adapted for your environment.

In docker-compose.yml you need to change INFLUXDB_HOST to be your
host IP.

In collectd/config/collectd.conf you need to change Host to your host IP.

Also, if you do docker-compose stop/kill you need to do a
docker-compose rm before doing a docker-compose up again. Otherwise
InfluxDB will ONLY listen on 127.0.0.1 on your host, not host IP or
0.0.0.0. How very weird!

[1]
docker-compose, one cannot say

	environment:
		INFLUXDB_HOST: $SOME_ENV_VARIABLE_EXPOSED_FROM_A_LINKED_CONTAINER

collectd cannot read from env-variables in the config.
