# usage

The math equation has some problem, here is my hot patch.


```python
from notion.client import NotionClient

from os import listdir
from os.path import isfile, join
from pathlib import Path
import urllib

from notion.block import PageBlock
from md2notion.upload import convert, uploadBlock, upload
from md2notion.NotionPyRenderer import NotionPyRenderer, addHtmlImgTagExtension, addLatexExtension

from custom.md import convert, CustomNotionPyRenderer

# Obtain the `token_v2` value by inspecting your browser cookies on a logged-in (non-guest) session on Notion.so
client = NotionClient(token_v2="")

client.get_top_level_pages()

page = client.get_block('')


onlyfiles = [join('markdown', f) for f in listdir('markdown') if isfile(join('markdown', f))]


for file in onlyfiles:
    with open(file, "r", encoding="utf-8") as mdFile:
        newPage = page.children.add_new(PageBlock, title=mdFile.name)

        rendered = convert(mdFile,addHtmlImgTagExtension(addLatexExtension(CustomNotionPyRenderer)))
        for blockDescriptor in rendered:
            print(mdFile)
            uploadBlock(blockDescriptor, newPage, mdFile.name)

```