# Use an official Python runtime as a parent image
FROM python:3.11

# Set environment variables for Python
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy the requirements file into the container at /usr/src/app/
COPY ./requirements.txt /usr/src/app/

# Install any needed packages specified in requirements.txt
RUN apt-get update -y \
    && apt-get install -y postgresql libpq-dev gcc \
    && pip install --no-cache-dir -r requirements.txt \
    && apt-get remove -y gcc libpq-dev \
    && apt-get autoremove -y

# Copy the current directory contents into the container at /usr/src/app/
COPY . /usr/src/app/

# Run database migrations and start the application
CMD ["sh", "-c", "python manage.py migrate && python manage.py runserver 0.0.0.0:8000"]