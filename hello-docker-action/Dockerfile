# Set the base image to use for subsequent instructions
FROM alpine:3.19

# Set the working directory inside the container
WORKDIR /hello-docker-action

# Copy any source file(s) required for the action
COPY entrypoint.sh .

# Configure the container to be run as an executable
ENTRYPOINT ["/hello-docker-action/entrypoint.sh"]
