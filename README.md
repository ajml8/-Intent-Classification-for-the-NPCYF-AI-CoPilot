# Intent-Classification-for-the-NPCYF-AI-CoPilot
Hybrid Feature-Based Intent Classifier for NPCYF AI CoPilot | LinearSVC + TF-IDF + Sentence Embeddings | IDEAS-TIH, ISI Kolkata
📌 Project Overview
An LLM deployed on an agriculture platform (NPCYF AI CoPilot) receives three very different types of questions:

Intent Class	Example
database_query	"What is the average yield of wheat in Punjab?"
platform_query	"How do I reset my password?"
general_query	"What is photosynthesis?"
This project builds a lightweight intent classifier that reads the user's question first, labels it as one of the 3 categories, and routes it to the correct handler — preventing the LLM from wasting compute on misrouted queries.
This project builds a lightweight intent classifier that reads the user's question first, labels it as one of the 3 categories, and routes it to the correct handler — preventing the LLM from wasting compute on misrouted queries.
