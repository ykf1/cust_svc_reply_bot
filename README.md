# Customer Reply Bot

A LLM project using Python and the LangChain framework to create an AI bot that can automatically generate responses to customer feedback and queries. Use cases are primarily in customer service like automating responses for customer reviews on an ecommerce site and email queries received from customers. 

Concepts used:
- Constructing chains with the LangChain Expression Language: LCEL chains are ideal when there are a series of pre-determined steps to take which may involve LLM calls or retriever tools to achieve the overall goal of the AI system. Used 7 sub-chains within an overall chain and used various Runnables like RunnableParallel and RunnableBranch.
- RAG: Used self-querying and semantic search retrievers to obtain extracts of information like product context and few shot examples respectively to insert into the prompt to the LLM to improve generation.
- NLP: Applied sentiment analysis, topic classification, language classification and translation. Useful to apply NLP concepts here because sentiment analysis can indicate urgency to respond (negative sentiment from customers should be attended more urgently), topic classification on subject can help to route to right department, and language translation to handle incoming queries in foreign languages.
- Prompt engineering like few shot prompting
- LangSmith as a debugging tool to improve observability of the intermediate steps taken during the execution of the chains.

More Details

Retrievers as tools:
Tool 1: Semantic search on similar examples to provide few shot examples for llm to answer customer questions.
Tool 2: Self-querying retriever over product data, to obtain product information to give context to the llm. Self-query retrieval is used as the product data is originally from Excel/CSV type data where product information can be stored in the Document metadata. 

Chains - steps:
1. Classify language from the customer feedback / complaint / query.
2. If language is not in English, translate to English.
3. Perform classification tasks – sentiment analysis and subject classification
4. Use the retriever tool to obtain few shot examples.
5. If subject is on product and if product information is required to answer the question, use self query retriever tool.
6. Construct the prompt with the few shot examples and product context, and prompt the LLM to construct the response to answer the customer’s question 
7. Translate back to customer's original language if necessary.

Notebooks:
- Main code: customer_reply_bot_notebook.ipynb
- Evaluate output using dataset of question and gold standard answer using LLM: evaluation.ipynb
