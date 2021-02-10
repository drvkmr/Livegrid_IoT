FROM debian:buster-slim

RUN apt-get -q update && apt-get install -yq --no-install-recommends \
	build-essential \
	&& apt-get clean && rm -rf /var/lib/apt/lists/*

# Uncomment the following if your binary requires additional dependencies
# RUN apt-get update && apt-get install -y libgraphicsmagick++-dev libwebp-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev mono-complete \
# curl \
# && rm -rf /var/lib/apt/lists/*

WORKDIR /usr/src/app

COPY . /usr/src/app

RUN make -C /usr/src/app/draft_codes

# CMD ./examples-api-use/demo -D0 --led-rows=32 --led-cols=64 --led-slowdown-gpio=2 --led-gpio-mapping=adafruit-hat-pwm

CMD ./draft_codes/noise --led-rows=32 --led-cols=64 --led-slowdown-gpio=2 --led-limit-refresh=240