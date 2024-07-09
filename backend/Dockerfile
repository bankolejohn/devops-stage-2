# ./backend/Dockerfile

# Use an official Python image as the base image
FROM python:3.9

# Set the working directory
WORKDIR /app

# Install Poetry
RUN curl -sSL https://install.python-poetry.org | python3 -

# Add Poetry to PATH
ENV PATH="/root/.local/bin:${PATH}"

# Copy the pyproject.toml and poetry.lock files
COPY pyproject.toml poetry.lock* /app/

# Install dependencies
RUN poetry install --no-root

# Copy the rest of the application code
COPY . .

# Ensure prestart.sh is executable
RUN chmod +x ./prestart.sh

# Run the prestart script to set up the database
RUN poetry run bash ./prestart.sh

# Expose port 8000
EXPOSE 8000

# Start the FastAPI application using uvicorn
CMD ["poetry", "run", "uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
