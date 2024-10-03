
# Language Translation Models for CTranslate2

This repository provides access to multiple language translation models that can be used with CTranslate2. The models support the following languages:

- English-Kurdish (https://models-for-github.s3.eu-central-1.amazonaws.com/en_ku.zip)
- Kurdish-English (https://models-for-github.s3.eu-central-1.amazonaws.com/ku_en.zip)
- English-Samoan (https://models-for-github.s3.eu-central-1.amazonaws.com/en_sm.zip)
- Samoan-English (https://models-for-github.s3.eu-central-1.amazonaws.com/sm_en.zip)
- English-Xhosa (https://models-for-github.s3.eu-central-1.amazonaws.com/en_xh.zip)
- Xhosa-English (https://models-for-github.s3.eu-central-1.amazonaws.com/xh_en.zip)
- English-Lao (https://models-for-github.s3.eu-central-1.amazonaws.com/en_lo.zip)
- Lao-English (https://models-for-github.s3.eu-central-1.amazonaws.com/lo_en.zip)
- English-Corsican (https://models-for-github.s3.eu-central-1.amazonaws.com/en_co.zip)
- Corsican-English (https://models-for-github.s3.eu-central-1.amazonaws.com/co_en.zip)
- English-Cebuano (https://models-for-github.s3.eu-central-1.amazonaws.com/en_ceb.zip)
- Cebuano-English (https://models-for-github.s3.eu-central-1.amazonaws.com/ceb_en.zip)
- English-Galician (https://models-for-github.s3.eu-central-1.amazonaws.com/en_gl.zip)
- Galician-English (https://models-for-github.s3.eu-central-1.amazonaws.com/gl_en.zip)
- English-Yiddish (https://models-for-github.s3.eu-central-1.amazonaws.com/en_yi.zip)
- Yiddish-English (https://models-for-github.s3.eu-central-1.amazonaws.com/yi_en.zip)
- English-Swahili (https://models-for-github.s3.eu-central-1.amazonaws.com/en_sw.zip)
- Swahili-English(https://models-for-github.s3.eu-central-1.amazonaws.com/sw_en.zip)
- English-Yoruba (https://models-for-github.s3.eu-central-1.amazonaws.com/en_yo.zip)
- Yoruba-English (https://models-for-github.s3.eu-central-1.amazonaws.com/yo_en.zip)

Due to space limitations, the models are hosted on AWS. You can easily load and run them in your Python environment as shown below.

## Requirements

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

