# KMP in Python
:kmp:algorithm:
	
```python
def get_failure_func(pattern:str):
  # initialize our two arrays
  p_list = [x for x in pattern] 
  f = [0 for x in pattern] # init failure function with 0s

  # init counter vars
  i = 1 
  j = 0
  m = len(p_list)
  
  while i < m:
	  if p_list[i] == p_list[j]:
		  f[i] = j+1
		  i += 1
		  j += 1
	  elif j > 0:
		  j = f[j-1]
	 else:
		  f[i] = 0
		  i += 1
  
  return f


def knuth_morris_pratt(pattern :str, text :str):
  f = get_failure_func(pattern) # failure function
  p = pattern # "AGAGACCT" pattern
  t = text # "TGTCACTAGAGACCT" text
  i = 0
  j = 0
  while i < len(t):
	  if t[i] == p[j]: # our two characters match, now we need to check:
		  if j == len(p) - 1: # Have we found our pattern?
			  return i-j # Pattern found, return index (i-j because the match starts at index i-j)
		  else: # no, we aren't done yet!
			  i += 1 # increment both i and j in order to see if next characters also match
			  j += 1
	  else: # Characters missmatched
		  if j > 0:
			  j = f[j-1] # Use failure function (index j-1 because we start counting at 0)
		  else:
			  i += 1 # j = 0, we only increment i => get next character in string
```

