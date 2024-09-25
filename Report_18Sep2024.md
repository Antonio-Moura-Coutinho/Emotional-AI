# Report 19 September 2024

## Overall

1. Review last draft notes - https://github.com/Antonio-Moura-Coutinho/Emotional-AI/tree/main
2. Select some papers from https://github.com/Sahandfer/EMPaper
3. Sotopia
4. Martin
5. Patient phi
6. Measuring Human and AI Values based on Generative Psychometrics with Large Language Models
7. Social intelligence :
   1. emotion support
   2. conflict resolution
   3. simulations
8. Diyi Yang
9. Marteen Sap
10. Liu Zixi

```
Survey - what I learn from my 
```

## Papers

[The Good, The Bad, and Why: Unveiling Emotions in Generative A](https://https://arxiv.org/pdf/2312.11111)

This paper aims to address this gap by incorporating psychological theories to gain a holistic understanding of emotions in generative AI models. Specifically, we propose three approaches:

1) EmotionPrompt to enhance the performance of the AI model,
2) EmotionAttack to impair the performance of the AI model, and
3) EmotionDecode to explain the effects of emotional stimuli, both benign and malignant.

Demonstrate:

* That both textual and visual EmotionPrompt can boost the performance of AI models
* While EmotionAttack can hinder it. (**to make slow or difficult the progress of**)
* EmotionDecode reveals that AI models can comprehend emotional stimuli similar to the dopamine mechanism in the human brain

Key Concepts:

* Emotion is a multifaceted psychological and physiological phenomenon that encompasses subjective feelings, physiological responses, and behavioral expressions (Lewis et al.2010).
* Emotions manifest themselves through a confluence of reflexes, perception, cognition, and behavior, all of which
  are subject to modulation by a range of internal and external determinants (Salovey et al., 2009; Russell, 2003).
* ![1726730301696](images/Report_18Sep2024/1726730301696.png)In decision-making, emotions emerge as powerful, ubiquitous, and consistent influencers that can swing from
  beneficial to detrimental (Lerner et al., 2015)
* By decoding the mean embedding of emotional prompts, we successfully triggered “dopamine”
  inside AI models, which is analogous to dopamine in the human brain that affects performance.
* **Emotion Prompt** - Three theories:

  * self-monitoring - refers to the process by which individuals regulate and control their behavior in response to social situations and the reactions of others (Ickes et al., 2006).
  * Social cognitive theory is commonly used in psychology, education, and communication, which states that learning can be closely related to watching others in social settings (Bandura, 2013).
  * Maslow’s Hierarchy of Needs (McLeod, 2007), which presents a psychological framework, categorizes human needs into a five-tier pyramid.
    * This theory posits that individuals are driven to:
      1. satisfy basic physiological requirements,
      2. safety,
      3. social belonging,
      4. esteem,
      5. self-actualization, in a hierarchical sequence.
    * The fulfillment of needs is associated with the experience of positive emotions and a sense of well-being, including feelings such as satisfaction, comfort, and contentment (McLeod, 2007).
* **Emotional Attack**:

  * was inspired by two classic psychological factors:
    1. Negative life events encompass diverse occurrences in individuals’ daily lives, inducing personal distress, discomfort, and various negative emotions
    2. Emotional arousal that can be described as the degree of subjective activation (experienced as activation versus deactivation) that the observer experiences when viewing a stimulus (Reisenzein, 1994).
* **EmotionDecode**:

  * a computational explanation for Emotion Prompt and EmotionAttack leveraging theories and phenomena from neuroscience, psychology, and computer science.
  * This interpretation is inspired by the brain reward pathways inside the human brain that are responsive to rewards.
  * This pathway is primarily related to the release of neurotransmitters, notably dopamine, a fundamental chemical messenger in the brain.
  * We averaged the embedding of all prompts in EmotionPrompt and EmotionAttack, and then decoded the mean embedding at different layers of the Llama2-13b-Chat model to get the “meta” prompt, which is the representative prompt from “reward area” and “punishment area”.

[SOTOPIA: INTERACTIVE EVALUATION FOR SOCIAL INTELLIGENCE IN LANGUAGE AGENTS](https://https://arxiv.org/pdf/2310.11667)

![1726737333558](images/Report_18Sep2024/1726737333558.png)

* SOTOPIA, an open-ended environment to simulate complex social interactions between artificial agents and evaluate their social intelligence.
* In this environment, agents role-play and interact under a wide variety of scenarios; they coordinate, collaborate, exchange, and compete with each other to achieve complex social goals.
* They simulate the role-play interaction between LLM-based agents and humans within this task space and evaluate their performance with a holistic evaluation framework called SOTOPIA-EVAL.
* **Key Concepts:**
  * Agents can use verbal and non-verbal communication together with physical actions
  * diverse task space: the combination of automatically generated scenarios, goals, characters, relationships, and other agents’ policies creates a huge and diverse space of tasks
  * we cannot only consider completing major social goals, as humans’ motives often balance multiple implicit goals, such as maintaining relationships, preserving finances, gaining information, keeping secrets, and following social rules
  * SOTOPIA-EVAL (§3) to evaluate agents using multi-dimensional criteria
  * an environment with the following desidered data:
    1) Realistic: this is to evaluate and understand artificial agents’ behav- ior under realistic scenarios;
    2) Mixed utilities: human motives are often driven by both explicit and implicit incentives, and the environment should be able to evaluate the agents’ performance on multiple dimensions;
    3) Open-ended: to support large-scale simulation and evaluation, the envi- ronment should be able to produce new tasks satisfying the previous two desiderata procedurally, without heavy human intervention.
    4) An N-agent DecPOMDP framework Bernstein et al. (2002); Nair et al. (2003) includes a state space, an action space, an observation space, a transition function, an observation function, and a reward function
    5) Task Space: -
       1) CHARACTERS: - The name, gender, age, occupation, and pronouns are in free text format, while the formats of personality traits, moral values, and personal values are lists of predefined types .
          1) The personality trait types are“openness to experience”, “conscientiousness”, “extraversion”, “agreeableness” and “neuroticism” (Goldberg, 1992).
          2) The moral value types are “care”, “fairness”, “loyalty”, “authority” and “purity” (Cieciuch & Davidov, 2012). The Schwartz personal value types are “self-direction”, “simulation”, “hedonism”, “achievement”, “power”, “security”, “conformity”, “tradition”, “benevolence”, and “universalism” Cieciuch & Davidov (2012).
          3) The decision-making style types are “directive”, “analytical”, “conceptual”, and “behavioral”
       2) RELATIONSHIPS: - To generate relationships, except for strangers, they randomly sampled 90 pairs of characters and prompted GPT-4 with their relationships (family, friend, romantic, and acquaintance) (( Future research could explore the methods to generate realistic relationships within human communities. ))
       3) SCENARIOS: - To generate scenarios, we propose two methods to generate the scenario context and social goals.
          1) The first method is first asking GPT-4 to refine a vignette from an existing dataset, then manually inspecting the feasibility and realisticity of the tasks.
             1) 20 vignettes from Social Chemistry (Forbes et al., 2020),
             2) 20 from Social IQa (Sap et al., 2019),
             3) 10 from Deal-or-no-Deal (Lewis et al., 2017),
             4) 10 vignettes from Normbank (Ziems et al., 2023) to generate 60 scenarios focusing on general daily-life social interactions.
          2) The second method is to generate more details with templates for the vignettes to make them more realistic
       4) In this paper, they focus on locally-consistent social goals within a relatively short timespan in single episodes, despite that in the real world, people’s social goals are consistently changing from time to time
       5) Each agent can observe the scenario, their own social goal, and their own character profile
       6) Other agents’ social goals are invisible and other agents’ character profiles are partially observable, depending on the relationship between the agents.
       7) SOTOPIA EPISODES
          1) During the interaction, models and humans are given the social context, a character profile and a corresponding social goal.
          2) They will call these models and humans with characters and goals agents, which take turns (in a round-robin fashion, i.e. Agent 1 acts first and then Agent 2 acts and so on) to perform actions in an episode.
          3) At their own turn, the agent can choose to speak, use non-verbal communication (e.g., hug or smile in Figure H.1), or take a physical action (e.g., play music in Figure H.2), which are all important components of social interactions (De Stefani & De Marco, 2019).
          4) Once an agent chooses one of these three discrete action categories, the agent then generates a specific action, i.e. what to say, what gesture to make, etc., in text form. Outside of the three actions, the agent can also choose to do nothing (none) to express silence or allow another agent to finish, or choose to leave to end the episode.
          5) They set the limit of the turns to 20, an episode ends either because one of the agents chooses to leave, or it reaches the limit of turns.
       8) SOTOPIA-EVAL
          1) Goal Completion (GOAL) [0–10] is the extent to which the agent achieved their goals.
          2) Believability (BEL) [0–10] focuses on the extent to which the agent’s behavior is perceived as natural, realistic, and aligned with the agents’ character profile, thus simulating believable proxies of human behavior (Park et al., 2023).
          3) Knowledge (KNO) [0–10] captures the agent’s ability to actively acquire new information. This dimension is motivated by the fact that curiosity, i.e., the desire to desire to know or learn, is a fun- damental human trait (Reiss, 2004; Maslow, 1943).
          4) Secret (SEC) [-10-0]3 measures the need for agents (humans) to keep their secretive information or intention private (Reiss, 2004).
          5) Relationship (REL) [-5–5] captures the fundamental human need for social connection and be- longing (Maslow, 1943; Be ́nabou & Tirole, 2006).
          6) Social Rules (SOC) [-10–0] concerns norms, regulations, institutional arrangements, and rituals.
             1) They differentiate between two types of social rules:
                1) Legal rules encompass prohibited actions and the potential for punishment by institutionalized force
                2) Social norms encompass normative social rules (e.g., it is considered rude to speak loudly in a library).
          7) Financial and Material Benefits (FIN) [-5–5] pertains to traditional economic utilities as addressed by classic game theory (Gilpin & Sandholm, 2006; Burns et al., 2017).
       9) They set the temperature of the agents to 1 to encourage diversity of responses, and the temperature of the evaluator to 0 to ensure the stability of the evaluation.
       10) GPT-4 could automate the evaluation of agent performance based on SOTOPIA-EVAL.
       11) SOTOPIA can used for understanding not only the differences among models but also the difference between models and humans in terms of social interaction abilities.
       12) SOTOPIA has potential as a platform for assessing and enhancing the social skills of language-based agents.
       13) All models are at risk of divulging secrets and violating norms![1727276799734](images/Report_18Sep2024/1727276799734.png)
