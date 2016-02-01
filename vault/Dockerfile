FROM alpine:edge

MAINTAINER Connor Atherton "c.liam.atherton@gmail.com"

ENV VAULT_VERSION 0.4.0

RUN  apk add --update ca-certificates \
  && wget https://releases.hashicorp.com/vault/${VAULT_VERSION}/vault_${VAULT_VERSION}_linux_amd64.zip \
	&& wget https://releases.hashicorp.com/vault/${VAULT_VERSION}/vault_${VAULT_VERSION}_SHA256SUMS -O - | grep vault_${VAULT_VERSION}_linux_amd64.zip > SHA256SUMS \
	&& sha256sum -c SHA256SUMS 2>&1 | grep OK \
  && unzip vault_${VAULT_VERSION}_linux_amd64.zip \
	&& mv vault /bin/ \
  && rm -f vault_${VAULT_VERSION}_linux_amd64.zip SHA256SUMS \
  && rm -rf /tmp/* /var/tmp/* /var/cache/apk/*

# We specify this in the .hcl file
EXPOSE 8200

COPY ./vault.hcl /etc/vault.hcl

ENTRYPOINT [ "/bin/vault" ]
CMD [ "server", "-config=/etc/vault.hcl"]
