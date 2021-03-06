BIN := ../../node_modules/.bin
JEST := $(BIN)/jest
FOHM := $(BIN)/fohm
FABLE_SPLITTER := $(BIN)/fable-splitter

# -- TASKS ------------------------------------------------------------
.PHONY: help
help:
	@echo "Building:"
	@echo "---------"
	@echo "  build              Compiles the project"
	@echo "  build-tests        Compiles the tests"
	@echo "  build-grammars     Compiles the grammar files"
	@echo ""
	@echo "Testing:"
	@echo "--------"
	@echo "  test               Compiles and runs the tests"
	@echo "  test-watch-build   Continuously compiles the tests"
	@echo "  test-watch-run     Continuously runs the tests"
	@echo ""
	@echo "Cleaning up:"
	@echo "------------"
	@echo "  distclean          Cleans up built artifacts"
	@echo "  clean              Cleans up the source folders"


.PHONY: build
build: build-grammars
	$(FABLE_SPLITTER) --config src/splitter.config.js

.PHONY: build-tests
build-tests: build-grammars
	$(FABLE_SPLITTER) --config test/splitter.config.js

.PHONY: build-grammars
build-grammars:
	$(FOHM) compile language/Purr.ohm --outDir src/Generated --name PurrGrammar

.PHONY: test
test: build-tests run-tests

.PHONY: run-tests
run-tests:
	$(JEST)

.PHONY: test-watch-build
test-watch-build: build-grammars
	$(FABLE_SPLITTER) --config test/splitter.config.js --watch

.PHONY: test-watch-run
test-watch-run:
	$(JEST) --watch

.PHONY: distclean
distclean:
	rm -rf build