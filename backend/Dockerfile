# Base image with Python 3.12 and dependencies
FROM tiangolo/uvicorn-gunicorn-fastapi:python3.10

# Set the working directory to /app
WORKDIR /app

# Install curl
RUN apt-get update && apt-get install -y curl

# Install Poetry
RUN curl -sSL https://install.python-poetry.org | python3 -

# Add Poetry bin directory to PATH
ENV PATH="/root/.local/bin:$PATH"

# Copy only requirements to cache them in docker layer
COPY .env ./
COPY pyproject.toml poetry.lock ./

# Install dependencies
RUN poetry install

# Copy the rest of the application code
COPY . .

EXPOSE 8000

