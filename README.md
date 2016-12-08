# ngxPy
## NGINX Plus Status API Python Wrapper

ngxPy is a python wrapper built for the nginx plus status dashboard.

### How to use ngxPy

Several ways you can create a new instance. By using the parameters available
```
n = ngxpy.ngxpy(host='192.168.99.100', port=8080)
```

Or create an `~/.ngxpy.ini` file 

```
nDefault = ngxpy.ngxpy(cfgSec='default')
nLb1 = ngxpy.ngxpy(cfgSec='lb1')
```

Example of `~/.ngxpy.ini`

```
[default]
schema = http
host = 127.0.0.2
port = 8080
status = status
upstreamConf = upstream_conf

[lb1]
host = 192.168.99.100
port = 8080
```

Pulling status data
```
# All status for a specific instance
print nLb1.get_status()

# Status for upstream servers only
upstreams = nLb1.get_upstreams()

# Number of peers in a upstream group
print nLb1.num_of_peers(upstream_name)
print nLb1.num_of_peers('backend')

# By default, calls will look up http blocks, to look up streams
print nLb1.num_of_peers(upstream_name, isHttp=False)
print nLb1.num_of_peers('backend', isHttp=False)

# Peer stats
print nLb1.get_peer_stats('backend')
# You can also specify a peer ID
print nLb1.get_peer_stats('backend', peer_id=1)

# Cache stats
print n2.get_caches()['mycache']
```
