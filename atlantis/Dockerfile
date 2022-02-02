FROM runatlantis/atlantis:v0.17.4

ARG TERRAGRUNT=0.34.3
ARG TERRAGRUNT_ATLANTIS_CONFIG=1.9.2

###
### Ensure Terragrunt version is present and validated
###
RUN set -eux \
	&& if [ "${TERRAGRUNT}" = "latest" ]; then \
		TERRAGRUNT="$( \
			curl -L -sS https://github.com/gruntwork-io/terragrunt/releases \
			| tac | tac \
			| grep -Eo '"/gruntwork-io/terragrunt/releases/tag/v?[0-9]+\.[0-9]+\.[0-9]+"' \
			| grep -Eo '[0-9]+\.[0-9]+\.[0-9]+' \
			| sort -V \
			| tail -1 \
		)"; \
	fi \
	&& curl -L -sS "https://github.com/gruntwork-io/terragrunt/releases/download/v${TERRAGRUNT}/terragrunt_linux_amd64" -o /usr/local/bin/terragrunt \
	&& chmod +x /usr/local/bin/terragrunt \
	&& terragrunt --version | grep "v${TERRAGRUNT}"

###
### Install https://github.com/transcend-io/terragrunt-atlantis-config
###
RUN set -eux \
    && wget https://github.com/transcend-io/terragrunt-atlantis-config/releases/download/v${TERRAGRUNT_ATLANTIS_CONFIG}/terragrunt-atlantis-config_${TERRAGRUNT_ATLANTIS_CONFIG}_linux_amd64.tar.gz \
    && tar xf terragrunt-atlantis-config_${TERRAGRUNT_ATLANTIS_CONFIG}_linux_amd64.tar.gz \
    && mv terragrunt-atlantis-config_${TERRAGRUNT_ATLANTIS_CONFIG}_linux_amd64/terragrunt-atlantis-config_${TERRAGRUNT_ATLANTIS_CONFIG}_linux_amd64 terragrunt-atlantis-config \
    && install terragrunt-atlantis-config /usr/local/bin