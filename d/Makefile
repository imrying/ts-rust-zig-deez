##
# Static part, don't change these:
##



help:
	@cat Makefile | grep -E "^\w+$:"

ready: fmt lint test

docker-build:
	docker build --no-cache . -t deez_$(notdir $(shell pwd))

docker-ready: docker-build
	docker run -v $(shell pwd):/deez -t deez_$(notdir $(shell pwd))

DC:=dmd
DFILES:=$(shell find src/ -name "*.d" -type f)
DFLAGS+=-preview=dip1000

fmt:
	@echo "===> Formatting"
	dfmt -i $(DFILES)

lint:
	@echo "===> Linting"
	dscanner -s $(DFILES)

test:
	@echo "===> Testing"
	$(DC) $(DFLAGS) -main -unittest -Isrc/ -of=unittest $(DFILES)
	./unittest

build:
	@echo "===> Building"
	$(DC) $(DFLAGS) -lib -of=deez $(DFILES)

prog:
	@echo "===> Building progam"
	$(DC) $(DFLAGS) $(DFILES) -of=deez
	