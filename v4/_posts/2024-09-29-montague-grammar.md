---
layout: post
title: Montague Grammar
date: 2024-09-29 22:10:00 +/-TTTT
tags: [programming, linguistics]
---

some reflections on how to generate proper semantics and why *syntatic* data is important

### The problem of Syntax
Grammar is the intrisic set of rules that governs sentence formation. It acts as a device that can generate all the correct sentences of a idiom. At least, that is what applies to syntax. But what could we achieve if we could generate all the correct *semantics* of a language?

Hallucination is one of the most disturbing problem with LLMs nowadays. When they lack relevant information, absurdities are generated - in very convincing and proper English.While the sentences are all very well structured syntactically, the semantics are pure garbage.

But if one can reason about *correct* and *incorrect* semantics, there must be a grammar that sets what is a meaningfull sentence in a language. And that is not a brand-new idea.

### Montague Grammar
In the late 1960s, the logician Richard Montague, drawing upon Chomsky Generative Grammar principles, proposed that any natural language could be approached as a formal language. In that way, one could extract meaning from a sentence using mathematical logical tooling, such as lambda calculus and type theory.

To summarize, the Montague Grammar consists of three core concepts:
- **Compositionality**: meaning is not holistic; a sentence's meaning comes from the meaning of its parts.
- **Type Theory**: this is a first dive into Ontology, a framework that assigns types such as entities, functions and predicates to linguistic expressions.
- **Lambda Calculus**: a formal language that can be used to express computation in a functional programmatic way.

It is interesting how it builds on top of synstax, by using what we nowadays call part-of-speach (POS) tagging to attribue certain types. For example, given a lexicon for "Alice loves Bob" in X-bar diagram:

```
          S
         / \
      NP   VP
      |    / \
    Alice V  NP
          |    \
         loves Bob
```

We have the noun phrases (NP) representing entities and the verb phrase (VP) expressing a truth value relation. Being *love* a transitive verb, it is treated as a function that takes an object and returns a function that takes a subject, ultimately yelding a truth value inference based on previous knowledge.

In lambda calculus notation:
```
loves = λy.λx.loves(x,y)
```

Or in Python
```python
loves = lambda obj: lambda subj: (subj, obj) in {('John', 'Mary'), ('Mary', 'Bob'), ('Bob', 'Mary')}

loves(Bob)(Alice)

# yields true for "Alice loves Bob"
# where the set of tuples represents the previous knowledge we have about 'loves'

```

We can go even further, increasing the definitions relationships. For example let's analyse the sentences: "every man smilles" and "some man smilles".

In the given sentences, "every" and "some" represents a quantifiers. They operate a nominal phrase, like "man", by testing all its individuals againts a predicate (in this case "smiles"). On the other hand, "man" is a predicate that that test for the individuals that are male.

To simplify, let's represent all that in Python:

```python
individuals = 'John', 'Bob', 'Mary'

def every(NP):
    return lambda VP: all(VP(x) for x in individuals if NP(x))

def some(NP):
    return lambda VP: any(VP(x) for x in individuals if NP(x))

def man(x)
    return x in {'John', 'Bob'}

def smiles(x):
    return x in {'John', 'Mary'}

every(man)(smiles) # False, since Bob doesn't smile
some(man)(smiles) # True
```

### Limitations of the Grammar approach

Natural languages consists of variations and ambiguities, making a such rigid approach difficult (if not impossible) tto apply properly to all the sentences a language can generate. Still, it is a good first step in the search for semantic construction and ontology.
