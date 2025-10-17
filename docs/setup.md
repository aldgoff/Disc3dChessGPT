# Setup

# Prepare a complete book ready manuscript, like 3D Chess

## Convert to markdown (manuscript.md)
script/tool
pandoc?

## Accurate determination of the token count
Use tiktoken.

```python3 token_counter.py <file>```

## Clean the markdown file
This removes meta data that increases token count but is not part of the 'manuscript.'

```python3 clean_markdown.py <file>```

```python3 compare_tokens.py <file> <file_clean>```

## Create a lesson plan
Select break points to stay below 32k tokens (~25k for a decent margin).

## Divide markdown manuscript into smaller files (lesson1.md, lesson2.md, etc.)
Use any editor.
Best practice, use binary search, divide in half, each half in half, etc.

## Test for vector collision
If there is too much parallelism, gpt ingestion will skip areas it thinks it already ingested.
With the figures manifest, this was easy, test figure ranges.
For more conventional manuscripts, may have to get creative.
GPT can help, ask for it.

## Split any lessons with incomplete ingestion
Typically two files is enough.
Builder instructions will say treat pair as one file.
```
# Mapping
- Manuscript refers to two files:
  - "3DCB_L5a_PK_clean.md"
  - "3DCB_L5b_PK_clean.md"
- Manifest refers to the "figsManifest_L5_C11_12.json" file.
- Lesson plan refers to the "lesson_plan" file.
```

# Create a github repo for the figures (and maybe the descriptions, if lengthy)
- Make it public.
- Create a figures directory (and maybe a descriptions folder).
- Upload the figures.

# Build a complete figures manifest

## A json array is typically sufficient
Each element contains
- id
- filename
- url
- caption
- description

## Clean the manifest file
This removes meta data that increases token count such as Word index markups.

## Accurate determination of the token count
Use tictock?

## Divide json manifest into smaller files (manifest1.md, manifest2.md, etc.)
Use any editor.
Make sure they align with the manuscript (the lesson plan is handy here, make it thorough).

# Create the custom GPTs

## Create each lesson
- Upload a profile image
-- Use the png file in the Knowledge base as the profile picture.
- Upload the lesson manuscript(s)
- Upload the lesson manifest

## Create the syllabus
Update the lesson plan with links to the lesson GPTs.
- Upload a profile image
- Upload the lesson plan

# Debugging

## Create diagonstic prompts
- How many figures in this lesson?
- How many tokens in the current context?

# UI

## General builder instructions
- Use mappings to simplify file references.
- A try next block can be very helpful for textbook like manuscripts.

## Overall feel
- A help prompt
- A limits prompt
- A diagnostics prompt
