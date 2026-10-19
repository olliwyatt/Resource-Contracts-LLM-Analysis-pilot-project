# Resource Contracts LLM Analysis pilot project
LLM-Assisted Analysis of Environmental Obligations from Mining Agreements: A Methodological Pilot

This project explores the use of large language models to extract structured information from publicly available mining agreements. The aim is to test whether contractual obligations can be identified, classified, and linked back to their original text in a reproducible, automated workflow.

It focuses on environmental obligations in cobalt-related joint-venture mining agreements from the Democratic Republic of the Congo (DRC). Contract metadata and text are retrieved through the ResourceContracts API, processed in R, and analyzed using Google's Gemini API.


**Data Collection**

The ResourceContracts API was used to retrieve metadata for agreements associated with cobalt in the DRC.

The initial search returned 136 documents across several categories, including joint-venture agreements, mining permits, annexes, and amendments.

For this pilot, I narrowed the collection to 48 documents categorized as joint-venture agreements. This provided a more consistent starting point for comparing contractual provisions, although agreements still vary considerably in length, structure, and content.

*In this pilot project, it is important to note than only 12 of these were actually processed due to the limitations of free tier of Gemini API.*

Contract text was retrieved directly through the API, preserving page numbers to allow extracted passages to be checked against the original documents.


**OCR error note**


There were some issues with OCR errors and passages including a page break in the middle. The code was updated to account for page changes, but cannot account for OCR errors in the initial contract text extracted with OCR from Resourcecontract API. The code will give a notice of which quotes with OCR errors that cannot be automatically verified and these must be verified manually. 

*Note: this error is seen in cell G8 of the environmental_obligations.csv file. The file claims that one quote cited by the LLM cannot be verified against the actual contract text. This is due to an OCR error in the original contract text data, which the LLM automatically corrected when quoting the contract. It has been manually verified to be an otherwise perfectly accurate quotation of the contract text.*

**Another note**

This is a methodological pilot, and the resulting observations should not be treated as a validated or representative dataset.



**Documents**

The analysis is organized into two Quarto documents:

Critical Minerals API Dataset.qmd

Retrieves contract metadata and text through the ResourceContracts API, examines document categories, and constructs the initial contract inventory.

Pilot LLM Mineral Contract Analysis.qmd

Loads the retrieved contract text, runs structured extraction using Gemini, and verifies supporting quotations against source documents.

Intermediate data and extraction outputs are saved locally to avoid repeated API requests.


