# munin-bukkit-plugins

This repository contains some useful [Munin](http://munin-monitoring.org/) plugins to monitor and observe a [Bukkit](http://bukkit.org) server:

* **bukkit-jsonapi-players** - players currently online
* **bukkit-jsonapi-ramusage** - RAM usage
* **bukkit-jsonapi-tps** - TPS (ticks per second)
* **bukkit-statistician-killshostile** - hostile mob kills
* **bukkit-statistician-killsneutral** - neutral mob kills
* **bukkit-statistician-killspassive** - passive mob kills
* **bukkit-statistician-players** - new players per day
* **bukkit-ultrabans-shame** - kicks/bans/mutes/etc. per day

bukkit-jsonapi-* requires [JSONAPI](https://github.com/alecgorge/jsonapi/)  
bukkit-statistician-* requires [Statistician](http://dev.bukkit.org/server-mods/statisticianv2/)  
bukkit-ultrabans-* requires [Ultrabans](http://dev.bukkit.org/server-mods/ultrabans/)  

Read more in my [blog post](http://blog.frd.mn/munin-bukkit-plugins/).

## Requirements

* Web server with `PHP` support and Munin (2)
* Bukkit server with JSONAPI for the JSONAPI plugins (`bukkit-jsonapi-*`)
* Bukkit server with Ultrabans for the Ultrabans plugins (`bukkit-ultrabans-*`)
* Bukkit server with Statistician for the MySQL plugins  (`bukkit-statistician-*`)
* MySQL server for the SQL plugins

## Configuration

1. Clone this repository: `git clone git@github.com:frdmn/munin-bukkit-plugins.git`
1. Adjust the JSONAPI variables in the bukkit-jsonapi-* files
1. Adjust the MySQL variables in the mcsql* files
1. Make sure the `PHP` binary in the Shebang line is executable

## Installation

1. Perform your configuration (see above)
1. Move the plugins into the Munin plugin directory: `mv mc* /usr/share/munin/plugins/`
1. Change the ownership: `chown munin:munin /usr/share/munin/plugins/mc*`
1. Make sure they are exectuable: `chmod 755 /usr/share/munin/plugins/mc*`
1. Enable the plugins: `ln -s /usr/share/munin/plugins/mc* /etc/munin/plugins/`
1. Restart your munin-node: `service munin-node restart`
1. Run your cron: `su - munin --shell=/bin/sh -c /usr/bin/munin-cron`

## Alerts and limits?

To setup alerts and limits add the following lines in your specific node in the `munin.conf` file:

	[obi-wan.yeahwh.at]
	   address 5.9.115.5
	   [...]
	   mctps_main.warning 19.9:      # Warning alert on < 19.9
	   mctps_main.critical 19:		# Critical alert on < 19.0
	   mcplayer_main.warning 20		# Warning alert when there are 20 players online
	   mcplayer_main.critical 30		# Critical alert when there are more than 30 players online

## License

[WTFPL](LICENSE)
