FROM python:3.10.2
# Last version check: 20 jan 2022. Newer versions may be available.

# Create non-root user (zero trust principle, least privileged principle)
RUN groupadd -g 1000 -r dev && \
    useradd -u 1000 -r -g dev -m -s $(which bash) dev
# Option '-m' to create home directory (see https://askubuntu.com/a/393470)
# Option '-s' to set shell for this user (see comment in https://askubuntu.com/a/393470)
# Option '-r' creates a system user which does not expire (see https://linuxize.com/post/how-to-create-users-in-linux-using-the-useradd-command/)

# How to add sudo support for the non-root user is described at https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user#_creating-a-nonroot-user
# However, standard practice is not to add sudo support for security reasons. VS Code will connect
# to the running dev container as the user specified in file ".devcontainer/devcontainer.json" in
# property "remoteUser". If you need to run commands as root to set up the dev container, use the
# "RUN" directive in Dockerfile or add suitable code to the script ".devcontainer/entrypoint.sh". 
# [Manfred, 16jan2022]

# Create working directory. Ownership will be changed in entrypoint.sh which
# executes *after* the volume has been mounted.
RUN mkdir /src

# Copy entrypoint script into container, make it executable, then make it the entrypoint for the
#  container:
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
# Option '+x' adds executable flag to the file
ENTRYPOINT ["/entrypoint.sh"]
