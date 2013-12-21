FROM linux/chef-solo

MAINTAINER Tom Eklöf tom@linux-konsult.com

# Expose the Postgresql port
EXPOSE 5432

RUN apt-get -y update

# Add postgres start script
ADD ./postgres.sh /postgres.sh

# Add chef files
ADD ./solo.rb /etc/chef/solo.rb
ADD ./node.json /etc/chef/node.json

# Add Berksfile to install cookbooks
ADD ./Berksfile /Berksfile

# Change the dbpassword string below to something good.
#RUN sed -i "s%md5sumhash%$(echo -n 'dbpassword%g''postgres' | openssl md5 | sed -e 's/.* /md5/')%g" /etc/chef/node.json
RUN sed -i "s%md5sumhash%$(echo -n 'dbpassword' | openssl md5 | sed -e 's/.* /md5/')%g" /etc/chef/node.json

# Install cookbooks defined in Berkshelf file
RUN /opt/chef/embedded/bin/berks install --path /etc/chef/cookbooks/

# Run cookbooks
RUN chef-solo

# Start the service
CMD ["/postgres.sh"]
