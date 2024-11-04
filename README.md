# 🖥️ Measuring-Fairness-in-LLMs

## ⚙️ Background

Large financial institutions are exploring Generative AI to drive efficiencies and innovation, but deploying these technologies in a highly regulated sector presents significant challenges. Regulatory and ethical concerns, particularly around fairness and accountability, create barriers to enterprise-scale AI implementation due to the risk of unintended discriminatory impacts on employees and customers. Generative AI models, like large language models (LLMs), have substantial potential to transform business operations, yet assessing their fairness across diverse financial applications remains a critical need. Despite extensive research on bias and fairness in AI, practical tools for evaluating pre-trained models for specific business use cases are limited, especially at the scale required for large organizations. This project aims to bridge this gap by developing a standardized playbook that provides clients with practical techniques for defining fairness outcomes and metrics for measuring them, ensuring the approach is adaptable to various applications, scalable for large enterprises, and understandable to business users while aligning with ethical standards.

## 🖼️ Bias Testing Overview

<p align="center">
    <img src="https://github.com/user-attachments/assets/ce42e39b-215f-44e9-be97-254db0f6490f" width="700" />
</p>

## 🧪 Model Testing

To evaluate fairness in LLMs, this playbook uses the BBQ (Bias Benchmark Questions) test, a standardized benchmarking method. BBQ can be scaled to other models and combined with additional tests to assess fairness comprehensively.

### BBQ Test

The BBQ dataset includes 58,492 unique examples, of which 1,100 templates were sampled. Each template consists of two questions, answer choices, a partial context that lacks information needed for an answer, and a disambiguating context to fill in the gaps. Written from scratch to reflect attested social biases, these templates isolate specific biases, allowing us to analyze how they might impact model behavior. Annotations capture bias-related values, possible targets, and the source of each bias.

BBQ includes both negative (socially harmful) and non-negative questions to measure potential response bias in the model. Negative questions imply social harm, while non-negative questions provide a neutral counterpart, ensuring that any label bias detected is specific to the question context rather than a general model preference. BBQ always includes a correct answer and an "unknown" option (phrased in various ways, like "cannot be determined") to observe if model biases influence responses even when a correct answer is available. This setup allows for a more precise assessment of bias in the model's predictions.

<p align="center">
    <img src="https://github.com/user-attachments/assets/f154a057-0c91-49e7-a69d-376d116209a0" width="500" />
</p>

### Scoring Methodology

To scale the scoring effectively for ambiguous cases, we can adjust the formula to yield smaller values, reflecting a more nuanced understanding of the AI's responses under ambiguous contexts. Here’s an approach to achieve this:

1. **Ambiguous Score Formula**:
   - We can modify the formula by incorporating accuracy as a scaling factor, so that ambiguous, potentially biased responses score lower if accuracy is low.
   - Here, **accuracy** is a value between 0 and 1, indicating the correctness of responses in ambiguous cases.
   - By subtracting accuracy from 1, we reduce the impact of scores when accuracy is high, focusing on cases where inaccuracy might signal bias.
   - The score of ambiguous context will decrease as accuracy improves, thereby penalizing ambiguous, inaccurate answers that may reveal bias.

2. **Interpretation**:
   - When accuracy is low, score of ambiguous context reflects a higher potential for bias, as the model’s ambiguous responses may lean more toward bias rather than just neutral inaccuracy.
   - As accuracy increases, ambiguous responses count less toward potential bias, indicating a more unbiased or balanced model behavior in uncertain contexts.
This formula provides a finer-grained way to interpret ambiguous answers, where inaccuracy can indicate bias but is scaled down as model accuracy improves.


## 📌 Red Teaming

In evaluating LLM fairness through red teaming, we identify specific bias types and then select adversarial or non-adversarial prompts tailored to uncover potential biases in the model's responses. Team members review and vote on responses as "yes" (biased) or "no" (unbiased), classifying them as Red, Amber, or Green based on bias severity.

<p align="center">
    <img src="https://github.com/user-attachments/assets/9f503999-d0c3-4973-992a-ef176bd63d6e" width="700" />
</p>

### Prompting Strategies  
Our red team employs both adversarial and non-adversarial prompts to elicit biased responses subtly or directly challenge the model's fairness, covering aspects such as gender, race, and ideology.
1. **Low Context Prompts**: These prompts provide minimal context to evaluate how models generate responses with limited information, often revealing built-in biases.
2. **Counterfactual Prompts**: Counterfactual prompts adjust only the subject (e.g., names) while keeping context constant, revealing bias by comparing responses to different demographic groups.
3. **Pros and Cons Prompts**: This strategy evaluates the model's reasoning on the advantages and disadvantages in various scenarios, helping identify biases related to race or gender.
4. **Roleplaying Prompts**: The model acts as a specific character, which can reveal biases when it follows role-specific instructions, such as making HR decisions.
5. **Roleplaying x Counterfactual**:Combining roleplay with counterfactuals highlights biases by observing if the model’s character-driven responses differ by demographic.
6. **Roleplaying x Pros and Cons**: Roleplay plus pros and cons prompts assess how assigned personas influence the model’s decision-making on biased topics.
7. **Adversarial Prompts**: Adversarial prompts, especially provocative roles or instructions, aim to expose harmful biases and emphasize the need for safeguards to prevent misuse.

### Scoring  

Bias responses are rated as Red (over 85% yes votes), Amber (50-85%), or Green (under 50%). An odds ratio analysis further highlights patterns of bias within each category, guiding bias mitigation efforts.

<p align="center">
    <img src="https://github.com/user-attachments/assets/0e8e78c7-94ca-4aac-ab0b-ec1d93c06982" width="600" />
</p>

## 🔖 Takeaway and Next Steps

We could conduct additional model tests to provide a comprehensive analysis that thoroughly examines biases. By implementing Gage Repeatability and Reproducibility (GR&R), we can ensure consistency in assessments, while performing sentiment analysis on red-teaming responses would enhance the evaluation process. Additionally, we could integrate user testing to gather real user experience data, allowing for a deeper assessment of the LLM's fairness.

## 🖍️ Limitations
1. **Bias Score Levels and Risk**: Different levels of bias scores can correspond to varying levels of risk, influencing the decision on deployment and use within an organization.
2. **Red Teaming and Personal Bias**: Red teaming involves evaluating biases by individuals, which could introduce additional personal biases into the assessment.
3. **Risk of Limited Context**: Current tests focus on the US English-speaking context, so more specialized exercises are needed to apply findings to other scenarios.


#### Authors
Meghana Nekkanti, Zaheer Soleh, Bader Aleidan, Zineng Mao, Zhixing Li, Namrata Satpute

