FROM ubuntu

MAINTAINER Tom Eklöf tom@linux-konsult.com

RUN apt-get -y update

### Install Chef
RUN apt-get -y install curl build-essential libxml2-dev libxslt-dev git
RUN curl -L https://www.opscode.com/chef/install.sh | bash
RUN echo "gem: --no-ri --no-rdoc" > ~/.gemrc

# Add chef files
ADD ./solo.rb /etc/chef/solo.rb
ADD ./node.json /etc/chef/node.json

# Add Berksfile to install cookbooks
ADD ./Berksfile /Berksfile


### Configuration ###
# Change the dbpassword string below to something good.
RUN sed -i "s%md5sumhash%$(echo -n 'dbpassword%g''postgres' | openssl md5 | sed -e 's/.* /md5/')%g" /etc/chef/node.json

### /Configuration ###

# Install Berkshelf and cookbooks
RUN /opt/chef/embedded/bin/gem install berkshelf
RUN /opt/chef/embedded/bin/berks install --path /etc/chef/cookbooks/

# Run cookbooks
RUN chef-solo
