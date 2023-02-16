# StanceSSR
A collection of stance detection datasets based on SemEval2016 Task 6 to assert whether stance detection models understand the task or simply overfit the training data.



## Description of the used data


These data are based on SemEval2016 Shared Task 6 "Stance Detection on Tweets", see the detailed description in this [paper](http://aclweb.org/anthology/S16-1003) and on this [site](https://alt.qcri.org/semeval2016/task6/).

In this following, we describe the data used in the [ssr-paper](https://aclanthology.org/2022.coling-1.596/). The structure of the constructed `SemEval2016_SSR.json` looks like this:
```json
{
    "all_instances":{} 
    
    "data_split_by_target": {
            "Hillary Clinton": {
                "train": list, indices in "all_instances",
                "valid": list, indices in "all_instances",
                "test": list, indices in "all_instances"
            },
            ...
            "mix": mixture of 5 targets used in subtask A
    
    "label_mapping": {
        "word2idx": {}, 
        "idx2word": {},
        ...
        "hasSenti2idx":  
        "targetIn2idx": dict, mapping target_in_tweet, target_not_in_tweet into indices
        }
    
    "hard_sets": {
        "tweet_only": TOF, samples in which 3 tweet_only BERT models failed
        "pmi": PMI, samples containing long-tailed features according to PMI scores
        "opinion_towards": OT, samples whose targets are implicitly or indirectly mentioned
        "dt": DT, 
        "target_mismatch": Replaced, samples whose target is replaced with another target that does not appear in the tweet
        "negate": Negated, samples whose targets are replaced their negated counterpart
    }
} 
```

One sample in `all_instances` looks like this:
```json
{
    "text": "Keep the faith. The most amazing things in life tend to happen right at the moment you're about to give up hope. #SemST", 
    "target": "Atheism", 
    "label": "AGAINST", 
    "opinion_towards": "1.  The tweet explicitly expresses opinion about the target, a part of the target, or an aspect of the target.", 
    "sentiment": "pos", 
    "orig_idx": 400,
    "target_in_tweet": "in_tweet", 
    "has_senti": "pos", 
    "stance_towards_target": "AGAINST",
}
```

And one sample in the hard set `opinion_towards` looks like this:
```json
{
    "text": "@someone Giving birth is not pushing women toward death. #SemST", 
    "target": "Legalization of Abortion", 
    "label": "AGAINST", 
    "opinion_towards": "2. The tweet does NOT expresses opinion about the target but it HAS opinion about something or someone other than the target.", 
    "sentiment": "neg", 
    "orig_idx": 3897, 
    "target_in_tweet": "not_in_tweet", 
    "stance_towards_target": "AGAINST",
}
```
where "orig_idx" refers to the original sample in `all_instances`.


