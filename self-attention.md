# Lecture Notes: Self-Attention Mechanism

## 1. The Problem We're Solving

**Context matters in language.** Consider:
- "The bank was steep" (riverbank)
- "The bank was closed" (financial institution)

The word "bank" needs to "look at" other words to determine its meaning. Self-attention is the mechanism that allows each word to look at all other words in a sequence.

## 2. The Core Intuition

Think of self-attention as a **relevance-weighted average**:

1. For each word, we ask: "Which other words are relevant to understanding me?"
2. We compute relevance scores between every pair of words
3. We create a new representation by taking a weighted average based on relevance

**Example:** In "The cat sat on the mat," when processing "sat":
- High attention to "cat" (who sat?)
- High attention to "mat" (sat where?)
- Lower attention to "the" (less informative)

## 3. The Three Components: Query, Key, Value

For each word, we create three vectors:

- **Query (Q)**: "What am I looking for?"
- **Key (K)**: "What do I contain?"
- **Value (V)**: "What information do I actually provide?"

**Analogy:** Library database
- Query = your search terms
- Key = book keywords/metadata
- Value = actual book content

## 4. The Mechanism (Step by Step)

For each word position:

**Step 1: Compute attention scores**
- Compare your Query with every word's Key
- Score = Q · K (dot product)
- High score = high relevance

**Step 2: Normalize scores**
- Apply softmax to get weights that sum to 1
- These are your "attention weights"

**Step 3: Aggregate information**
- Take weighted sum of all Values
- Output = Σ (attention_weight × Value)

## 5. Simple Mathematical View

```
Attention(Q, K, V) = softmax(QK^T / √d_k) V
```

Where:
- QK^T: All query-key comparisons (relevance scores)
- √d_k: Scaling factor (prevents large values)
- softmax: Converts scores to probabilities
- Multiply by V: Get weighted information

## 6. Why "Self" Attention?

**Self** = attending to the same sequence
- Each word attends to all words (including itself)
- Contrast with encoder-decoder attention (cross-attention)

## 7. Multi-Head Attention

Instead of one attention mechanism, use multiple "heads" in parallel:
- Each head learns different relationships
- Head 1 might learn syntax (subject-verb)
- Head 2 might learn semantics (related concepts)
- Head 3 might learn position (nearby words)

Then concatenate outputs from all heads.

## 8. Key Properties

1. **Permutation invariant** (without positional encoding)
   - Order doesn't matter inherently
   - That's why we need to add position information

2. **No sequence length limit**
   - Can attend to any length sequence
   - (Though computational cost is O(n²))

3. **Parallel computation**
   - Unlike RNNs, can process all positions simultaneously

## 9. Concrete Example

Sentence: "The cat chased the mouse"

When processing "chased":
- High attention to "cat" (subject)
- High attention to "mouse" (object)
- Lower attention to "the" (grammatical)

The output representation of "chased" now contains information from "cat" and "mouse," helping the model understand the complete action.

## 10. Common Student Questions

**Q: Why three separate matrices (Q, K, V)?**
A: Separates "what I'm looking for" from "what I contain" from "what I output." This flexibility allows richer representations.

**Q: Why the scaling factor √d_k?**
A: Prevents dot products from getting too large (which would make softmax very peaky).

**Q: How is this different from RNNs?**
A: RNNs process sequentially; attention sees everything at once. Attention has no built-in notion of order.

## Summary

Self-attention = **learned, dynamic routing of information**
- Each position decides what's relevant
- Creates context-aware representations
- Foundation of transformer architecture
