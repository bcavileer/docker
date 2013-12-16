# Install Atlassian Jira
FROM proppen/java7

MAINTAINER Tom Eklöf tom@linux-konsult.com

# Fetch the Jira binary
ADD http://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-6.1.2-x64.bin /opt/

# Fetch the unattended answer file
ADD ./response.varfile /opt/response.varfile

# Unattended Jira install
RUN sh /opt/atlassian-jira-6.1.2-x64.bin -q -varfile /opt/response.varfile

# Remove the file
RUN rm -f /opt/atlassian-jira-6.1.2-x64.bin

EXPOSE 8080

# Start the service
CMD ["/etc/init.d/jira", "start"]
