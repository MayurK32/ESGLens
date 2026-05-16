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

1. https://www.youtube.com/watch?v=nkbtOplq9jM
-- While watching the video came to know that PageIndex builds a tree from document and then keep summarised content of each page as a node and it maintains parent child relationship. So context loss can be the issue, may be concluding earlier(not completed the video) but its thing which we cant ignore. From this tree it creates a json. and we need to send full json to LLM (High token cost) we can use techniques like TOON to reduce the same.
