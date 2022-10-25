FROM python:3.10-slim

ENV PYTHONUNBUFFERED 1

RUN apt update && apt install git libxml2 libxml2-dev libxslt-dev gcc python3-dev musl-dev -y

RUN mkdir -p /code && \
    mkdir -p /code/public/static && \
    mkdir -p /code/public/media

COPY Pipfile Pipfile.lock /code/

WORKDIR /code

RUN pipenv install --system

COPY backend /code/backend/
COPY frontend /code/frontend/

COPY ./run.sh /code/
COPY ./uwsgi.ini /code/

RUN mkdir -p /var/log/uwsgi/

WORKDIR /code/backend/

EXPOSE 8080
