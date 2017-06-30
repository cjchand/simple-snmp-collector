# Overview

This is a *very* simple docker-compose setup with InfluxDB, Telegraf, and Grafana specifically targeted at grabbing SNMP metrics. It's good to have data when you call `$YOUR_INTERNET_PROVIDER` and ask for a refund :)

I just cooked this up after dinner one night, so don't expect much. As it stands, this supports SNMPv2 only, as that's all my ghetto home router supports. It shoudl go without saying that this is really only acceptable for personal use inside a closed network.

Speaking of not letting the Internet snoop on your router, if you want to use SNMPv3, config file is in `/telegraf` with the SNMP bits at the top. Modify it to your heart's content (and submit a PR if you do it in a reusable fashion).

Grafana lives at [http://localhost:3000](). Login with `admin/secret`. Should you want to change the password for Grafana, there's an environment variable in `docker-compose.yml` to do that.

InfluxDB's endpoint lives at [http://localhost:8086]().

# Configuration

There's not much config here. It's just 3 environment variables that live in the `docker-compose.yml`:

1. `SNMP_HOST`
2. `SNMP_PORT`
3. `SNMP_COMMUNITY`

I presume those are self-explanatory enough.

If you're new to Grafana, [check out here](http://docs.grafana.org/features/datasources/influxdb/) for how to get it to talk to InfluxDB. 

Also, while my router only supports MIBs that most any other device should support, I'll slap a YMMV disclaimer. You might have to - or want to - modify `./telegraf.conf` to use more/different MIBs. I found the [Telegraf example for the SNMP input](https://github.com/influxdata/telegraf/blob/master/plugins/inputs/snmp/CONFIG-EXAMPLES.md) to be pretty lacking, but eventually hacked my way through it. Just know that it's not the most intuitive thing in the universe once it comes time to map attributes to tags, etc.

# To-Dos

Once I get a dashboard setup that I like, I'll automate getting the Data Source setup and bake in that dashboard. It all depends on if it ends up being generic  enough to be useful. 
