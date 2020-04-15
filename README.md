# issues
1. macOS Catalina, linecache.py
```python
#linecache.py
def getlines(filename, module_globals=None):
    """Get the lines for a Python source file from the cache.
    Update the cache if it doesn't contain an entry for this file already."""

    if filename in cache:
        entry = cache[filename]
        if len(entry) != 1:
            return cache[filename][2]

    try:
        if module_globals is None:
            #변경부분
            v = sys.modules.copy()
            for mod in v:
            #변경종료
                if getattr(mod, '__file__', None) == filename:
                    module_globals = mod.__dict__
                    break
        return updatecache(filename, module_globals)
    except MemoryError:
        clearcache()
        return []

```
2. cv2 has no member
- command+shift+p -> open settings (settings.json)
```
{
    "python.linting.pylintArgs": ["--generate-members"]
}
```

# BeautyGAN

See [test.ipynb](test.ipynb), includes:
- Face detection from random images
- Facial landmarks detection
- Face alignment
- Inference

![](imgs/result.png)

### Introduction

BeautyGAN: Instance-level Facial Makeup Transfer with Deep Generative Adversarial Network

Website: [http://liusi-group.com/projects/BeautyGAN](http://liusi-group.com/projects/BeautyGAN)

Essays and datasets are provided, but no open source code and no trained models are provided.

### Result

![](result.jpg)

### Usage

- Python3.6
- TensorFlow 1.9

Download pretrained model

- [https://pan.baidu.com/s/1wngvgT0qzcKJ5LfLMO7m8A](https://pan.baidu.com/s/1wngvgT0qzcKJ5LfLMO7m8A)，7lip
- [https://drive.google.com/drive/folders/1pgVqnF2-rnOxcUQ3SO4JwHUFTdiSe5t9](https://drive.google.com/drive/folders/1pgVqnF2-rnOxcUQ3SO4JwHUFTdiSe5t9)

Save pretrained model to `models`

`imgs` contains 11 non-makeup, 9 makeup images

`imgs/no_makeup/xfsy_0068.png` default non-makeup source image

```
python main.py
```

If you need to put makeup on someone else's face image, pass through the image path. Use a proper size face images.

```
python main.py --no_makeup xxx.xxx
```
