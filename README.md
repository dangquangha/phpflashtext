
# Flashtext for PHP


[![Build Status](https://travis-ci.org/shdev/phpflashtext.svg?branch=master)](https://travis-ci.org/shdev/phpflashtext) [![Coverage Status](https://coveralls.io/repos/github/shdev/phpflashtext/badge.svg?branch=master)](https://coveralls.io/github/shdev/phpflashtext?branch=master)

It's a port from the wonderful python project https://github.com/vi3k6i5/flashtext,
for internals of the algorithm look there. 

This algorithm allows you to extract or replace several keywords at ones.
If you deal with 300 keywords, which have 5 variants each a regex approach is slower than the flashtext approach.
For 1000 keyword with 5 variants each the regex can't be build.

In PHP 5.6 using regex is really slow. In newer verions it performs better. 

## Install

```bash
composer require dangquangha/phpflashtext
```

## Usage

```php
<?php

use Shdev\FlashText\KeywordProcessor;

$keywordProcessor= new KeywordProcessor();

$keywords = [
	'java'               => ['java_2e', 'java programing'],
	'product management' => ['product management techniques', 'product management'],
];

$keywordProcessor->addKeywordsFromAssocArray($keywords);

$sentence = 'I know java_2e and product management techniques';

$keywordsExtracted = $keywordProcessor->extractKeywords($sentence);
// $keywordsExtracted = ['java', 'product management']

$keywordsExtractedWithSpanInfo = $keywordProcessor->extractKeywords($sentence, true);
// $keywordsExtractedWithSpanInfo = [
//	['java', 7, 14],
// 	['product management', 19, 48],
//]


$sentenceNew = $keywordProcessor->replaceKeywords($sentence);
// $sentenceNew = 'I know java and product management';

```

## Citation


The original paper published on [FlashText algorithm](https://arxiv.org/abs/1711.00046).

```tex
    @ARTICLE{2017arXiv171100046S,
       author = {{Singh}, V.},
        title = "{Replace or Retrieve Keywords In Documents at Scale}",
      journal = {ArXiv e-prints},
    archivePrefix = "arXiv",
       eprint = {1711.00046},
     primaryClass = "cs.DS",
     keywords = {Computer Science - Data Structures and Algorithms},
         year = 2017,
        month = oct,
       adsurl = {http://adsabs.harvard.edu/abs/2017arXiv171100046S},
      adsnote = {Provided by the SAO/NASA Astrophysics Data System}
    }

```
The article published on [Medium freeCodeCamp](https://medium.freecodecamp.org/regex-was-taking-5-days-flashtext-does-it-in-15-minutes-55f04411025f).