BUNDLER_VERSION = 1.15.1
BUNDLE = bundle _${BUNDLER_VERSION}_
JEKYLL = ${BUNDLE} exec jekyll

dev:
	code .
	open http://localhost:4000
	make serve

clean:
	rm -rf _site local-generated generated_site

setup:
	gem install bundler \
		-v ${BUNDLER_VERSION} \
		--no-rdoc \
		--no-ri
	NOKOGIRI_USE_SYSTEM_LIBRARIES=true ${BUNDLE} install \
		--path vendor/bundle

build: clean
	${JEKYLL} build \
		--config _config.yml

apache: clean
	JEKYLL_ENV=production ${JEKYLL} build \
		--config _config.yml,_config.apache.yml

javadoc:
	scripts/javadoc-gen.sh "all"

latest_javadoc:
	scripts/javadoc-gen.sh "latest"

staging: clean
	${JEKYLL} build --config _config.yml,_config.staging.yml

serve: build
	${JEKYLL} serve \
		--incremental \
		--config _config.yml,_config.local.yml

publish: javadoc-gen build
