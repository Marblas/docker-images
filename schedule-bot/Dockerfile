FROM python:3.9@sha256:7e2a5829970d072caac429607271c838cd83715e8f77867cb5f30b7e13a3835d
COPY ./requirements.txt .
RUN pip install -r ./requirements.txt
COPY ./lib .
CMD ["python", "main.py"]