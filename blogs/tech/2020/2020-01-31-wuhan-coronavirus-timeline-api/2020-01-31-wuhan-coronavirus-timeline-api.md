---
title:  "A Test App with Istio"
description: "A Test App with Istio"
date: 2020-01-30 15:04:23
hidden: false
categories: [Tech]
tags: [Wuhan, Coronavirus, Timeline, API, Pneumonia]
---
# A Test App with Istio

> * Author: [Damon Yuan](https://www.damonyuan.com)
> * Date: 2020-01-30

![Wuhan Coronavirus API](wuhan-coronavirus-api-istio.png "Wuhan Coronavirus API")

Recently the situation of Wuhan Coronavirus is getting serious, more and more foreign friends are aware of it and taking preventive measures to protect themselves from getting infected. Some of them are even interested in what is happening in China, and drop their jaws when hearing something like [China building 1,000-bed hospital in 10 days to treat coronavirus](https://www.dezeen.com/2020/01/27/china-wuhan-huoshenshan-hospital-coronavirus/). 

To get the related credible information from China propagated easier with less language barrier and without second hand modification, I have just created a project to provide the API for English speaking forks consuming. For now it only crawls some Timeline information and I might add more in the future if the time is allowed.

The project is consisted by,

- One MongoDB service
- One MongoExpress service
- One crawler based on Scrapy, and integrated with Google Translation API
- One SpringBoot based API server
- One Swagger UI instance
- One React.js based web app

All of them are deployed to Kubernetes with Istio enabled. 

