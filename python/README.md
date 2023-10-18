# Python FastAPI
````dockerfile
FROM python:3.8

WORKDIR /usr/app/

COPY . .

RUN pip3 install -r requirements.txt

EXPOSE 5000

CMD ["python3","entrypoint.py"]
````

---
# Python Django
````dockerfile
FROM python:3.8

WORKDIR /usr/app/

COPY . .

RUN pip3 install -r requirements.txt

EXPOSE 8000

CMD ["python3","manage.py","runserver","0.0.0.0:8000","--noreload"]
````
## Recordar modificar 
- ALLOWED_HOSTS
- CSRF_TRUSTED_ORIGINS
