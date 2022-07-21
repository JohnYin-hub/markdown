## Hunggingface

### option1 ：configure  指定模型路径

```python
DOWNLOADED_MODEL_PATH = 'model'
MODEL_NAME = 'allenai/longformer-base-4096'

if DOWNLOADED_MODEL_PATH == 'model':
    # os.mkdir('model')
    
    tokenizer = AutoTokenizer.from_pretrained(MODEL_NAME)
    # tokenizer.save_pretrained('model')

    config = AutoConfig.from_pretrained(MODEL_NAME) 
    # config.save_pretrained('model')

    backbone = TFAutoModel.from_pretrained(MODEL_NAME, config=config)
    # backbone.save_pretrained('model')
```

