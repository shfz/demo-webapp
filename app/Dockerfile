FROM python:alpine

WORKDIR /app

RUN pip install -U flask PyMySQL shfzflask

COPY ./ /app

CMD ["python", "main.py"]
