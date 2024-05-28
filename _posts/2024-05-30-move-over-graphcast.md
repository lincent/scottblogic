---
title: Move over GraphCast
date: 2024-05-30 00:00:00 Z
categories:
- Tech
tags:
- javascript
- TypeScript
- Node.js
- Bun
- Christmas
summary: Is AI really going to take over from Super Computers for Weather Forecasting?
author: lvincent
---

I was going to write a blog detailing why I thought Weather Forecasting AI models like Graphcast weren’t that great, but while researching how meteorological organisations are making use of machine learning and artificial intelligence, I came across some great work that the European Centre for Medium-Range Weather Forecasts (ECMWF) have been up to.

Before I detail what, the ECMWF have been up to, I’ll cover what I was going to say.

## AI models won’t replace HPC forecasts.

Yeah, that’s right. I was going to say global weather forecasting models like Googles Graphcast won’t suddenly mean that meteorological organisations will kill off their vast Super Computing resources. The physics-based models like the Met Offices Unified Model and the ECMWF’s Integrated Forecasting System, that have been steadily improved and refined over decades, won’t suddenly become redundant. There are no signs that this will change, the Met Office is working on a replacement for their Unified Model, it’s called LFRic which will move away from the latitude-longitude coordinate based grid to one where data points are equally spaced across the globe. The main aim of this change is to reduce the number of calculations required to create global forecasts; the north south lines are closer together by a factor of 1000 at the poles compared to the equator.

## The Weather Pipeline

Another factor to consider is the whole weather forecasting pipeline that is required to take place before the app of your phone can tell you that yes, it will rain later. 

### Observations

First in the pipeline is observing the weather, how can we forecast the weather if we don’t know what it’s currently like? Observations can come from a variety of sources including Satellites, Radar, Weather Stations and Weather Balloons. No one of these sources can give us a complete view of the current climate for a given area, for that we need the next step.

### Assimilation

This is the process that takes the observations and updates a view of what the current weather looks like. This itself is a computationally expensive operation, constantly making short term forecasts and adjusting them so that the forecast matches the “live” observations. Assimilation looks at filling in the gaps. Only then when our short-term forecasts are matching the incoming observations can we use them to make simulations of the future. After all, if your starting conditions for your simulation are wrong, how can you trust the output?

### Simulation

The forecasting part of the pipeline. Forecasts will be generated based on the starting conditions determined during Assimilation. The starting conditions of the AI models will be using the same data as NPW forecasts.

### Analysis

What does the forecast tell us? The global forecasts can be many gigabytes in size, this step looks at the HPC outputs. In this step they will be looking at what rain will be coming, are there any features in the forecast like hurricane or things we need to be urgently aware of?

### Products

How the forecasts get disseminated to the users

## So why won’t AI models suddenly replace everything?

So, as you can guess, these new fancy AI models only cover the Simulation section of the pipeline. We still need HPC to cover the rest of the pipeline. 

It’s also worth considering that the AI models are trained on data, but where did that data come from? They were all trained using ECMWF’s ERA5 reanalysis data set. That data was created over decades by the Assimilation part of the forecast, using the HPC that the AI models seek to replace. Observations are continuously fed back into the short-term forecasts as they come in, when all observations are integrated then the climate conditions for that time-period are appended to ERA5.

This ERA5 data that the AI models have been trained on has a resolution of 0.25 degrees. ECMWF’s main medium-range forecast created by the IFS model creates an output at 0.1 degrees. To be able to create a higher resolution AI forecast, it is highly likely that the ERA5 will need to be downscaled to that higher resolution before that can happen.

## How did the forecast predict that there was going to be a storm? 

Well, the old-fashioned NWP forecasts are built upon physics, this makes them inherently explainable. Meteorologists can point at the maths and physics that are derived from centuries of research and understanding of how the weather systems work. How did the AI model predict the weather forecast? Umm... well this black box of self-taught parameters said so. Granted it’s not as black and white, but I like the romance of having to understand the weather before we can predict it.

## But wait…

The ECMWF have entered the AI model age.
They’ve decided to create their own AI model to forecast weather. They’ve called it Artificial Intelligence Integrated Forecasting System, or the AIFS for short. This is based on the Graph Neural Networks proposed in GraphCast, initially they started with a small model with lower resolution and variables but have rapidly built upon its abilities. 

The first version was to create a lower resolution version and run it on their own systems. Not long afterwards they increased the resolution and updated to using an attention-based graph neural network, which is like transformer architecture. This is highly efficient, resulting in a model that is both faster to train and make predictions with. The accuracy of the forecasts is also better.

In the ECMWF’s latest update, they announced they have teamed up with MET Norway. MET Norway had been looking into using Graph Neural Networks for limited area modelling (LAM), which MET Norway have called Neural-LAM. It forecasts at a resolution of 10 km over the Nordic region and is trained using around 10 years of data, though it does take the boundary conditions from traditional forecasts NWP.

The collaboration looked at integrating Neural-LAM with AIFS to allow high-resolution data within the global model. This method maintains global coverage while enhancing local accuracy, allowing seamless interaction between global and regional weather systems.

The project has shown promising results, with models generating higher-resolution forecasts in target areas. Future work will optimize the model structure and increase resolution to 2.5 km for the local areas.

The ECMWF are creating a new framework, called Anemoi, built on top of PyTorch, to facilitate the creation of data-driven weather models at both regional and global scales. This open-source tool will allow meteorological services to train their own models using customized datasets and configurations.

A pilot project, involving 13 European meteorological organizations, will further develop these tools and explore the role of data-driven models in weather prediction.
Maybe this is going somewhere...

## Conclusion
Hopefully I’ve shown you the rapid progress being made with in the Weather Forecasting domain, it is a highly complex field and the pipeline to get the forecasts on to your phone is full of lots of data processing and with many steps.

The ECMWF are pushing the boundaries with machine learning data-driven forecasts, but what I’ve hopefully shown is that there are many steps to weather forecasting and some of them still rely heavily on those big Super Computers to crunch data.

For the foreseeable future, Super Computers will still be required, but if meteorologists can reduce the amount of time that they are needed to create the forecasts, then then they can be used for other things like more research into other important weather things. Like running simulations of what the weather was doing back millions of years ago.

