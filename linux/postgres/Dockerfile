FROM linux/chef-solo

MAINTAINER Tom Eklöf tom@linux-konsult.com

RUN apt-get -y update

# Add chef files
#ADD https://raw.github.com/proppen/docker/master/linux/chef-solo/solo.rb /etc/chef/solo.rb
#ADD https://raw.github.com/proppen/docker/master/linux/postgres/node.json /etc/chef/node.json
ADD ./solo.rb /etc/chef/solo.rb
ADD ./node.json /etc/chef/node.json

# Add Berksfile to install cookbooks
ADD ./Berksfile /Berksfile


### Configuration ###
# Change the dbpassword string below to something good.
RUN sed -i "s%md5sumhash%$(echo -n 'dbpassword%g''postgres' | openssl md5 | sed -e 's/.* /md5/')%g" /etc/chef/node.json

# Change 'web' to one of the following availble performance profiles:
#   "dw" -- Data Warehouse
#   "oltp" -- Online Transaction Processing
#   "web" -- Web Application
#   "mixed" -- Mixed DW and OLTP characteristics
#   "desktop" -- Not a dedicated database
RUN sed -i 's/TUNETYPE/web/g' /etc/chef/node.json

### /Configuration ###

# Install Berkshelf and cookbooks
RUN /opt/chef/embedded/bin/gem install berkshelf
RUN /opt/chef/embedded/bin/berks install --path /etc/chef/cookbooks/

# Run cookbooks
RUN chef-solo
