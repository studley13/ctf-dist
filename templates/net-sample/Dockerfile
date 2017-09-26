# Basic Xinetd Docker Container

FROM debian
MAINTAINER ctf@unswsecurity.com
ENTRYPOINT ["xinetd", "-dontfork"]

# Apt-get update
RUN apt-get update

# Install xinetd
RUN apt-get install -y xinetd gcc make
RUN update-rc.d xinetd disable

# Add the ctf dir
RUN mkdir /home/ctf
RUN chmod 775 /home/ctf

# Add the ctf user
RUN useradd -M -U\
    -d /home/ctf \
    ctf

RUN chown ctf:ctf /home/ctf

# Add the content
# The content.tar.bz2 will come from the 'content' directory'
ADD content.tar.bz2 /home/ctf/
RUN cp /home/ctf/xinetd.conf /etc/xinetd.conf
RUN chmod 775 /home/ctf/challenge

# Make the binary
RUN /home/ctf/makeproxy

# Expose the service port
EXPOSE 9091
