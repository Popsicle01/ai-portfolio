# RAG System — Learning Observations

## What Worked
- Q1 (attack method): retrieved correct GCG chunk, answered well
- Q3 (defense): retrieved defense chunk, gave detailed accurate answer
- Q5 (attention): retrieved transformer chunk, answered correctly

## What Failed + Why
- Q2 (attack success rate): retriever returned defense chunk instead
  of attack chunk. "Success rate" matched "mitigation success" in 
  defense text — semantic overlap caused wrong retrieval.
  
- Q4 (gender bias %): "56.5%" was in the text but retriever returned
  duplicate chunks, missing the specific statistic.

## Key Insight
Retrieval quality > model size in RAG systems.
A small model with the RIGHT chunk beats a large model with the wrong one.
Duplicate chunks in vectorstore cause retrieval failures — always deduplicate.

## Fix Applied
- Added deduplication before storing chunks
- More specific queries reduce semantic ambiguity
- verbose=True mode prints retrieved chunks for debugging

## Real-World Implication
Production RAG systems use chunk IDs, metadata filtering, and 
hybrid search (semantic + keyword) to avoid these failures.
This is an active research area — knowing the failure modes is 
what separates junior from senior ML engineers.
```
