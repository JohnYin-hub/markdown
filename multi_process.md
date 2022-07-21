```python
from multiprocessing import Pool
pool = Pool(processes=30)
pool.map(download_github, data) 
pool.close()
pool.join()
```

