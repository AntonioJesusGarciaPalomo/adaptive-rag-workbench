FROM python:3.12-slim

WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    gcc \
    && rm -rf /var/lib/apt/lists/*

# Install Poetry
RUN pip install poetry

# Copy poetry files
COPY pyproject.toml ./

# Configure poetry: Don't create a virtual environment
RUN poetry config virtualenvs.create false

# Generate lock file and install dependencies
RUN poetry lock && poetry install --only=main --no-root

# # Install dependencies (without installing the current project)
# RUN poetry lock --no-update && poetry install --only=main --no-root

# Copy application code
COPY . .

# Expose port
EXPOSE 8000

# Run the application
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
