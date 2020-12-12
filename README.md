# Kotlin website
[![Official project][project-badge]][project-url] [![Slack][slack-badge]][slack-url] 

This is the source for the [http://kotlinlang.org](http://kotlinlang.org).

- [Installation](#installation)
- [How to run](#how-to-run)
- [Project structure & overview](#project-structure)
- [Writing content](#writing-content)
- [Filing bugs](#filing-bugs)

## Installation

1. You will need Docker to run site lifecycle tasks. Installation for [macOS](https://docs.docker.com/docker-for-mac/install/#download-docker-for-mac) and 
   [Windows](https://docs.docker.com/docker-for-windows/install/#download-docker-for-windows).
2. If you want to develop frontend Yarn package manager is also needed ([installation instructions](https://yarnpkg.com/lang/en/docs/install/)).
   Don't forget to install frontend dependencies - `yarn install`.
3. All specific app parameters stored in env-file. Copy sample file `.env.sample` and rename it to `.env`. 
   Change variables values if needed.

## How to run

- **All in one option (suitable for content authors/writers)**:
  - `docker-compose up`. It will build all stuff and create site on [localhost:5000](http://localhost:5000).
- **Developer has 2-step option**:
  - `docker-compose up website` will run only site at [localhost:5000](http://localhost:5000).
  - `yarn start` will run webpack-dev-server on [localhost:9000](http://localhost:9000).
     This address should be used for development. All pages from origin server will be proxied.
     
<a id="project-structure"></a>
## Project structure & overview

### Data

All data is stored in the \*.yml files in folder `data`:

- [_nav.yml](data/_nav.yml) site navigation and PDF building.
- [releases.yml](data/releases.yml) info about releases.
- [videos.yml](data/videos.yml) data for the Videos page. The `content` property is used to create categories.
  It contains a list of videos or other categories. Maximum tree depth level is 3.
- [events.xml](data/events.xml) event data.

### Templates

Kotlinlang uses [Jinja2](http://jinja.pocoo.org/docs/dev/) templates that can be found in templates folder.
Note that all Markdown files are processed as Jinja templates before being converted to HTML. 
This allows you to use all Jinja power inside Markdown (for example, build urls with url_for function).

### Page metadata

Every page can have an unlimited number of metadata fields. More information [here](http://jekyllrb.com/docs/frontmatter/).
The most important of them are the page template (e.g. `layout: reference`) and its type (e.g. `type: tutorial`). `category` and `title` fields are added for future development.

### Kotlin grammar reference

The Kotlin grammar reference (grammar.xml) is generated by the [Kotlin grammar generator](https://github.com/JetBrains/kotlin-grammar-generator) from the 
[Kotlin grammar definition](https://github.com/JetBrains/kotlin/tree/master/grammar).

## Writing content

### Markup

kramdown with some additions (like GitHub fenced code blocks) is used as Markdown parser.
See the complete syntax reference at the [kramdown site](http://kramdown.gettalong.org/syntax.html).

### Specifying page element attributes

With kramdown you can assign HTML attributes to page elements via `{:%param%}`. E.g.:

- `*important text*{:.important}` - produces `<em class="important">important text</em>`
- `*important text*{:#id}` - produces `<em id="id">important text</em>`

For block elements this instruction must be specified on the line following element definition:

```
This is a paragraph
{:.important}

This is a paragraph
```

More information about attributes can be found [here](http://kramdown.gettalong.org/syntax.html#inline-attribute-lists).

### Custom element styles

#### Inline elements

- `{:.keyword}` highlights a keyword.
- `{:.error}` highlights an error.
- `{:.warning}` highlights a warning.

#### Tables

- `{:.wide}` stretches a table to occupy the entire width of a page.
- `{:.zebra}` interleaves table rows.

E.g.:

```
| Expression | Translated to |
|------------|---------------|
| `a++` | `a.inc()` + see below |
| `a--` | `a.dec()` + see below |
{:.wide.zebra}
```

#### Quotation blocks

They're used in a slightly other manner that they were originally designed for: as universal block container elements.

- `{:.note}` highlights a note block.

E.g.:

```
> **`inc()/dec()` shouldn't mutate the receiver object**.
>
> By "changing the receiver" we mean `the receiver-variable`, not the receiver object.
{:.note}
```

## Filing Bugs
We use [YouTrack](http://youtrack.jetbrains.com/issues/KT) for bug reports and suggestions. 
Click [here to report an issue](http://youtrack.jetbrains.com/newIssue?project=KT&clearDraft=true&c=Subsystems+Web+Site).


[project-url]: https://confluence.jetbrains.com/display/ALL/JetBrains+on+GitHub
[project-badge]: http://jb.gg/badges/official.svg
[slack-url]: http://slack.kotlinlang.org
[slack-badge]: http://slack.kotlinlang.org/badge.svg
#1
