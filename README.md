# AxiiaGraph

## plan


## research on other framework

structured outputs

too many new syntax : lmql, guidance

seems trying to give chat a very unique position

RAG and Agent(tool calling) are heavilty emphasized

## thoughts
1. assume you have all the prompts as fun , and write code using llm. make sure it runs
2. write all the llm funs, (remember take care of outputs)
3. maybe always write one function as the final res
4. always think about inputs and outputs

## goals

1. simple call to llm, easy to **parse** output
2. easy for llm to write 
3. we need to let prompt take **variables** and prompt can be **seperated** from code
4. easier to write **batch** evals , where we run workflow on multiple inputs and **compare** their outputs to reference answer
5. how does chat happen? expilicitly maintain states?
6. test individual prompt inside the workflow node
7. need to confine how user uses it
8. some pre processing of data is needed, adviced need provided
   - maybe always csv ?


## questions


## sample 
### question from list 
1. prompt for no llm calls:
   -  write a function that takes input a user_question string, a Question and Answer list. if the user_question is in the QNA list ,then output True and the answer in the list, otherwise output False . The qna list will initlaly loeded from a csv file, where first col is Que, and second col is Ans
   - assume the first col of qna list is id(from 0 to n) ; assume there exist a function called cmp_q which takes input two string q1, q2, and outputs true if q1 and q2 are semanticaly similar q, and false otherwsie



### scratch 

```
def cmp_q(q1, q2):
return q1.strip().lower() == q2.strip().lower()


q1 and q2 are two strings of questions

rewrite the above function 
use prompt and claude_gpt to judge whether q1, q2 are semantically similar
the function should output true if they are , and false otherwise
if llm output something unexpcted , please raise exception



use the following prompt

prompt = """
Are the following two questions semantically similar?
are they ask for similar answers?
\nQuestion 1: {q1_str}\nQuestion 2: {q2_str}\n

Please answer 'yes' or 'no' in 
<answer>[yes or no]</answer>
""".format(q1_str=q1, q2_str=q2)

use the following function for llm call

def claude_chat(prompt, model_name="claude-3-haiku-20240307"):
# Initialize the model with the given model name
model = ChatAnthropic(model=model_name)
# Generate the response from the model
response = model.invoke(prompt)
# Return the response
return response.content
```
