---
date: '2025-09-05T20:40:23+08:00'
draft: false
title: 'Project: A specialized Wikipedia Research Assistant'
tags: ['crawl4ai','AI Agent']
categories: ['LLM project']
---

# A specialized Wikipedia Research Assistant

## 1. Project Overview

This project is an AI-powered, fully automated research system designed to scrape information from unstructured sources like Wikipedia, perform intelligent information extraction and structuring using Large Language Models (LLMs), and provide an interactive query and analysis platform accessible via natural language.

The system constitutes an end-to-end data intelligence pipeline, from data acquisition and processing to analysis and visualization, demonstrating how modern AI technology can transform complex web information into actionable knowledge.

*   **Research Domain**: Scientific Discoveries and Breakthroughs
*   **Core Technologies**: Python, OpenAI API (GPT-4o-mini), Pydantic, Web Scraping, Matplotlib
*   **Student**: Li Jinxuan

---

## 2. System Architecture and Core Components

The system is composed of four core modules that work in concert to complete the entire workflow from raw data to final insights.

### Part 1: Wikipedia Data Scraper (`WikipediaScraper`)

This module is responsible for automatically acquiring raw data from the web.

*   **Functionality**:
    *   Automatically generates Wikipedia URLs from a given list of keywords (e.g., "CRISPR", "Quantum computing").
    *   Utilizes `crawl4ai` and `asyncio` for efficient, asynchronous web scraping.
    *   Performs deep cleaning of the scraped HTML content using `BeautifulSoup` to remove irrelevant elements like navigation, references, and infoboxes, retaining only high-quality body text.
    *   Implements robust error handling and rate-limiting to ensure scraping stability.
*   **Outputs**:
    *   `scientific_discoveries.json`: A JSON file containing raw scraped metadata and content.
    *   `content.md`: Cleaned, plain-text content ready for AI analysis.
    *   `section.md`: The section structure of the articles.

### Part 2: Structured Data Extractor (`StructuredDataExtractor`)

This module is the core of the system, responsible for converting unstructured text into machine-readable, structured data.

*   **Functionality**:
    *   Defines a `ScientificDiscoveryExtraction` Pydantic model, which precisely specifies the data fields to be extracted (e.g., discoverers, discovery years, applications, mechanism), forcing the LLM to output formatted JSON.
    *   Calls the OpenAI API (`gpt-4o-mini`) with a carefully designed system prompt that instructs the model to act as a "scientific literature analyst."
    *   Includes retry logic with exponential backoff to handle potential API rate limits or transient errors.
*   **Output**:
    *   `structured_extractions.json`: A JSON file containing the structured information for all articles, which serves as the foundation for all subsequent analysis.

### Part 3: Intelligent Querying and Function Calling

This module provides the user with the ability to interact with the data, showcasing the system's intelligence.

*   **`ScientificDataQuery` Class**:
    *   Encapsulates the query logic for the structured data, such as searching by name, scientist, or application.
    *   Integrates an `OpenAIAnalyzer` that uses the LLM for semantic fuzzy matching when an exact match fails (e.g., intelligently matching the query "gene editing" to "CRISPR").
*   **`ScientificResearchAssistant` Class**:
    *   This is an intelligent assistant built on OpenAI's Function Calling feature.
    *   It understands natural language questions (e.g., "Please compare CRISPR and mRNA vaccines") and automatically selects the most appropriate tool from a predefined set of functions (`compare_discoveries`, `get_research_timeline`, etc.) to execute.
    *   This enables a seamless transition from natural language to specific code execution.

### Part 4: Integration and Visualization

This module integrates all functionalities and presents the analysis results in intuitive visual formats.

*   **`ComprehensiveDemoFixed` Class**:
    *   Orchestrates the entire pipeline—scraping, extraction, querying, and visualization—into a single, one-click runnable process.
    *   Operates in a "memory data flow" mode, where data from intermediate steps is passed directly in memory, enhancing efficiency by avoiding frequent file I/O.
*   **Visualization Functions**:
    *   Leverages `Matplotlib` and `Seaborn` to automatically generate various analytical charts from the extracted structured data, including:
        1.  **Scientific Discovery Timeline**: Shows the distribution of major breakthroughs over history.
        2.  **Discoverer Contribution Network**: Analyzes the contribution frequency of key scientists.
        3.  **Breakthrough Intensity Analysis**: Measures the impact of discoveries based on metrics like the number of participants.

---

## 3. How to Run

1.  **Environment Setup**:
    *   Run the first code cell in the notebook to install all necessary Python libraries (`crawl4ai`, `openai`, `matplotlib`, etc.).
2.  **Configure API Key**:
    *   Execute the API key setup cell. The system will prompt you to securely enter your OpenAI API Key, which will be valid for the current session.
3.  **Execute the Main Function**:
    *   Scroll to the end of the notebook and run the cell containing the `main()` function.
    *   This function will automatically execute all the steps described above: scraping data -> extracting information -> initializing the assistant -> generating visualizations.

---

## 4. Project Highlights

*   **End-to-End Automation**: Achieves full automation from raw information to final insight, minimizing manual intervention.
*   **Practical LLM Agent**: The `ScientificResearchAssistant` is a classic example of a small-scale AI Agent application that can autonomously make decisions and use tools to complete tasks.
*   **Robust Design**: Detailed error handling and retry logic are implemented in both the data scraping and AI-calling stages, ensuring system stability.
*   **Modularity and Extensibility**: The code is well-structured, with each component (scraping, extraction, querying) encapsulated in its own class, making it easy to maintain and extend.
*   **Data-Driven Visualization**: All charts are dynamically generated from the AI-extracted structured data, providing intuitive visual insights into the patterns and trends behind scientific discoveries.

## Project Link
https://github.com/lijinxuan1101/crawl_rag_20250903