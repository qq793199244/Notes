### Python 生成随机数
在 Python 中用于生成随机数的模块是 random ，在使用前需要 import random 包。 如下列举：
- random.random()：生成一个 0-1 之间的随机浮点数
- random.uniform(a, b)：生成[a,b]之间的浮点数
- random.randint(a, b)：生成[a,b]之间的整数
- random.randrange(a, b, step)：在指定的集合[a,b)中，以 step 为基数随机取一个数
- random.choice(sequence)：从特定序列中随机取一个元素，这里的序列可以是字符串，列表，元组等
