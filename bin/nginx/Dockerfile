FROM nginx:1.19.0

# Use non interactive mode to prevent TUI popups
ENV DEBIAN_FRONTEND noninteractive

# Update environment
RUN apt-get update -y && apt-get upgrade -y

# Install tools
RUN apt-get install -y vim

# Clean-up
RUN apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /myapp/