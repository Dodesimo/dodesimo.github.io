---
layout: page
title: The Bioinformagician
description: Bioinformatics and RAG
img: assets/img/bio.png
importance: 2
category: work
giscus_comments: false
---

This project was an extension of my work at Hackensack Meridian Health.

I wanted to see how I could chain a series of bioinformatics packages and pipe the data effiicently such that an analysis workflow could be run.

From there, I integrated an LLM to analyze results.

Ultimately, in this project, I:

- Engineered a chatbot that trains bioinformatics models using natural language, with a **LangChain** backend and **Django**-routed frontend, authenticated via **Firebase**
- Developed **FastAPI** endpoints to generate research papers from user queries, storing them in **MongoDB Atlas**

The code can be found [here](https://github.com/Dodesimo/seqMateApp).
