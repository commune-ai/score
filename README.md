# Score : Mixture of Experts to Score Anything

A module for evaluating the inappropriateness of text messages using multiple language models.

## Overview

The Score module provides a way to assess text content and determine its level of inappropriateness on a scale of 0.0 to 1.0. It leverages multiple language models (like Claude and OpenAI) to get a consensus score, where scores above 0.5 indicate inappropriate content that should be flagged.

## Features

- Multi-model scoring system
- Configurable weights for different models
- Automated model selection from available options
- Score aggregation with mean and standard deviation
- Optional ticket-based history tracking
- Customizable scoring bounds and default values

## Installation

```bash
# Assuming commune is installed
pip install commune
```

## Usage

### Basic Usage

```python
import commune as c

# Initialize the scorer
scorer = c.Score()

# Score a text
result = scorer.forward("text to analyze")
```

### Advanced Usage

```python
# Initialize with custom parameters
scorer = c.Score(
    lower=0.0,
    upper=1.0,
    default_score=0.5,
    n=5,
    models=['claude', 'openai'],
    weights=[1, 1]
)

# Score with timeout
result = scorer.forward("text to analyze", timeout=10)
```

## Response Format

The module returns a dictionary containing:
- `mean`: Average inappropriateness score across models
- `std`: Standard deviation of scores
- `n`: Number of successful model responses
- `latency`: Processing time
- `timestamp`: Time of scoring
- `models`: List of models used

Example response:
```python
{
    'mean': 0.3,
    'std': 0.05,
    'n': 5,
    'latency': 2.5,
    'timestamp': 1234567890,
    'models': ['claude', 'openai']
}
```

## Parameters

- `goal`: Scoring objective (customizable)
- `lower`: Lower bound for scores (default: 0.0)
- `upper`: Upper bound for scores (default: 1.0)
- `default_score`: Fallback score (default: 0.5)
- `n`: Number of models to use (default: 5)
- `weights`: Model weights (optional)
- `score_feature`: Score label in response (default: 'inappropriate')
- `models`: List of model types to use

## License

[Add your license information here]
```

This README provides a comprehensive overview of the module's functionality, installation instructions, usage examples, and parameter descriptions. You may want to customize it further based on specific requirements or add additional sections like:
