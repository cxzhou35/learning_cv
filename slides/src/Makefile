LECNO = 0
FLAGS = --scripts https://cdn.tonycrane.cc/heti/heti.js,heti_worker.js --template template.html
BASE_DIR = ../site/2023-fall-pbfx

.PHONY: live build all clean live-home build-home

live:
	@echo "Previewing lec$(LECNO) slides..."
	-@reveal-md lec$(LECNO).md -w $(FLAGS) || true

build:
	@echo "Building lec$(LECNO) slides..."
	@reveal-md lec$(LECNO).md $(FLAGS) --static $(BASE_DIR)/lec$(LECNO) --assets-dir assets
	@mkdir -p $(BASE_DIR)/pdfs
	@rm $(BASE_DIR)/lec$(LECNO)/lec$(LECNO).html
	@cp -r assets/lec$(LECNO) $(BASE_DIR)/lec$(LECNO)/
	@if [ -f pdfs/lec$(LECNO).pdf ]; then \
		cp pdfs/lec$(LECNO).pdf $(BASE_DIR)/pdfs/lec$(LECNO).pdf; \
	fi

live-home:
	@echo "Previewing home slides..."
	-@reveal-md home.md -w $(FLAGS) || true

build-home:
	@echo "Building home slides..."
	@reveal-md home.md $(FLAGS) --static $(BASE_DIR) --assets-dir assets
	@rm $(BASE_DIR)/home.html

all:
	@echo "Building all slides..."
	@make build-home
	@for i in `seq 0 6`; do \
		make LECNO=$$i build; \
	done

clean:
	@echo "Cleaning up..."
	rm -rf ../site/
