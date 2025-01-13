#balanced brackets
def isBalanced(s):
    stack = []
    matching_brackets = {')': '(', ']': '[', '}': '{'}

  for char in s:
      if char in "({[":
          stack.append(char)
      elif char in ")}]":
          if not stack or stack[-1] != matching_brackets[char]:
              return "NO"
          stack.pop()
  return "YES" if not stack else "NO"
       
import sys
input = sys.stdin.read
data = input().splitlines()

t = int(data[0]) 
results = []

for i in range(1, t + 1):
    results.append(isBalanced(data[i]))  
print("\n".join(results))

#queue using two stacks

class QueueUsingTwoStacks:
  def __init__(self):
        self.stack1 = [] 
        self.stack2 = []  

  def enqueue(self, x):
        self.stack1.append(x)

  def dequeue(self):
        if not self.stack2:
            while self.stack1:
                self.stack2.append(self.stack1.pop())
        if self.stack2:
            self.stack2.pop()

  def front(self):
        if not self.stack2:
            while self.stack1:
                self.stack2.append(self.stack1.pop())
        if self.stack2:
            return self.stack2[-1]
        return None


def process_queries(queries):
    queue = QueueUsingTwoStacks()
    for query in queries:
        if query[0] == 1:
            queue.enqueue(query[1])
        elif query[0] == 2:
            queue.dequeue()
        elif query[0] == 3:
            print(queue.front())


import sys
input = sys.stdin.read
data = input().splitlines()

q = int(data[0])
queries = []
for i in range(1, q + 1):
    query = list(map(int, data[i].split()))
    queries.append(query)

process_queries(queries)

#games of two stacks
def twoStacks(maxSum, a, b):
    sum_a = 0
    count = 0
    max_count = 0

  prefix_a = [0]
    for x in a:
        if prefix_a[-1] + x > maxSum:
            break
        prefix_a.append(prefix_a[-1] + x)

  sum_b = 0
    for i in range(len(b) + 1):
        if i > 0:
            sum_b += b[i - 1]
        if sum_b > maxSum:
            break

  while prefix_a and prefix_a[-1] + sum_b > maxSum:
            prefix_a.pop()

  max_count = max(max_count, len(prefix_a) - 1 + i)

  return max_count


def main():
    g = int(input().strip())
    results = []
    for _ in range(g):
        n, m, maxSum = map(int, input().strip().split())
        a = list(map(int, input().strip().split()))
        b = list(map(int, input().strip().split()))
        results.append(twoStacks(maxSum, a, b))

  for res in results:
        print(res)

if __name__ == "__main__":
    main()



