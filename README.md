# Infographic-
timeline Infographic 

1. 用户输入
工作流节点：接收用户输入
任务：收集用户提供的内容、类别、尺寸和描述
输入：用户界面输入
输出：UserInput 对象
数据流：用户界面 -> 应用服务器

2. 文本分析和结构化
工作流节点：内容分析
任务：使用 meta/meta-llama-3-70b-instruct 模型分析文本
输入：UserInput 对象
输出：StructuredContent 对象
数据流：应用服务器 -> Replicate API -> 应用服务器

3. 提示工程 - 文本分析
工作流节点：生成文本分析提示
任务：基于用户输入构建文本分析提示
输入：UserInput 对象
输出：AnalysisPrompt 对象
数据流：内部处理

4. 提示工程 - 信息图生成
工作流节点：生成信息图提示
任务：基于结构化内容构建信息图生成提示
输入：StructuredContent 对象
输出：InfographicPrompt 对象
数据流：内部处理

5. 信息图生成
工作流节点：生成信息图
任务：使用 black-forest-labs/flux-schnell 模型生成信息图
输入：InfographicPrompt 对象
输出：GeneratedImage 对象
数据流：应用服务器 -> Replicate API -> 应用服务器

6. 图像存储
工作流节点：存储生成的图像
任务：将生成的图像上传到 Supabase 存储
输入：GeneratedImage 对象
输出：StoredImage 对象
数据流：应用服务器 -> Supabase 存储

7. 数据保存
工作流节点：保存信息图数据
任务：将信息图相关数据保存到 Supabase 数据库
输入：UserInput, StructuredContent, StoredImage 对象
输出：InfographicRecord 对象
数据流：应用服务器 -> Supabase 数据库

8. 结果返回
工作流节点：返回结果
任务：将生成的信息图数据返回给用户
输入：InfographicRecord 对象
输出：InfographicResult 对象

数据流：应用服务器 -> 用户界面![image](https://github.com/user-attachments/assets/d235d53d-a887-410e-9522-1118a680a529)
