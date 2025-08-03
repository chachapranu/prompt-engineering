# Basic Prompt Engineering Techniques

This section covers fundamental techniques for crafting effective prompts.

## 1. Be Clear and Specific

Ambiguity is the enemy of good prompts.  Clearly define the task, the desired output, and any relevant constraints.

**Example:**

*   **Poor Prompt:** "Write something about cats."
*   **Good Prompt:** "Write a short paragraph describing the physical characteristics of a Siamese cat."

## 2. Use Keywords and Phrases

Incorporate relevant keywords and phrases to guide the LLM towards the desired topic and vocabulary.

**Example:**

*   **Poor Prompt:** "Explain how computers work."
*   **Good Prompt:** "Explain the architecture of a computer, including the CPU, memory, and storage."

## 3. Provide Context

Give the LLM enough background information to understand the task and generate relevant responses.

**Example:**

*   **Poor Prompt:** "What is the capital?"
*   **Good Prompt:** "What is the capital of France?"

## 4. Specify the Output Format

Clearly define the desired output format, such as a paragraph, bullet points, a table, or a specific code format.

**Example:**

*   **Poor Prompt:** "Summarize this."
*   **Good Prompt:** "Summarize this in three bullet points."

## 5. Use Examples (Few-Shot Prompting)

Provide a few examples of the desired input-output pairs to demonstrate the task.

**Example:**

```
Input:  Translate "Hello, world!" to French.
Output: Bonjour, le monde !

Input: Translate "Goodbye, world!" to French.
Output: Au revoir, le monde !

Input: Translate "Thank you, world!" to French.
Output:
```

## 6. Iterative Refinement

Prompt engineering is an iterative process. Experiment with different prompts, analyze the results, and refine your prompts based on the LLM's responses.