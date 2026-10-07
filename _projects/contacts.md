---
layout: page
title: Contacts
description: Information Retrieval and Concurrency
importance: 2
category: work
giscus_comments: false
---

I built this because a professor of mine complained about how hard literature review is — specifically, how hard it is to tell whether an idea you have is actually novel.

It's also an extension of my work at **InPharmD**, where I first started thinking about research as a traversal problem rather than a search problem.

In this project, I:

- Built a **FastAPI** research discovery tool that generates topic knowledge graphs from academic search terms by traversing works, references, and related publications across journals through the **OpenAlex** API
- Engineered a multithreaded graph expansion pipeline with concurrent search requests, enabling discovery across **400+** papers per query while ranking candidates with **BM25** relevance scoring
- Visualized the resulting graph in a **React** frontend, where each node carries the authors, abstract, and references for a paper

### How the search works

Given an initial query phrase, the tool scrapes a seed set of papers from **OpenAlex**. For each paper, it pulls every reference, scores that reference's relevance against the original paper with **BM25**, and continues the search from the top five.

Every paper encountered goes into a store, with its references kept in an adjacency list that distinguishes between papers the search continued through and papers that were merely cited. That distinction is what makes the final graph useful — you can see not just how papers connect, but which paths the search actually explored and which it pruned.

### Concurrency

Expansion is parallelized across threads, where each thread takes a different paper off the current frontier, calls OpenAlex for its neighboring works, and runs the relevance calculations itself.

Since multiple threads can discover or update the same paper at once, the graph store is guarded by a lock. This keeps inserts and adjacency appends thread-safe and avoids the race conditions that show up when two threads reach the same paper from different directions.

### The frontend

The adjacency lists feed a knowledge graph in **React**. Each node exposes its authors, abstract, and references, with references disambiguated by whether the search continued through them. Seed papers are highlighted so you can always see where the traversal began.

The backend can be found [here](https://github.com/Dodesimo/contacts).
The frontend can be found [here](https://github.com/Dodesimo/contacts_frontend).
