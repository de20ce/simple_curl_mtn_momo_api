sandboxCreateAPIUser:
# Documentation of this operation can be found here: https://momodeveloper.mtn.com/api-documentation/api-description/
# This operation is only on Momo Sandbox API
# First, we have to create a sandbox API User, from that point, 
# X-Reference-Id is a random UUID, you can find one online here: https://www.uuidgenerator.net/
# X-Reference-Id is represented by the
# Ocp-Apim-Subscription-Key is given in your account, once you subscribed to the product
# providerCallbackHost is for example your website
# For example: REFERENCE_ID=e46188c5-3fcc-4ebe-829a-057e1e79120c
# For example: OCP_APIM_SUBSCRIPTION_KEY=2ed120a8621741e5903f690331db3083
# For example: CALLBACK=localhost
# arguments should be given before the "make" command (example below)
	curl -H "X-Reference-Id: $(REFERENCE_ID)" \
			-H "Content-Type: application/json" \
			-H "Ocp-Apim-Subscription-Key: $(OCP_APIM_SUBSCRIPTION_KEY)" \
			-X POST --data-ascii '{"providerCallbackHost":"$(CALLBACK)"}' \
			"https://sandbox.momodeveloper.mtn.com/v1_0/apiuser"

sandboxCreateUserAPIKey:
# Documentation of this operation can be found here: https://momodeveloper.mtn.com/api-documentation/api-description/
# REFERENCE_ID
# An example of running this command on CLI: 
# OCP_APIM_SUBSCRIPTION_KEY=2ed120a8621741e5903f690331db3083 \
 		CALLBACK=localhost REFERENCE_ID=46188c5-3fcc-4ebe-829a-057e1e79120c \
 		make sandboxCreateUserAPIKey
	curl -H "Content-Type: application/json" \
			-H "Ocp-Apim-Subscription-Key: ${OCP_APIM_SUBSCRIPTION_KEY}" \
			-X POST --data-ascii '{"providerCallbackHost":"${CALLBACK}"}' \
			"https://sandbox.momodeveloper.mtn.com/v1_0/apiuser/${REFERENCE_ID}/apikey"

sandboxGetAPIUserDetails:
# Documentation of this operation can be found here: https://momodeveloper.mtn.com/api-documentation/api-description/
	curl -H "Ocp-Apim-Subscription-Key: ${OCP_APIM_SUBSCRIPTION_KEY}" \
			-X GET --data-ascii '{"providerCallbackHost":"${CALLBACK}"}' \
			"https://sandbox.momodeveloper.mtn.com/v1_0/apiuser/${REFERENCE_ID}"