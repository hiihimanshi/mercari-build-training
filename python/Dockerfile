FROM python:3.9-alpine
RUN apk add --no-cache python3 py3-pip

# Create user and group
RUN addgroup -S mercari && adduser -S trainee -G mercari

WORKDIR /app

# Create the images folder with proper permissions
RUN mkdir -p /app/images && chown -R trainee:mercari /app/images

# Switch to non-root user
USER trainee

# Install dependencies (layer 1)
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

# Copy rest of code (layer 2)
COPY main.py ./
COPY db/items.sql ./db/items.sql

# Run backend
CMD ["python3", "-m", "uvicorn", "main:app", "--host", "0.0.0.0", "--port", "9000"]
