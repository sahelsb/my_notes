### Machine Learning methods

##### bayesin inference :

Bayesian inference is a statistical method that allows us to update our beliefs about a particular hypothesis based on new evidence. It’s rooted in Bayes' Theorem.

Bayes' Theorem provides a way to revise existing predictions or theories (known as prior beliefs) in light of new evidence

P(H ∣ E)=P(E ∣ H)⋅P(H)​  /  P(E)

- P(H ∣ E) is the **posterior probability**: the probability of the hypothesis H given the evidence E.

- P(E ∣ H) is the **likelihood**: the probability of observing the evidence E given that the hypothesis H is true.

- P(H) is the **prior probability**: the initial probability of the hypothesis HHH before considering the new evidence.

- P(E) is the **marginal likelihood** or **evidence**: the total probability of the evidence EEE, which acts as a normalizing constant to ensure that the posterior probabilities sum to one.

The Bayesian update is the process of incorporating new evidence into our existing beliefs. Here’s how it works:

1. **Start with a Prior:** You begin with an initial belief about the hypothesis, represented by the prior probability P(H).
    
2. **Gather Evidence:** You collect new data or evidence E.
    
3. **Compute the Likelihood:** Determine how likely the evidence is under the hypothesis, represented by P(E ∣ H)
    
4. **Update Beliefs:** Use Bayes' Theorem to compute the posterior probability P(H ∣ E), which reflects your updated belief after considering the new evidence.


Suppose you're testing whether a coin is fair. Your hypothesis HHH is that the coin is fair (i.e., it has a 50% chance of landing heads). You flip the coin 10 times and get 8 heads. To update your belief about the fairness of the coin:

1. **Prior Probability:** Before the experiment, you might believe the coin is fair with a prior probability of 0.5.
    
2. **Evidence:** You observed 8 heads out of 10 flips.
    
3. **Likelihood:** The probability of observing 8 heads in 10 flips given that the coin is fair can be calculated using the binomial distribution.
    
4. **Posterior Probability:** Use Bayes' Theorem to update your belief about the fairness of the coin in light of the observed evidence.
