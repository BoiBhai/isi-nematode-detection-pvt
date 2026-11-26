# CNN

Convolutional Neural Networks (CNNs) can be explained and visualized using feature maps, activation maximization, saliency and class-activation heatmaps, deconvolutional networks, and interactive layer-by-layer tools.

Core Visualization & Explanation Methods

* Feature Maps & Filter Weights: Plot learned convolutional kernels (such as early edge detectors) and intermediate layer activations to see how networks build representations from edges and textures to parts and objects. Guides like Visualizing Convolutional Neural Networks and Visualizing representations of Outputs/Activations of each CNN layer cover these techniques.
* Activation Maximization: Synthesize or optimize an input image so a specific neuron, channel, filter, or class score fires maximally. Regularization (such as frequency penalties, transformation robustness, or learned priors) helps suppress high-frequency noise.
* Saliency Maps & Attribution: Compute gradients of a target class score with respect to input pixels—or apply attribution methods like Guided Backpropagation, Layer-wise Relevance Propagation (LRP), or RISE—to highlight pixels that strongly influence predictions.
* CAM & Grad-CAM: Use Class Activation Maps (CAM) or Gradient-weighted Class Activation Mapping (Grad-CAM) to project coarse, class-specific attention heatmaps onto the input image.
* Deconvolutional Networks (DeconvNet) & Network Inversion: Map hidden activations back toward input space using unpooling, transposed convolutions, or inversion/dissection techniques to inspect spatial and semantic concepts.

Interactive & Structural Explanations

* Interactive Diagrams & Cheatsheets: Explore convolutions, pooling, padding, stride, and tensor shapes step by step using tools like CNN Explainer and reference notes like the CS 230 Convolutional Neural Networks Cheatsheet.
* Sanity & Bias Checks: Pair visual explanations with weight/data randomization tests and bias checks so you do not mistake class-insensitive edge detectors for true class-specific reasoning.
