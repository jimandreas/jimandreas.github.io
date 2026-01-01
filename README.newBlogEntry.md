# How to Add a New Blog Entry

## Quick Start

1. Create a new `.md` file in the appropriate content folder
2. Add front matter at the top
3. Write your content in Markdown
4. Commit and push to deploy

## Step-by-Step

### 1. Choose the Right Folder

Place your new post in one of these folders based on the topic:

| Topic | Folder |
|-------|--------|
| OpenGL/Graphics | `content/opengl/` |
| Molecular Biology | `content/molbio/` |
| Android/Kotlin | `content/android-kotlin/` |

### 2. Create the File

Name your file using this format:
```
YYYY-MM-DD-short-title.md
```

Example: `2026-01-15-new-opengl-tutorial.md`

### 3. Add Front Matter

Every post starts with front matter between `---` markers:

```yaml
---
title: "Your Post Title"
date: 2026-01-15
draft: false
categories:
  - OpenGL
tags:
  - android
  - graphics
twitterImage: "/images/your-image.jpg"
---
```

#### Front Matter Fields

| Field | Required | Description |
|-------|----------|-------------|
| `title` | Yes | The post title displayed on the page |
| `date` | Yes | Publication date (YYYY-MM-DD) |
| `draft` | Yes | Set to `false` to publish, `true` to hide |
| `categories` | No | Main category (OpenGL, Molecular Biology, etc.) |
| `tags` | No | List of tags for the post |
| `twitterImage` | No | Image for Twitter/social cards |
| `toc` | No | Set to `true` to show table of contents |

### 4. Write Your Content

After the front matter, write your post using Markdown:

```markdown
---
title: "Learning Shaders on Android"
date: 2026-01-15
draft: false
categories:
  - OpenGL
tags:
  - shaders
  - android
---

## Introduction

Your introduction paragraph here.

## Main Section

More content with **bold** and *italic* text.

### Subsection

- Bullet point 1
- Bullet point 2

## Code Examples

```kotlin
fun main() {
    println("Hello, World!")
}
```

## Links and Images

[Link text](https://example.com)

![Alt text](/images/your-image.jpg)

## References

- Reference 1
- Reference 2
```

### 5. Add Images (Optional)

1. Place images in `static/images/`
2. Reference them in your post as `/images/filename.jpg`

### 6. Preview Locally

Run the Hugo development server:

```bash
cd C:\a\j\html\jimandreas.github.io
hugo server
```

View your site at `http://localhost:1313/`

### 7. Publish

Commit and push to deploy:

```bash
git add .
git commit -m "Add new blog post: Your Title"
git push
```

GitHub Actions will automatically build and deploy the site.

## Markdown Cheat Sheet

| Element | Syntax |
|---------|--------|
| Heading | `## Heading 2`, `### Heading 3` |
| Bold | `**bold text**` |
| Italic | `*italic text*` |
| Link | `[text](url)` |
| Image | `![alt](/images/file.jpg)` |
| Code | `` `inline code` `` |
| Code block | ` ```language ... ``` ` |
| List | `- item` or `1. item` |
| Blockquote | `> quoted text` |

## Example Complete Post

```markdown
---
title: "Understanding Vertex Buffers in OpenGL ES"
date: 2026-01-15
draft: false
categories:
  - OpenGL
tags:
  - android
  - graphics
  - vertex-buffers
twitterImage: "/images/opengl-vertex-buffers.jpg"
---

## Introduction

Vertex buffers are essential for efficient rendering in OpenGL ES...

## Creating a Vertex Buffer

```kotlin
val buffer = FloatBuffer.allocate(vertices.size)
buffer.put(vertices)
buffer.position(0)
```

## Binding and Drawing

Once created, bind the buffer before drawing...

## Conclusion

Vertex buffers improve performance by...

## References

- [LearnOpenGL - Vertex Buffers](https://learnopengl.com/)
- [Android OpenGL ES Guide](https://developer.android.com/guide/topics/graphics/opengl)
```
