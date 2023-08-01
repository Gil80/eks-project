FROM python:alpine
ENV PYTHONUNBUFFERED=1
RUN apk add --update --no-cache python3 && ln -sf python3 /user/bin/python
RUN python3 -m ensurepip
RUN pip3 install --no-cache --upgrade pip setuptools

# create and activate virtual env
# using final folder name to avoid path issues with packages

RUN python3 -m venv /home/gil/venve
ENV VIRTUAL_ENV=/home/gil/venve
ENV PATH="home/gil/venve/bin:$PATH"
RUN source /home/gil/venve/bin/activate

# create user without password
RUN adduser gil -D

WORKDIR /home/gil/app

COPY requirements.txt .

# install bash
RUN apk add --no-cache bash

# install all the requirements
RUN python3 -m pip install --upgrade pip
RUN pip3 install -r requirements.txt

# copy all the flask project files into the workdir
COPY . .

# expose the port 5000 of the docker container
EXPOSE 5000

# exexcute the flask app inside the container
CMD python3 app.py
