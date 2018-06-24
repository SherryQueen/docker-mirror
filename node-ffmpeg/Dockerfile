FROM jrottenberg/ffmpeg:3.4-alpine as ffmpeg
LABEL author="56"

FROM node:8.11.3-alpine
COPY --from=ffmpeg / /
EXPOSE 3000
VOLUME [ "/app" ]

CMD [ "node" ]
