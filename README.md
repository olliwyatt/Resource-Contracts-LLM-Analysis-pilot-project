# Resource Contracts LLM Analysis pilot project
LLM-Assisted Analysis of Environmental Obligations from Mining Agreements: A Methodological Pilot

This project explores the use of large language models to extract structured information from publicly available mining agreements. The aim is to test whether contractual obligations can be identified, classified, and linked back to their original text in a reproducible workflow.

The pilot focuses on environmental obligations in cobalt-related joint-venture agreements from the Democratic Republic of the Congo (DRC). Contract metadata and text are retrieved through the ResourceContracts API, processed in R, and analyzed using Google's Gemini API.

The project is exploratory and is not intended to provide a comprehensive assessment of environmental governance in the DRC.

**Data Collection**

The ResourceContracts API was used to retrieve metadata for agreements associated with cobalt in the DRC.

The initial search returned 136 documents across several categories, including joint-venture agreements, mining permits, annexes, and amendments.

For this pilot, I narrowed the collection to 48 documents categorized as joint-venture agreements. This provided a more consistent starting point for comparing contractual provisions, although agreements still vary considerably in length, structure, and content.

*In this pilot project, it is important to note than only 12 of these were actually processed due to the limitations of free tier of Gemini API.*

Contract text was retrieved directly through the API, preserving page numbers to allow extracted passages to be checked against the original documents.

**Methodology**

The analysis was developed in R using Quarto, with the httr2 package for API requests and ellmer for interaction with Gemini.

The workflow consists of four main stages:

Data retrieval: Collect contract metadata and page-level text from ResourceContracts API.

Text preparation: Clean formatting artifacts while retaining the original text and page references.

LLM extraction: Use Gemini API to identify environmental obligations and return structured observations, including the responsible party, an English description, the original supporting quotation, and a classification of specificity.

Quotation verification: Compare extracted quotations against the source text using R, including checks for passages that span page boundaries.

The extraction distinguishes between general environmental compliance requirements and more specific or quantified obligations.

**Initial results**

The pilot has so far processed 12 joint-venture agreements and identified 13 environmental obligations across nine of them.

The extracted provisions include general requirements to comply with internationally recognized environmental standards, as well as more specific commitments relating to environmental protection and management.

Several agreements contain similar environmental language, suggesting that standardized contractual provisions may be worth investigating in a larger study.

The automated quotation checks have also pointed out practical challenges associated with OCR errors and passages including a page break in the middle. The code was updated to account for page changes, but cannot account for OCR errors in the initial contract text extracted with OCR from Resourcecontract API. The code will give a notice of which quotes with OCR errors that cannot be automatically verified and these must be verified manually. 

*Note: this error is seen in cell G8 of the environmental_obligations.csv file. The file claims that one quote cited by the LLM cannot be verified against the actual contract text. This is due to an OCR error in the contract text, which the LLM automatically corrected when citing the contract. It has been manually verified to be an otherwise perfectly accurate quotation of the contract test.*

**Limitations**

This is a methodological pilot, and the resulting observations should not be treated as a validated or representative dataset.

In particular:

Successfully matching a quotation to its source does not establish that the LLM has interpreted the meaning of the text correctly.

The model may overlook relevant obligations or classify them inconsistently.

ResourceContracts includes publicly available agreements and does not necessarily represent all mining agreements signed in the DRC.

Multiple agreements may concern the same mining project.

Contractual requirements do not necessarily reflect implementation, regulatory enforcement, or environmental outcomes.

A larger study would require a clearly defined coding framework, systematic manual validation, and additional consideration of document coverage and comparability.


**Project structure**

The analysis is organized into two Quarto documents:

Critical Minerals API Dataset.qmd

Retrieves contract metadata and text through the ResourceContracts API, examines document categories, and constructs the initial contract inventory.

Pilot LLM Mineral Contract Analysis.qmd

Loads the retrieved contract text, runs structured extraction using Gemini, and verifies supporting quotations against source documents.

Intermediate data and extraction outputs are saved locally to avoid repeated API requests.


**Tools**

The contract-retrieval stage uses the publicly accessible ResourceContracts API.

The extraction stage requires access to the Gemini API. The API key should be stored as an environment variable named GEMINI_API_KEY, rather than included directly in the Quarto files.

This project used only the free version of the Gemini API key, which accounts for the small number of contracts analyzed. 


**Further development**

The broader objective is to explore whether unstructured mining agreements can provide useful quantitative measures of environmental protection data through automating LLM analysis. 


Whether this approach is suitable for a larger research project will depend on the availability of comparable documents, the reliability of the extracted variables, and their relevance to the underlying research question.


**Sources**

ResourceContracts (a repository of publicly available extractive-industry contracts and related documents)
Gemini API (free tier)
