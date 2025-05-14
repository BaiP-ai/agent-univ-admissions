# University Admissions Data Generator

This system provides an AI-powered agent for generating comprehensive data about universities, their degree programs, admission requirements, and deadlines. The data is designed to train Small Language Models (SLMs) that can help students choose appropriate universities and degree programs.

## Features

- **Web Scraping**: Automated collection of university data from official websites and educational resources
- **Dynamic Data Generation**: Uses Groq API to enhance and structure university data
- **Data Enrichment**: Combines scraped information with AI-generated insights
- **Customizable Output**: Generate data for specific countries, universities, or degree types
- **ETL Pipeline**: Extract, transform, and load university data for SLM training
- **API Integration**: Connect with external educational databases
- **Export Formats**: Generate data in various formats (JSON, CSV, Markdown)

## System Architecture

```
agent-univ-admissions/
├── data/                # Data storage
│   ├── raw/             # Raw scraped data
│   ├── processed/       # Processed and structured data
│   └── enriched/        # AI-enhanced data
├── src/                 # Source code
│   ├── scrapers/        # Web scrapers for different university websites
│   ├── processors/      # Data processing modules
│   ├── enrichers/       # AI enrichment using Groq API
│   ├── api/             # API connections
│   ├── utils/           # Utility functions
│   └── export/          # Data export modules
├── docs/                # Documentation
├── tests/               # Testing modules
├── config.py            # Configuration settings
├── main.py              # Main execution script
└── requirements.txt     # Dependencies
```

## Installation

### Prerequisites

- Python 3.10 or higher
- Pip package manager
- Groq API key
- Internet connection for web scraping

### Setup

1. Clone the repository:
   ```
   git clone https://github.com/yourusername/agent-univ-admissions.git
   cd agent-univ-admissions
   ```

2. Create and activate a virtual environment:
   ```
   python -m venv venv
   # On Windows
   venv\Scripts\activate
   # On macOS/Linux
   source venv/bin/activate
   ```

3. Install dependencies:
   ```
   pip install -r requirements.txt
   ```
   
   For CI environments or minimal installations:
   ```
   pip install -r requirements-ci.txt
   ```

4. Set up your environment variables:
   ```
   # On Windows
   set GROQ_API_KEY=your_api_key_here
   # On macOS/Linux
   export GROQ_API_KEY=your_api_key_here
   ```

   Alternatively, create a `.env` file in the root directory:
   ```
   GROQ_API_KEY=your_api_key_here
   ```

## Usage

### Quick Start

For convenience, we provide scripts to quickly generate data for top US universities:

#### Unix/macOS:
```bash
# Make the script executable
chmod +x generate_top_universities.sh

# Run the script
./generate_top_universities.sh
```

#### Windows:
```
generate_top_universities.bat
```

These scripts will generate comprehensive data for Harvard, MIT, and Stanford in Markdown format.

### API Key Setup

To use the GROQ API for AI enrichment, you'll need an API key. We provide a setup script to help you configure it:

```bash
python setup_api_key.py
```

This will guide you through the process of setting up your GROQ API key securely.

### Basic Usage

Run the main script to generate university data:

```
python main.py
```

### Command-Line Options

```
python main.py --universities "Harvard University,MIT,Stanford" --countries "US,UK" --degrees "Computer Science,Engineering,Business" --output json
```

Options:
- `--universities`: Comma-separated list of universities to include
- `--countries`: Comma-separated list of countries to include
- `--degrees`: Comma-separated list of degree programs to focus on
- `--output`: Output format (json, csv, markdown)
- `--enrichment`: Level of AI enrichment (basic, standard, comprehensive)
- `--limit`: Maximum number of universities to process

### Configuration

You can customize the behavior by editing the `config.py` file:

- Scraping settings (request delays, timeout, user agents)
- Target websites and scraping strategies
- Default data enrichment settings
- API configuration

### Using as a Library

You can also use the system programmatically:

```python
from src.university_agent import UniversityAgent

agent = UniversityAgent()
data = agent.generate_data(
    universities=["Harvard University", "MIT"],
    degrees=["Computer Science"],
    enrichment_level="comprehensive"
)

# Export to JSON
agent.export_data(data, format="json", path="output.json")
```

## Data Structure

The generated data follows this structure:

```json
[
  {
    "name": "University Name",
    "country": "Country",
    "url": "Official Website URL",
    "programs": [
      {
        "name": "Program Name",
        "description": "Program Description",
        "degree_type": "Degree Type",
        "duration": "Duration in Years"
      }
    ],
    "admissions": {
      "requirements": [
        "Requirement 1",
        "Requirement 2"
      ],
      "deadlines": {
        "early_action": "Early Action Deadline",
        "regular_decision": "Regular Decision Deadline"
      },
      "acceptance_rate": "Acceptance Rate",
      "average_gpa": "Average GPA"
    },
    "metadata": {
      "generated_at": "Timestamp",
      "enrichment_level": "Enrichment Level",
      "confidence_score": "Confidence Score"
    }
  }
]
```

## Training an SLM

After generating the data, you can use it to train a Small Language Model:

1. Export the data in a suitable format (JSON or CSV)
2. Use the data as input for your SLM training pipeline
3. Fine-tune the model for university advisory use cases

For detailed instructions on SLM training, refer to the documentation in the `docs/` directory.## GitHub Integration

### GitHub Actions Workflow

This repository includes a GitHub Actions workflow that automatically generates university data:

- **Scheduled Runs**: The workflow runs monthly to keep data up-to-date
- **Manual Triggers**: You can manually trigger the workflow from the GitHub Actions tab
- **Customizable**: You can specify universities, output format, and enrichment level when triggering manually
- **Artifacts**: Generated data is uploaded as artifacts and can be downloaded from GitHub

### Setting Up GitHub Actions

1. Create a GitHub repository and push your code
2. Go to the repository's "Settings" > "Secrets and variables" > "Actions"
3. Add a new repository secret:
   - Name: `GROQ_API_KEY`
   - Value: Your GROQ API key
4. Go to the "Actions" tab and enable workflows

The workflow will now run automatically according to the schedule and can be triggered manually when needed.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

See the [CONTRIBUTING.md](CONTRIBUTING.md) file for more detailed information on contributing.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- Educational data sources and university websites
- Groq AI for providing the language model API
- Open-source libraries used in this project

---
*Note: Make sure to respect universities' terms of service when scraping their websites and to use the generated data in compliance with applicable laws and regulations.*