# Bayes' Rule

## Table of Contents
- [Introduction](#introduction)
- [The Formula](#the-formula)
- [Intuitive Understanding](#intuitive-understanding)
- [Example Applications](#example-applications)
- [Interview Tips](#interview-tips)
- [Common Interview Questions](#common-interview-questions)

## Introduction

Bayes' rule (also called Bayes' theorem) is a fundamental principle in probability theory that describes how to update the probability of a hypothesis based on new evidence. Named after Reverend Thomas Bayes, this theorem has applications in various fields including machine learning, statistics, medicine, and data science.

Bayes' rule allows us to reverse conditional probabilities - if we know P(B|A), we can find P(A|B).

## The Formula

Bayes' rule can be expressed as:

$$P(A|B) = \frac{P(B|A) \times P(A)}{P(B)}$$

Where:
- P(A|B) is the posterior probability: the probability of event A given that B has occurred
- P(B|A) is the likelihood: the probability of event B given that A has occurred
- P(A) is the prior probability: the initial probability of event A
- P(B) is the marginal probability: the total probability of event B

The denominator P(B) can also be expanded using the law of total probability:

$$P(B) = P(B|A) \times P(A) + P(B|\text{not }A) \times P(\text{not }A)$$

So the full formula becomes:

$$P(A|B) = \frac{P(B|A) \times P(A)}{P(B|A) \times P(A) + P(B|\text{not }A) \times P(\text{not }A)}$$

## Intuitive Understanding

Bayes' rule can be understood as a way to update our beliefs based on new evidence:

1. Start with a prior belief about something (P(A))
2. Observe some evidence (B)
3. Calculate how likely this evidence would be if our belief is true (P(B|A))
4. Update our belief considering the new evidence (P(A|B))

The theorem quantifies this update process, telling us exactly how much to adjust our beliefs based on the strength of the evidence.

## Example Applications

### Medical Testing

Consider a medical test for a disease that affects 1% of the population:
- The test is 95% sensitive (P(Positive|Disease) = 0.95)
- The test is 90% specific (P(Negative|No Disease) = 0.90)

If someone tests positive, what's the probability they actually have the disease?

Using Bayes' rule:
- P(Disease|Positive) = ?
- P(Positive|Disease) = 0.95
- P(Disease) = 0.01
- P(Positive) = P(Positive|Disease) × P(Disease) + P(Positive|No Disease) × P(No Disease)
  = 0.95 × 0.01 + 0.10 × 0.99 = 0.0095 + 0.099 = 0.1085

Therefore:
- P(Disease|Positive) = (0.95 × 0.01) ÷ 0.1085 ≈ 0.088 or about 8.8%

This counterintuitive result shows why Bayes' rule is so important - even with a positive test, the probability of having the disease is only about 8.8%, not 95% as many might incorrectly assume.

### Spam Filtering

Email spam filters use Bayes' rule to classify emails:
- P(Spam|Words) = P(Words|Spam) × P(Spam) ÷ P(Words)

The filter learns P(Words|Spam) from known spam emails and uses this to calculate the probability that a new email with certain words is spam.

## Interview Tips

1. **Understand the components**: Be clear about what represents the prior, likelihood, and posterior in any problem.

2. **Draw a tree diagram**: For complex problems, visualizing with a probability tree can help.

3. **Use natural frequencies**: Sometimes expressing probabilities as frequencies (e.g., "8 out of 100 people") makes calculations more intuitive.

4. **Watch out for the base rate fallacy**: This is a common error where people ignore the prior probability (P(A)) and focus only on the likelihood (P(B|A)).

5. **Apply to real-world scenarios**: Practice applying Bayes' rule to practical scenarios like medical testing, A/B testing, or machine learning.

## Common Interview Questions

### 1. Disease Testing Problem

**Question**: A disease affects 1% of the population. A test for the disease has a false positive rate of 5% and a false negative rate of 2%. If a person tests positive, what is the probability they have the disease?

**Solution**:
- P(Disease) = 0.01 (prior)
- P(Positive|Disease) = 0.98 (true positive rate = 1 - false negative rate)
- P(Positive|No Disease) = 0.05 (false positive rate)
- P(Positive) = P(Positive|Disease) × P(Disease) + P(Positive|No Disease) × P(No Disease)
  = 0.98 × 0.01 + 0.05 × 0.99 = 0.0098 + 0.0495 = 0.0593

Therefore:
- P(Disease|Positive) = (0.98 × 0.01) ÷ 0.0593 ≈ 0.165 or about 16.5%

### 2. Monty Hall Problem

**Question**: In a game show, you're given the choice of three doors. Behind one door is a car; behind the others are goats. You pick door 1. The host, who knows what's behind each door, opens door 3, revealing a goat. Should you switch to door 2 or stay with door 1?

**Solution using Bayes' rule**:
- Let's define:
  - A = "Car is behind door 1"
  - B = "Host opens door 3"

- We want to find P(A|B) vs P(Car is behind door 2|B)

- P(A) = 1/3 (prior probability that car is behind door 1)
- P(B|A) = 1/2 (if car is behind door 1, host can open either door 2 or 3)
- P(B|Car is behind door 2) = 1 (if car is behind door 2, host must open door 3)
- P(B|Car is behind door 3) = 0 (if car is behind door 3, host cannot open door 3)

Using Bayes' rule:
- P(A|B) = (1/2 × 1/3) ÷ [(1/2 × 1/3) + (1 × 1/3) + (0 × 1/3)] = (1/6) ÷ (1/6 + 1/3) = 1/3
- P(Car is behind door 2|B) = (1 × 1/3) ÷ (1/6 + 1/3) = 2/3

Therefore, you should switch to door 2, as it has a 2/3 probability of having the car.

### 3. Email Classification

**Question**: A spam filter finds that 80% of spam emails contain the word "free," while 10% of legitimate emails contain this word. If 20% of all emails are spam, what is the probability that an email containing "free" is spam?

**Solution**:
- P(Spam) = 0.2 (prior)
- P("free"|Spam) = 0.8 (likelihood)
- P("free"|Not Spam) = 0.1 (likelihood for alternative)

Using Bayes' rule:
- P(Spam|"free") = (0.8 × 0.2) ÷ [(0.8 × 0.2) + (0.1 × 0.8)]
- P(Spam|"free") = 0.16 ÷ (0.16 + 0.08) = 0.16 ÷ 0.24 = 2/3 ≈ 66.7%

### 4. A/B Testing

**Question**: In an A/B test, version A has a 5% conversion rate from previous data (prior). In a new test with 100 visitors, version A gets 8 conversions. What is the updated probability that the true conversion rate is greater than 7%?

**Solution**: This requires using Bayesian inference with a prior distribution, typically using beta distribution for conversion rates. The calculation involves integrating the posterior distribution above 7%, which is beyond what can be calculated by hand in an interview. Be prepared to discuss the approach and how you would implement this using computational methods.

---

[Back to Probability Main Page](./README.md)
