# Concept Bottleneck Model

$X \to g(X) = Z$ concepts (derived/estimated features)
$Z \to f(Z) = Y$ prediction

## Concept Discovery

* LLM + Vision-Language Alignment: Large language models generate candidate concept lists, and multimodal models like CLIP align visual features with those concepts via embedding similarity.
* Vision-First / Data-Driven Discovery: Methods such as V2C-CBM extract visual patterns directly from images rather than depending purely on text priors.
* Mechanistic / Representation Discovery: Frameworks like Discover-then-Name-CBM (Discover-then-Name: Task-Agnostic Concept Bottlenecks via Automated Concept Discovery) use sparse autoencoders to uncover concepts already learned inside a feature extractor, name them, and then train linear classifiers.
* Hierarchical & Sparse Selection: Approaches such as Hierarchical Concept Discovery Models: A Concept Pyramid and Sparse Linear Concept Discovery Models organize concepts across granularities or enforce sparsity so explanations stay concise and faithful.