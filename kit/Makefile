GO ?= go
GO15VENDOREXPERIMENT = 1
COVERAGEDIR = coverage
BINARY = a.out

all: fmt build test cover
install-deps:
	glide install
fmt:
		find . -not -path "./vendor/*" -name '*.go' -type f | sed 's#\(.*\)/.*#\1#' | sort -u | xargs -n1 -I {} bash -c "cd {} && goimports -w *.go && gofmt -w -l -s *.go"
clean:
	$(GO) clean
	rm -f bin/
	rm -rf $(COVERAGEDIR)
build:
	if [ ! -d bin ]; then mkdir bin; fi
	$(GO) build -v -o bin/$(BINARY)
test:
	if [ ! -d $(COVERAGEDIR) ]; then mkdir $(COVERAGEDIR); fi
	$(GO) test -v . -cover -coverprofile=$(COVERAGEDIR)/main.coverprofile
cover:
	$(GO) tool cover -html=$(COVERAGEDIR)/main.coverprofile -o $(COVERAGEDIR)/main.html
