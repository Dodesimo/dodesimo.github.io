---
layout: page
title: Toffee
description: Full Stack and AI Engineering
img: assets/img/toffee.png
importance: 3
category: work
giscus_comments: false
---

This project was built out of necessity.

When studying for my computer architecture final, I needed a way to efficiently memorize some information.

However, **everything on the market sucked.** Quizlet was pay-walled, Anki has a unintuitive UI.

My friends also faced this issue, so I built Toffee.

Toffee has AI at its core. You upload a document, a YouTube video, or even an Anki deck, and generate unique MCQ or true/false questions on demand — setting the number of questions, the difficulty, and example questions you want yours to look like. Every run gives you a fresh set shaped around what you actually need, and your past sets stick around.

In this project, I:
 
 - Developed a full-stack AI study tool with **React** and **FastAPI** that converts documents into quizzes and flashcards
- Designed five API endpoints to convert PDFs, plaintext, and YouTube transcripts into JSON-formatted quiz questions using **Google Gemini Flash** and **regex**, deployed on **Vercel**
- Used **Firestore** to save user sessions and **100+** generated flashcards across MCQ, T/F, and FITB quiz formats

### How it works

Source material hits a **FastAPI** backend with LLM helpers configured through **OpenRouter**, each specialized by format, that pull the key information out of the text. That text gets cleaned up with regex and stored in **Firebase**.

When you ask for questions, specialist models generate them from the cleaned text, then hand them to a hallucination-checking model that has to cite a line number in the source for every question. Anything it can't ground gets thrown out. What survives is formatted as JSON, rendered to the frontend, and stored in Firebase keyed by question ID alongside the user ID, creation date, and content.

It helped me pass my final, which I'd call a successful evaluation.

The backend can be found [here](https://github.com/toffeedevs/nougat).
The frontend can be found [here](https://github.com/toffeedevs/toffee).
