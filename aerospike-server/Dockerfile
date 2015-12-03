#
# Aerospike Server Dockerfile
#
# http://github.com/aerospike/aerospike-server.docker
#

FROM debian:7

# Install Aerospike
RUN \
  apt-get update -y \
  && apt-get install -y wget logrotate ca-certificates \
  && wget "http://browser.qe.aerospike.com/citrusleaf/aerospike-server/3.6.4-275-ge4364d7/build/debian-7/community/artifacts/aerospike-server-community-3.6.4-275.debian7.x86_64.deb" \
  && dpkg -i aerospike-server-*.deb \
  && apt-get purge -y --auto-remove wget ca-certificates \
  && rm -rf aerospike-server*.deb aerospike /var/lib/apt/lists/*

# Add the Aerospike configuration specific to this dockerfile but provide a volume mount point so it can be overriden
VOLUME ["/etc/aerospike/"]
ADD aerospike.conf /etc/aerospike/aerospike.conf

# Mount the Aerospike data directory
VOLUME ["/opt/aerospike/data"]

# Expose Aerospike ports
#
#   3000 – service port, for client connections
#   3001 – fabric port, for cluster communication
#   3002 – mesh port, for cluster heartbeat
#   3003 – info port
#
EXPOSE 3000 3001 3002 3003

# Execute the run script in foreground mode
ENTRYPOINT ["/usr/bin/asd"]
CMD ["--foreground"]