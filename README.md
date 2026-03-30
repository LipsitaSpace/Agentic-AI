# Agentic-AI

## Defination

### Simple chatbot vs agent
-----------------------------------------------------
A normal chatbot usually does this:
1. User asks something
2. LLM replies once
3. Conversation ends


An agent does this:
1. User asks something
2. LLM thinks about the goal
3. It may call a tool
4. It reads the tool result
5. It decides the next move
6. It repeats until done


>Chatbot = answer

>Agent = act + observe + adapt


### Why agents matter
----------------------------------------------------------
LLMs are good at language, but not always reliable for:
```
current data
exact calculations
searching documents
performing external actions
```
Agents solve this by connecting the LLM to tools.

Example:

User: “What is the weather in Delhi and should I carry an umbrella?”

Agent flow:
```
identify location -> call weather tool -> read forecast -> reason about rain probability -> answer naturally
```
> Without tools, the model would have to guess. With tools, it can verify.

### Core parts of an agent
-------------------------------------------------
#### A basic agent has 3 parts:
1. **LLM** : The reasoning engine.

2. **Tools** : External functions the agent can use.

3. **Loop** : The repeat cycle that lets the agent act step by step.

> So the formula is :  **Agent = LLM + Tools + Loop**

### When to use an agent
---------------------------------------------------
Use an agent when the task:
```
  has multiple steps
  needs decision-making
  depends on external data
  needs repeated checking
  may change based on results
```
>Examples: scheduling, search and summarize, customer support workflows, coding assistants, research assistants, data extraction pipelines

💡 Do not use a full agent when a simple prompt is enough. If the task is one-shot and stable, a normal LLM call is often better.

### What makes an agent intelligent
--------------------------------------------------------------
An agent is not “smart” only because the LLM is smart.
It becomes useful because it can:
```
break work into steps
choose tools at the right time
react to tool output
stop when the goal is achieved
recover from errors
```
That ability to adapt is the key.

### A basic agent loop in plain English
-------------------------------------------------
Here is the simplest loop:
```
Read the user request.
Decide whether a tool is needed.
If yes, call the tool.
Read the result.
Decide whether more action is needed.
Repeat until complete.
Give the final answer.
```

### Why loops are powerful
---------------------------------------------------
The loop gives the agent the ability to improve its own next step.

Without loop:
```
one prompt
one response
```
With loop:
```
think
act
observe
revise
continue
```
> That makes it possible to handle complex tasks like: troubleshooting, multi-step research, planning workflows, iterative problem solving

## LLM as the Brain

### What does “LLM = Brain” actually mean?
-------------------------------------------------------------------
In an agent system, the LLM is not just generating text.

It is responsible for:
```
understanding the goal
reasoning about what to do next
deciding whether to use a tool
interpreting tool outputs
controlling the flow of the loop
```
So instead of: 👉 “generate answer”

it becomes: 👉 “think → decide → act → evaluate”

### LLM responsibilities inside an agent
-------------------------------------------------------
Think of the LLM as handling 4 core jobs

1. Understanding

  It reads:
```
user input
previous steps
tool results
```
  Example:
```
“Find best camera lens for open mic event under 30k”
It understands:
  domain → photography
  constraint → budget
  goal → recommendation
```

2. Reasoning

  This is where intelligence comes in.
  
  The LLM:
```
breaks the problem
decides steps
evaluates options
```

  Example reasoning:
```
open mic → low light
need wide aperture
budget constraint
maybe check current prices
```

3. Decision Making

  The LLM decides:
```
Do I need a tool?
Which tool?
What input to pass?
```

  Example:
```
needs price → call product API
needs weather → call weather API
simple question → answer directly
```

4. Response Generation

  Finally:
```
combine reasoning + tool outputs
generate a human-readable answer
```

### The “Thinking” problem (very important)
--------------------------------------------------------
Here’s a key truth:
```
👉 LLMs don’t actually “think” like humans
👉 They simulate reasoning using patterns
```
So how do we make them behave like thinkers?

By giving:
```
structured prompts
clear instructions
examples
constraints
```

### Prompt = Brain Instructions
-----------------------------------------------
The prompt defines how the LLM behaves.

A weak prompt:
```
“Answer the question”
```
A strong agent prompt:
```
“You are an AI agent.
Decide if a tool is needed.
If yes, return tool name + arguments.
Otherwise, answer directly.”
```
This is how we turn LLM into a decision-maker.

### Types of reasoning in agents
------------------------------------------------
1. Direct Answer

No tool needed.

Example:
```
“What is O(n)?”
```

2. Tool-based reasoning

LLM decides:

👉 “I cannot solve this alone”

Example:
```
“What is current weather?”
```

3. Multi-step reasoning

LLM plans multiple steps.

Example:
```
“Plan a 2-day trip under 10k”
```
Steps:
```
choose location
estimate travel cost
estimate stay
suggest itinerary
```

4. Reflective reasoning (advanced)

LLM checks itself:

 a. Is the answer correct?

 b. Did the tool fail?

 c. Do I need another step?


### Tool selection logic
------------------------------------------------
The LLM internally does something like:
```
IF:
information missing → use search tool
calculation needed → use calculator
real-time data needed → use API
ELSE:
answer directly
```

### How LLM thinks in an agent

User:
```
“What’s the temperature in Bangalore and should I go out?”
```
LLM internal flow:
```
Understand:
    location = Bangalore
    need current data
Decide:
    call weather tool
After tool result:
    temp = 32°C, no rain
Reason:
    hot but safe
```
Answer:
```
“It’s warm, you can go out but stay hydrated”
```

Common mistakes in LLM-as-brain design

    1. Over-trusting LLM
    2. Poor prompts
    3. No structure
    4. No stopping logic

> Agents usually force LLM to respond in format like JSON. (This makes the system: predictable, debuggable, reliable)

### Temperature & Control
-------------------------------------------------
LLM behavior depends on settings:
```
Low temperature (0–0.3)
→ more deterministic (good for agents)
High temperature (0.7+)
→ more creative (bad for tool decisions)
```
> For agents: keep temperature LOW

>design system to support the LLM, not blindly trust it
