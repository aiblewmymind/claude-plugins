---
name: use-prompts
description: Guide for using AI Blew My Mind prompts — searching, interviewing, and generating images. Use when the user wants to find or use a prompt from AI Blew My Mind.
user-invocable: true
argument-hint: [search query]
---

# Using AI Blew My Mind Prompts

## Workflow

1. **Search**: Call `search_prompts` with the user's query (or no query to browse all)
2. **Select**: Present the results and let the user pick a prompt
3. **Use**: Call `use_prompt` with the selected prompt ID
4. **Interview**: Follow the returned instructions to fill placeholders one at a time
5. **Execute**: For text prompts, run or copy. For image prompts, call `generate_image`.

## Image Generation with References

When the user wants to include reference images:

- **If the user mentions a file on their computer** (e.g., "use this photo on my desktop"): Ask for the file path and pass it as `image_paths` to `generate_image`.
- **If the user uploaded an image to this conversation**: Save it to a temporary file first, then pass the file path as `image_paths`. This is more reliable than passing base64 directly.
- **If the image is small** (screenshots, icons): You may pass it directly as `image_base64`.

## Authentication

- If `use_prompt` says you need to log in, call the `login` tool first.
- If `generate_image` says quota is exhausted, suggest the user run `set_gemini_key` with their own key from aistudio.google.com.

## Example

User: "Find me an image prompt for making tiny objects"
→ Call search_prompts with query "tiny objects"
→ Present results
→ User picks "Nano Banana Generator"
→ Call use_prompt with that ID
→ Interview: "What object?" → "banana", "What style?" → "photorealistic"
→ Call generate_image with filled prompt
→ Show the generated image
