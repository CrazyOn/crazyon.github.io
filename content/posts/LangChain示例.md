+++
title = 'LangChain示例'
date = 2024-06-05T08:29:34+08:00
draft = true
+++
Conda环境
``` bash
conda create -n langchain-env python=3.11
conda activate langchain-env
```

依赖项
``` bash
pip install --upgrade langchain
pip install -U langchain-community
```

Python调用示例
``` python
import os
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain_core.runnables import RunnablePassthrough
from langchain_community.llms import Tongyi

# 设置环境变量
os.environ["DASHSCOPE_API_KEY"] = "sk-xxx"

if __name__ == "__main__":
    # 初始化通义千问模型
    model = Tongyi(model_name="qwen-turbo")
    prompt = ChatPromptTemplate.from_template(
        "Tell me a short joke about {topic}"
    )
    output_parser = StrOutputParser()
    chain = (
        {"topic": RunnablePassthrough()}
        | prompt
        | model
        | output_parser
    )

    print(chain.invoke("ice cream")) 
```

运行结果
`Why did the ice cream truck break down? Because it couldn't hold its load!`

模块拆解
- 导入必要的模块：
    ```python
    import os
    from langchain_core.prompts import ChatPromptTemplate
    from langchain_core.output_parsers import StrOutputParser
    from langchain_core.runnables import RunnablePassthrough
    from langchain_community.llms import Tongyi
    ```
- 设置环境变量：
    ``` python
    os.environ["DASHSCOPE_API_KEY"] = "sk-xxx"
    ```
    这里设置了一个环境变量 `DASHSCOPE_API_KEY`，用于API认证。


- 主函数：
    ``` python
    if __name__ == "__main__":
        # 初始化通义千问模型
        model = TongYi(model_name="qwen-turbo")
        prompt = ChatPromptTemplate.from_template(
            "Tell me a short joke about {topic}"
        )
        output_parser = StrOutputParser()
        chain = (
            {"topic": RunnablePassthrough()}
            | prompt
            | model
            | output_parser
        )

        print(chain.invoke("ice cream"))
    ```
- 传送门
    - [`langchain-ai/langchain`](https://github.com/langchain-ai/langchain/tree/master/libs/community/langchain_community/llms)
    - [`Tongyi`](https://github.com/langchain-ai/langchain/blob/234394f6316d854972e65009c7a94921dd780f51/libs/community/langchain_community/llms/tongyi.py#L160) 
    - [`ChatPromptTemplate`](https://github.com/langchain-ai/langchain/blob/234394f6316d854972e65009c7a94921dd780f51/libs/core/langchain_core/prompts/chat.py#L709)
    - [`StrOutputParser`](https://github.com/langchain-ai/langchain/blob/234394f6316d854972e65009c7a94921dd780f51/libs/core/langchain_core/output_parsers/string.py#L6)
    - [`RunnablePassthrough`](https://github.com/langchain-ai/langchain/blob/234394f6316d854972e65009c7a94921dd780f51/libs/core/langchain_core/runnables/passthrough.py#L65)

- 初始化模型：
    ``` python
    model = Tongyi(model_name="qwen-turbo")
    ```
    使用 `Tongyi` 初始化了一个名为 `qwen-turbo` 的模型。
    在 `langchain-ai/langchain` 仓库中，`Tongyi` 类是用于与阿里巴巴的通义（Qwen）大语言模型进行交互的一个类。

- 创建提示模板：
    ``` python
    prompt = ChatPromptTemplate.from_template(
        "Tell me a short joke about {topic}"
    )
    ```
    创建了一个聊天提示模板`ChatPromptTemplate`，模板内容是`Tell me a short joke about {topic}`。

- 创建输出解析器：
    ``` python
    output_parser = StrOutputParser()
    ```
    使用 `StrOutputParser` 解析模型的输出。

- 创建链条：
    ``` python
    chain = (
        {"topic": RunnablePassthrough()}
        | prompt
        | model
        | output_parser
    )
    ```
    创建了一个链条，依次执行传递主题`RunnablePassthrough`、生成提示、调用模型和解析输出的操作。

- 调用链条：
    ``` python
    print(chain.invoke("ice cream"))
    ```
    调用链条并传入主题`ice cream`，然后打印生成的笑话。