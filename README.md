# Simple cURL Program for MTN Momo API

## Short Description
This repository is a quick familiarization of the type of data that can be returned by the MTN Momo API for an average developer. MTN Momo is a mobile payment solution offered by the mobile operator MTN. The sandbox platform is accessible via this [link](https://momodeveloper.mtn.com/docs/). The API consists of four product groups: 
	
- Collections
- Disbursement
- Remittances
- Collections Widget

In principle, to start working with the API in the Sandbox environment, it is necessary to receive the confidential data related to the four products mentioned above. The confidential developer data are obtained from your [Momo MTN Sandbox] https://momodeveloper.mtn.com/ account and from sending some requests to the `Sandbox User Provisioning` product on that website. 

As a developer, you just need to choose the products you want to use for your platform. This operation must be done by someone with an account on the website. Once the developer has chosen the products (s)he wants, (s)he is offered to upload documents to be filled and submitted on the site. When the uploaded documents are compliant, the developer is invited to go to the Momo MTN production API.

The purpose of the work presented here is to give an idea of the type of data sent by the API. This will allow, for example, the developer to go faster in the integration of his/her solution. This discovery of the Momo MTN API will be done progressively on each product. 

## Collection product

A simple use case for this product is: You are a merchant and you want to receive payments from your customers via your online store. This Momo MTN API product allows you to do just that 