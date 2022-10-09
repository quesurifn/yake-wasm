# YAKE (Yet Another Keyword Extractor) Rust WASM

Yake is based on this paper: https://repositorio.inesctec.pt/server/api/core/bitstreams/ef121a01-a0a6-4be8-945d-3324a58fc944/content

Yake is a language agnostic statistical keyword extractor weighing several factors such as acronyms, position in paragraph, capitalization, how many sentences the keyword appears in, stopwords, punctuation and more.

However, this version of Yake makes a few optimizations to ensure the most accuracy. The optimizations are:

- We assume that substrings of a complete ngram are should be removed. E.g. If data, science and data science are all candidates, data and science should be removed from candidacy to leave the fuller and more complete term "data science"

- Coming Soon: Good keywords should be in the imperative mood in the simple present tense with nouns and limited adjectives. Soon, the algorithm will account for this.

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
 [
  {
    "keyword": "kaggle",
    "raw": "Kaggle",
    "score": 0.034743798859937204
  },
  {
    "keyword": "google",
    "raw": "Google",
    "score": 0.03946072940468415
  },
  {
    "keyword": "acquiring kaggle",
    "raw": "acquiring Kaggle",
    "score": 0.3017882425537463
  },
  {
    "keyword": "data science",
    "raw": "data science",
    "score": 0.30873986543219967
  },
  {
    "keyword": "goldbloom",
    "raw": "Goldbloom",
    "score": 0.3981554971375386
  },
  {
    "keyword": "google cloud",
    "raw": "Google Cloud",
    "score": 0.40955463454967833
  },
  {
    "keyword": "google cloud platform",
    "raw": "Google Cloud Platform",
    "score": 0.5018536215405839
  },
  {
    "keyword": "cloud",
    "raw": "Cloud",
    "score": 0.5218291888896703
  },
  {
    "keyword": "acquiring data science",
    "raw": "acquiring data science",
    "score": 0.5494143207629893
  },
  {
    "keyword": "san francisco",
    "raw": "San Francisco",
    "score": 0.7636151899513093
  }
]
yake benchmark: 12.124ms
```

# Tests
There are a limited amount of tests in the repo. To test ensure you have `wasm-pack` installed along with your normal Rust based tooling.

To run: `wasm-pack test --node --lib`

