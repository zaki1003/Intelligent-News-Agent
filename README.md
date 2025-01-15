# Intelligent-News-Agent
This project showcases a news summarization agent that leverages large language models (LLMs) for decision-making andsummarization, combined with a news API.

## Overview
- This project showcases a news summarization agent that leverages large language models (LLMs) for decision-making and summarization, combined with a news API. It integrates LangGraph for process coordination, OpenAI for article selection and condensation, NewsAPI for retrieving metadata, and BeautifulSoup for web scraping. Together, these tools enable the creation of concise current event summaries (TL;DRs) from a single query.
- Although LLMs demonstrate excellent conversational and educational ability, they lack access to knowledge of current events. This project allow users to ask about a news topic they are interested and receive a TL;DR of relevant articles. The goal is to allow users to conveniently follow their interest and stay current with their connection to world events.
- Used Libraries: LangGraph, GPT-4o-mini , NewsAPI, BeautifulSoup, Asyncio.

## Used Tools
1. **LangGraph**: Orchestrates the overall workflow, managing the flow of data between different stages of the process.
2. **GPT-4o-mini (via LangChain)**: Generates search terms, selects relevant articles, parses html, provides article summaries
3. **NewsAPI**: Retrieves article metadata from keyword search
4. **BeautifulSoup**: Retrieves html from page
5. **Asyncio**: Allows separate LLM calls to be made concurrently for speed efficiency.

## Method
The news research follows these high-level steps:

1. **NewsAPI Parameter Creation (LLM 1)**: Given a user query, the model generates a formatted parameter dict for the news search.

2. **Article Metadata Retrieval**: An API call to NewsAPI retrieves relevant article metadata.

3. **Article Text Retrieval**: Beautiful Soup scrapes the full article text from the urls to ensure validity.

4. **Conditional Logic**: Conditional logic either: repeats 1-3 if article threshold not reached, proceeds to step 5, end with no articles found.

5. **Relevant Article Selection (LLM 2)**: The model selects urls from the most relevant n-articles for the user query based on the short synopsis provided by the API.

6. **Generate TL;DR (LLM 3+)**: A summarized set of bullet points for each article is generated concurrently with Asyncio.

This workflow is managed by LangGraph to make sure that the appropriate prompt is fed to the each LLM call.

## Conclusion
This news TL;DR agent highlights the utility of coordinating successive LLM generations in order to
achieve a higher level goal.

Although the current implementation only retrieves bulleted summaries, it could be elaborated to start
a dialogue with the user that could allow them to ask questions about the article and get 
more information or to collectively generate a coherent opinion.