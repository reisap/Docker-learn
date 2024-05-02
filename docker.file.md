```docker
FROM python:3.12-rc-bookworm #[name image:version]

# Set the working directory in the container to /app
WORKDIR /app

COPY . /app

RUN pip install --no-cache-dir -r requirements.txt

# Set the environment variable for Flask
ENV FLASK_APP=app.py

# Add labels to the image
# LABEL Formatting Option 1
LABEL "com.example.vendor"="Big Star Collectibles"
LABEL version="1.0"
LABEL description="The Big Star Collectibles Website \
using the Python base image."


```

``` docker
FROM nginx:alpine
COPY ./index.html /usr/share/nginx/html/
COPY ./kineteco_scheduler_files /usr/share/nginx/html/schedule_files

```