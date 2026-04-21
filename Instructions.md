# Task: Research Rumble - Tokenizers

**Time Limit:** 45 Minutes
---

## 1. Background: What Standard BPE Does

Byte Pair Encoding (BPE) is a simple, greedy compression/tokenization algorithm:

* Start with a sequence of bytes (characters).
* Count all adjacent pairs.
* Merge the **most frequent pair** into a new token.
* Repeat for **K merges**.

Identify what are the possible issues with this approach.

---

## 2. The Core Problem with Greedy BPE

```python
def generate_adversarial_corpus():
    """
    Constructs a corpus specifically designed to test your BPE implementation.
    """
    s1 = "abacaba" * 100
    s2 = "aaaaa" * 50
    s3 = ("xf" * 50) + ("xe" * 50) + ("xd" * 50)
    s4 = "zyxwvutsrqponmlkjihgfedcba" * 20

    return s1 + s2 + s3 + s4

corpus = generate_adversarial_corpus()
```
Test your implementation of BPE On the above tokenizer and try to identify the issues that exist.

---

## 3. Phase 1 — Implement Standard BPE

### Task

Implement a basic BPE tokenizer:

```python
class BPETokenizer:
    def train(self, corpus: str, k_merges: int):
        pass

    def encode(self, text: str):
        pass

    def decode(self, tokens):
        pass
```

### Requirements

* Treat input as a sequence of **bytes/characters**
* At each step:

  * Count all adjacent pairs
  * Merge the most frequent pair
* Replace **all non-overlapping occurrences**
* Repeat for `k_merges`

---

### Reflection (Important)

After implementing, answer:

> What are the weaknesses of your implementation?

You are expected to identify issues such as:

* Overlap ambiguity
* Non-deterministic tie-breaking
* Loss of globally optimal merges
* Sensitivity to merge order

---

## 4. Phase 2 — Design an improved version of BPE that can handle the issues identified in Phase 1.

```python
class ImprovedTokenizer:
    def train(self, corpus: str, k_merges: int):
        pass

    def encode(self, text: str):
        pass

    def decode(self, tokens):
        pass

    def get_vocab(self):
        pass
```

---

## 5. Constraints

* Do NOT use:

  * `tokenizers`
  * `sentencepiece`
  * `tiktoken`

* You must:

  * Work directly on sequences
  * Maintain deterministic state
  * Ensure lossless encode/decode - i.e. just test with the same string whether the encoded string comes back the same way as the normal string.

---

## 6. Evaluation Criteria

### Correctness

* Deterministic vocabulary
* Perfect reconstruction

### Algorithm Design

* Proper handling of overlaps
* Clean tie-breaking implementation

### Efficiency

* Target: **O(K · N)**
* Avoid quadratic recomputation where possible

### Robustness

* Handles adversarial inputs like:

  * `"AAAAAA..."`
  * `"abababab..."`
  * `"abacaba..."`

---

## 8. Hidden Test

Your solution will be evaluated on a corpus designed to break:

* Greedy merging
* Naive counting
* Unstable tie-breaking

---

## 9. What This Tests

This is not just a coding task.

It evaluates:

* State management across iterations
* Deterministic algorithm design
* Ability to reason about **future consequences of local actions**

---

## Optional Add-on (for stronger candidates)

* Can you design a heuristic that approximates optimal merge ordering?
* Can you prove whether Stable-BPE is globally optimal?

---
