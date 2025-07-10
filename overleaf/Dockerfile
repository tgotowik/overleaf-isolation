FROM sharelatex/sharelatex:5.5.2

SHELL ["/bin/bash", "-cx"]

RUN apt-get update

WORKDIR /tmp

# Download Apptainer https://apptainer.org/docs/admin/main/installation.html
RUN wget https://github.com/apptainer/apptainer/releases/download/v1.4.1/apptainer_1.4.1_amd64.deb
RUN wget https://github.com/apptainer/apptainer/releases/download/v1.4.1/apptainer-suid_1.4.1_amd64.deb

# Install Apptainer and SUID helper
RUN apt-get install -y ./apptainer_1.4.1_amd64.deb
RUN dpkg -i ./apptainer-suid_1.4.1_amd64.deb
RUN rm -f apptainer_1.4.1_amd64.deb apptainer-suid_1.4.1_amd64.deb

# Backup original latexmk
RUN mv /usr/local/bin/latexmk /usr/local/bin/latexmkoriginal

# Copy proof-of-concept latexmk
COPY latexmk /usr/local/bin/latexmk
RUN chmod 777 /usr/local/bin/latexmk

CMD ["/bin/bash"]