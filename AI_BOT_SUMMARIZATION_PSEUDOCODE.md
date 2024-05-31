# AI Bot Summarization Pseudocode

## Purpose
The AI bot "Hal" will process user requests to summarize content using the `fabric` project's summarization capabilities. The bot will follow the instructions outlined in the `system.md` file within the `summarize` pattern directory.

## Pseudocode

### Function: infer_user_request
- Input: user_input (string)
- Output: command (string)

1. Define a list of available commands: `command_list = ["summarize", "analyze_claims", "extract_wisdom"]`
2. Analyze the `user_input` to determine the user's intent.
3. If the intent is to summarize content, return the command "summarize".
4. If the intent is to analyze claims, return the command "analyze_claims".
5. If the intent is to extract wisdom, return the command "extract_wisdom".
6. If the intent is unclear, return a default command or prompt the user for clarification.

### Function: run_command
- Input: command (string), content (string)
- Output: result (string)

1. If the command is "summarize":
    - Call the `fabric` project's summarization function with the provided content.
    - Format the output according to the instructions in the `system.md` file:
        - Create a section called "ONE SENTENCE SUMMARY:" with a single 20-word sentence summary.
        - Create a section called "MAIN POINTS:" with a list of the 10 most important points (no more than 15 words per point).
        - Create a section called "TAKEAWAYS:" with a list of the 5 best takeaways.
    - Return the formatted result.
2. If the command is "analyze_claims":
    - Call the `fabric` project's claim analysis function with the provided content.
    - Format the output as needed.
    - Return the formatted result.
3. If the command is "extract_wisdom":
    - Call the `fabric` project's wisdom extraction function with the provided content.
    - Format the output as needed.
    - Return the formatted result.
4. If the command is unknown, return an error message or prompt the user for clarification.

### Example Usage

```python
# Example user input
user_input = "Can you summarize this document for me?"

# Infer the user's request
command = infer_user_request(user_input)

# Example content to be summarized
content = """
The quick brown fox jumps over the lazy dog. This sentence contains all the letters of the English alphabet.
"""

# Run the command and get the result
result = run_command(command, content)

# Output the result
print(result)
```

## Implementation

### Function: infer_user_request
```python
def infer_user_request(user_input):
    command_list = ["summarize", "analyze_claims", "extract_wisdom"]
    if "summarize" in user_input.lower():
        return "summarize"
    elif "analyze" in user_input.lower() and "claim" in user_input.lower():
        return "analyze_claims"
    elif "extract" in user_input.lower() and "wisdom" in user_input.lower():
        return "extract_wisdom"
    else:
        return "summarize"  # Default command if intent is unclear
```

### Function: run_command
```python
def run_command(command, content):
    if command == "summarize":
        # Call the fabric project's summarization function (placeholder)
        summary = fabric_summarize(content)
        # Format the output according to the instructions in the system.md file
        one_sentence_summary = "ONE SENTENCE SUMMARY: " + summary['one_sentence']
        main_points = "MAIN POINTS:\n" + "\n".join([f"{i+1}. {point}" for i, point in enumerate(summary['main_points'])])
        takeaways = "TAKEAWAYS:\n" + "\n".join([f"{i+1}. {takeaway}" for i, takeaway in enumerate(summary['takeaways'])])
        result = f"{one_sentence_summary}\n\n{main_points}\n\n{takeaways}"
        return result
    elif command == "analyze_claims":
        # Call the fabric project's claim analysis function (placeholder)
        analysis = fabric_analyze_claims(content)
        return analysis
    elif command == "extract_wisdom":
        # Call the fabric project's wisdom extraction function (placeholder)
        wisdom = fabric_extract_wisdom(content)
        return wisdom
    else:
        return "Error: Unknown command"
```
