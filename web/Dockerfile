FROM python:3.11-alpine as build-image

WORKDIR '/app'

COPY ./requirements.txt ./

RUN apk add --no-cache linux-headers g++ postgresql-dev gcc python3-dev musl-dev

RUN pip wheel --wheel-dir=/root/wheels -r requirements.txt



FROM python:3.11-alpine as production-image

WORKDIR '/app'

COPY --from=build-image /root/wheels /root/wheels

COPY --from=build-image /app/requirements.txt ./

RUN pip install --no-index --find-links=/root/wheels -r requirements.txt

RUN apk add --no-cache postgresql-dev

COPY ./ ./