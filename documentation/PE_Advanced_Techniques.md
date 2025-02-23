## Zero-shot Prompting

*   Description: This technique involves prompting the LLM to perform a task without providing any examples. The LLM relies on its pre-existing knowledge and understanding of language to generate the response.
*   Example: "Translate the following English sentence into French: 'The quick brown fox jumps over the lazy dog.'"
*   Use Case: Suitable for tasks that are relatively straightforward and well-defined, where the LLM is likely to have sufficient prior knowledge.
*   When to Use:  Tasks the LLM is likely to have learned during pre-training (e.g., translation, summarization of common topics).
*   When *Not* to Use:  Tasks requiring specialized knowledge, unusual formats, or complex reasoning that the LLM hasn't been explicitly trained on.

## Few-shot Prompting

*   Description: This technique involves providing the LLM with a few examples of the desired input-output pairs. This helps the LLM learn the desired behavior and generate similar outputs for new inputs.
*   Example: "Translate the following English sentences to French: 'Hello' -> 'Bonjour', 'Goodbye' -> 'Au revoir', 'Thank you' -> 'Merci'. Now translate 'Good morning'."
*   Use Case: Useful when the task is more complex or requires a specific style or format that the LLM may not be able to infer from a zero-shot prompt.
*   When to Use:  When you need a specific output style or format, or when the task is slightly more complex than what the LLM can reliably handle with zero-shot prompting.
*   When *Not* to Use: When the LLM already performs well with zero-shot prompting, or when creating examples is too time-consuming or difficult.

## Chain-of-Thought (CoT) Prompting

*   Description: This technique involves explicitly guiding the LLM's reasoning process by providing a sequence of intermediate steps or thought processes, mimicking human-like problem-solving.
*   Example: "Solve the following problem: A farmer has 15 sheep. All but 8 die. How many are left? Let's think step by step. First, identify the total number of sheep. Then, subtract the number of sheep that died from the total. The answer is 8."
*   Use Case: Effective for tasks that require logical reasoning, problem-solving, or step-by-step instructions.

### When to Use and Not Use CoT

Chain-of-Thought prompting works by leveraging the LLM's ability to simulate a step-by-step reasoning process.  It's based on the idea that explicitly guiding the LLM through intermediate steps improves its ability to solve complex problems.  Variations include using self-consistency to generate multiple CoT chains and selecting the most frequent answer.  Limitations include increased computational cost and potential for the LLM to get stuck in incorrect reasoning paths.  CoT is best suited for tasks requiring logical reasoning, multi-step problem solving, and where transparency of the reasoning process is important. It's less effective for tasks that rely primarily on pattern recognition or factual recall.

*   When to Use: Problems involving math, logic, multi-step reasoning, or where explaining the reasoning is important.
*   When *Not* to Use: Simple factual recall, tasks where the reasoning is obvious, or when speed is more critical than explainability.

## Meta Prompting

*   Description: This technique involves prompting the LLM to generate prompts for other tasks. It allows you to leverage the LLM's knowledge and creativity to design effective prompts for specific use cases.
*   Example: "You are an expert prompt engineer. Generate three different prompts that could be used to summarize a scientific article for a general audience."
*   Use Case: Helpful when you need to generate a variety of prompts for different tasks or when you want to explore different prompting strategies.
*   When to Use: When you need to generate many prompts for similar tasks, or when you want to explore different prompting approaches.
*   When *Not* to Use:  When you already have a well-defined prompt that works well.

## Self-Consistency

*   Description: This technique involves generating multiple responses to the same prompt and then selecting the most consistent and reliable answer. It helps to mitigate the LLM's tendency to sometimes produce incorrect or inconsistent outputs.
*   Example: "What is the capital of Australia? Generate five different responses and then select the most common answer."
*   Example (Math Problem): "Solve the following equation: 2x + 5 = 11. Generate three different solution paths and select the most consistent answer."
*   Example (Factual Question): "Who was the first president of the United States? Generate four different responses and select the answer that appears most frequently."
*   Use Case: Useful when accuracy and reliability are critical, such as in question answering or fact verification.
*   When to Use: When accuracy is paramount, and you're willing to expend more computational resources to get a more reliable answer.
*   When *Not* to Use: When speed is the primary concern, or when the task is relatively simple and the LLM is already highly accurate.

## Generate Knowledge Prompting

*   Description: This technique involves prompting the LLM to generate relevant knowledge or background information *before* attempting to solve a problem. This helps the LLM to access and utilize relevant information that may not be explicitly provided in the prompt.
*   Example: "Before answering the question 'What are the main causes of World War I?', first generate a list of key events and figures leading up to the war."
*    Example: "Question: What is the airspeed velocity of an unladen swallow?  Knowledge: First, we need to determine if this is an African or European swallow.  African swallows are generally larger and faster than European swallows..."
*   Use Case: Effective for tasks that require domain-specific knowledge or historical context.
*   When to Use: When the question requires specialized knowledge that the LLM might not have readily available or might hallucinate.
*   When *Not* to Use: When the question is straightforward and doesn't require any background information.

## Prompt Chaining

*   Description: This technique involves breaking down a complex task into a series of smaller, more manageable subtasks and then using the output of one prompt as the input for the next.
*   Example:
    *   Prompt 1: "Summarize the following article: \[insert article text here]."
    *   Prompt 2: "Based on the summary, identify the three main arguments presented in the article."
*   Use Case: Useful for complex tasks that require multiple steps or stages of processing.
*   When to Use: For complex, multi-step tasks that can be logically broken down into smaller, independent sub-tasks.
*   When *Not* to Use: For simple tasks that can be accomplished with a single prompt.

## Tree of Thoughts (ToT)

*   Description: ToT extends Chain-of-Thought by allowing the LLM to explore multiple reasoning paths concurrently, creating a tree-like structure of possible solutions. The LLM generates a "tree" of thoughts, where each node represents a partial solution or intermediate step.  The LLM then evaluates each branch of the tree, using a heuristic or scoring function to determine the most promising paths to explore further.  Unpromising paths are pruned, reducing the search space and improving efficiency. This allows for a more comprehensive exploration of the solution space, making it particularly useful for problems with a large number of possible solutions or where backtracking is necessary.
*   Use Case: Ideal for tasks requiring exploration of multiple possibilities, such as planning, game playing, or creative writing.
*  When to Use: Complex problem-solving, planning, or creative tasks where exploring multiple solution paths is beneficial.
*  When *Not* to Use:  Simple tasks, or when computational resources are severely limited.
*   Conceptual Example: For example, imagine asking an LLM to plan a surprise birthday party. ToT would allow it to consider different themes (e.g., superhero, princess, pirate), locations (e.g., park, backyard, restaurant), and guest lists simultaneously, evaluating the pros and cons of each (e.g., cost, feasibility, guest preferences) before settling on the best plan.  The LLM might generate a branch for a superhero party at the park, another for a princess party at home, and so on, evaluating each option and expanding the most promising ones.

## Retrieval Augmented Generation (RAG)

*   Description: RAG enhances LLM responses by retrieving relevant information from an external knowledge source (e.g., a database, a website, or a document repository) and incorporating it into the prompt.
*   Use Case: Essential when the LLM's internal knowledge is insufficient or outdated. RAG ensures responses are grounded in accurate and up-to-date information.
*   Example: "Answer the following question using information from the provided document: \[Question] \[Document]".
*   When to Use: When the LLM needs to answer questions based on specific, external information (e.g., a document, a database, a website).
*   When *Not* to Use: When the LLM's internal knowledge is sufficient, or when no relevant external knowledge source is available.

## Automatic Reasoning and Tool-use

*   Description: This technique empowers LLMs to automatically determine when and how to use external tools (e.g., calculators, APIs, search engines) to enhance their reasoning and problem-solving abilities.
*   Use Case: Enables LLMs to tackle tasks that require access to real-time information or specialized functionalities.
*    When to Use: When the task requires access to external tools or data that the LLM doesn't have internally.
*   When *Not* to Use: When the task can be solved solely with the LLM's internal knowledge.
*   Example: "Solve the following equation: 345 * 678 + 123 / 4. You can use a calculator."

## Automatic Prompt Engineer (APE)

*   Description: APE automates the process of prompt engineering by using an LLM to generate and evaluate different prompts for a given task. It iteratively refines the prompts based on their performance, leading to more effective prompts.
*   Use Case: Useful for optimizing prompts for specific tasks or datasets, especially when manual prompt engineering is time-consuming or difficult.
*   When to Use: When you have a large dataset and want to automatically optimize prompts for a specific task.
*   When *Not* to Use: When you have a small dataset or when you need very precise control over the prompt.

## Active-Prompt

*   Description: Active-Prompt allows the LLM to actively ask clarifying questions to the user *before* attempting to answer the original question. This helps to ensure that the LLM has a clear understanding of the user's intent and can generate a more relevant and accurate response.
*   Use Case: Beneficial when the initial prompt is ambiguous or lacks sufficient information.
*   When to Use:  When the user's query is likely to be ambiguous, incomplete, or require further clarification.
*   When *Not* to Use: When the user's query is already clear and unambiguous.
*   Example:
    *   **User:** "Tell me about bats."
    *   **LLM (with Active-Prompt):** "Are you interested in a specific type of bat, their biology, their role in the ecosystem, or something else?"

## Directional Stimulus Prompting

*   Description: This technique involves providing the LLM with a specific "stimulus" or example to guide its response in a particular direction. The stimulus can be a sentence, a phrase, or even an image.
*   Use Case: Helpful for controlling the style, tone, or content of the LLM's output.
*   When to Use:  When you want to influence the style, tone, or specific aspects of the content.
*   When *Not* to Use: When you want a completely open-ended response.
*   Example: "Write a story about a cat. Stimulus: 'The moon was full, and the cat's eyes gleamed.'"

## Program-Aided Language Models (PAL)

*   Description: PAL combines the strengths of LLMs with the precision of programming languages. The LLM generates a program that performs the desired task, and the program's output is then used as the final answer.
*   Use Case: Well-suited for tasks that require complex calculations, data manipulation, or logical reasoning.
*   When to Use:  For tasks involving precise calculations, logical reasoning, or data manipulation where a programmatic approach is beneficial.
*   When *Not* to Use: For tasks that are primarily text-based and don't require complex calculations or logic.

## ReAct (Reason + Act)

*   Description: ReAct enables LLMs to interleave reasoning and action steps. The LLM first reasons about the task, then takes an action (e.g., searching the web), observes the result, and then reasons about the next step.  While true "acting" requires an environment the LLM can interact with, the *principle* of ReAct can be simulated in prompts.
*   Use Case: Ideal for tasks that require exploration of the environment or interaction with external systems.  In a prompting context, it's useful for tasks requiring information gathering.
*  When to Use:  When the task requires a combination of reasoning and information gathering (often simulated through searching).
*  When *Not* to Use: When the task is purely reasoning-based or purely action-based (and you don't have an environment for the LLM to act in).
*   Example (Simulated ReAct in a prompt):
    ```
    Question: What is the population of the capital city of the country where the Eiffel Tower is located?

    Reasoning: 1. I need to identify the country where the Eiffel Tower is located. 2. I need to find the capital city of that country. 3. I need to find the population of that capital city.
    Action: Search for "country where the Eiffel Tower is located".
    Observation: The Eiffel Tower is located in France.
    Action: Search for "capital of France".
    Observation: The capital of France is Paris.
    Action: Search for "population of Paris".
    Observation: The population of Paris is approximately 2.1 million.
    Answer: The population of the capital city of the country where the Eiffel Tower is located is approximately 2.1 million.
    
## Reflexion

*   Description: Reflexion equips LLMs with the ability to reflect on their past actions and learn from their mistakes. The LLM maintains a memory of its previous attempts and uses this information to improve its future performance.
*   Use Case: Useful for tasks that require trial and error or iterative refinement.
*   When to Use: Tasks where iterative improvement and learning from past attempts are beneficial.
*   When *Not* to Use: Tasks that are straightforward and don't require learning from past attempts.
*   Example (Conceptual - Requires a system that can track LLM attempts):
    *   **Prompt (Attempt 1):** "Write a short poem about a cat."
    *   **LLM Response (Attempt 1):** (Generates a poem)
    *   **Reflexion Prompt:** "You previously wrote this poem: [previous poem]. It was too short and didn't rhyme. Try again, making it longer and using an AABB rhyme scheme."

## Multimodal CoT

*   Description: Multimodal CoT extends CoT to handle multimodal inputs, such as images, audio, and video. The LLM reasons about the different modalities and integrates them to arrive at the final solution.
*   Use Case: Enables LLMs to tackle tasks that require understanding of both text and other types of data.
*   When to Use: When the input includes multiple modalities (e.g., text and images).
*   When *Not* to Use: When the input is purely text-based.

## Graph Prompting

*   Description: Graph Prompting structures the prompt as a graph, where nodes represent concepts or entities and edges represent relationships between them. This allows the LLM to reason about the relationships between different elements of the prompt. This technique is particularly useful when dealing with knowledge graphs or scenarios where entities have complex interdependencies. By representing information in a graph format, the LLM can more easily understand and reason about the connections between different pieces of information.
*   Use Case: Helpful for tasks that involve complex relationships or dependencies between different entities. For example, consider a scenario where you want to query a knowledge graph about historical figures and their relationships. A graph prompt might represent individuals as nodes and relationships (e.g., 'spouse of', 'child of', 'ruled over') as edges.  The LLM could then use this graph structure to answer questions like, "Who was the spouse of Henry VIII's son?"
* Example: "Represent the following information as a graph: (Node: Albert Einstein, Edge: 'Developed', Node: Theory of Relativity), (Node: Marie Curie, Edge: 'Discovered', Node: Radium), (Node: Marie Curie, Edge: 'Discovered', Node: Polonium). Now, using this graph, answer: What did Marie Curie discover?"
*   When to Use: When dealing with relationships between entities, especially in knowledge graphs or complex systems.
*   When *Not* to Use: When relationships between entities are simple or not relevant to the task.

## Chain-of-Verification (CoV)
* Description: First, answer the question, and then create verification questions to double check the answer.
* Example:
     *Question:* What is the capital of France?
     *Answer:* The capital of France is Paris.
     *Verification Questions:*
        1.  Is Paris a city in France?
        2.  Does France have a capital city?
        3.  Is there any other city that could be considered the capital of France?
*   Use Case: Useful when accuracy and reliability are critical
*   When to Use: When accuracy of the output needs to be confirmed.
*   When *Not* to Use: When the user is asking for a creative task such as story creation.
