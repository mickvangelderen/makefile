# This file serves as a proxy to any project-wide makefile. The project makefile will be executed in the current directory
PROJECT_MAKEFILE:=ProjectMakefile
PROJECT_DIR_PATTERN:=$(PROJECT_MAKEFILE)
# Searches up the file system until it finds directory containing $PROJECT_DIR_PATTERN.
# $PROJECT_DIR_PATTERN is a pattern and can be used like "PROJECT_DIR_PATTERN:=*.project".
PROJECT_DIR := $(shell \
	CURRENT_DIR="$$PWD"; LAST_DIR=""; \
	while [ "$$CURRENT_DIR" != "$$LAST_DIR" ]; do \
		ls "$$CURRENT_DIR/$(PROJECT_DIR_PATTERN)" >/dev/null 2>&1 && echo "$$CURRENT_DIR" && break; \
		LAST_DIR="$$CURRENT_DIR"; CURRENT_DIR=$$(dirname "$$CURRENT_DIR"); \
	done \
)

# A rule to match everything
.PHONY: default %
default %:
	@make -f "$(PROJECT_DIR)/$(PROJECT_MAKEFILE)" --directory . --no-print-directory $* || true

# default is required because % does not match ""
# || true is required because it allows the make to fail without, unlike prepending -, printing additional warnings/errors
# this works better then including because the relative paths in ProjectMakefile will be relative to the current directory