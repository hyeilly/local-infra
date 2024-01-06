# Flask API
ARG PYTHON_VERSION
FROM python:${PYTHON_VERSION}

RUN apt-get update \
    && apt upgrade -y \
    && apt install python3-pip -y \
    && apt install build-essential python3-dev

COPY . /var/www
WORKDIR /var/www/hani-serving-data

COPY ./requirements.txt /var/www/hani-serving-data/requirements.txt

RUN pip install --upgrade pip
RUN pip install -r requirements.txt


CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]