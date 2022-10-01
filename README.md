# YAKE (Yet Another Keyword Extractor) RUST

Yake is based on this paper: https://repositorio.inesctec.pt/server/api/core/bitstreams/ef121a01-a0a6-4be8-945d-3324a58fc944/content

Yake is a language agnostic statistical keyword extractor weighing several factors such as acronyms, position in paragraph, capitalization, how many sentences the keyword appears in, stopwords, punctuation and more. 



## Example 

```
import * as yake from './pkg/yake_wasm.js'
console.time('yake benchmark');
const instance = new yake.Yake();
const testString = `
    Google is acquiring data science community Kaggle. Sources tell us that Google is acquiring Kaggle, a platform that hosts data science and machine learning 
    competitions. Details about the transaction remain somewhat vague, but given that Google is hosting its Cloud 
    Next conference in San Francisco this week, the official announcement could come as early as tomorrow. 
    Reached by phone, Kaggle co-founder CEO Anthony Goldbloom declined to deny that the acquisition is happening. 
    Google itself declined 'to comment on rumors'. Kaggle, which has about half a million data scientists on its platform, 
    was founded by Goldbloom  and Ben Hamner in 2010. 
    The service got an early start and even though it has a few competitors like DrivenData, TopCoder and HackerRank, 
    it has managed to stay well ahead of them by focusing on its specific niche. 
    The service is basically the de facto home for running data science and machine learning competitions. 
    With Kaggle, Google is buying one of the largest and most active communities for data scientists - and with that, 
    it will get increased mindshare in this community, too (though it already has plenty of that thanks to Tensorflow 
    and other projects). Kaggle has a bit of a history with Google, too, but that's pretty recent. Earlier this month, 
    Google and Kaggle teamed up to host a $100,000 machine learning competition around classifying YouTube videos. 
    That competition had some deep integrations with the Google Cloud Platform, too. Our understanding is that Google 
    will keep the service running - likely under its current name. While the acquisition is probably more about 
    Kaggle's community than technology, Kaggle did build some interesting tools for hosting its competition 
    and 'kernels', too. On Kaggle, kernels are basically the source code for analyzing data sets and developers can 
    share this code on the platform (the company previously called them 'scripts'). 
    Like similar competition-centric sites, Kaggle also runs a job board, too. It's unclear what Google will do with 
    that part of the service. According to Crunchbase, Kaggle raised $12.5 million (though PitchBook says it's $12.75) 
    since its   launch in 2010. Investors in Kaggle include Index Ventures, SV Angel, Max Levchin, Naval Ravikant,
    Google chief economist Hal Varian, Khosla Ventures and Yuri Milner`;

const results = instance.get_n_best(testString)
console.log(results)
console.timeEnd('yake benchmark');
```

Result:

```
  { raw: 'kaggle', keyword: 'kaggle', score: 0.034743798859937204 },
  { raw: 'google', keyword: 'google', score: 0.03946072940468415 },
  { raw: 'data', keyword: 'data', score: 0.23971332973044301 },
  { raw: 'science', keyword: 'science', score: 0.25215955136759277 },
  {
    raw: 'acquiring kaggle',
    keyword: 'acquiring kaggle',
    score: 0.3017882425537463
  },
  {
    raw: 'data science',
    keyword: 'data science',
    score: 0.30873986543219967
  },
  { raw: 'acquiring', keyword: 'acquiring', score: 0.364289463693419 },
  { raw: 'platform', keyword: 'platform', score: 0.39586953475013703 },
  { raw: 'goldbloom', keyword: 'goldbloom', score: 0.3981554971375386 },
  {
    raw: 'google cloud',
    keyword: 'google cloud',
    score: 0.40955463454967833
  }
]
yake benchmark: 12.124ms
```




