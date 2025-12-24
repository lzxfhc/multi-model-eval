# CLAUDE.md - AI Assistant Guide for multi-model-eval

## Project Overview

**multi-model-eval** is a project designed for evaluating and comparing multiple AI models. This document serves as a comprehensive guide for AI assistants working on this codebase.

### Repository Information
- **Repository**: lzxfhc/multi-model-eval
- **Primary Development Branch**: `claude/claude-md-mjjohzl1isfcxgkm-usHhQ`
- **Status**: Early stage / Initial setup

---

## Table of Contents

1. [Project Structure](#project-structure)
2. [Development Workflow](#development-workflow)
3. [Coding Conventions](#coding-conventions)
4. [Testing Guidelines](#testing-guidelines)
5. [Git Practices](#git-practices)
6. [Common Tasks](#common-tasks)
7. [AI Assistant Guidelines](#ai-assistant-guidelines)

---

## Project Structure

### Expected Directory Layout

As this project develops, the following structure is recommended:

```
multi-model-eval/
├── src/                    # Source code
│   ├── models/            # Model interface definitions
│   ├── evaluators/        # Evaluation logic and metrics
│   ├── datasets/          # Dataset loaders and processors
│   ├── utils/             # Utility functions
│   └── cli/               # Command-line interface
├── tests/                 # Test files
│   ├── unit/             # Unit tests
│   └── integration/      # Integration tests
├── configs/              # Configuration files
├── data/                 # Data files (gitignored)
├── results/              # Evaluation results (gitignored)
├── scripts/              # Utility scripts
├── docs/                 # Documentation
├── requirements.txt      # Python dependencies (if Python)
├── package.json          # Node.js dependencies (if Node.js)
├── README.md            # User-facing documentation
└── CLAUDE.md            # This file - AI assistant guide
```

### Key Principles

- **Modularity**: Each model adapter should be independent
- **Extensibility**: Easy to add new models and evaluation metrics
- **Reproducibility**: All evaluations should be reproducible with version-controlled configs
- **Performance**: Efficient handling of large datasets and model outputs

---

## Development Workflow

### Initial Setup

When setting up the development environment:

1. **Check runtime requirements**
   ```bash
   # For Python projects
   python --version
   pip --version

   # For Node.js projects
   node --version
   npm --version
   ```

2. **Install dependencies**
   ```bash
   # Python
   pip install -r requirements.txt
   pip install -r requirements-dev.txt  # if exists

   # Node.js
   npm install
   # or
   yarn install
   ```

3. **Set up environment variables**
   ```bash
   cp .env.example .env  # if exists
   # Edit .env with necessary API keys and configurations
   ```

### Branch Strategy

- **Feature branches**: `feature/<feature-name>`
- **Bug fixes**: `bugfix/<bug-name>`
- **Claude branches**: `claude/<session-id>` (for AI assistant work)
- **Main branch**: Will be established as the primary integration branch

### Making Changes

1. **Understand before modifying**: Always read existing code before making changes
2. **Plan complex changes**: For multi-file changes, create a plan first
3. **Incremental commits**: Make small, logical commits with clear messages
4. **Test as you go**: Run tests after each significant change

---

## Coding Conventions

### General Principles

- **Clarity over cleverness**: Write code that's easy to understand
- **No over-engineering**: Implement only what's needed
- **Consistent style**: Follow existing patterns in the codebase
- **Type safety**: Use type hints (Python) or TypeScript where applicable

### Python Conventions (if applicable)

```python
# Use type hints
def evaluate_model(model: ModelInterface, dataset: Dataset) -> EvaluationResult:
    """Evaluate a model on a dataset.

    Args:
        model: The model to evaluate
        dataset: The dataset to use

    Returns:
        Evaluation results with metrics
    """
    pass

# Use dataclasses for structured data
from dataclasses import dataclass

@dataclass
class ModelConfig:
    name: str
    api_key: str
    max_tokens: int = 1000
```

### JavaScript/TypeScript Conventions (if applicable)

```typescript
// Use TypeScript interfaces
interface ModelConfig {
  name: string;
  apiKey: string;
  maxTokens?: number;
}

// Use async/await for asynchronous operations
async function evaluateModel(
  model: ModelInterface,
  dataset: Dataset
): Promise<EvaluationResult> {
  // Implementation
}
```

### File Naming

- **Python**: `snake_case.py` (e.g., `model_evaluator.py`)
- **JavaScript/TypeScript**: `camelCase.js` or `kebab-case.js` (follow existing pattern)
- **Test files**: `test_*.py` or `*.test.js` / `*.spec.js`
- **Config files**: `config.yaml`, `config.json`, etc.

---

## Testing Guidelines

### Test Structure

- **Unit tests**: Test individual functions and classes in isolation
- **Integration tests**: Test interactions between components
- **End-to-end tests**: Test complete evaluation workflows

### Test Naming

```python
# Python
def test_model_returns_valid_response():
    """Test that model returns a properly formatted response."""
    pass

def test_evaluator_handles_empty_dataset():
    """Test that evaluator gracefully handles empty datasets."""
    pass
```

### Running Tests

```bash
# Python
pytest
pytest tests/unit  # specific directory
pytest -v          # verbose
pytest -k "test_name"  # specific test

# Node.js
npm test
npm run test:unit
npm run test:integration
```

### Test Coverage

- Aim for high coverage on core logic
- Don't obsess over 100% coverage
- Focus on critical paths and edge cases

---

## Git Practices

### Commit Messages

Follow conventional commit format:

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks

**Examples:**
```
feat(evaluator): add support for GPT-4 model evaluation

Implement GPT-4 model adapter with streaming support
and cost tracking for evaluation metrics.

fix(dataset): handle malformed JSON in dataset loader

Gracefully skip malformed entries and log warnings
instead of crashing the entire evaluation.

docs(readme): add installation instructions
```

### Pushing Changes

Always push to the correct branch with upstream tracking:

```bash
git push -u origin <branch-name>
```

For Claude assistant branches, ensure the branch name starts with `claude/` and matches the session ID.

### Handling Network Failures

Retry git operations with exponential backoff:
- 1st retry: 2 seconds
- 2nd retry: 4 seconds
- 3rd retry: 8 seconds
- 4th retry: 16 seconds

---

## Common Tasks

### Adding a New Model Adapter

1. Create model interface file (if not exists)
2. Implement adapter class following existing pattern
3. Add configuration schema
4. Write unit tests
5. Update documentation
6. Add example usage

### Adding Evaluation Metrics

1. Define metric function with clear signature
2. Add to metrics registry/module
3. Write tests with known inputs/outputs
4. Document metric calculation method
5. Add examples in docs

### Running Evaluations

```bash
# Example commands (adjust based on actual implementation)
python -m src.cli evaluate --model gpt-4 --dataset benchmark-v1
python -m src.cli compare --models gpt-4,claude-3 --dataset benchmark-v1
python -m src.cli analyze --results results/eval-2024-01-01.json
```

### Debugging

- Use logging instead of print statements
- Set appropriate log levels (DEBUG, INFO, WARNING, ERROR)
- Include context in error messages
- Use debugger for complex issues

---

## AI Assistant Guidelines

### Before Making Changes

1. **Read existing code**: Use `Read` tool to understand current implementation
2. **Search codebase**: Use `Grep` to find related code and patterns
3. **Check for tests**: Look for existing tests to understand expected behavior
4. **Review recent commits**: Check git history for context

### When Writing Code

1. **Follow existing patterns**: Match the style and structure of existing code
2. **Avoid over-engineering**: Don't add unnecessary abstractions or features
3. **Security first**: Avoid SQL injection, XSS, command injection, etc.
4. **Use type hints**: Add type annotations for better code clarity
5. **Write tests**: Add tests for new functionality
6. **Document complex logic**: Add comments for non-obvious code

### What NOT to Do

- ❌ Don't create documentation files unless requested
- ❌ Don't add features beyond what's requested
- ❌ Don't refactor unrelated code
- ❌ Don't add excessive error handling for impossible scenarios
- ❌ Don't create abstractions for single-use code
- ❌ Don't use emojis unless explicitly requested
- ❌ Don't commit without reading the files first

### Tool Usage Best Practices

- **Parallel tool calls**: When operations are independent, run them in parallel
- **Use specialized tools**: Prefer `Read` over `cat`, `Edit` over `sed`
- **Task tool for exploration**: Use `Task` tool with `Explore` agent for codebase exploration
- **Plan complex changes**: Use planning for multi-file architectural changes

### Communication Style

- Be concise and technical
- Focus on facts, not validation
- Provide objective guidance
- Disagree when necessary
- No unnecessary superlatives or praise

---

## Project-Specific Conventions

### Model Evaluation Standards

When implementing model evaluations:

1. **Consistent interfaces**: All models should implement the same interface
2. **Error handling**: Gracefully handle API failures, timeouts, rate limits
3. **Cost tracking**: Track API costs per evaluation
4. **Reproducibility**: Log model versions, parameters, timestamps
5. **Data privacy**: Never log sensitive data or API keys

### Configuration Management

- Store configurations in version-controlled files
- Use environment variables for secrets
- Provide sensible defaults
- Validate configurations on load
- Document all configuration options

### Result Storage

- Use structured formats (JSON, JSONL, Parquet)
- Include metadata (timestamp, model version, config hash)
- Make results easily queryable
- Consider storage efficiency for large evaluations

### Performance Considerations

- Batch requests when possible
- Implement caching for repeated evaluations
- Use async/parallel processing for multiple models
- Monitor memory usage with large datasets
- Implement progress tracking for long evaluations

---

## Security Considerations

### API Keys and Secrets

- ✅ Use environment variables
- ✅ Use secrets management tools
- ✅ Add `.env` to `.gitignore`
- ❌ Never commit API keys
- ❌ Never log API keys

### Input Validation

- Validate all user inputs
- Sanitize file paths
- Validate configuration files
- Check dataset integrity

### Dependencies

- Regularly update dependencies
- Review security advisories
- Pin dependency versions
- Use lock files

---

## Troubleshooting

### Common Issues

**Import errors:**
- Check virtual environment is activated
- Verify dependencies are installed
- Check Python/Node version compatibility

**API failures:**
- Verify API keys are set
- Check rate limits
- Verify network connectivity
- Review API endpoint URLs

**Test failures:**
- Run tests in isolation to identify conflicts
- Check test data fixtures
- Verify mocked dependencies
- Review test environment setup

**Git push failures:**
- Verify branch name format (should start with `claude/`)
- Check network connectivity
- Retry with exponential backoff
- Verify remote repository access

---

## Resources

### Documentation

- [README.md](README.md) - User-facing documentation
- [docs/](docs/) - Additional documentation (when created)

### External Resources

- Model API documentation (links to be added)
- Evaluation methodology papers (links to be added)
- Best practices guides (links to be added)

---

## Maintenance

### Updating This Document

This CLAUDE.md file should be updated when:

- Project structure changes significantly
- New conventions are established
- New tools or workflows are adopted
- Common issues are identified
- Best practices evolve

### Version History

- **2025-12-24**: Initial creation for new repository

---

## Quick Reference

### Essential Commands

```bash
# Setup
git clone <repository-url>
cd multi-model-eval
pip install -r requirements.txt  # or npm install

# Development
git checkout -b feature/my-feature
# Make changes
git add .
git commit -m "feat: add new feature"
git push -u origin feature/my-feature

# Testing
pytest  # or npm test
pytest -v tests/unit

# Running
python -m src.cli <command>  # adjust based on implementation
```

### File Reference Template

When referencing code locations, use format: `file_path:line_number`

Example: `src/evaluators/model_evaluator.py:142`

---

## Contact and Support

For questions or issues:

1. Check existing documentation
2. Review similar implementations in codebase
3. Check git history for context
4. Consult external API documentation

---

*This document is maintained for AI assistants working on the multi-model-eval project. Keep it updated as the project evolves.*
