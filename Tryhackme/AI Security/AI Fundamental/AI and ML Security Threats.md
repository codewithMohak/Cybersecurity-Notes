# Learning Objective
- Understand AI .ML and their impact on the cyber security industry.
- Understand Deep Learning (DL) and neural networks and how they have made the applications of AI, we see today, possible.
- Understand  how adversaries  use AI, to enhance existing attacks and take. advantage of AI  Model Vulnerability.
- Understand the key role of AI play in defending  against AI.
# The Building Blocks of AI
## Let's start by discussing ho we can define Artificial Intelligences . Artificial Intelligence refer to a machine or computer system that is able to carry out tasks that would otherwise require human reasoning , comprehension , problem solving or creativity.
# Machine Learning (ML)
## The next major step in development of Artificial Intelligence  (AI) was introduction of Machine Learning (ML).
Machine Learning is a branch of Artificial Intelligence that allows computers to learn from the data without being directly programmed. It works in a way that is similar to how human learn from experience. As the model receives more data over time, it becomes better at making accurate predictions and decisions.
# Machine Learning Lifecycle
## Machine Learning follows a step-by-step process to build and use reliable models.

 It starts by **defining the problem**, for example, deciding whether an email is spam or not. Next, **data is collected, cleaned, and prepared**. During this stage, **feature engineering** is used to select the most useful information from the data while reducing the chances of **overfitting** (when a model learns the training data too well and performs poorly on new or unseen data).

After the data is ready, a suitable **Machine Learning algorithm** is chosen, and the model is **trained**. Once training is complete, the model is **tested and improved** by adjusting its settings to achieve better accuracy. The final model is then **deployed** into a real-world environment, where it can perform tasks such as detecting spam emails automatically.

The process does not stop after deployment. The model is **continuously monitored** to make sure it still performs well. If its accuracy decreases because of new data or changing conditions, it is trained again with updated data. For this reason, the **Machine Learning Lifecycle is an ongoing and repetitive process**.
## Machine Learning Algorithms

**Machine Learning algorithms** are mathematical methods that help computers find patterns in data. A **model** is the final result created after an algorithm has been trained on data.

Every Machine Learning algorithm has **three main parts**:

- **Decision Process:** Makes predictions or classifications using the input data.
- **Error Function:** Measures how accurate the predictions are and identifies mistakes.
- **Model Optimization:** Adjusts the model to reduce errors and improve accuracy.

These three steps are repeated many times until the model reaches a good level of performance.
## Types of Machine Learning
Machine Learning algorithms are divided into **four main types**:
### 1. Supervised Learning
Uses **labeled data**, where the correct answers are already known. It is mainly used for **classification** and **regression** tasks, such as detecting spam emails or predicting house prices.
### 2. Unsupervised Learning
Uses **unlabeled data**, where no correct answers are provided. The goal is to discover hidden patterns in the data using techniques such as **clustering**, **association**, and **dimensionality reduction**.
### 3. Semi-Supervised Learning
Uses a combination of **a small amount of labeled data** and **a large amount of unlabeled data**. The labeled data helps guide the learning process and improve the model's performance.
### 4. Reinforcement Learning
Works by allowing an **agent** to learn through **rewards and penalties**. Correct actions are rewarded, while incorrect actions receive penalties. Over time, the agent learns the best actions to maximize rewards and achieve the desired goal.
# Neural Networks and Deep Learning

The main goal of **Artificial Intelligence (AI)** is to make computers think and behave like humans. One way to achieve this is by using **Neural Networks**.

The idea of a neural network comes from the **human brain**. The brain is made up of billions of **neurons**, which are special cells that send and receive information. These neurons communicate with each other through **synapses**, which are connections between neurons. When we learn something new, the strength of these connections changes based on our experiences and the patterns we recognize. Neural networks copy this same learning process.
## Neural Networks
A neural network is made up of **layers of connected nodes (neurons)** that work together to process information.
### Input Layer
The **input layer** receives the raw data. The number of input nodes depends on the type of data. For example, a **4 × 4 pixel image** contains **16 pixels**, so the input layer would have **16 nodes**.
### Hidden Layers
The **hidden layers** process the input data step by step. Each connection between nodes has a **weight**, which shows how important that connection is. More important information is given a higher weight.
For example, when classifying emails, the **email body** may have a higher weight than the **subject line** because it usually contains more useful information.
### Output Layer
The **output layer** gives the final prediction or classification based on what the hidden layers have learned.
## Example: Recognizing Numbers

Imagine a neural network that identifies handwritten numbers from images.
- The **first hidden layers** detect simple features such as **lines, edges, and curves**.
- The **deeper hidden layers** combine these features to recognize complete numbers.
- For example:
    - Straight lines may suggest the number **1** or **7**.
    - Curves may suggest **0**, **3**, or **8**.
- Finally, the **output layer** contains **10 nodes**, one for each digit from **0 to 9**. The node with the highest prediction value is selected as the final answer.

This learning process is similar to how the human brain recognizes patterns. When a neural network has **more than three layers**, it is called a **Deep Learning (DL)** model. This is why it is known as **"deep" learning**.
# What is LLMs, and how do they work?
## Larger Language Model (or LLMs) are Deep learning-based AI models that can process  and generate text by predicting the next word in a sequence.
For example , imagine the sentence :
> "The Sky is blue because of the_________"

The LLM tries to predict the missing word. This is exactly what happens when you chat with an AI chatbot like ChatGPT. Behind the scenes, the model keeps predicting the next word until it forms a complete response.
# How are LLMs trained?
LLMs first go through a stage called pre-training.
![[Cyber-Security/Attachment/AI and ML Security Threats-1783243003992.webp]]
