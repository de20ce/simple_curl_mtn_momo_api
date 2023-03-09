export REFERENCE_ID := $(shell uuidgen)

# The API directives begin at "sandboxCreateAPIUser" directive in the current file, and 
# they are ordered: You should run them from that directive from top to bottom

# You can either generate X-Reference-Id with the command above within Makefile or run
# the following in your CLI (I assume you installed Linux uuid tools): $ uuidgen
# To deals with (local env) variables, I recommend you export all of them in your shell,
# and comment all their declaration in the current Makefile
# For example:
# $ REFERENCE_ID=$(uuidgen)
# $ AUTH_CREATION=$(echo -ne "$(REFERENCE_ID):$(API_KEY)" | base64 --wrap 0)
# Above you will get API_KEY from "sandboxCreateUserAPIKey" directive
# $ BASIC_AUTHORIZATION=$(echo "Basic $(AUTH_CREATION)")
# etc
# For those who have trouble understanding the rest, there is enough here and there 
# to allow you to find out	 the construction of the other environment variables.

testEnvVar: 
	@echo "$(REFERENCE_ID)"
	@echo "$(REFERENCE_ID)"


# REFERENCE_ID_INIT := $(shell uuidgen)
TIMEOUT=5
#generateBasicAuthorization: 
# Gonna create the Basic Authorization token here:
AUTHORIZATION_KEY := $(shell echo -ne "${REFERENCE_ID}" | base64 --wrap 0)
BASIC_AUTHORIZATION = $(shell echo "Basic ${AUTHORIZATION_KEY}")
OCP_APIM_SUBSCRIPTION_KEY ?= 2ed120a8621741e5903f690331db3083
# CALLBACK value is generated with the command: $ ngrok http 80
# Request2Pay does not work with this Header parameter, so we remove for now!
CALLBACK=http://6fdb-41-138-89-226.ngrok.io



sleepSomeSecondwithPing:
	@ping mtn.com  -w $(TIMEOUT) > /dev/null

sleepSomeSecondwithPing1:
	@ping mtn.com  -w $(TIMEOUT) > /dev/null

sleepSomeSecondwithPing2:
	ping mtn.com  -w $(TIMEOUT) > /dev/null

generateApiKey: API_KEY := $(shell grep -Po '"apiKey": *\K"[^"]*"' api_key.json | tr -d '"') 

generateApiKey:
	@echo "$(API_KEY)"

printApiKey: generateApiKey
	@echo "$(API_KEY)"

generateBasicAuthorization: AUTH_CREATION := $(shell echo -ne "$(REFERENCE_ID):$(API_KEY)" | base64 --wrap 0)
	
generateBasicAuthorization: BASIC_AUTHORIZATION := $(shell echo "Basic $(AUTH_CREATION)")
	
	
generateBasicAuthorization: 
	@echo "$(BASIC_AUTHORIZATION)"


generateReferenceID: REFERENCE_ID ?= $(shell uuidgen)

generateReferenceID:
	@echo "$(REFERENCE_ID)"


sandboxCreateAPIUser: 
# Documentation of this operation can be found here: https://momodeveloper.mtn.com/api-documentation/api-description/
# This operation is only on Momo Sandbox API
# First, we have to create a sandbox API User, from that point, 
# X-Reference-Id is a random UUID, you can find one online here: https://www.uuidgenerator.net/
# X-Reference-Id is represented by the variable REFERENCE_ID here
# Ocp-Apim-Subscription-Key is given in your account, once you subscribed to the product
# providerCallbackHost is for example your website
# For example: REFERENCE_ID=e46188c5-3fcc-4ebe-829a-057e1e79120c
# For example: OCP_APIM_SUBSCRIPTION_KEY=2ed120a8621741e5903f690331db3083
# For example: CALLBACK=localhost
# arguments should be given before the "make" command (example below)
# CLI example:
# $ REFERENCE_ID=e46188c5-3fcc-4ebe-829a-057e1e79120c \
OCP_APIM_SUBSCRIPTION_KEY=2ed120a8621741e5903f690331db3083 \
CALLBACK=localhost make sandboxCreateAPIUser
	@curl -H "X-Reference-Id: $(REFERENCE_ID)" \
			-H "Content-Type: application/json" \
			-H "Ocp-Apim-Subscription-Key: $(OCP_APIM_SUBSCRIPTION_KEY)" \
			-X POST --data-ascii '{"providerCallbackHost":"$(CALLBACK)"}' \
			"https://sandbox.momodeveloper.mtn.com/v1_0/apiuser"

sandboxCreateUserAPIKey:
# Documentation of this operation can be found here: https://momodeveloper.mtn.com/api-documentation/api-description/
# REFERENCE_ID
# An example of running this command on CLI: 
# OCP_APIM_SUBSCRIPTION_KEY=2ed120a8621741e5903f690331db3083 \
 		CALLBACK=localhost REFERENCE_ID=The_Previous_Generated_User_ID \
 		make sandboxCreateUserAPIKey
	@curl -H "Content-Type: application/json" \
			-H "Ocp-Apim-Subscription-Key: ${OCP_APIM_SUBSCRIPTION_KEY}" \
			-X POST --data-ascii '{"providerCallbackHost":"${CALLBACK}"}' \
			"https://sandbox.momodeveloper.mtn.com/v1_0/apiuser/${REFERENCE_ID}/apikey" > api_key.json

sandboxUserKey:
# Run the following command in your shell: $ REFERENCE_ID = $(uuidgen)
#@export REFERENCE_ID:=$(shell uuidgen)
	REFERENCE_ID=$(REFERENCE_ID) make sandboxCreateAPIUser 
	make sleepSomeSecondwithPing
	REFERENCE_ID=$(REFERENCE_ID) make sandboxCreateUserAPIKey

sandboxGetAPIUserDetails:
# Documentation of this operation can be found here: https://momodeveloper.mtn.com/api-documentation/api-description/
	curl -H "Ocp-Apim-Subscription-Key: ${OCP_APIM_SUBSCRIPTION_KEY}" \
			-X GET  \
			"https://sandbox.momodeveloper.mtn.com/v1_0/apiuser/${REFERENCE_ID}"

collectionsCreateAccessToken: 
# AUTHORIZATION is basic authorization obtained thanks to  the output of the command 'sandboxCreateUserAPIKey' (USER_API_KEY)
# and your user id represented by the variable REFERENCE_ID. One way to get this value is to 
# run the following commands  in your browser console:
# $ 'allow pasting'
# $ AUTHORIZATION = "Basic " + window.btoa('REFERENCE_ID:USER_API_KEY')
# That is: AUTHORIZATION="Basic MTYwYjE2OGQtNjJmNS00YTBjLWFjNjMtYWNhM2E0MTU0YzhlOjA4OWQ3MDhhOTE5ZDQ5MjI5Y2E0YzI1MDBlMDU4Yjc0" for example
# --data-ascii can be empty data as well: '{}'
	curl -H "Authorization: ${BASIC_AUTHORIZATION}" \
			-H "Content-Type: application/json" \
			-H "Ocp-Apim-Subscription-Key: ${OCP_APIM_SUBSCRIPTION_KEY}" \
			-X POST --data-ascii '{"providerCallbackHost":"${CALLBACK}"}' \
			"https://sandbox.momodeveloper.mtn.com/collection/token/"

collectionsGetAccountBalance:
# Authorization here is needed (That the case of all ops that are not related to access)
# AUTHORIZATION="Bearer " + AccessTokenObtainedFromOutputOfThePreviousCommand (that is collectionsCreateAccessToken)
# 
	curl -H "Authorization: ${AUTHORIZATION}" \
			-H "Content-Type: application/json" \
			-H "Ocp-Apim-Subscription-Key: ${OCP_APIM_SUBSCRIPTION_KEY}" \
			-H "X-Target-Environment: ${TARGET_ENVIRONMENT}" \
			-X GET  \
			"https://sandbox.momodeveloper.mtn.com/collection/v1_0/account/balance"

collectionsRequest2Pay:
# Documentation: https://momodeveloper.mtn.com/api-documentation/use-cases/#request-to-pay
#  Here, unlike previous steps, you should generate new X-Reference-ID for each transaction
# -H "X-Callback-Url: ${CALLBACK}" \

	curl  -H "Authorization: ${AUTHORIZATION}" \			
			-H "X-Reference-Id: ${REFERENCE_ID}" \
			-H "X-Target-Environment: ${TARGET_ENVIRONMENT}" \
			-H "Content-Type: application/json" \
			-H "Ocp-Apim-Subscription-Key: ${OCP_APIM_SUBSCRIPTION_KEY}" \
			-X POST -d @request2pay_data.json \
			"https://sandbox.momodeveloper.mtn.com/collection/v1_0/requesttopay"


collectionsRequest2PayTransactionStatus:
# The easiest for checking the previous command is to run the current one
	curl  -H "Authorization: ${AUTHORIZATION}" \
			-H "X-Target-Environment: ${TARGET_ENVIRONMENT}" \
			-H "Content-Type: application/json" \
			-H "Ocp-Apim-Subscription-Key: ${OCP_APIM_SUBSCRIPTION_KEY}" \
			-X GET \
			"https://sandbox.momodeveloper.mtn.com/collection/v1_0/requesttopay/${REFERENCE_ID}"


# You could not make the "all" directive works without some tricks
all: sandboxCreateAPIUser sleepSomeSecondwithPing \
		sandboxCreateUserAPIKey sleepSomeSecondwithPing1 \
		generateApiKey  sleepSomeSecondwithPing2 printApiKey \
		generateBasicAuthorization collectionsCreateAccessToken

#https://sandbox.momodeveloper.mtn.com/v1_0/apiuser/160b168d-62f5-4a0c-ac63-aca3a4154c8e/apikey

# {"apiKey":"bd55270f469249daac13e7dced93a291"}

# Authorization: MTYwYjE2OGQtNjJmNS00YTBjLWFjNjMtYWNhM2E0MTU0YzhlOmJkNTUyNzBmNDY5MjQ5ZGFhYzEzZTdkY2VkOTNhMjkx