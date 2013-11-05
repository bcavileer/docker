# Docker container with chef-solo & berkshelf
FROM ubuntu
#FROM base
MAINTAINER Tom Eklöf "tom@linux-konsult.com"

RUN apt-get -y update
# Install Chef
RUN apt-get -y install curl build-essential libxml2-dev libxslt-dev git
RUN curl -L https://www.opscode.com/chef/install.sh | bash
RUN echo "gem: --no-ri --no-rdoc" > ~/.gemrc
# Add latest default chef-solo config file
ADD https://raw.github.com/proppen/docker/master/linux/chef-solo/solo.rb /solo.rb

# Install Berkshelf with chef's own ruby
RUN /opt/chef/embedded/bin/gem install berkshelf

