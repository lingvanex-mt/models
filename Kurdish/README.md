
# Kurdish to English Translation

This repository provides pre-trained multilingual translation models designed for fast and accurate translations between various languages, such as Kurdish, Samoan, Xhosa, Lao, Corsican, Cebuano, Galician, Yiddish, Swahili, Belarusian and Yoruba. These models can be used to translate texts from these languages into English and vice versa, making them suitable for machine translation tasks, language localization projects, and building custom translation tools.

## Key Features:

- Kurdish to English Translation
- English to Kurdish Translation
- Support for multiple languages (see full list below)
- Pre-trained and optimized for accuracy
- Easy integration into existing translation workflows

## Other Languages:

- Kurdish
- Samoan
- Xhosa
- Lao
- Corsican
- Cebuano
- Galician
- Yiddish
- Swahili
- Yoruba
- Belarusian

## Use Cases:

- Machine translation of texts from underrepresented languages
- Localization of websites, apps, or documents into multiple languages
- Developing multilingual NLP tools for research and production environments

## Download Models
- [English-Kurdish](https://models-for-github.s3.eu-central-1.amazonaws.com/en_ku.zip)
- [Kurdish-English](https://models-for-github.s3.eu-central-1.amazonaws.com/ku_en.zip)

## Requirements:

To run the models, you need to install ctranslate2 and sentencepiece:

```bash
pip install ctranslate2 sentencepiece
```

### Simple Usage Example
The following code demonstrates how to load and use a model for translation from English to Kurdish (en → ku).
```python
import sentencepiece as spm
from ctranslate2 import Translator

path_to_model = <here_is_your_path_to_the_model>
source = 'en'
target = 'ku'

translator = Translator(path_to_model, compute_type='int8')
source_tokenizer = spm.SentencePieceProcessor(f'{path_to_model}/{source}.spm.model')
target_tokenizer = spm.SentencePieceProcessor(f'{path_to_model}/{target}.spm.model')

text = [
  'I need to make a phone call.',
  'Can I help you prepare food?',
  'We want to go for a walk.'
]

input_tokens = source_tokenizer.EncodeAsPieces(text)
translator_output = translator.translate_batch(
  input_tokens,
  batch_type='tokens',
  beam_size=2,
  max_input_length=0,
  max_decoding_length=256
)

output_tokens = [item.hypotheses[0] for item in translator_output]
translation = target_tokenizer.DecodePieces(output_tokens)
print('\n'.join(translation))
```

### Keywords:

[Kurdish to English Translation](https://lingvanex.com/translation/kurdish-kurmanji-english), [Samoan to English Translation](https://lingvanex.com/translation/samoan-english), [Xhosa Translation](https://lingvanex.com/translation/english-to-xhosa), [Lao to English](https://lingvanex.com/translation/lao-english), [Corsican Translation](https://lingvanex.com/translation/english-to-corsican), [Cebuano Translation](https://lingvanex.com/translation/english-to-cebuano), [Galician to English Translation](https://lingvanex.com/translation/english-to-galician), [Yiddish to English Translation](https://lingvanex.com/translation/yiddish-english), [Swahili Translation](https://lingvanex.com/translation/english-to-swahili), [Yoruba to English Translation](https://lingvanex.com/translation/english-to-yoruba), [Multilingual Machine Translation](https://lingvanex.com/en/machine-translation/), [NLP](https://lingvanex.com/en/services/nlp-translation-api/), [Neural Networks](https://lingvanex.com/en/neural-network-translation/), [eLearning](https://lingvanex.com/en/education-elearning/)

### License

This project is licensed under the MIT License.

### Contact:

If you have any questions, just email info@lingvanex.com
