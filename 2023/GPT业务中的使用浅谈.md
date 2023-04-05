
# 一、关键词

`通用AI`、`Fine-tune`、`Prompt Engineering`	、`应用落地`、`GPT`

# 二、大模型使用思路

大模型（LLMs），简单来说是一类参数数量庞大、需要大量计算资源和数据来训练的神经网络模型。在自然语言处理领域，大模型已被广泛应用于语言模型、文本生成、情感分析和机器翻译等任务。在计算机视觉领域，大模型被用于物体检测、图像分类和图像生成等任务。在语音识别领域，大模型被用于语音转文本和语音生成等任务。

> 从ChatGPT的发展历程看我们是不是训练大模型只需要大数据和大算力就足够了？开始，OpenAI收集了大量的文本资料训练这样一个大模型，但是他只能从这些资料中学习，答案不受控制（GPT3）；引入了监督学习，人类提供校正资料来微调，之后又引入了RL（PPO），人类打分才最终获得了ChatGPT。

## 2.1、两条研究路径

### 2.1.1、专才

在已经预训练好的大型神经网络模型上，通过使用少量的目标任务相关数据进行训练，从而将该模型优化到该特定任务。

- 外挂和Fine-tune的配合（外挂：就是加一些分类层等等，适应下游任务）
- Fine-tune：用预训练模型的做初始化参数

> 如Meta开源的 LLaMA + 斯坦福开源的LoRA （针对超大的模型，降低微调门槛）

### 2.1.2、通才

能够在多个领域和任务中表现优异。ChatGPT是一种通用AI大模型，它已经被广泛应用于各种自然语言处理任务，如对话生成、文本生成、问答等。

- instruction learning + in-context learning
- 用指令和答案的数据训练，即instruction learning（Prompt）
- 给一些例子，来唤醒模型，即in-context learning（Chain of Thought）

## 2.2、对比两种研究路径

### 2.2.1、Fine-tuning（微调）

优点：

- 模型通过在特定任务的数据集上进行进一步训练，专注于特定任务，能更好地理解和解决任务相关问题。

缺点：

- 微调可能需要大量的计算资源和时间，尤其是对于大型模型。
- 需要高质量的标注数据，以便在特定任务上进行微调。获取这些数据可能耗时且昂贵。

### 2.2.2、Prompting（提示）

优点：

- 对模型进行提示不需要额外的训练，因此计算成本较低。
- 通过设计合适的提示，可以引导模型生成所需的答案，而无需对模型进行微调。
- 提示方法对于许多任务来说可能已经足够有效。

缺点：

- 设计有效的提示可能需要一定的经验和试验，以找到能引导模型生成理想输出的最佳提示。
- 对于某些任务，仅使用提示可能无法达到微调模型的性能水平，模型可能输出幻想的内容。

## 2.3、落地Prompting要考虑的问题

- 了解业务需求。
- 设计有效的prompt：尝试设计和测试不同的提示，以找到最能引导GPT生成满足业务需求的输出。有效的提示对于提高模型表现至关重要。
- 解决幻想问题：考虑到ChatGPT、GPT4的训练资料领域的局限性，补充文本知识。
- 监控模型性能：定期评估模型的性能，以确保其持续满足业务需求。根据反馈对提示进行优化，以提高模型的准确性和可靠性。
    - 准确性：通过定期抽样和人工审核，检查模型提供的答案是否准确、相关和合适。这可以帮助您了解模型是否能够正确理解用户问题并提供有效的解决方案。（**没有大量的数据进行提前评估**）
    - 反馈机制：建立用户反馈机制，让用户对智能客服的回答进行评价。这可以帮助您收集有关模型性能的直接反馈，并据此不断优化模型。
    - 响应时间：评估模型的响应速度。用户可能希望获得快速的回答，因此关注响应时间对于提供良好的用户体验至关重要。
    - 模型偏见：密切关注模型是否表现出不当的偏见或歧视。这可能会导致不准确或不公平的回答。定期对模型输出进行审查，以确保其遵循道德和公平性原则。
    - 用户满意度：通过问卷调查、在线评价等方式，收集用户对智能客服的满意度。了解用户对服务的满意程度有助于您持续改进服务质量。
    - 数据监控：对智能客服处理的问题和回答进行数据分析，了解用户的需求、痛点和常见问题。这可以帮助您调整和优化回答经验库，以提高模型性能。
- 错误处理和应对：为模型可能产生的错误输出设定相应的应对措施，例如为用户提供人工干预通道，以便在遇到问题时能够快速解决。
    - 人工干预：在某些情况下，当用户遇到困难或模型无法提供满意答案时，提供人工客服支持作为备选方案。这可以确保用户始终能得到解决问题的帮助。
    - 错误修正：对于已知的模型错误，定期更新和优化模型以减少这些错误。这可以包括调整模型参数、提供更具针对性的prompt，或者优化回答经验库。
    - 透明沟通：对于智能客服无法解决的问题，向用户说明模型的局限性，并提供其他途径（如联系人工客服或查看帮助文档）来解决问题。用户提供常见问题解答（FAQ）、教程或指南。
- 成本和资源管理：评估实施ChatGPT服务所需的计算资源、时间和成本。确保这些投入与预期的回报相匹配，以实现可持续发展。
- 数据安全和隐私：确保在与ChatGPT互动过程中，对敏感数据和用户隐私进行保护。遵循相关法规和公司政策，避免数据泄露风险。
    - 信息过滤：在从经验库检索答案时，确保过滤掉可能包含敏感数据和个人隐私的内容。您可以设定规则，对检索到的内容进行审查和处理，以防止泄露。
    - 用户隐私保护：对用户提供的信息进行匿名化处理，避免将个人身份信息与查询内容关联。例如，去除姓名、电话号码、电子邮件地址等个人标识。
- 保证客户体验的多方面考虑：
    - 模型规模选择：选择较小规模的模型，例如GPT-4的缩减版本。较小规模的模型通常在计算速度方面表现更优，但可能在某些情况下牺牲一些生成质量。
    - 缓存策略：对于高频或通用问题，可以使用缓存策略来存储预先生成的答案。这样，当用户询问相同或类似的问题时，可以直接从缓存中提取答案，而无需重新调用模型。**（和知识库很像，看具体延迟情况，可以视为数据增强）**
    - 优化Prompt：尽量减少模型输入的长度，因为模型处理较长输入时需要更多的计算时间。精简和优化您的提示，以便它们仍然清晰地表达问题，同时保持简洁。**已有框架限制长度**
    - 预测：对于某些常见问题，您可以考虑使用缓存策略，将预先计算好的答案存储在本地，从而减少API调用次数。此外，您还可以尝试预测用户可能会提出的问题，并提前获取答案，以便在用户实际提问时立即提供答案。这可以通过分析用户行为、历史问题等数据来实现。**(预测可能做起来比较复杂了，提前去请求API可能也是一个负担)**

# 三、基于OpenAI模型的Prompting

## 3.1、基础用法

- 安装openai包
- 在OpenAI官网里面获取你的OpenAI key，才能调用服务

```python
#!pip install openai

import openai
openai.api_key = "OPENAI_API_KEY"
```

- 写出prompt，传给模型获得结果
    - 模型选择（也涉及最大token数）
    - max_tokens+prompt的token数，不能超过最大模型的最大token数

```python
prompt = """回答我下面的提问

问题: 鸡年一共有多少天？

答案是: """

res = openai.Completion.create(
    model='gpt-4', # gpt-3.5-turbo
    prompt=prompt,
    max_tokens=256 #输出token的长度限制
)

print(res['choices'][0]['text'].strip()) #API response结果中只取出文字部分

# 12
```

- 添加例子（来自James Briggs）

```python
prompt = """The following are exerpts from conversations with an AI assistant.
The assistant is typically sarcastic and witty, producing creative 
and funny responses to the users questions. Here are some examples: 

User: How are you?
AI: I can't complain but sometimes I still do.

User: What time is it?
AI: It's time to get a watch.

User: What is the meaning of life?
AI: """

res = openai.Completion.create(
    model='text-davinci-003',
    prompt=prompt,
    max_tokens=256,
    temperature=1.0  # 0的话输出概率值最大的值，1.0会增强随机性，结果更有意思
)

print(res['choices'][0]['text'].strip())

# As the great philosopher Shrek once said: "Fiona, the meaning in life is to find your passion."
```

## 3.2、知识库增强

- 我们咨询的内容可能比较新（21年后），或者领域比较窄，就需要补充内容
- 基本实现就类似于给出的以下示例，只不过我们是输入一些文本知识，比如这样：

```python
prompt = """回答我下面的提问，并参考以下的文字

###

Contexts:
{xxxx}

###

问题: 鸡年一共有多少天？

答案是: """

res = openai.Completion.create(
    model='gpt-4', # gpt-3.5-turbo
    prompt=prompt,
    max_tokens=256 #输出token的长度限制
)

print(res['choices'][0]['text'].strip()) #API response结果中只取出文字部分

# 13.5
```

- 但很多时候，专家库是比较庞大的。受到token等限制，需要考虑根据输入内容，来取出对应的Contexts
- 实现过程如下
    - 利用Embedding模型将所有的专家经验库资料转成向量形式
    - 存入Pinecone，方便快速索引
    - 传入prompt时候，从存的向量中找到k个相似的文本作为Contexts，来提升模型生成的效果

```python
#1.导入专家数据
raw_data = load_dataset('xxxx_of_yourcompany')

#2.转换成向量并存入Pinecone
# 初始化pineone, 本段来自 https://docs.pinecone.io/docs/openai
import pinecone
pinecone.init(...)
index = pinecone.Index('openai')

#3.转换向量
embed_model = "text-embedding-ada-002"  # 或者使用sentence-bert
data_embedding= openai.Embedding.create(input=raw_data , engine=embed_model)

#4.插入向量信息到pinecone
..upsert..

#5.执行查询
query_embedding = openai.Embedding.create(input=[query],engine=embed_model)
result = index.query(query_embedding['data'][0]['embedding'], top_k=2, include_metadata=True)
```

- 当然考虑到文本长度，可以写规则限制查询到的原始文本最大长度，达到limit就停止

## 3.3、工具协同

ChatGPT Plugin

# 四、基于LangChain的实现

LangChain是一个最近才有不久的框架，允许用户围绕**大型语言模型**（如ChatGPT，或FLAN等）快速构建应用程序和Pipeline。它可以用于聊天机器人、生成问题回答（GQA）、摘要等等。一般来说，有下面一些模块：

- **Prompt templates**: Prompt templates are, well, templates for different types of prompts. Like "chatbot" style templates.
- **LLMs**: Large language models like GPT-3.
- **Agents**: Agents use LLMs to decide what actions should be taken, tools like web search or calculators can be used, and all packaged into logical loop of operations.
- **Memory**: Short-term memory, long-term memory.

## 4.1、基础用法

- 把模板template、Question、model分离开

```python
from langchain import PromptTemplate, LLMChain
from langchain.llms import OpenAI

# QA的模板
template = """Question: {question}
Answer: """
prompt = PromptTemplate(template=template, input_variables=["question"])

# 定义用的模型
Model= OpenAI(model_name='gpt4', openai_api_key="YOUR_API_KEY") 
llm_chain = LLMChain(
    prompt=prompt,
    llm=Model
)

question = "鸡年有多少天"
print(llm_chain.run(question))

```

- 可以批量提问

```python
multi_template = """Answer the following questions one at a time.

Questions:
{questions}

Answers:
"""

qs = [
    "xxxxx1?",
    "xxxxx2",
    "xxxxx3",
    "xxxxx4"
]
print(llm_chain.run(qs))
```

## 4.2、知识库增强

- 同样可以添加context

```python
template = """根据以下上下文回答问题/以下是一些例子

Context: xxxx

Question: {query}

Answer: """

prompt_template = PromptTemplate(
    input_variables=["query"],
    template=template
)

#定义模型
openai = OpenAI(
    model_name="gpt4",
    openai_api_key="YOUR_API_KEY"
)

#输出结果
print(openai(
    prompt_template.format(
        query="Which libraries and model providers offer LLMs?"
    )
))
```

- 同样为了克服token限制、也为了更灵活取出内容，利用**Few Shot Prompt Templates**从知识库中抽取

```python
#1. 专家库
Knowledge = []

# the prefix is our instructions
prefix = """回答提问，并参考下面的例子: 
"""
# 创建模板
example_template = """
User: {query}
AI: {answer}
"""
# create a prompt example from above template
example_prompt = PromptTemplate(
    input_variables=["query", "answer"],
    template=example_template
)

# and the suffix 
suffix = """
User: {query}
AI: """

#2. 导入选择器
from langchain.prompts.example_selector import SemanticSimilarityExampleSelector
from langchain.vectorstores import Chroma
from langchain.embeddings import OpenAIEmbeddings

example_selector = SemanticSimilarityExampleSelector.from_examples(
    Knowledge ,
    #转成embedding
    OpenAIEmbeddings(),
    # 存起来做搜索的
    Chroma,
    # 取几个文本
    k=1
)

#3. 动态选择context
dynamic_prompt_template = FewShotPromptTemplate(
    example_selector=example_selector,  # use example_selector instead of examples
    example_prompt=example_prompt,
    prefix=prefix,
    suffix=suffix,
    input_variables=["query"],
    example_separator="\n"
)

# 输出结果
query = "鸡年有多少天?"
print(openai(
    dynamic_prompt_template.format(query=query)
))

```

## 4.3、Chain

Chain是核心内容，前面的就是最基础的chain：把prompt template、user input给模型，输出LLM的结果。当然可以连接很多个Chain，以下是一个简单的例子。

```python
#1. 一个Chain

# QA的模板
template = """Question: {question}
Answer: """
prompt = PromptTemplate(template=template, input_variables=["question"])

# 定义用的模型
Model= OpenAI(model_name='gpt4', openai_api_key="YOUR_API_KEY") 
llm_chain = LLMChain(
    prompt=prompt,
    llm=Model
)

question = "鸡年有多少天"
print(llm_chain.run(question))

1. 定义第二个Chain
second_prompt = PromptTemplate(
    input_variables=["fist_chain_answer"],
    template="xx{fist_chain_answer}",
)
chain_two = LLMChain(llm=llm, prompt=second_prompt)

from langchain.chains import SimpleSequentialChain
overall_chain = SimpleSequentialChain(chains=[chain, chain_two], verbose=True)

# 还是输入第一个问题的提问就行
Answer= overall_chain.run("鸡年有多少天？")
print(Answer)
```

## 4.4、Memory

一般来说， Chain之间是独立的。但是像是聊天机器人这种，需要用到之前的信息。

- 官网样例（使用ConversationBufferMemory）

```python
from langchain.llms import OpenAI
from langchain.chains import ConversationChain

llm = OpenAI(temperature=0)
conversation = ConversationChain(
    llm=llm, 
    verbose=True, 
    memory=ConversationBufferMemory()
)
conversation.predict(input="Hi there!")
```

```markdown
> Entering new ConversationChain chain...
Prompt after formatting:
The following is a friendly conversation between a human and an AI. The AI is talkative and provides lots of specific details from its context. If the AI does not know the answer to a question, it truthfully says it does not know.

Current conversation:

Human: Hi there!
AI:

> Finished chain.

" Hi there! It's nice to meet you. How can I help you today?"
```

```python
conversation.predict(input="I'm doing well! Just having a conversation with an AI.")
```

```markdown
> Entering new ConversationChain chain...
Prompt after formatting:
The following is a friendly conversation between a human and an AI. The AI is talkative and provides lots of specific details from its context. If the AI does not know the answer to a question, it truthfully says it does not know.

Current conversation:
Human: Hi there!
AI:  Hi there! It's nice to meet you. How can I help you today?
Human: I'm doing well! Just having a conversation with an AI.
AI:

> Finished chain.

" That's great! It's always nice to have a conversation with someone new. What would you like to talk about?"
```

- ConversationBufferMemory会比较消耗token，还有其他如**ConversationSummaryMemory、ConversationBufferWindowMemory**

## 4.5、与工具协同-Agent

Agents 就是给大小模型的工具，比如访问谷歌搜索、进行复杂计算甚至做SQL查询

在LangChain里面的概念：

- Tool: A function that performs a specific duty. This can be things like: Google Search, Database lookup, Python REPL, other chains. The interface for a tool is currently a function that is expected to have a string as an input, with a string as an output. 
- LLM: The language model powering the agent.
- Agent: The agent to use. This should be a string that references a support agent class. 

看一个官网的案例：

```python
from langchain.agents import load_tools
from langchain.agents import initialize_agent
from langchain.llms import OpenAI

llm = OpenAI(temperature=0)

# load 要用的工具：搜索和计算
tools = load_tools(["serpapi", "llm-math"], llm=llm)
# 选择想要用的agent类型
agent = initialize_agent(tools, llm, agent="zero-shot-react-description", verbose=True)
```

- serpapi ：搜索引擎
- "zero-shot-react-description"自行决定要使用的工具。当然也有更详细的一些如“react-docstore”、“conversational-react-description”

```markdown
> Entering new AgentExecutor chain...
 I need to find out who Leo DiCaprio's girlfriend is and then calculate her age raised to the 0.43 power.
**Action: Search
Action Input: "Leo DiCaprio girlfriend"**
Observation: Camila Morrone
**Thought: I need to find out Camila Morrone's age
Action: Search
Action Input: "Camila Morrone age"**
Observation: 25 years
**Thought: I need to calculate 25 raised to the 0.43 power
Action: Calculator
Action Input: 25^0.43**
Observation: Answer: 3.991298452658078

**Thought: I now know the final answer
Final Answer:** Camila Morrone is Leo DiCaprio's girlfriend and her current age raised to the 0.43 power is 3.991298452658078.

> Finished chain.
```

- 现在有能力“推理”如何最好地使用工具来解决我们的查询，并可以以智能的方式将它们结合起来，只需对每一个工具进行简要描述
- **Thought：**在使用一个工具后，它会将自己的想法和观察添加到草稿簿中，然后从那里开始。

# 参考

- https://www.bilibili.com/video/BV1oX4y1R7df/
- https://www.bilibili.com/video/BV1nL411S7fE/