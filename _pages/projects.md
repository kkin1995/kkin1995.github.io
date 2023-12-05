---
layout: single
title: Projects
permalink: /projects/
---
{% if jekyll.environment == 'production' and site.google_analytics %}
{% include analytics.html %}
{% endif %}

## Modelling Interstellar Dust and it's impact on starlight in Messier 8

My research focused on developing a detailed model for the interaction of ultraviolet (UV) radiation with interstellar dust in the H-II region Messier 8. This involved simulating the scattering and absorption properties of dust grains in the UV spectrum. The properties simulated were the albedo (a) and phase asymmetry (g), from the Henyey - Greenstein Function, of the dust grains.

A significant challenge addressed was the asymmetric UV background distribution around the stars in M8 partly due to the sensor faliure aboard the GALEX spacecraft. 

![hip_88469_nuv_distribution](/assets/88469_nuv_coordinates.jpg)

In an effort to resolve this, the model integrated both infrared data and a revised approach to the interstellar medium surrounding these stars. Specifically, I used infrared emission models from Hensley and Draine 2022 (Astrodust) to calculate the infrared emission as a function of the stellar radiation field and use Chi Square minimisation to fit this to observational data from IRAS and [Murthy 2014](https://archive.stsci.edu/prepds/uv-bkgd/)

The outcomes of this research contribute to the understanding of the role of interstellar dust in modifying the characteristics of starlight, particularly in the context of star formation regions, and the subsequent distribution of the re-emitted infrared radiation from dust. Eventhough my MSc thesis has been completed, my work on this project is an ongoing effort and I am in the process of writing a paper.