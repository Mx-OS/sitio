# GNUmakefile for MxOS Sitio

# Robust shell configuration
SHELL := /usr/bin/bash
.SHELLFLAGS := -ec

# Default goal
.DEFAULT_GOAL := all

# Executables
HUGO ?= hugo

# Source files to track dependencies for timestamp-based rebuilds
HUGO_SOURCES := $(shell find content assets layouts static themes hugo.yaml -type f 2>/dev/null)

# Phony targets (Action targets, not actual files on disk)
.PHONY: all dev clean help

all: public

# File-based target tracking site compilation
public: $(HUGO_SOURCES)
	$(HUGO)

# Development server with auto-reload/LiveReload (polling & full re-renders prevent rebuild storms/corruption)
dev:
	$(HUGO) server --watch --disableFastRender --poll 500ms

# Clean build directory
clean:
	rm -rf public

# Help target
help:
	@echo "MxOS website build targets:"
	@echo "  all    - Build the production site into 'public/' directory"
	@echo "  dev    - Start the local Hugo development server with LiveReload"
	@echo "  clean  - Delete the compiled 'public/' directory"
	@echo "  help   - Show this help menu"
