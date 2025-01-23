# Stage 1: Build Stage
FROM python:2.7-alpine as builder

# Set environment variables to avoid prompts during installation
ENV PYTHONUNBUFFERED=1

# Install build tools and dependencies
RUN apk add --no-cache gcc musl-dev libffi-dev make

# Set the working directory
WORKDIR /app

# Copy application code and dependencies
COPY requirements.txt /app/
COPY flask-app /app/

# Install Python dependencies
RUN pip install --prefix=/install --no-cache-dir -r requirements.txt

# Copy static files to the host
RUN cp -r /app/static /static && cp -r /app/templates /templates

# Stage 2: Production Stage
FROM python:2.7-alpine

# Copy only the installed dependencies and application code
COPY --from=builder /install /usr/local
COPY flask-app /app
RUN rm -r /app/static /app/templates

# Set the working directory
WORKDIR /app

# Expose the Flask application's port
EXPOSE 5000

# Set the entrypoint to run the application
ENTRYPOINT ["python", "app.py"]
