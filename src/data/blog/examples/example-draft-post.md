---
title: Example Draft Post - Blog Template Guide
author: atooooomic
pubDatetime: 2024-01-01T00:00:00Z
modDatetime: 2024-01-02T00:00:00Z
slug: example-draft-post
featured: false
draft: true
tags:
  - docs
  - guide
  - example
description:
  This is a comprehensive template demonstrating all the patterns and structures
  used in AstroPaper blog posts. Use this as a reference when creating new posts.
timezone: "America/New_York"
# ogImage: ../../assets/images/example.png
# canonicalURL: https://example.org/canonical-url
---

This is a comprehensive template that demonstrates common patterns, structures, and features used in AstroPaper blog posts. You can use this as a reference when creating your own blog posts.

<figure>
  <img
    src="https://images.pexels.com/photos/1181244/pexels-photo-1181244.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1"
    alt="Person writing in a notebook"
  />
  <figcaption class="text-center">
    Photo by <a href="https://www.pexels.com/photo/person-writing-on-notebook-1181244/">Pexels</a>
  </figcaption>
</figure>

## Table of contents

## Introduction

Start your blog post with a brief introduction paragraph. Explain what the post is about and what readers can expect to learn. Keep it concise and engaging - typically 2-3 sentences.

> Tip! You can use blockquotes like this to highlight important tips, notes, or warnings throughout your post.

## Main Section with Headings

Use H2 (`##`) headings for your main sections. Remember, the post title (from frontmatter) serves as the H1, so your content should start with H2 headings.

### Subsection Example

You can use H3 (`###`) for subsections. This helps organize your content hierarchically and improves readability.

#### Deeper Subsection

And H4 (`####`) for even deeper levels if needed. However, try not to go too deep - H2 to H4 is usually sufficient.

## Writing Code Examples

AstroPaper uses Shiki for syntax highlighting. You can specify the language and even the file name.

### Basic Code Block

```js
// Simple JavaScript example
function greet(name) {
  return `Hello, ${name}!`;
}

console.log(greet("World"));
```

### Code Block with File Name

```ts file="src/config.ts"
export const SITE = {
  website: "https://example.com/",
  author: "Your Name",
  desc: "A minimal, responsive and SEO-friendly Astro blog theme.",
  title: "AstroPaper",
  lightAndDarkMode: true,
} as const;
```

### Code with Highlighting

```js file="example.js"
function calculateTotal(items) {
  // [!code highlight:3]
  const total = items.reduce((sum, item) => {
    return sum + item.price * item.quantity;
  }, 0);

  return total;
}
```

### Code with Diff (Additions/Deletions)

```js file="astro.config.ts"
export default defineConfig({
  // [!code --:1]
  site: "https://old-site.com",
  // [!code ++:1]
  site: "https://new-site.com",
  integrations: [react(), tailwind()],
});
```

## Using Tables

Tables are great for organizing structured information like configuration options or feature comparisons.

| Property      | Type      | Description                           | Required |
| ------------- | --------- | ------------------------------------- | -------- |
| `title`       | `string`  | The title of your post                | Yes      |
| `description` | `string`  | Brief description for SEO             | Yes      |
| `pubDatetime` | `string`  | Publication date in ISO 8601 format   | Yes      |
| `featured`    | `boolean` | Show in featured section              | No       |
| `draft`       | `boolean` | Mark as draft (won't be published)    | No       |
| `tags`        | `array`   | Array of tags for categorization      | No       |

## Images and Media

### Using Markdown Image Syntax

You can use simple markdown syntax for images:

![Example image](https://images.pexels.com/photos/577585/pexels-photo-577585.jpeg?auto=compress&cs=tinysrgb&w=800)

### Using Figure with Caption

For better semantic HTML and captions, use the `<figure>` element:

<figure>
  <img
    src="https://images.pexels.com/photos/1181263/pexels-photo-1181263.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1"
    alt="Laptop with code on screen"
  />
  <figcaption class="text-center">
    An example of code on a laptop screen
  </figcaption>
</figure>

### Storing Images

- **Recommended**: Store in `src/assets/images/` for automatic optimization
  ```md
  ![something](@/assets/images/example.jpg)
  ```
- **Alternative**: Store in `public/` directory (unoptimized)
  ```md
  ![something](/assets/images/example.jpg)
  ```

## Lists and Formatting

### Unordered Lists

Here are some key points to remember:

- First important point
- Second important point
- Third important point
  - Nested point A
  - Nested point B
- Fourth important point

### Ordered Lists

Follow these steps:

1. First step in the process
2. Second step with details
3. Third step to complete
4. Final step

### Text Formatting

You can use **bold text** for emphasis, _italic text_ for subtle emphasis, and even `inline code` for technical terms or commands.

You can also use ~~strikethrough~~ for text that's no longer relevant.

## Links and References

You can create [inline links](https://astro.build) or [links with titles](https://astro.build "Astro Official Website").

For internal references, link to other posts: Check out [how to add new posts](/posts/adding-new-posts-in-astropaper-theme).

## Advanced Features

### Details/Summary (Collapsible Content)

<details>
<summary>Click to expand and see more details</summary>

This is hidden content that users can reveal by clicking. Great for optional information, FAQs, or detailed explanations that might clutter the main content.

You can include any markdown here:

- Lists
- **Formatted text**
- Even code blocks!

```js
console.log("Hidden code example");
```

</details>

### Horizontal Rules

You can add horizontal rules to separate sections:

---

Like the one above! They're created with three or more hyphens.

## Best Practices

Here are some recommendations for writing great blog posts:

1. **Keep it focused**: Each post should have a clear topic and purpose
2. **Use headings wisely**: Organize content with H2-H4 headings
3. **Add examples**: Code examples and images make concepts clearer
4. **Optimize for SEO**: Use descriptive titles, meta descriptions, and alt text
5. **Check accessibility**: Use semantic HTML and descriptive link text
6. **Proofread**: Check for typos and formatting issues before publishing

## Common Frontmatter Options

Here's a reference for all available frontmatter options:

```yaml
---
# Required fields
title: Your Post Title
description: Brief description for SEO and post excerpt
pubDatetime: 2024-01-01T00:00:00Z

# Optional but recommended
author: Your Name (defaults to SITE.author)
tags:
  - tag1
  - tag2

# Optional fields
modDatetime: 2024-01-02T00:00:00Z # Only add when post is modified
slug: custom-url-slug # Defaults to filename
featured: false # Show in featured section
draft: false # Mark as unpublished
ogImage: path/to/image.jpg # Social media image
canonicalURL: https://example.org/original # If posted elsewhere first
hideEditPost: false # Hide edit button for this post
timezone: Asia/Seoul # Override global timezone
---
```

## Resources and Further Reading

For more information about specific features:

- [Adding new posts](https://astro-paper.pages.dev/posts/adding-new-posts-in-astropaper-theme/)
- [Customizing color schemes](https://astro-paper.pages.dev/posts/customizing-astropaper-theme-color-schemes/)
- [Dynamic OG images](https://astro-paper.pages.dev/posts/dynamic-og-image-generation-in-astropaper-blog-posts/)
- [AstroPaper documentation](https://astro-paper.pages.dev/)

## Conclusion

This template demonstrates the common patterns and structures used in AstroPaper blog posts. When creating your own posts:

- Start with a clear introduction
- Use proper heading hierarchy (H2-H4)
- Include code examples with syntax highlighting
- Add images with alt text and captions
- Organize content with tables and lists
- End with a conclusion or summary

Remember to set `draft: false` when you're ready to publish your post!

## Project Links (Optional)

If you're writing about a specific project, you can include relevant links:

- Website: [https://example.com](https://example.com)
- GitHub Repository: [https://github.com/username/repo](https://github.com/username/repo)
- Live Demo: [https://demo.example.com](https://demo.example.com)
