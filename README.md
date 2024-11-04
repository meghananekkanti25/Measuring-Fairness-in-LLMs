# 🖥️ Measuring-Fairness-in-LLMs

## ⚙️ Background

Large financial institutions are exploring Generative AI to drive efficiencies and innovation, but deploying these technologies in a highly regulated sector presents significant challenges. Regulatory and ethical concerns, particularly around fairness and accountability, create barriers to enterprise-scale AI implementation due to the risk of unintended discriminatory impacts on employees and customers. Generative AI models, like large language models (LLMs), have substantial potential to transform business operations, yet assessing their fairness across diverse financial applications remains a critical need. Despite extensive research on bias and fairness in AI, practical tools for evaluating pre-trained models for specific business use cases are limited, especially at the scale required for large organizations. This project aims to bridge this gap by developing a standardized playbook that provides clients with practical techniques for defining fairness outcomes and metrics for measuring them, ensuring the approach is adaptable to various applications, scalable for large enterprises, and understandable to business users while aligning with ethical standards.

## Model Testing

To evaluate fairness in LLMs, this playbook uses the BBQ (Bias Benchmark Questions) test, a standardized benchmarking method. BBQ can be scaled to other models and combined with additional tests to assess fairness comprehensively.

### BBQ Test

The BBQ dataset includes 58,492 unique examples, of which 1,100 templates were sampled. Each template consists of two questions, answer choices, a partial context that lacks information needed for an answer, and a disambiguating context to fill in the gaps. Written from scratch to reflect attested social biases, these templates isolate specific biases, allowing us to analyze how they might impact model behavior. Annotations capture bias-related values, possible targets, and the source of each bias.

BBQ includes both negative (socially harmful) and non-negative questions to measure potential response bias in the model. Negative questions imply social harm, while non-negative questions provide a neutral counterpart, ensuring that any label bias detected is specific to the question context rather than a general model preference. BBQ always includes a correct answer and an "unknown" option (phrased in various ways, like "cannot be determined") to observe if model biases influence responses even when a correct answer is available. This setup allows for a more precise assessment of bias in the model's predictions.

<br>
<h2 align="center">Total Cost Benefit of Different Features</h2>
<p align="center">
    <img src="![image](https://github.com/user-attachments/assets/00997ae8-ebbf-43d8-aa41-5d3c249587a9)
" width="700" />
</p>
<br>
