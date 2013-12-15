# Docker container with chef-solo & berkshelf
FROM ubuntu
MAINTAINER Tom Eklöf "tom@linux-konsult.com"

# Add latest default chef-solo config files
ADD linux/chef-solo/solo.rb /etc/chef/solo.rb
ADD linux/chef-solo/node.json /etc/chef/node.json

RUN apt-get -y update

# Install Chef
RUN apt-get -y install curl build-essential libxml2-dev libxslt-dev git
RUN curl -L https://www.opscode.com/chef/install.sh | bash
RUN echo "gem: --no-ri --no-rdoc" > ~/.gemrc


# Install Berkshelf with chef's own ruby
RUN /opt/chef/embedded/bin/gem install berkshelf
