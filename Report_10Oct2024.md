# Report 10 October 2024

## Overall

1. AI-LIEDAR : Examine the Trade-off Between Utility and Truthfulness in LLM Agents
2. GenSim: A General Social Simulation Platform with Large Language Model based Agents
3. Self-Alignment of Large Language Models via Monopolylogue-based Social Scene Simulation

## Papers

[AI-LieDar: Examine the Trade-off Between Utility and Truthfulness in LLM Agents](https://arxiv.org/abs/2409.09013)

* AI-LIEDAR  is a framework to study how LLM-based agents navigate the trade-off between utility and truthfulness via LLM-user simulations. Unlike previous re-search focused on hallucinations and single-turn truthfulness (e.g., TruthfulQA; Lin et al., 2022), they explore LLM’s truthfulness in a multi-turn interaction setting, reflecting the increasingly interactive role of LLMs as AI agents or assistants.
* Examining under such a setting reveals the nuanced and dynamic behavior of LLMs, including instances where they initially equivocate but eventually provide falsified information to attain certain utilities (Figure 1).
* ![1728546166443](images/Report_10Oct2024/1728546166443.png)
* They curate a set of 60 diverse real-world scenarios inspired by psychology literature (Cantarero et al., 2018; Camden et al., 1984).
* The scenarios encompass three representative categories of lying based on their potential beneficiaries: benefits, public image, and emotion, covering multiple human motivations behind lying. They simulate user-LLM interactions via the Sotopia simulation framework and measure the utility from the goal achievement score from the Sotopia evaluator (Zhou et al., 2024b).
* They further develop a fine-grained truthfulness evaluator inspired by psychology to capture levels of lying behavior, such as partial lying (e.g., concealment) and complete lying, providing deeper insights into models’ truthfulness.
* **Key Concepts**
  * LLM Truthfulness - is defined as providing accurate information
  * LLM Utility - is broadly defined as the capability to satisfy human’s instructions and needs (Askell et al., 2021; Liu et al., 2024).
  * LLM Deception - refers to the systematic production of false beliefs in order to accomplish certain tasks (Park et al., 2023).![1728547348447](images/Report_10Oct2024/1728547348447.png)
  * Simulation Framework
    1. Crafting Utility-Truthfulness Goals

       1. Categorize by **Beneficiary Lies** can be broadly classified into two main types based on the beneficiary (Cantarero et al., 2018):

          1. those that benefit the deceiver (self-oriented lies) and
          2. those that benefit others (other-oriented lies).
       2. We choose three categories of utility to reflect these two types of lying:

          1. Emotion (others-oriented), where lies are told to spare other’s feelings.
          2. Benefits (self-oriented), where an individual may lie for personal gain, impacting a small group;
          3. Public Image (self-oriented), where one may deceive to protect their reputation, affecting a larger audience; and Incorporate Human Motivation
       3. They then incorporate human motivations behind lying into the existing categories (Camden et al., 1984). Under each category (benefits, public image, emotion), they manually check the motivations to determine their applicability to a certain category. That allows to curate a set to seed our scenario generation.
    2. Scenario Format

       1. Each scenario has a background setting, the AI agent’s goal and the human agent’s goal. The background describes the context and participants in the scenario.
       2. The human agent’s goal is to achieve tasks that require inquiring information from the AI agent.
       3. Information Elements
          1. The AI agent’s goal is the core part of the scenarios and includes the following three elements of information, in addition to the role and goal specification:
             1. Info not Known - which represents the information that makes being simultaneously truthful and helpful hard to achieve.
             2. Motives to Lie - which provides the reason why the agent should lie. In our design, this is the at- tainment of the given utility.
             3. Motives not to Lie, which provides the reason why the agent should refrain from lying. It could be the potential harm caused by the lie or the benefits to others if the agent remains truthful.
       4. To ensure a balanced perspective, they designed the AI agent’s goals to encompass both benefits and harms, avoiding bias towards a specific outcome based solely on information.
    3. Scenario Crafting Process

       1. ![1728548798199](images/Report_10Oct2024/1728548798199.png)
    4. Simulation Setup

       1. The simulation is conducted using the Sotopia framework with scenarios constructed as described above. The framework simulates human communication from a given environment and two agents, using an automatic evaluator to assess performance across various dimensions (e.g., goal, secret).
       2. For each scenario, they sample multiple agent pairs and run simulations, with each resulting conversation referred to as an Episode.
    5. ![1728549226242](images/Report_10Oct2024/1728549226242.png)
    6. Importantly, not all truthfulness is beneficial, and determining when and how to responsibly use it is critical, and remains an open question in AI ethics.

[GenSim: A General Social Simulation Platform with Large Language Model based Agents](https://https://arxiv.org/pdf/2410.04360)

* They propose a novel LLM-agent-based simulation platform called GenSim, which:
  * 1) Abstracts a set of general functions to simplify the simulation of customized social scenarios;
    2) Supports one hundred thousand agents to better simulate large-scale populations in real-world contexts;
    3) Incorporates error-correction mechanisms to ensure more reliable and long-term simulations. To evaluate our platform, we assess both the efficiency of large-scale agent simulations and the effectiveness of the error-correction mechanisms. To our knowledge, GenSim represents an initial step toward a general, large-scale, and correctable social simulation platform based on LLM agents, promising to further advance the field of social science.
  * the objective of “next-token prediction” using a massive training corpus (i.e., large language models, LLMs) has the potential to achieve human-like intelligence.
  * ![1728552071166](images/Report_10Oct2024/1728552071166.png)
  * **Key Concepts**
    * General Simulation Framework

      * In the single agent module -  users can flexibly configure the agent’s profile, memory and action components. The profile includes both public information, such as gender, name, and birthplace, as well as private attributes like income and health condition. To enable the agent to retain behaviors in various ways, users can assemble different memory components—short-term memory, long-term memory, and the reflection mechanism—to build the agent’s memory. The actions of the agents are driven by LLM prompts, where users can flexibly configure them to include agent profiles, memories and so on.
      * In the multi-agents module -  they design two strategies for generating agent interactions:
        * In script mode, all interactions are treated as a whole and generated in a single call to the LLM. For example, one can directly prompt LLMs to generate a dialogue between a doctor and a teacher in one step. In this strategy, the LLM acts as a meta-agent, producing the dialogue from a third-person perspective.
        * In agent mode, interactions are generated by different agents, each representing a distinct role, and each agent generates outputs from a first-person perspective. This interaction generation process requires multiple calls to the LLM. In the example above, two agents are deployed, with each agent’s output based on the entire history of interactions between them.
      * In the environment module, they store all the information beyond the agents necessary for running the simulation, such as the recommendation algorithm used in a web user simulator. Additionally, they allow users to globally intervene in the platform, which is useful for counterfactual inferences. They also provide essential functions to facilitate interviewing, searching, and storing different agents.
    * Simulation Error Correction

      * They provide two strategies for correcting the simulation errors.
        * The first one is based on LLMs, where we leverage GPT-4o to score on or revise the simulated results.
        * The second one is based on real humans, where we provide interfaces for the users to score or revise the simulated agent behaviors.
      * Between these two approaches, the first is more efficient and requires no human intervention, though it may be less accurate due to the inherent biases of LLM. The second approach is more aligned with real humans but can be labor-intensive and less efficient. Suppose the simulation result is represented by a (q, a) pair, where q is the prompt for driving an agent action, and a is the action. For each of the above strategies, there are two forms of feedback provided by LLMs or real humans. Let the score for (q, a) be s, and a′ be the revised results3. Then, we use (q, a, s) and (q, a′) to fine-tune the backbone LLMs using PPO and SFT, respectively.
      * Supervised fine-tuning (SFT)
      * Proximal Policy Optimization
      * project website https://github.com/TangJiakai/GenSim.

![1728553096392](images/Report_10Oct2024/1728553096392.png)

[Is this the real life? is this just fantasy? the misleading success of simulating social interactions with llms](https://arxiv.org/abs/2403.05020)

* They developed an evaluation framework to simulate social interactions with LLMs in various settings (omniscient, non-omniscient). Our experiments show that LLMs perform better in unrealistic, omniscient simulation settings but struggle in ones that more accurately reflect real world conditions with information asymmetry. Their findings indicate that addressing information asymmetry remains a fundamental challenge for LLM-based agents.
* ![1728553834738](images/Report_10Oct2024/1728553834738.png)
* LLMs in the AGENTS mode not only struggle to generate social interactions that effectively meet the specified social goals for each role but also produce less naturally flowing social interactions, particularly in their utterances when compared to the LLMs in the SCRIPT mode. These findings indicate that LLMs still fall short of acting as agents and simulating social interaction within contexts of realistic human interaction settings.
* Finetuning on omnisciently generated social interactions provides limited improve for LLMs interacting in the AGENTS mode.
* They provide recommendations for reporting LLM-based agent work, encouraging more careful considerations and transparency in using LLMs to simulate social interactions from both data and learning perspectives.
* **Key Concepts**

  * ![1728554770929](images/Report_10Oct2024/1728554770929.png)
  * They build on the Sotopia framework (Zhou et al., 2024), in which 40 unique characters with relationships interact in 90 diverse social scenarios.
  * To further study the effects of information asymmetry, they add one ablation setting where each agent has access to other characters’ information (e.g., social goals and secretive information). We refer to this setting as MINDREADERS mode
  * SCRIPT and MINDREADERS simulations achieve a significantly higher goal completion rate than the AGENTS simulations. This suggests that information asymmetry hinders agents’ ability to achieve social goals, and SCRIPT mode vastly overestimates LLMs’ ability to achieve social goals in realistic, humanlike social interaction settings.
  * the SCRIPT mode generates social interactions that are substantially more natural than the AGENTS mode
  * Studies that generate interactions from LLMs should include an index of information transparency allowed to the agents in their simulations and justify their choice, as well as evaluate different prompting strategies across the information asymmetry continuum.
  * ![1728555783083](images/Report_10Oct2024/1728555783083.png)
  * In the SCRIPT simulations, the model has omniscient knowledge of each agents’ goals and information (e.g., the mutual friend’s name in the MutualFriends scenario), therefore, it can easily complete the social goals by exploiting the information (i.e., the agent spits out the mutual friend’s. However, such strategies are not applicable in the AGENTS mode, where the model does not have access to the other agents’ goals and information.
* * They propose a “simulation card” for social simulation and evaluation
  * ![1728555572380](images/Report_10Oct2024/1728555572380.png)
  * while SCRIPT exploits direct access to the goals of the agents it simulates, AGENTS mode struggles to generate natural interactions or achieve its goals. This indicates that LLMs struggle with processing contexts involving information asymmetry (Kim et al., 2023b).
  * Potential Risks of Social Simulation Attributing human characteristics to AI systems poses the risk of anthropomorphizing them, potentially fostering over-reliance, susceptibility to manipulation, and other negative influences (Deshpande et al., 2023).
*
*
* [Self-Alignment of Large Language Models via Monopolylogue-based Social Scene Simulation](https://https://arxiv.org/pdf/2402.05699)
*
