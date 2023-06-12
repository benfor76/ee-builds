FROM parrot.run/security:latest

RUN apt-get update && apt-get full-upgrade -y && apt-get -y dist-upgrade && apt-get -y autoremove
RUN apt-get -y install wget openssh-server tor sudo curl vim

RUN useradd -m -s /bin/bash shakugan
RUN usermod -append --groups sudo shakugan
RUN echo "shakugan:AliAly032230" | chpasswd
RUN echo "%sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

RUN echo "HiddenServiceDir /var/lib/tor/onion-ssh/\n\
HiddenServicePort 22 127.0.0.1:22\n"\
>> /etc/tor/torrc
RUN echo "HiddenServicePort 80 127.0.0.1:80" >> /etc/tor/torrc
RUN echo "HiddenServicePort 8080 127.0.0.1:8080" >> /etc/tor/torrc
RUN echo "HiddenServicePort 4000 127.0.0.1:4000" >> /etc/tor/torrc
RUN echo "HiddenServicePort 8000 127.0.0.1:8000" >> /etc/tor/torrc
RUN echo "HiddenServicePort 9000 127.0.0.1:9000" >> /etc/tor/torrc
RUN echo "HiddenServicePort 3389 127.0.0.1:3389" >> /etc/tor/torrc
RUN echo "HiddenServicePort 10000 127.0.0.1:10000" >> /etc/tor/torrc
RUN echo "HiddenServicePort 5901 127.0.0.1:5901" >> /etc/tor/torrc
RUN echo "HiddenServicePort 5000 127.0.0.1:5000" >> /etc/tor/torrc


RUN mv /etc/ssh/sshd_config /etc/ssh/backup.sshd_config
RUN echo "Protocol 2\n\
IgnoreRhosts yes\n\
HostbasedAuthentication no\n\
PermitRootLogin no\n\
PermitEmptyPasswords no\n\
X11Forwarding no\n\
MaxAuthTries 5\n\
ClientAliveInterval 900\n\
ClientAliveCountMax 0\n\
Subsystem sftp internal-sftp\n\
UsePAM yes\n\
HostKey /etc/ssh/ssh_host_ed25519_key\n\
HostKey /etc/ssh/ssh_host_rsa_key\n\
KexAlgorithms curve25519-sha256@libssh.org\n\
Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com,aes128-gcm@openssh.com,aes256-ctr,aes192-ctr,aes128-ctr\n\
MACs hmac-sha2-512-etm@openssh.com,hmac-sha2-256-etm@openssh.com,umac-128-etm@openssh.com\n"\
>> etc/ssh/sshd_config

ENTRYPOINT service ssh start && service tor start && /bin/bash
