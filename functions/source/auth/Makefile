PROJECT = LaceworkCTAuth
DIR_NAME = auth
FUNCTION = $(PROJECT)
DIST_DIR ?= "$(BASE)"/functions/packages/$(DIR_NAME)

all: build

.PHONY: clean build

clean:
	rm -rf build
	rm $(DIST_DIR)/$(FUNCTION).zip || true

build: clean
	mkdir -p build
	cp ../common/* build
	buildid=$$(git describe --all --long | cut -d "/" -f 2); \
	sed -e "s|\$$BUILD|$$buildid|g" -e "s|\$$DATASET|$(HONEY_DATASET)|g" auth.py > build/auth.py
	pip3 install -r requirements.txt -t build
	cd build; zip -r $(DIST_DIR)/$(FUNCTION).zip . -x "*.DS_Store*" "*.git*" "build*" "Makefile"
	rm -rf build
