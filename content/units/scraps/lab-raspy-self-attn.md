## Part 1: Programming with Self-Attention

If you haven't, finish:

- {{% notebook name="Programming with Self-Attention" nbname="u11n1-self-attention.ipynb" %}}

Additional challenge (optional):

Make a network that outputs "1" after prefixes that have the same number of open parens (`(`) and close parens (`)`). Strategy: 

```python
raspy.visualize.EXAMPLE = '( () ) ()'

# Count the number of open parens that occur before each token.
# num_open = ...
num_open = (key(indices) <= query(indices)).value(tokens == '(')
# Count the number of close parens
# num_close = ...
num_close = (key(indices) <= query(indices)).value(tokens == ')')
# Check if they're equal.
num_open == num_close
```

To make this a true validator for matched parens, we'd need to add two conditions: the last token is balanced, and `num_close - num_open` never goes negative. See the RASP paper for a complete implementation.
