# Use an official Python runtime as a parent image
FROM python:3.11.7-slim-bullseye
# Set environment variables
ENV PYTHONUNBUFFERED 1
ENV PYTHONDONTWRITEBYTECODE 1

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install system dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*
    
RUN python -m venv venv
RUN /bin/bash -c "source venv/bin/activate"

# Install any needed packages specified in requirements.txt
RUN pip3 install -r requirements.txt
RUN python3 manage.py migrate
RUN python3 manage.py makemigrations
#RUN python3 manage.py collectstatic --noinput
# Set the default command to run when the container starts
CMD ["python3", "manage.py", "runserver", "0.0.0.0:8000"]
