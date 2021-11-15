FROM alpine as build

RUN apk add --no-cache \
	gcc \
	g++ \
	make \
	git \
	cvs \
	zlib-dev

RUN cvs -d :pserver:cvs@cvs.fefe.de:/cvs -z9 co libowfat \
	&& cd libowfat \
	&& make

RUN git clone git://erdgeist.org/opentracker \
		&& cd opentracker \
                && sed -i 's/#FEATURES+=-DWANT_ACCESSLIST_WHITE/FEATURES+=-DWANT_ACCESSLIST_WHITE/' Makefile \
		&& make

FROM alpine

COPY --from=build opentracker/opentracker /usr/bin/opentracker

EXPOSE 6969

CMD ["opentracker", "-f", "/etc/opentracker/opentracker.conf"]
