# Install Atlassian Jira
FROM proppen/java7

MAINTAINER Tom Eklöf tom@linux-konsult.com

# Fetch the Jira binary
RUN wget --directory-prefix=/opt http://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-6.1.2-x64.bin

# Fetch the unattended answer file
RUN wget --directory-prefix=/opt https://raw.github.com/proppen/docker/master/atlassian/jira/response.varfile

# Unattended Jira install
RUN sh /opt/atlassian-jira-6.1.2-x64.bin -q -varfile /opt/response.varfile

EXPOSE 8080
