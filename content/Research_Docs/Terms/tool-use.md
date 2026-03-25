# Tool Use

Tool use is the mechanism by which LLM agents interact with external systems, databases, APIs, calculators, search engines, and any other capability beyond text generation. It extends the model from a reasoning engine into a system that can retrieve data, perform computation, communicate with services, and take action in the world.

## How It Works

An LLM generates text. It cannot natively query a database, call an API, send an email, or search the web. Tool use bridges this gap through a structured protocol. The agent harness registers available tools by providing the model with descriptions: each tool's name, purpose, required parameters, and expected return format. When the model determines it needs external capability, it generates a structured tool call (typically JSON) that the harness intercepts, validates, executes against the actual system, and returns the result to the model's context.

Tools fall into several functional categories. **Data retrieval tools** query databases, search knowledge bases, and fetch documents. **Computation tools** perform calculations, run code, and execute transformations the model cannot do reliably through text generation. **Communication tools** send emails, post messages, and create notifications. **Action tools** update records, trigger workflows, and modify system state. **Search tools** provide web search, semantic search, and specialized domain search.

The model does not inherently understand any specific tool. It learns to use tools through the descriptions provided by the harness, combined with general tool-use capabilities acquired during training. This means the quality of tool descriptions directly affects the quality of tool usage. Vague descriptions produce incorrect tool selections. Ambiguous parameter documentation produces malformed calls. Precise, well-structured tool descriptions are as important as the tools themselves.

The **Model Context Protocol (MCP)** is emerging as a universal adapter standard for tool integration. Rather than building custom integrations for every tool-model combination, MCP defines a standard interface that any tool provider can implement and any model framework can consume. This is analogous to USB standardizing peripheral connections: instead of proprietary connectors for every device, a single protocol enables universal interoperability. MCP accelerates the tool ecosystem by making it trivial to expose any system capability to any agent framework.

Professional domains typically require 20 or more tools per workflow. A sales agent might need CRM access, email integration, calendar management, document retrieval, pricing calculator, approval workflow, and analytics dashboard tools. Each tool expands what the agent can accomplish, and the combination of tools enables workflows that no single tool supports alone.

## Medical Analogy

Tools are the physician's instruments and diagnostic systems. The stethoscope, the blood pressure cuff, the lab order system, the imaging equipment, the pharmacy database, the electronic prescribing system. The physician's knowledge tells them which instrument to use and when. The instruments extend their capability beyond observation and reasoning into measurement, diagnosis, and treatment. A brilliant physician without tools is limited to history-taking and physical exam. With tools, they can practice the full scope of medicine.

## Why It Matters for Enterprise AI

Tool use is what transforms AI from a knowledge system into a workflow system. The difference between answering "What is our return policy?" and actually processing a return, updating inventory, issuing a refund, and notifying the customer is the difference between information and action. That gap is where the >80% of organizations failing to see EBIT impact from AI are stuck: they built information systems when they needed action systems.

Your enterprise tools are your strategic moat. Every organization has GPT-4 access. Not every organization has an agent that can query their proprietary ERP, their custom pricing engine, their internal compliance checking system, and their domain-specific analytics platform. The tools you expose to your agents, and the quality of those tool descriptions, encode your operational knowledge. This is ground truth at the infrastructure level: your systems, your data, your processes, made available to AI through tool interfaces that reflect how your organization actually operates.

## Key Technical Details

- Tool descriptions: structured format (name, purpose, parameters, returns) presented to models
- Categories: data retrieval, computation, communication, action, search
- MCP (Model Context Protocol): emerging universal adapter standard for tool integration
- Tool selection: model chooses tools based on descriptions, not hard-coded logic
- Description quality: vague tool docs produce poor tool selection and malformed calls
- 20+ tools per professional domain workflow is typical for enterprise agents
- Tool chaining: output of one tool becomes input to the next in multi-step workflows
- Validation: harness validates tool calls before execution to prevent errors

## Related Terms

- [Agents](agents.md) - the autonomous systems that use tools
- [Agent Harnesses](agent-harnesses.md) - the infrastructure that registers and manages tools
- [Trajectories](trajectories.md) - records of tool calls and their results in agent workflows
- [Reasoning](reasoning.md) - the cognitive process that determines which tools to use and when

*Part of the [Understanding LLMs Through the Medical Training Analogy](../../00-overview-the-journey.md) research collection.*
