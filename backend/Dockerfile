# FROM python:3.11-slim

# RUN pip install poetry

# WORKDIR /backend

# COPY pyproject.toml poetry.lock ./

# RUN poetry install 

# COPY . .


# CMD poetry run sh ./prestart.sh; poetry run uvicorn app.main:app --host 0.0.0.0

# Start with a base image that has Python 3.8
FROM python:3.11-slim

ENV POETRY_NO_INTERACTION=1 \
    POETRY_VIRTUALENVS_IN_PROJECT=1 \
    POETRY_VIRTUALENVS_CREATE=1 \
    POETRY_CACHE_DIR=/tmp/poetry_cache

# # Install system dependencies
RUN pip install poetry

# Set the working directory
WORKDIR /backend

# Copy only the pyproject.toml and poetry.lock files to leverage Docker cache
COPY . /backend/


# Install dependencies
RUN poetry install --without dev  && chmod +x ./prestart.sh && rm -rf $POETRY_CACHE_DIR


# Expose the port the app runs on
EXPOSE 8000

# Run the FastAPI application with Uvicorn
CMD ["poetry", "run", "uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]