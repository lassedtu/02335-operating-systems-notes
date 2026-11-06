# Task: Convert Lecture Notes into Atomic Obsidian Notes

Go through every lecture note in `/lectures` and convert the material into a well-structured collection of atomic notes in `/atomic`.

The goal is to transform the existing lecture material into a connected knowledge base where each note covers one clearly defined concept and can be understood independently.

## 1. Source Material

- `/lectures` contains the original lecture notes.
- `/atomic` is the destination for the atomic notes.
- Treat `/lectures` as the source of truth.
- Go through every lecture note and make sure no concepts, definitions, explanations, or relevant details are lost.
- Do not modify the original lecture notes.

## 2. Creating Atomic Notes

Break the lecture material into individual notes, with each note covering one specific concept.

A note should be atomic in the sense that it focuses on one subject, but it should still contain enough context to be understood independently.

For example, a lecture covering processes might be divided into notes such as:

- `Processes.md`
- `Process Creation.md`
- `Process Identifiers.md`
- `Fork System Call.md`
- `Exec System Call.md`
- `Process States.md`
- `Zombie Processes.md`
- `Orphan Processes.md`
- `Process Synchronisation.md`
- `Shared Memory.md`

These are examples of the desired granularity, not a fixed list of required notes.

Avoid both extremes:
- Do not create one enormous note containing multiple unrelated concepts.
- Do not split every individual sentence or trivial detail into its own note.

Each note should have a clear, well-defined subject.

## 3. Preserving and Expanding Content

This is particularly important.

**The primary source of content must always be the existing lecture notes.**

When creating atomic notes:

- Reuse the existing text from the lecture notes.
- You may restructure paragraphs, move explanations around, and rewrite sentences to make them fit the atomic note.
- Preserve all technical details, definitions, terminology, and important distinctions.
- Do not unnecessarily summarise or shorten the original material.
- Add examples, code snippets, explanations, and practical applications where they improve understanding.
- Additional explanations should clarify the existing material rather than introduce unrelated topics.
- Do not invent technical claims or present uncertain information as fact.
- Correct obvious technical inaccuracies where necessary, but make sure corrections are factually sound.

The objective is to make the notes more useful for learning and revision without losing the depth of the original lecture material.

## 4. Note Structure and Formatting

Use consistent Markdown formatting compatible with Obsidian.

Follow this general structure:

```markdown
# Concept Name

A concise introduction explaining what the concept is and why it is relevant.

## How It Works

Detailed explanations of the concept and its underlying mechanisms.

## Examples

Practical examples, preferably including code where relevant.

## Related Concepts

Only include this section if it adds actual explanatory value. Prefer inline links throughout the note instead.
```

The structure is a guideline, not a mandatory template. Use headings that naturally fit the subject.

Formatting preferences:

- Use `#` for the note title.
- Use `##` for major sections and `###` for subsections.
- Use fenced code blocks with the appropriate language identifier.
- Use Markdown tables when comparing structured information.
- Use LaTeX for mathematical expressions, with `$$` for display equations.
- Keep paragraphs reasonably short and explanations direct.
- Avoid unnecessary introductions, conclusions, and filler.
- Do not use em dashes.
- Maintain a consistent technical writing style across all notes.

## 5. Obsidian Linking

The notes must form a properly interconnected knowledge base.

Use standard Obsidian wikilinks:

```markdown
[[System Calls]]
[[Process Creation]]
[[File Descriptors]]
```

**Links must be integrated naturally into the text.**

For example:

Instead of:

```markdown
A process can create another process using the fork system call.

Also read:
- [[Fork System Call]]
- [[Process Management]]
```

Write:

```markdown
A process can create a child process using the [[Fork System Call]].
```

Another example:

```markdown
The [[Exec System Call]] replaces the current process image with a new executable. Unlike [[Fork System Call]], it does not create a new process.
```

Linking requirements:

- Link relevant concepts whenever they are mentioned in a note.
- Prefer linking the first meaningful occurrence of a concept, but also link later occurrences when they provide useful navigation.
- Link technical terms, system calls, algorithms, data structures, and other concepts that have their own atomic notes.
- Use the exact filename of the destination note inside the wikilink.
- Ensure that every internal link points to an existing note.
- Do not create links to notes that have not been created.
- Avoid excessive linking of ordinary words that do not represent meaningful concepts.
- Do not use separate "Also Read", "Related Notes", or similar lists as a substitute for inline linking.

For example, if a note discusses `fork()`, it should naturally link to notes covering [[Processes]], [[System Calls]], [[Process Identifiers]], [[Exec System Call]], and [[Process States]] where relevant.

The relationships between concepts should be apparent from the actual explanations, not just from a collection of links.

## 6. Atomic Note Independence

Each note should be understandable on its own, without requiring the reader to have just read the original lecture or another atomic note.

- Introduce the concept before discussing its details.
- Define technical terminology when necessary.
- Include enough context to explain why the concept matters.
- Use inline links to provide access to deeper explanations.
- Avoid relying on phrases such as "as explained in the previous note".
- Avoid duplicating entire explanations from other notes. Brief contextual explanations are fine.

## 7. Organisation and File Management

- Place all atomic notes in `/atomic`.
- Use descriptive, consistent filenames.
- Do not create unnecessary nested folders unless there is a clear organisational benefit.
- Do not overwrite existing atomic notes blindly.
- If a relevant atomic note already exists, update and expand it instead of creating a duplicate.
- Reuse existing filenames and links wherever possible.
- Ensure there are no duplicate notes covering the same concept.

## 8. Quality Assurance

After processing all lecture notes, perform a final review.

Check that:

1. Every lecture note has been processed.
2. All meaningful concepts from the original lectures are represented.
3. No important technical details or explanations have been lost.
4. Each atomic note focuses on a clearly defined concept.
5. Examples and explanations are sufficient to understand the material.
6. All Obsidian links point to existing notes.
7. Concepts are linked naturally throughout the text.
8. There are no unnecessary duplicate notes.
9. Formatting and terminology are consistent across the entire knowledge base.
10. The original `/lectures` directory remains unchanged.

Do not stop after processing the first lecture. Process the entire directory.

## 9. Execution Strategy

Work systematically:

1. Inspect the entire `/lectures` directory.
2. Identify the concepts covered across all lectures.
3. Build an overview of the atomic notes that need to exist.
4. Identify overlapping concepts between lectures to avoid duplication.
5. Create or update the atomic notes in `/atomic`.
6. Add and verify inline Obsidian links between notes.
7. Perform the final quality assurance review.

Do not merely generate a plan and present it to me. Execute the task and make the actual changes to the files.

The final result should be a comprehensive, interconnected Obsidian knowledge base derived from the lecture material, rather than a collection of shortened lecture summaries.