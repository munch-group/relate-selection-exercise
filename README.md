

Creating the parquet file:

```python
from pathlib import Path
import pandas as pd
path = Path("tmp")
df_list = []
merged = None
for p in path.glob("**/*.sele"):    
    print(p.parent.name, p.name)
    df = pd.read_csv(p, sep=' ', usecols=['pos', 'when_mutation_has_freq2']).rename(columns={'when_mutation_has_freq2': p.parent.name})
    if merged is None:
        merged = df
    else:
        merged = merged.merge(df, on='pos', how='outer')
merged.head()
merged.to_parquet('relate_log10pvals_1000g_pops.parquet')
```

[rs182549](https://genome-euro.ucsc.edu/cgi-bin/hgTracks?db=hg38&dbSnp153Common=pack&position=chr2:135859084-135859284&hgFind.matches=rs182549&dbSnp153Common_sel=1&dbSnp153ViewVariants_sel=1&addHighlight=hg38.chr2%3A135859184-135859184%23fcfcac): chr2 135859084