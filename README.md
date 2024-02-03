# Customer Service Reply Bot

A LLM project using Python and the LangChain framework to create an AI bot that can automatically generate responses to customer feedback and queries. Use cases can be for an ecommerce site customer reviews and email queries received from customers. 

Concepts used:
- Constructing chains with the LangChain Expression Language (7 sub-chains within an overall chain). Used various Runnables like RunnableParallel and RunnableBranch
- RAG: Used self-querying and semantic search retrievers to obtain pieces of information like context and few shot examples to add to the prompt to improve reply generation.
- NLP: sentiment analysis, topic classification, language classification and translation. Useful to apply NLP concepts here because: sentiment analysis can indicate urgency to respond (negative sentiment from customers should be attended more urgently), topic classification on subject can help to route to right department, and language translation for incoming queries in foreign languages.
- Prompt engineering like few shot prompting
- LangSmith as a debugging tool to improve observability of the intermediate steps taken during the execution of the chains.

More Details

Retrievers:
Tool 1: Semantic search on similar examples to provide few shot examples for llm to answer customer questions.
Tool 2: Self-querying retriever over product data, to obtain product information to give context to the llm. Self-query retrieval is used as the product data is originally from Excel/CSV type data where product information can be stored in the Document metadata. 

Chains - steps:
o	Input: Customer feedback / complaint / query
o	Check if foreign language. If so, translate to English
o	Perform NLP tasks – sentiment analysis and subject classification (for record keeping and tracking purpose)
o	Use semantic search with similar examples tool, take the few shot examples and insert into a prompt that is passed to an LLM (Retrieval to provide few shot examples)
o	If product information is required to answer the question, use self query product info retriever tool. Insert relevant information to the prompt (RAG – provide context)
o	With the prompt including the above examples and context, get the LLM to answer the customer’s question 
o	Translate back to original language if necessary.
o	Final output should be a json with keys sentiment, subject, language, reply in English and customer’s language


Chain - diagram:
