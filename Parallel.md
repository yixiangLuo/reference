https://docs.python.org/3/library/multiprocessing.html

```
from multiprocessing import Pool
import tqdm

def GLOBAL_FUNCTION(args_tuple):
	a, b = args_tuple
	return a + b

args_list = [(1, 2), (3, 4)]

pool = Pool(processes = n_core)

# basic usage
results = list(pool.imap_unordered(GLOBAL_FUNCTION, args_list))
# with progress bar
results = list(
	tqdm.tqdm(
		pool.imap_unordered(GLOBAL_FUNCTION, args_list),
		total = len(args_list)
	)
)
```
