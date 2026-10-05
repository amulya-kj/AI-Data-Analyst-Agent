# AI Data Analyst Agent

An AI-powered data analysis agent that converts natural-language business questions into structured analytical plans, executes them using Pandas, verifies the results programmatically, and generates concise business insights.

## Project Overview

This project demonstrates how Large Language Models (LLMs) can be combined with traditional data-analysis workflows to create a reliable AI-assisted analytics system.

Instead of directly asking an AI model to calculate results, the agent separates **question understanding** from **numerical computation**.

The AI model creates a structured JSON analysis plan, while Pandas performs the actual calculation. The result is then independently verified before a business insight is generated.

## Architecture

```text
User Question
      │
      ▼
┌─────────────────────┐
│     AI Planner      │
│    Qwen 2.5 3B      │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│     JSON Plan       │
│ group_by / metric   │
│ operation / filter  │
│ sort / limit        │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│    Pandas Engine    │
│   Data Processing   │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Result Verification │
│  Independent Check  │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Business Insight   │
└─────────────────────┘
```

## Key Features

* Natural-language data analysis
* AI-generated JSON analysis plans
* Pandas-based data processing
* Grouping and aggregation
* Sum, average, and count operations
* Sorting and Top-N analysis
* Conditional filtering
* Programmatic result verification
* Automated business insight generation
* Error handling

## Dataset

The project uses a retail sales dataset containing:

* **9,994 records**
* **13 columns**

Key fields include:

`Category`, `Sub-Category`, `Region`, `Sales`, `Quantity`, and `Profit`

## Example Questions

The agent can answer questions such as:

* Which category has the highest profit?
* Which region has the highest sales?
* Which sub-category has the lowest profit?
* How many records are in each region?
* What are the top 3 sub-categories by profit?
* Which category has the highest profit in the West region?

## Validation Results

The agent was tested against six analytical questions.

| Test Case                       | Result                                             | Verification |
| ------------------------------- | -------------------------------------------------- | ------------ |
| Highest category profit         | Technology — 145,454.95                            | ✅ Passed     |
| Highest region sales            | West — 725,457.82                                  | ✅ Passed     |
| Lowest sub-category profit      | Tables — -17,725.48                                | ✅ Passed     |
| Records by region               | West 3,203; East 2,848; Central 2,323; South 1,620 | ✅ Passed     |
| Top 3 sub-categories by profit  | Copiers, Phones, Accessories                       | ✅ Passed     |
| Highest category profit in West | Office Supplies — 52,609.85                        | ✅ Passed     |

### Verification Approach

Each AI-generated analysis plan is executed using Pandas and independently verified against the dataset.

A business insight is generated only when the analytical result passes verification.

This approach separates:

**AI reasoning/planning → deterministic data computation → verification**

which helps reduce incorrect analytical outputs and unsupported business conclusions.

## Technologies

* Python
* Pandas
* Ollama
* Qwen 2.5 3B
* Jupyter Notebook
* JSON

## Project Structure

```text
AI-Data-Analyst-Agent/
│
├── AI_Data_Analyst_Agent.ipynb
├── README.md
└── retail_sales.csv
```

> Update the notebook and dataset filenames above if your actual filenames are different.

## How It Works

### 1. User asks a business question

Example:

```text
Which region has the highest sales?
```

### 2. AI creates a structured plan

```json
{
    "group_by": "Region",
    "metric": "Sales",
    "operation": "sum",
    "sort": "descending",
    "limit": 1
}
```

### 3. Pandas executes the plan

The analysis engine groups the dataset by region, calculates total sales, sorts the results, and returns the highest-performing region.

### 4. Result is verified

The result is independently checked against the dataset using the same analytical logic.

### 5. Business insight is generated

Example:

```text
West has the highest total sales, with 725,457.82.
```

## Limitations

* The current agent is designed for structured analytical questions that map to supported Pandas operations.
* Supported operations include sum, average, and count.
* Filtering currently focuses on categorical conditions such as region and category.
* The agent operates on the provided retail dataset and does not connect to external databases or live data sources.
* Business insights are generated only after the analytical result passes programmatic verification.
* Complex natural-language questions outside the supported analytical patterns may require additional planning rules.

## Future Enhancements

Potential extensions include:

* Automatic chart generation
* More advanced statistical analysis
* Additional filtering and analytical operations
* SQL database connectivity
* Support for larger datasets
* Multi-step analytical questions
* Interactive web interface
* Conversational follow-up questions

## Project Outcome

This project demonstrates practical application of:

* Python and Pandas
* Data analysis
* LLM-based planning
* Structured JSON workflows
* Data validation
* Business insight generation
* AI-assisted analytics

The project focuses on combining AI capabilities with deterministic data-processing methods rather than relying on an LLM alone for numerical analysis.
