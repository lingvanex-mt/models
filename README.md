# Lingvanex Translator

[Try it online!](https://lingvanex.com/translate/) | [Translation API](https://lingvanex.com/products/translationapi/) | [Blog](https://lingvanex.com/blog/)

[![Python versions](https://lingvanex.com/download/static-images/python-image.svg)](https://pypi.org/project/lingvanex/)

Free and Open Source Machine Translation Models in 12 languages, entirely self-hosted. Unlike other APIs, it doesn't rely on proprietary providers such as Google or AWS to perform translations. Instead, its translation engine is powered by the open source [CTranslate2](https://github.com/OpenNMT/CTranslate2) library.

![Translation](https://lingvanex.com/download/static-images/demo-translator.png)

[Try it online!](https://lingvanex.com/translate/) | [API Docs](https://docs.lingvanex.com/reference/overview)

## Free Language Translation Models for CTranslate2

The models support the following languages:

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
Also we have translation models for [100 other languages](https://lingvanex.com/products/on-premise-machine-translation/). Contact us info@lingvanex.com
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

## Usage Examples in Different Languages
You can use the Lingvanex API using the following different languages:

- JavaScript: https://github.com/lingvanex-mt/js-translation-api
- PHP: https://github.com/lingvanex-mt/php-api-translator
- Swift: https://github.com/lingvanex-mt/swift-api-translator
- Python: https://github.com/lingvanex-mt/python-translation-api
- C#: https://github.com/lingvanex-mt/csharp-translation-api
- GO: https://github.com/lingvanex-mt/lingvanex-mt-go-pkg
- R: https://github.com/lingvanex-mt/lingvanex-r-pkg


## Desktop Apps

- [Translator for MacOS](https://lingvanex.com/products/macos-translator/) that uses the Lingvanex API.
- [Translator for Windows](https://lingvanex.com/products/windows-translator/) that uses the Lingvanex API.

## Mobile Apps

- [Lingvanex Translator](https://lingvanex.com/products/mobile-translator/) is an Android and iOS apps [available on the Play Store](https://play.google.com/store/apps/details?id=com.nordicwise.translator) and [available on the App Store](https://apps.apple.com/us/app/lingvanex-language-translator/id1254981151) that uses the Lingvanex API.
- [Phone Call Translator](https://lingvanex.com/products/phone-call-translator/) is an Android and iOS apps [available on the Play Store](https://play.google.com/store/apps/details?id=com.nordicwise.translator_call) and [available on the App Store](https://apps.apple.com/us/app/phone-call-translator-ip/id1367461351) that uses the Lingvanex API.

## Web Browser

- [Translator for Browser](https://lingvanex.com/products/all-extensions/) is a web extension with integrated Lingvanex support.

## Translator bot for Slack

- [Translator for Slack](https://mickey-hod7786.slack.com/marketplace/A8KHN4EDV-translator-translate-languages) is a bot for Slack with integrated Lingvanex support.

## License

This project is licensed under the MIT License.

## Contact

If you have any questions, just email info@lingvanex.com
