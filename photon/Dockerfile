FROM rtuszik/photon-docker:latest

# Switch to root to set up wrapper script and permissions
USER root

# Copy wrapper entrypoint script
COPY run.sh /run.sh
RUN chmod a+x /run.sh

# Set the wrapper script as the entrypoint
ENTRYPOINT ["/run.sh"]
