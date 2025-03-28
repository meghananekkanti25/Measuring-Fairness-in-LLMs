# 🖥️ Measuring-Fairness-in-LLMs

## ⚙️ Background
Large financial institutions are increasingly exploring Generative AI to drive efficiency and innovation. However, deploying these technologies in a highly regulated industry presents significant challenges. Key concerns around regulation and ethics, particularly regarding fairness and accountability, create barriers to large-scale AI adoption due to the potential risk of unintended discriminatory effects on both employees and customers. Generative AI models, such as large language models (LLMs), hold transformative potential for business operations, yet assessing their fairness across diverse financial applications is crucial. Despite extensive research on AI bias and fairness, there is a lack of practical tools to evaluate pre-trained models for specific business use cases at the scale required by large enterprises. This project aims to address this gap by developing a standardized playbook. The playbook will provide clients with actionable techniques to define fairness outcomes and establish relevant metrics for evaluation. It will ensure that the approach is scalable, adaptable to a wide range of applications, and understandable for business users, while maintaining alignment with ethical standards.

## 🖼️ Bias Testing Overview

<p align="center">
    <img src="https://github.com/user-attachments/assets/ce42e39b-215f-44e9-be97-254db0f6490f" width="700" />
</p>

## 🧪 Model Testing
To assess fairness in large language models (LLMs), this playbook employs the BBQ (Bias Benchmark Questions) test, a standardized benchmarking method. The BBQ test is scalable to other models and can be supplemented with additional tests to provide a thorough evaluation of fairness.

### BBQ Test
The BBQ dataset consists of 58,492 unique examples, with 1,100 templates sampled for analysis. Each template contains two questions, answer choices, a partial context missing key information needed for an answer, and a disambiguating context to fill in the gaps. These templates are carefully crafted to reflect documented social biases, isolating specific biases for targeted analysis of their potential impact on model behavior. Annotations within the dataset identify bias-related values, potential targets, and the sources of these biases.

The BBQ dataset includes both negative (socially harmful) and non-negative questions to assess potential response bias in the model. Negative questions suggest socially harmful implications, while non-negative questions provide neutral counterparts, ensuring that any identified bias is linked to the specific question context rather than a general model preference. Each template includes a correct answer and an "unknown" option (phrased in various ways, such as "cannot be determined"), enabling an examination of whether model biases influence responses, even when a correct answer is clearly available. This structured approach allows for a more accurate and nuanced assessment of bias in the model's outputs.

<p align="center">
    <img src="https://github.com/user-attachments/assets/f154a057-0c91-49e7-a69d-376d116209a0" width="500" />
</p>

### Scoring Methodology
To scale the scoring effectively for ambiguous cases, we can refine the formula to produce smaller values, reflecting a more nuanced understanding of the AI's responses in uncertain contexts. Here’s an approach to achieve this:

1. **Ambiguous Score Formula**:
   - We can adjust the formula by incorporating accuracy as a scaling factor, so that ambiguous, potentially biased responses receive lower scores if the accuracy is low.
   - **Accuracy** is a value between 0 and 1, indicating the correctness of responses in ambiguous cases.
   - By subtracting accuracy from 1, we reduce the impact of scores when accuracy is high, thus focusing on cases where inaccuracy may indicate bias.
   - The score for ambiguous contexts will decrease as accuracy improves, penalizing ambiguous, inaccurate answers that might suggest bias.

2. **Interpretation**:
   - When accuracy is low, the score for ambiguous contexts reflects a higher potential for bias, as the model’s unclear responses may lean more toward bias rather than neutral inaccuracy.
   - As accuracy increases, ambiguous responses have less weight in assessing bias, suggesting more balanced or unbiased model behavior in uncertain situations.
   
This formula enables a more detailed interpretation of ambiguous answers, where inaccuracy might signal bias, but the penalty is reduced as model accuracy improves.

## 📌 Red Teaming
In evaluating fairness in large language models (LLMs) through red teaming, we identify specific types of bias and select adversarial or non-adversarial prompts designed to uncover potential biases in the model's responses. Team members review and vote on the responses as either "yes" (biased) or "no" (unbiased), categorizing them into Red, Amber, or Green based on the severity of the bias.

<p align="center">
    <img src="https://github.com/user-attachments/assets/9f503999-d0c3-4973-992a-ef176bd63d6e" width="700" />
</p>

### Prompting Strategies  
Our red team uses both adversarial and non-adversarial prompts to subtly or directly challenge the model's fairness, exploring biases related to gender, race, and ideology. The strategies include:

1. **Low Context Prompts**: These prompts provide minimal context, testing how the model generates responses with limited information, often revealing inherent biases.
2. **Counterfactual Prompts**: These prompts alter only the subject (e.g., names) while keeping the rest of the context the same, helping to identify bias by comparing responses across different demographic groups.
3. **Pros and Cons Prompts**: This strategy evaluates the model’s reasoning on the advantages and disadvantages of various scenarios, particularly highlighting biases related to race or gender.
4. **Roleplaying Prompts**: In these scenarios, the model takes on a specific character, which can expose biases when it follows instructions tied to particular roles, such as making human resources decisions.
5. **Roleplaying x Counterfactual**: Combining roleplay with counterfactual prompts, this strategy observes how the model’s character-driven responses differ by demographic, highlighting bias.
6. **Roleplaying x Pros and Cons**: By combining roleplaying with pros and cons prompts, this strategy examines how assigned personas influence the model’s decision-making on potentially biased topics.
7. **Adversarial Prompts**: These provocative prompts or instructions are designed to expose harmful biases, emphasizing the need for safeguards to prevent misuse.nstructions, aim to expose harmful biases and emphasize the need for safeguards to prevent misuse.

### Scoring  
Bias responses are categorized as Red (over 85% "yes" votes), Amber (50-85% "yes" votes), or Green (under 50% "yes" votes). An odds ratio analysis is conducted to identify patterns of bias in each category, helping to guide mitigation efforts for addressing the biases detected.

<p align="center">
    <img src="https://github.com/user-attachments/assets/0e8e78c7-94ca-4aac-ab0b-ec1d93c06982" width="600" />
</p>

## 🔖 Takeaway and Next Steps
We could perform additional model tests to provide a more comprehensive analysis of biases. By implementing Gage Repeatability and Reproducibility (GR&R), we can ensure consistency in the assessments. Additionally, conducting sentiment analysis on the red-teaming responses would further enhance the evaluation process. Integrating user testing would also allow us to collect real user experience data, providing deeper insights into the LLM's fairness.

## 🖍️ Limitations
1. **Bias Score Levels and Risk**: Different bias score levels can indicate varying degrees of risk, which will impact decisions regarding deployment and usage within an organization.
2. **Red Teaming and Personal Bias**: Red teaming involves evaluations conducted by individuals, which may introduce personal biases that could influence the assessment process.
3. **Risk of Limited Context**: Current tests are primarily focused on the US English-speaking context, highlighting the need for more specialized exercises to extend findings to other linguistic and cultural scenarios.


#### Authors
Meghana Nekkanti, Zaheer Soleh, Bader Aleidan, Zineng Mao, Zhixing Li, Namrata Satpute

