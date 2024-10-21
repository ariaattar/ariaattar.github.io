# Vertical vs. General AI Agents: Where is the value?

The next major paradigm shift in technology is clearly shaping up to be autonomous AI systems (Agents), with a growing distinction between general and specialized vertical agents. Here are my thoughts on where I think value will be built—specifically around the commoditization of general agents and the unique value of vertical agents.

### The Commoditization of General Agents

I think general agents will be commoditized first by the big labs like OpenAI, Anthropic, and DeepMind. We've already seen this happen with voice-to-voice AI companies, which got commoditized with OpenAI's new `gpt-4o` model. We're already seeing OpenAI slowly rolling out agentic capabilities with their [swarm](https://github.com/openai/swarm) framework.

### Where's the Value in a World of General Intelligence?

The majority of new value will be created by startups building highly specialized agents for vertical markets. These agents will tackle tasks that general language models struggle with, even as general models continue to scale up in parameter size and improve their reasoning capabilities.

### Task Distribution and Entropy


A recent paper by Apple, [**"GSM-Symbolic: Understanding the Limitations of Mathematical Reasoning in Large Language Models,"**](https://arxiv.org/pdf/2410.05229) provides insights into the performance of LLMs, including state-of-the-art models like OpenAI's o1 and o1-mini. 

The study introduces **GSM-Symbolic**, a benchmark that generates diverse variants of grade-school math questions. Below are the performance metrics across different models:

### Model Performance on GSM-Symbolic vs. GSM8K

| Model               | GSM-Symbolic Accuracy (%) | GSM8K Accuracy (%) | Performance Variation (±) |
|---------------------|---------------------------|--------------------|---------------------------|
| `o1-mini`         | 94.5                      | 93.0               | ±1.6%                     |
| `o1-preview`      | 92.7                      | 96.0               | ±1.8%                     |
| `gpt-4o`          | 94.9                      | 95.0               | ±1.87%                    |
| `Llama3-8b-instruct` | 74.6                  | 74.0               | ±2.94%                    |

While the models perform well on GSM8K, they exhibit **non-negligible performance variation** on GSM-Symbolic, with `o1-preview` showing a slight dip in accuracy.

---

### Performance on GSM-NoOp Dataset (Irrelevant Information)

| Model               | GSM-NoOp Accuracy (%) | Performance Variation (±) |
|---------------------|-----------------------|---------------------------|
| `o1-mini`         | 66.0                  | ±4.60%                    |
| `o1-preview`      | 77.4                  | ±3.84%                    |
| `gpt-4o`          | 63.1                  | ±4.53%                    |
| `Llama3-8b-instruct` | 18.6               | ±3.86%                    |

---

### Key Observations

1. LLMs, even state-of-the-art ones including `o1-preview` and `o1-mini`, have difficulty generalizing to diverse variants of problems they are supposed to be good at.  
2. Performance decreases and variance increases as task complexity grows.  
3. Models struggle significantly with irrelevant information.

   > *"As the difficulty increases from GSM-M1 → GSM-Symb → GSM-P1 → GSM-P2, the distribution of performance shifts to the left (i.e., accuracy decreases), and the variance increases."* 

Another relevant paper on this topic: [Large Language Models Struggle to Learn Long-Tail Knowledge](https://arxiv.org/pdf/2211.08411)

### Implications for Agentic Systems

- Enterprise-specific workflows are often not represented in general-purpose LLM training data.  
- In-context learning falls short for complex, multi-step tasks.  
- High variability between enterprises exacerbates the out-of-distribution (OOD) problem.  
- Native chain-of-thought reasoning doesn't seem to solve these issues.

This is all consistent with what we've seen empirically with TensorStax.

### Opportunities for Vertical-Specific AI Agents

These challenges, particularly the multiplicative nature of errors in agentic systems, indicate that general LLMs face substantial hurdles in **specialized, enterprise-specific scenarios**. Each additional step in an agent's process introduces new opportunities for error, and those errors can accumulate exponentially.

This opens up substantial opportunities for **vertical-specific agents** that are built from the ground up to handle the unique, high-entropy tasks of specific industries or business processes. These specialized agents need to outperform general-purpose agents by **orders of magnitude** to provide true value over general agents.

<img src="https://i.imgur.com/Lvdzp7W.png" alt="Performance Decay Curve" width="600" height="auto">

### Solving Vertical Agent Challenges

The right question to ask here is: how can we build autonomous agents that outperform general agents on OOD tasks? There are two main approaches we've found to be most promising, both of which can help build a competitive moat:

1. **Synthetic/Proprietary Data** - Creating high-quality, domain-specific training data to get convergence on specialized tasks.  
2. **LLM Compiler Paradigm** - Developing a middle layer between existing software and LLMs to provide a more abstract interface to existing software. This allows for more deterministic and reliable agent behavior. The challenge lies in finding the right balance of abstraction that allows for generality while maintaining determinism.

I'll spend more time digging deeper into these ideas in a future blog post.

At TensorStax, we're working on a mix of both but are more focused on the latter, as we've seen it has the highest impact on reliability while laying the foundation for a compounding moat. There's an art to finding the sweet spot between generality and deterministic behavior in vertical agents, which is crucial for their effectiveness.

## Types of Vertical Agents

We can categorize vertical agents into two main types:

1. **Product Ecosystem-Native Agents** - These are specialized for a specific product or platform.  
   - `Example: An agent built specifically for a new agent-native CRM system.`  
2. **Vertical-Specific, Tool-Agnostic Agents** - These are optimized for a certain industry or function, but can work across different tools.  
   - `Example: An agent optimized for operating both Salesforce and HubSpot for SalesOps tasks.`

I think the latter is particularly interesting and potentially a lot more valuable as it drives the friction of change to zero, which is often a major barrier for many B2B companies, especially those selling mission-critical software like CRMs or infrastructure.

### Why Incumbents Will Struggle with Vertical Agents

A common question is why incumbents can't simply build their own vertical agents. The answer lies in the key advantage of platform-agnostic vertical agents: flexibility and broad applicability across entire verticals (e.g., SalesOps or Data Engineering).

Incumbents face challenges in creating versatile agents due to ecosystem lock-in incentives. For example, in data engineering:

- A typical stack includes Apache Airflow, dbt, Snowflake, and Fivetran.  
- An agent built by Fivetran would excel at Fivetran-specific tasks but likely struggle with competing tools.  
- A platform-agnostic vertical agent could work seamlessly across the entire stack, providing value no single incumbent can match.

This holistic approach reduces friction for businesses using diverse toolsets, particularly valuable as tasks become more complex and entropy increases—areas where general-purpose LLMs often struggle.


### Looking Ahead

I believe the most significant opportunities in the agent space lie in creating highly specialized, vertical-specific agents that can seamlessly integrate with existing workflows and tools, giving end-to-end value to customers given some input—for us at TensorStax, that input is data. The main focus for these agents should be optimizing accuracy and precision, on more and more complex tasks over time.

Building in this space isn't just about maximizing intelligence—it's about applying that intelligence in highly specific, valuable ways. I think there's a lot left to be discovered around the role of base LLMs in agentic systems. 

If I had to bet, I would say the key is building the right abstractions optimized for allowing the LLMs to interact more easily with the world. An example I often give is: we don't code in 0s and 1s just because machines understand them better; we've built abstractions called programming languages that allow us to interact with machines in a way that is natural and easy for humans. I think the same approach is needed for LLMs.
