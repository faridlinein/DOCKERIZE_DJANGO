# For more information, please refer to https://aka.ms/vscode-docker-python
FROM python:3.8.0-alpine

# set work directory
WORKDIR /usr/src/app

# Keeps Python from generating .pyc files in the container
ENV PYTHONDONTWRITEBYTECODE 1
# Turns off buffering for easier container logging
ENV PYTHONUNBUFFERED 1

# install psycopg2 dependencies
RUN apk update \
    && apk add postgresql-dev gcc python3-dev musl-dev

# Install pip requirements
RUN pip install --upgrade pip
COPY ./requirements.txt /usr/src/app/requirements.txt
RUN python -m pip install -r requirements.txt

# copy entrypoint.sh
COPY ./entrypoint.sh /usr/src/app/entrypoint.sh

# copy project
COPY . /usr/src/app/

# run entrypoint.sh
ENTRYPOINT ["/usr/src/app/entrypoint.sh"]

# During debugging, this entry point will be overridden. For more information, refer to https://aka.ms/vscode-docker-python-debug
# File wsgi.py was not found in subfolder:DOCKERIZE_DJANGO. Please enter the Python path to wsgi file.
# CMD ["gunicorn", "--bind", "0.0.0.0:8000", "pythonPath.to.wsgi"]
# CMD ["gunicorn", "--bind", "0.0.0.0:8000", "web\config\wsgi.py"]
