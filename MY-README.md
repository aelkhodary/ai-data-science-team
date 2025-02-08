# AI Data Science Team Framework

A comprehensive framework for creating AI agents that can write, execute, and fix code with support for both automated and human-in-the-loop workflows.

## Overview

This framework provides a robust foundation for building AI agents that can:
- Generate and execute code
- Handle various data sources (pandas DataFrames, SQL databases)
- Self-repair code when errors occur
- Provide explanations of code functionality
- Support human review and intervention
- Generate structured reports

## Core Components

### BaseAgent Class

The foundation class for all agents, inheriting from `CompiledStateGraph`.

```python
class BaseAgent(CompiledStateGraph):
def init(self, params):
"""Initialize agent with parameters"""
```

Key features:
- Parameter management
- State graph operations
- Synchronous and asynchronous execution
- Streaming capabilities
- State inspection and visualization

Key methods:
- `invoke()`: Synchronous execution
- `ainvoke()`: Asynchronous execution
- `stream()`: Synchronous streaming
- `astream()`: Asynchronous streaming
- `get_state_keys()`: List available state keys
- `get_state_properties()`: Get detailed state properties
- `show()`: Visualize the agent's graph

### Graph Creation

```python
def create_coding_agent_graph(
GraphState,
node_functions,
recommended_steps_node_name,
create_code_node_name,
execute_code_node_name,
fix_code_node_name,
explain_code_node_name,
error_key,
...
)
```

Creates a workflow graph with configurable nodes for:
- Recommending steps
- Creating code
- Executing code
- Fixing errors
- Explaining results
- Human review (optional)

Features:
- Configurable retry logic
- Error handling
- Conditional paths
- Optional human-in-the-loop review
- Checkpointing support

### Node Functions

#### Human Review

```python
def node_func_human_review(
    state,
    prompt_text,
    yes_goto,
    no_goto,
    ...
)
```

Handles human interaction in the workflow:
- Displays code and instructions
- Processes user feedback
- Routes workflow based on response
- Maintains modification history

#### Code Execution

```python
def node_func_execute_agent_code_on_data(
    state,
    data_key,
    code_snippet_key,
    result_key,
    error_key,
    ...
)
```

Executes generated code on data:
- Supports pandas DataFrames
- Pre/post-processing hooks
- Error handling
- Result management

#### SQL Execution

```python
def node_func_execute_agent_from_sql_connection(
    state,
    connection,
    code_snippet_key,
    ...
)
```

Executes code with SQL databases:
- SQLAlchemy connection support
- Database operations
- Error handling
- Result processing

#### Code Fixing

```python
def node_func_fix_agent_code(
    state,
    code_snippet_key,
    error_key,
    llm,
    ...
)
```

Repairs code using LLM:
- Error-based code fixing
- Retry management
- Logging support
- Code organization

#### Code Explanation

```python
def node_func_explain_agent_code(
    state,
    code_snippet_key,
    result_key,
    ...
)
```

Generates code explanations:
- LLM-based explanations
- Error case handling
- Formatted messaging

#### Output Reporting

```python
def node_func_report_agent_outputs(
    state,
    keys_to_include,
    result_key,
    ...
)
```

Creates structured reports:
- State information gathering
- Formatted reporting
- Message structuring

## Usage

### Basic Agent Creation

```python
agent = BaseAgent(
    # Add your parameters here
)
```

### Creating a Workflow

```python
workflow = create_coding_agent_graph(
    GraphState=YourGraphState,
    node_functions={
        "recommend_steps": your_recommend_function,
        "create_code": your_create_function,
        "execute_code": your_execute_function,
        "fix_code": your_fix_function,
        "explain_code": your_explain_function
    },
    recommended_steps_node_name="recommend_steps",
    create_code_node_name="create_code",
    execute_code_node_name="execute_code",
    fix_code_node_name="fix_code",
    explain_code_node_name="explain_code",
    error_key="error"
)
```

## Features

- **Modular Design**: Easy to extend and customize
- **Error Handling**: Robust error management and recovery
- **Human-in-the-Loop**: Optional human review and intervention
- **Multiple Data Sources**: Support for various data formats
- **Async Support**: Both synchronous and asynchronous operations
- **Streaming**: Real-time output streaming
- **Visualization**: Graph visualization capabilities
- **Reporting**: Structured output reporting

## Dependencies

- langchain
- langgraph
- pandas
- sqlalchemy
- IPython
- typing

## Best Practices

1. Always implement proper error handling
2. Use type hints for better code clarity
3. Provide clear documentation for custom node functions
4. Test workflows with both success and error cases
5. Monitor retry counts and error patterns
6. Use checkpointing for long-running workflows

## Contributing

[Add your contribution guidelines here]

## License

[Add your license information here]