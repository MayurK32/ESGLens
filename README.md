# ESGLens

ESGLens is a .NET 8 document intelligence API built for ESG analysts and enterprise teams.

# Journey

I will be documenting every decision I will take during design, development of this project under this section.

## Design

### Day 1 - 16/05/2026

I started with asking myself some clarifying questions for the scope of version 1.

#### a. What type of documents are allowed in ESGLens
- For now only PDF with less than 50 MB size.

#### b. Any restrictions on token limits per session or user?
- This version will give unlimited access to everyone.

#### c. Tradeoff between Fast but less accurate vs slow but high accurate?
- Going with a system which will respond within seconds but reasonably give good amount of accuracy (around 80-90%).

Now because I have created similar thing for company projects (not exactly same), I have experience with RAG, but I dont want to jump straight into design using RAG. Few days back I have heard of PageIndex, so will first compare both and then will make decision of which technique suits our application better.

### Resources for this decision

#### 1. https://www.youtube.com/watch?v=nkbtOplq9jM

- While watching the video came to know that PageIndex builds a tree from document and then keep summarised content of each page as a node and it maintains parent child relationship.
- So context loss can be the issue, may be concluding earlier(not completed the video) but its thing which we cant ignore.
- From this tree it creates a json.
- and we need to send full json to LLM (High token cost)
- we can use techniques like TOON to reduce the same.

#### 2. https://github.com/VectifyAI/PageIndex#agentic-vectorless-rag-an-example

- According to benchmark for financial document analysis, pageindex has great accuracy.
- Benchmark results: https://github.com/VectifyAI/Mafin2.5-FinanceBench

<img width="1013" height="612" alt="image" src="https://github.com/user-attachments/assets/c19ffde6-ef35-4b9c-a38a-0840396feeee" />

#### 3. Now I am using chatgpts deep research to get more information on this
Prompt used:
Act as a senior architect who has 10+ years of experience in AI productions applications. You have knowledge of current rapidly changing AI scene.

I am working on a project ESGLens, which will allow users to put ESG documents and chat with them.

I have experience with RAG, and I heard about PageIndex and accuracy that its giving is great in comparison to RAG based tools.

I want you to research and create a comparison report with all tradeoffs so that i can take a decision to ahead with either of the option.

The project stack would be .Net primarily, angular and python if we need to use python only packages which are not available in .net

##### Chat - https://chatgpt.com/share/6a081830-a6a4-83ec-9310-d7cbefe6b5a1
---
### Decision

I would argue that because ESGLens is domain specific and has higher accuracy but there is scalability issues but for our application we need to answer from attached documens itself so we wil put limit to number of pdfs attached. So after looking at accuracy I have decided to go ahead with pageindex.
