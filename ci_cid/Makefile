# Makefile
include secrets.env
export


IMAGE_NAME = azure-connector
TAG = latest
FULL_IMAGE = $(ACR_NAME).azurecr.io/$(IMAGE_NAME):$(TAG)
CONTAINER = data

upload-dir:
	az storage blob upload-batch \
		--account-name $(STORAGE_ACCOUNT) \
		--destination $(CONTAINER) \
		--source . \
		--pattern "root_cicd/*"




# Build image
build:
	docker build -t $(FULL_IMAGE) .

# Login to Azure and ACR
login:
	az acr login --name $(ACR_NAME)

# Push image to ACR
push: build login
	docker push $(FULL_IMAGE)



# YAML files' path
CONFLUENT_YAML = k8s/confluent-platform.yaml
PRODUCER_YAML = k8s/producer-app-data.yaml


# Confluent deployment
deploy-confluent:
	kubectl apply -f $(CONFLUENT_YAML)

# Producer-app deployment
deploy-producer:
	kubectl apply -f $(PRODUCER_YAML)	

# Confluent deletion
delete-confluent:
	kubectl delete -f $(CONFLUENT_YAML) 

# Producer-app deletion
delete-producer:
	kubectl delete -f $(PRODUCER_YAML)	
	
# Status verification
status:
	kubectl get pods -o wide  
	
	
# 1. Port forward Control Center
port-forward-controlcenter:
	Start-Process powershell -WindowStyle Hidden -ArgumentList 'kubectl port-forward controlcenter-0 9021:9021 *> $null'


# 2. Port forward Kafka Connect
port-forward-connect:
	Start-Process powershell -WindowStyle Hidden -ArgumentList 'kubectl port-forward connect-0 8083:8083 *> $null'

# 3. Kafka topic creation (expedia)
create-topic:
	kubectl exec kafka-0 -c kafka -- bash -c "/usr/bin/kafka-topics --create --topic expedia --replication-factor 3 --partitions 3 --bootstrap-server kafka:9092"

# 4. Delete alias
fix-curl:
	Remove-Item alias:curl -Force

# 5. Kafka Connect connector upload from JSON file
upload-connector:
	powershell -Command "Invoke-RestMethod -Method Post -Uri http://localhost:8083/connectors -ContentType 'application/json' -Body (Get-Content -Raw -Path azure-source-cc.json)"