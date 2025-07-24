# Safety Analysis and Control for AI Agents - Annotated Bibliography 
Author: Aarya Doshi, Carnegie Mellon University

## Context


## 1. Key Resources
Mislav Balunovic, Luca Beurer-Kellner, Marc Fischer, and Martin Vechev. 2024. [AI Agents with Formal Security Guarantees](https://openreview.net/forum?id=c6jNHPksiZ).
>  Proposes a formal security analyzer that enforces constraints on agent actions using a DSL and information flow control, preventing specific tool call sequences or data flows. Security rules are theoretically sound, with IFC proofs, but rely on classifiers and pattern-matching to detect PII, secrets, unsafe code, etc, which aren't necessarily reliable. Supports that having this info explicitly provided by tool developers can help provide an actual guarantee. Very helpful for showing that policy enforcement is possible, but also focuses mostly on blocking security risks like prompt injection and data leaks. Building on this would also allow developers to write policies that allow safe actions without user confirmation, allowing for controlled autonomy.

Edoardo Debenedetti, Ilia Shumailov, Tianqi Fan, Jamie Hayes, Nicholas Carlini, Daniel Fabian, Christoph Kern, Chongyang Shi, Andreas Terzis, and Florian Tramèr. 2025. [Defeating Prompt Injections by Design](https://doi.org/10.48550/arXiv.2503.18813). 
> CaMeL wraps the LLM in an interpreter that controls both data and control flow of agent to enforce security policies and prevent prompt injection. Introduces idea of "capabilities" as metadata assigned to data, describing where it came from and who is allowed to read it. Capabilities are automatically assigned by the system and focus only on data visibility to only block behavior that violates access permissions. Can easily be adapted to block other tool operations and enable more controlled autonomy. Utilizes Dual LLM pattern. Discusses finding balance between system security and minimizing user fatigue, depending on application.

Luca Beurer-Kellner, Beat Buesser Ana-Maria Creţu, Edoardo Debenedetti, Daniel Dobos, Daniel Fabian, Marc Fischer, David Froelicher, Kathrin Grosse, Daniel Naeff, Ezinwanne Ozoani, Andrew Paverd, Florian Tramèr, and Václav Volhejn. 2025. [Design Patterns for Securing LLM Agents against Prompt Injections](https://doi.org/10.48550/arXiv.2506.08837). 
> Proposes a set of design patterns for building agents resistant to prompt injections, through different ways of constraining the agent's actions. They discuss each pattern in terms of the tradeoff between utility and security, which is a very relevant framing that supports our approach of treating each design choice as mindful risk acceptance rather than pursuing absolute security. They also use 10 varying case studies to demonstrate how their designs would apply, which is helpful in showing how different risk tolerance policies would be more appropriate for different tasks and contexts.

K. J. Kevin Feng, David W. McDonald, and Amy X. Zhang. 2025. [Levels of Autonomy for AI Agents](https://doi.org/10.48550/arXiv.2506.12469). 
> Working paper that argues an agent's level of autonomy can be treated as a deliberate design choice, proposing 5 different increasing levels of autonomy and a framework to mechanism to "prescribe" a max level of autonomy for an agent based on its capabilities and environment. Supports our proposal to push tool developers to think about and openly communicate the capabilities of their tools, and for agent designers to mindfully build in controls depending on task and environment. The autonomy certificates are a little beyond our scope, but I think starting with thinking about what level of autonomy would be safe and then working backwards to figure out how to enforce it is the mindset we want.

> Manuel Costa, Boris Köpf, Aashish Kolluri, Andrew Paverd, Mark Russinovich, Ahmed Salem, Shruti Tople, Lukas Wutschitz, and Santiago Zanella-Béguelin. 2025. [Securing AI Agents with Information-Flow Control](https://doi.org/10.48550/arXiv.2505.23643). 
  > Dynamic taint-tracking paper. Tracks confidentiality and integrity labels to deterministically enforce security policies. Also uses Dual LLM pattern, variable masking, and IFC. Enforces policies during planning, to avoid "unsafe plans". Assumes that labels are statically attached to data or can be easily inferred, directly supporting need for MCP extension for increased metadata for tool outputs. Overly formal writing, but demonstrates that labels can help enforce safety without too much of a loss of utility. Evalutes using AgentDojo.


Peter Yong Zhong, Siyuan Chen, Ruiqi Wang, McKenna McCall, Ben L. Titzer, Heather Miller, and Phillip B. Gibbons. 2025. [RTBAS: Defending LLM Agents Against Prompt Injection and Privacy Leakage](https://doi.org/10.48550/arXiv.2502.08966).
> Dynamic taint-tracking with dependency screening to detect prompt injection and privacy leakage. Uses LLM-as-a-judge and attention-based salency to determine which regions of context influence tool calls and responses, to selectively propagrte security metadata. Shows that IFC can help enforce security policies at runtime, but is limited by the need for manually labeled user/tool messages and the cost of dependency screening.


**Note**: Many of these authors show up across multiple key papers in this list, Debenedetti, Beurer-Kellner, Tramèr, etc. They seem to be leading a lot of the work on prompt injection defenses for agents and formal agent security. Might be worth keeping an eye on their future papers or seeing who builds on or cites their work.

## Other Resources 
Edoardo Debenedetti, Jie Zhang, Mislav Balunović, Luca Beurer-Kellner, Marc Fischer, and Florian Tramèr. 2024. [AgentDojo: A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses for LLM Agents] (https://doi.org/10.48550/arXiv.2406.13352). 
> Present AgentDojo, an evaluation framework for agents that execute tools over untrusted data. Focus on prompt injection tasks, but very helpful to evaluate agent security in adversarial settings.
