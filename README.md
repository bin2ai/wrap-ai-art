# Pycurtain

A community-maintained python package for wrapping REST APIs that interface with a variety of different AI models.  Think "curtain", like wizard of oz behind the curtain. This tool lets the developer close the curtains and only focus on implementing one code base for any supported AI models.

![](pycurtain.png?raw=true)

# Install

```bash
pip install pycurtain
```

# Usage

There are tasks (image-related) and sources (AI art models) that are supported.  The following is an example of how to use the package to generate an image from a model source.

```python
import pycurtain

source = pycurtain.source.SourceType.STABLE_DIFFUSION
prompt = "A blooming flower in the middle of a desert"
img_o = pycurtain.task.image.generate(source, prompt)[0]
img_o.save('output.png')
```

## Supported Tasks

image

- [x] generate (text2img, creation)
- [x] vary (img2img, style transfer)
- [x] edit (img2img, with masks)
- [x] interrogate (img2text, description)

text

- [x] summarize (tl;dr)
- [x] fix_grammar (punctuation, spelling, capitalization, etc.)
- [x] tag (subject matter, genres, subgenres, etc.)

## Supported Processes

A process is a way to combine multiple tasks together.  For example, you can convert a sequence of images into a video.

- [x] text_to_video_zoom (zoom_in and_out)

<img src="text-to-video-zoom.gif" width="256" height="256"/>

```python
from pycurtain.process import text_to_video_zoom
from pycurtain.source import SourceImageType
text_to_video_zoom.zoom_in(prompts=["A grateful dead poster"], source=SourceImageType.STABLE_DIFFUSION, n_imgs=10, file_name="output.mp4")
```

# AI Model Sources

Currently all but one supported AI Models require an API key generated from the REST API host (Craiyon being the exception). Pycurtain is a third-party (open-source / community driven) python wrapper SDK and is not associated with any of the AI Model providers.  Each API key can be generated by signing up from the AI Model hosting site. The current implementation requires each (in-use) API key to be set in the environment variables following the [\secrets\stuff.py](https://github.com/bin2ai/pycurtain/blob/main/src/pycurtain/secrete/stuff.py) format.  

No API Key or private information is stored by Pycurtain.

## Sources Offical Sites

- [x] DeepAi SRGAN <https://deepai.org/>
- [x] StabilityAi Stable Diffusion <https://stability.ai/>
- [x] OpenAi Dalle2, GPT3 <https://openai.com/>
- [x] Craiyon (Formally DALL-E Mini) <https://www.craiyon.com/>
- [x] Replicate <https://replicate.com/>

# Road Map

- provide prelimiary wrappers for these AI model sources
  - hugging_face <https://huggingface.co/>

- allow users to adjust common parameters between models
- provide utility features beyond the model wrapper
  - equirectangluar images (360 degree images)
  - simple inpainting mask creation
- beyond images... videos, text, audio.  All leveraging the available REST API accessible ML models of today.

# Developing Pycurtain

To install pycurtain, along with the tools you need to develop and run test, run the following in your virtual environment:

```bash
pip install -e .[dev]
```
