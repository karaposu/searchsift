# SearchSift

SearchSift is a fully implemented pipeline module where you can obtain relevant information given a keyword. It combines Google search result retrieval, page source fetching, and smart filtering to deliver concise and accurate information.

## Overview
SearchSift simplifies the process of obtaining targeted data from the internet by automating search, fetching, and filtering. Its modular design allows it to seamlessly integrate with other systems, such as data imputation modules, for enhanced functionality.

### Key Features
- **Google Search API Integration**: Efficiently retrieves search results based on user-provided keywords and filters results by domain, location, or other validation conditions.
- **BrightData WebUnlocker**: Fetches the source pages of links returned by the search, bypassing standard blockers or restrictions.
- **Information Filtering**: Leverages both manual regex-based parsers and OpenAI models for extracting structured information. If regex-based parsers fail, OpenAI models provide intelligent fallback filtering.
- **Customizable Configurations**: Supports prioritization and domain-based filtering via a configuration file (`priority_config.yaml`).

## How It Works
1. **Input**: User provides a search keyword, required validation conditions, and the type of information to extract.
2. **Search**: The module uses the Google Search API to fetch relevant search links and their metadata.
3. **Fetch**: BrightData WebUnlocker is used to access page sources of the retrieved links.
4. **Filter**: Extracted content is processed using:
   - Regex parsers (for pre-defined structured data).
   - OpenAI models (for complex or unstructured data).
5. **Output**: Delivers structured, reduced, and task-relevant information.

## Installation
Ensure the following dependencies are installed:
- **Google Search API** for retrieving search results.
- **BrightData WebUnlocker** for fetching page sources.
- **OpenAI Python SDK** for advanced filtering.

To install required packages, run:
```bash
pip install google-api-python-client brightdata-sdk openai
```

## Configuration
SearchSift requires a configuration file (`priority_config.yaml`) to set the following parameters:
- **allowed_domains**: List of domains to prioritize.
- **forbidden_domains**: Domains to exclude.
- **output_format**: Desired output structure (JSON, XML, etc.).
- **filter_LLM**: Enable or disable the use of OpenAI models for filtering.

Example `priority_config.yaml`:
```yaml
allowed_domains:
  - example.com
  - example.org
forbidden_domains:
  - spam.com
output_format: JSON
filter_LLM: true
```

## Usage
### Basic Example
```python
from searchsift import SearchSift

# Initialize SearchSift
search_sift = SearchSift(config_path="priority_config.yaml")

# Input keyword
keyword = "climate change impact"

# Fetch and filter results
results = search_sift.run(keyword)
print(results)
```

### Advanced Options
- Customize validation conditions such as region-specific results (e.g., USA only).
- Adjust the number of URLs to process by modifying configuration parameters.
- Use task-specific reducers for structured output.

## Key Components
### 1. Search Engine Agent
Handles the query input, validation, and interaction with the Google Search API to retrieve search links and metadata.

### 2. Web Fetcher
Fetches the content of URLs returned by the search agent. It comprises:
- **PageSource Fetcher**: Uses BrightData WebUnlocker to fetch raw page sources.
- **Structured Crawler**: Extracts structured data using BrightData API.

### 3. Reducer
Filters and reduces raw content into structured data. It includes:
- **Task Customized Reducer**: Task-specific filtering logic.
- **Generic HTML Reducer**: General-purpose content reduction.

## Future Improvements
- Integration with more search APIs for broader coverage.
- Enhanced support for multilingual data extraction.
- Improved fallback mechanisms for unstructured data parsing.

## License
SearchSift is released under the MIT License. See LICENSE for details.

---

For additional information or support, contact the development team.


