# variables
POSTGRES_USER := postgres.nbdhkkludjyhinzkmibl #quabynah
POSTGRES_PASSWORD := YS8rUSINtLMTWi8y
POSTGRES_DB := postgres #qwallet
REDIS_PASSWORD := sJNeeINuWKI7Gdc3
TOKEN_SECRET := Qf10d159aWAL23a5739df23cb65deLET
CLOUDFLARE_API_TOKEN := 3Go7S-rsfDCWe1_0r_NeYYE-C4NBoMSUTqhWvrxq

# rules
create-db-secret:
	@echo "Creating secret for postgres database"
	@kubens qwallet
	@if kubectl get secret postgres-credentials -n qwallet; then \
		kubectl delete secret postgres-credentials -n qwallet; \
	fi
	@kubectl create secret generic postgres-credentials --from-literal=username=$(POSTGRES_USER) --from-literal=password=$(POSTGRES_PASSWORD) \
	--from-literal=repmgr-username=$(POSTGRES_USER) --from-literal=repmgr-password=$(POSTGRES_PASSWORD) --from-literal=admin-password=$(POSTGRES_PASSWORD) \
	--from-literal=database=$(POSTGRES_DB) -n qwallet
	@echo "Secret created successfully"

create-cache-secret:
	@echo "Creating secret for redis cache"
	@kubens qwallet
	@if kubectl get secret redis-credentials -n qwallet; then \
		kubectl delete secret redis-credentials -n qwallet; \
	fi
	@kubectl create secret generic redis-credentials --from-literal=authKey=$(REDIS_PASSWORD) -n qwallet
	@echo "Secret created successfully"

create-server-secret:
	@echo "Creating secret for server"
	@kubens qwallet
	@if kubectl get secret server-credentials -n qwallet; then \
		kubectl delete secret server-credentials -n qwallet; \
	fi
	@kubectl create secret generic server-credentials --from-literal=token_secret=$(TOKEN_SECRET) -n qwallet
	@echo "Secret created successfully"

create-cloudflare-secret:
	@echo "Creating secret for cloudflare"
	@if kubectl get secret cloudflare-dns-credentials -n cert-manager; then \
		kubectl delete secret cloudflare-dns-credentials -n cert-manager; \
	fi
	@kubectl create secret generic cloudflare-dns-credentials --from-literal=api_token=$(CLOUDFLARE_API_TOKEN) -n cert-manager
	@echo "Secret created successfully"
