# Lingvanex Translator

[Try it online!](https://lingvanex.com/translate/) | [API](https://lingvanex.com/products/translationapi/) | [Blog](https://lingvanex.com/blog/)

[![Python versions](https://lingvanex.com/download/static-images/python-image.svg)](https://pypi.org/project/lingvanex/)

Free online language translation in 109 languages.
[Try our API!](https://lingvanex.com/products/translationapi/)
After creating an account, you will receive your first 200,000 characters for FREE.

![Translation](https://lingvanex.com/download/static-images/demo-translator.png)

[Try it online!](https://lingvanex.com/translate/) | [API Docs](https://docs.lingvanex.com/reference/overview)

## Free Language Translation Models for CTranslate2

Language translation models that can be used with CTranslate2 for free. These machine translation models are designed and trained to work with the CTranslate2 library, optimized for fast translation on both CPUs and GPUs. The models support the following languages:
- [English-Kurdish](https://models-for-github.s3.eu-central-1.amazonaws.com/en_ku.zip)
- [Kurdish-English](https://models-for-github.s3.eu-central-1.amazonaws.com/ku_en.zip)
- [English-Samoan](https://models-for-github.s3.eu-central-1.amazonaws.com/en_sm.zip)
- [Samoan-English](https://models-for-github.s3.eu-central-1.amazonaws.com/sm_en.zip)
- [English-Xhosa](https://models-for-github.s3.eu-central-1.amazonaws.com/en_xh.zip)
- [Xhosa-English](https://models-for-github.s3.eu-central-1.amazonaws.com/xh_en.zip)
- [English-Lao](https://models-for-github.s3.eu-central-1.amazonaws.com/en_lo.zip)
- [Lao-English](https://models-for-github.s3.eu-central-1.amazonaws.com/lo_en.zip)
- [English-Corsican](https://models-for-github.s3.eu-central-1.amazonaws.com/en_co.zip)
- [Corsican-English](https://models-for-github.s3.eu-central-1.amazonaws.com/co_en.zip)
- [English-Cebuano](https://models-for-github.s3.eu-central-1.amazonaws.com/en_ceb.zip)
- [Cebuano-English](https://models-for-github.s3.eu-central-1.amazonaws.com/ceb_en.zip)
- [English-Galician](https://models-for-github.s3.eu-central-1.amazonaws.com/en_gl.zip)
- [Galician-English](https://models-for-github.s3.eu-central-1.amazonaws.com/gl_en.zip)
- [English-Yiddish](https://models-for-github.s3.eu-central-1.amazonaws.com/en_yi.zip)
- [Yiddish-English](https://models-for-github.s3.eu-central-1.amazonaws.com/yi_en.zip)
- [English-Swahili](https://models-for-github.s3.eu-central-1.amazonaws.com/en_sw.zip)
- [Swahili-English](https://models-for-github.s3.eu-central-1.amazonaws.com/sw_en.zip)
- [English-Yoruba](https://models-for-github.s3.eu-central-1.amazonaws.com/en_yo.zip)
- [Yoruba-English](https://models-for-github.s3.eu-central-1.amazonaws.com/yo_en.zip)

The models are available for download and you can use them in your projects.
You can easily run them in your Python environment as shown below.
### Requirements

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


## API Usage Examples

### Simple

Request:

```javascript
const url = 'https://api-b2b.backenster.com/b1/api/v3/translate';
const options = {
  method: 'POST',
  headers: {
    accept: 'application/json',
    'content-type': 'application/json',
    Authorization: 'API Key'
  },
  body: JSON.stringify({
      platform: 'api',
      from: 'en', 
      to: 'es',
      data: 'Hello'
    })
};

fetch(url, options)
  .then(res => res.json())
  .then(json => console.log(json))
  .catch(err => console.error(err));
```

Response:

```javascript
{
  "err": null,
  "result": "Hola"
}
```

List of language codes: https://docs.lingvanex.com/reference/user-guide

### Auto Detect Language

Request:

```javascript
const url = 'https://api-b2b.backenster.com/b1/api/v3/translate';
const options = {
  method: 'POST',
  headers: {
    accept: 'application/json',
    'content-type': 'application/json',
    Authorization: 'API Key'
  },
  body: JSON.stringify({
      platform: 'api',
      to: 'en',
      data: 'Auf Wiedersehen'
    })
};

fetch(url, options)
  .then(res => res.json())
  .then(json => console.log(json))
  .catch(err => console.error(err));
```

Response:

```javascript
{
  "err": null,
  "result": "Goodbye",
  "from": "de"
}
```

### HTML

Request:

```javascript
const url = 'https://api-b2b.backenster.com/b1/api/v3/translate';
const options = {
  method: 'POST',
  headers: {
    accept: 'application/json',
    'content-type': 'application/json',
    Authorization: 'API Key'
  },
  body: JSON.stringify({
      platform: 'api',
      translateMode: 'html',
      from: 'en', 
      to: 'en',
      data: '<h1>Welcome to the test page</h1>'
    })
};

fetch(url, options)
  .then(res => res.json())
  .then(json => console.log(json))
  .catch(err => console.error(err));
```

Response:

```javascript
{
  "err": null,
  "result": "<h1>Bienvenido a la página de prueba</h1>"
}
```

### Transliteration

Request:

```javascript
const url = 'https://api-b2b.backenster.com/b1/api/v3/translate';
const options = {
  method: 'POST',
  headers: {
    accept: 'application/json',
    'content-type': 'application/json',
    Authorization: 'API Key'
  },
  body: JSON.stringify({
      platform: 'api',
      from: 'en', 
      to: 'zh-Hans_CN',
      data: 'Hello',
      enableTransliteration: true
    })
};

fetch(url, options)
  .then(res => res.json())
  .then(json => console.log(json))
  .catch(err => console.error(err));
```

Response:

```javascript
{
  "err": null,
  "result": "你好",
  "sourceTransliteration": "Hello",
  "targetTransliteration": "Ni Hao"
}
```

## Usage examples in different languages
You can use the Lingvanex API using the following different languages:

- JavaScript: https://github.com/lingvanex-mt/js-translation-api
- PHP: https://github.com/lingvanex-mt/php-api-translator
- Swift: https://github.com/lingvanex-mt/swift-api-translator
- Python: https://github.com/lingvanex-mt/python-translation-api
- C#: https://github.com/lingvanex-mt/csharp-translation-api
- GO: https://github.com/lingvanex-mt/lingvanex-mt-go-pkg
- R: https://github.com/lingvanex-mt/lingvanex-r-pkg


## Desktop Apps
- [Lingvanex Translator](https://lingvanex.com/products/translator-for-pc/) is an Android and iOS apps [available on the Microsoft Store](https://apps.microsoft.com/detail/9pgwf6lbx4s4?hl=en-il&gl=IL) and [available on the App Store](https://apps.apple.com/us/app/lingvanex-offline-translator/id1254982908?mt=12) that uses the Lingvanex API.

## Mobile Apps

- [Lingvanex Translator](https://lingvanex.com/products/mobile-translator/) is an Android and iOS apps [available on the Play Store](https://play.google.com/store/apps/details?id=com.nordicwise.translator) and [available on the App Store](https://apps.apple.com/us/app/lingvanex-language-translator/id1254981151) that uses the Lingvanex API.
- [Phone Call Translator](https://lingvanex.com/products/phone-call-translator/) is an Android and iOS apps [available on the Play Store](https://play.google.com/store/apps/details?id=com.nordicwise.translator_call) and [available on the App Store](https://apps.apple.com/us/app/phone-call-translator-ip/id1367461351) that uses the Lingvanex API.

## Web browser

- [Translator for Browser](https://lingvanex.com/products/all-extensions/) is a web extension with integrated Lingvanex support.

## Bot

- [Translator for Slack](https://lingvanex.com/products/slack/) is a bot for Slack with integrated Lingvanex support.

## License

This project is licensed under the MIT License.

## Contact

If you have any questions, just email info@lingvanex.com
