# Code Completion model
The "code completion" model component is used to support autocomplete suggestions and is also referred to as the "tab-autocomplete model". Tab-autocomplete models use models trained with special templates, such as FiM(Fill in the Middle), that specialize in code infilling, and typically use small models, on the order of 1-15B for low latency. Because developers need a suggestion within 500ms, you generally need to use a smaller model in order to meet the latency requirements. However, the quality of suggestions you get from models that are too small is bad. Thus, the tab-autocomplete model is optimized primarily with these two constraints in mind. Examples of models used for tab-autocomplete are shown below:

OpenSource Models
2B Class
- codegemma-2b	
- deepseek-coder-1.3b-base
- starcoder2-3b	

7B Class
- codegemma-7b
- codellama-7b
- deepseek-coder-6.7b-base
- starcoder2-7b

10B+ Class
- codellama-13b
- deepseek-coder-33b-base
- starcoder2-15b

ClosedSource Model 
- Codex-001
- Codex-002
