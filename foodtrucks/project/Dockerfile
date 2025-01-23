# Use Alpine 3.11 for Python2 compatibility
FROM alpine:3.11

# Set environment variables to avoid prompts during installation
ENV PYTHONUNBUFFERED=1

# Install necessary packages
RUN apk add --no-cache \
    python2 \
    py2-pip \
    nodejs \
    npm \
    bash \
    curl \
    git

# Set the working directory
WORKDIR /app

# Copy the application code
COPY flask-app /app

# Navigate to the `flask-app` directory for Node.js setup
WORKDIR /app

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Install Node.js dependencies and build the frontend
WORKDIR /app
RUN npm install && npm run build

# Expose the Flask application's port
EXPOSE 5000

# Set the entrypoint to run the application
ENTRYPOINT ["python", "app.py"]
