# Use the latest slim Python image as the base image
FROM python:slim@sha256:5dc6f84b5e97bfb0c90abfb7c55f3cacc2cb6687c8f920b64a833a2219875997

# Set the environment variable to not buffer Python outputs
ENV PYTHONUNBUFFERED 1

# Set an argument for the app directory
ARG APP=/app
WORKDIR $APP
VOLUME $APP

# Install system dependencies and clean up apt cache
RUN apt-get update \
    && apt-get install --no-install-recommends -y \
        gcc \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/*

# Copy the requirements.txt file and install Python dependencies
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

# Set the default command to run the Django server
CMD ["./manage.py", "runserver", "0:3000"]

# Expose the Django server port
EXPOSE 3000
