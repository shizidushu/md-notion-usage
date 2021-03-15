# usage

The math equation has some problem, here is my hot patch.

Thanks to notion-py and md2notion
- https://github.com/jamalex/notion-py
- https://github.com/Cobertos/md2notion

```python
from os import listdir
from os.path import isfile, join

from notion.client import NotionClient
from notion.block import PageBlock
from md2notion.upload import uploadBlock
from md2notion.upload import convert
from md2notion.NotionPyRenderer import addHtmlImgTagExtension, addLatexExtension

from custom.md import convert, CustomNotionPyRenderer

# Obtain the `token_v2` value by inspecting your browser cookies on a logged-in (non-guest) session on Notion.so
client = NotionClient(token_v2="")

client.get_top_level_pages()

page = client.get_block('')

folder_name = 'markdown'

onlyfiles = [join(folder_name, f) for f in listdir(folder_name) if isfile(join(folder_name, f))]


for file in onlyfiles:
    with open(file, "r", encoding="utf-8") as mdFile:
        newPage = page.children.add_new(PageBlock, title=mdFile.name)

        rendered = convert(mdFile, addHtmlImgTagExtension(addLatexExtension(CustomNotionPyRenderer)))
        for blockDescriptor in rendered:
            print(blockDescriptor)
            uploadBlock(blockDescriptor, newPage, mdFile.name)
```