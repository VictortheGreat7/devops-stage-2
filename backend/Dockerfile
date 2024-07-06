# Base image with Python 3.8 and dependencies
FROM python:3.12-slim

# Set working directory
WORKDIR /app

# Install curl and other necessary packages
RUN apt-get update && apt-get install -y curl

# Install Poetry
RUN curl -sSL https://install.python-poetry.org | python3 -

# Add Poetry bin directory to PATH
ENV PATH="/root/.local/bin:$PATH"

# Copy .env file (optional, for environment variables)
COPY .env ./

# Copy poetry.lock (essential for Poetry dependency management)
COPY pyproject.toml poetry.lock ./

# Install dependencies using Poetry
RUN poetry install --no-interaction

# Copy remaining backend code (including main.py)
COPY . .

# Expose port for FastAPI app
EXPOSE 8000

# Start command (using Poetry to run uvicorn)
CMD ["bash", "-c", "poetry run bash ./prestart.sh && poetry run uvicorn app.main:app --reload"]

