REPO = repo
APP = $(patsubst %.json,%,$(wildcard *.json))
VER = stable

all: app
build: app
app: $(APP)

test:
	@echo $(APP:%=%.bundle)

uninstall:
	@flatpak --user uninstall $(APP)

install: build
	@flatpak --user install --bundle $(APP:%=%.flatpak)

reinstall: uninstall install

clean:
	@rm -rf app repo .flatpak-builder $(APP:%=%.flatpak)


%: %.json
	@rm -rf app
	@echo $@
	@flatpak-builder --ccache --require-changes --repo=$(REPO) --subject="Build of $@ `date`" ${EXPORT_ARGS} app $<
	@flatpak build-bundle repo $(patsubst %.json,%.flatpak,$<) $@ $(VER)

.PHONY: all clean test uninstall install build
