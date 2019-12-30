# pandoc-html2docx-comments
perl script to convert html comments in markdown files to pandoc/docx syntax, in order to make them visible in docx files created with pandoc

## Requirements

Tested with Perl v5.26.1 (Ubuntu 18.04). It should work also with other versions of Perl. 

## Installation

copy `convert-html2docx-comments` to `/usr/bin` (or other path of your choice) and make it executable. For example:

```bash
sudo cp convert-html2docx-comments /usr/bin
sudo chmod +x /usr/bin/convert-html2docx-comments
```

## Usage

A typical command would be:

```
convert-html2docx-comments mydoc.md | pandoc -o mydoc.docx
```

## Syntax

A markdown file like this:

```markdown
# sample header 1 

sample text <!-- (John Doe) This is my little comment -->

## sample header 2

sample text <!-- (John Smith) This is another useless comment -->

### sample header 3

sample text <!-- Nobody's comment -->
```

is converted like this:

```markdown
# sample header 1

sample text [This is my little comment]{.comment-start author="John Doe" id="1" date="2019-12-0030T18:59:07Z"}[]{.comment-end id="1"}

## sample header 2

sample text [This is another useless comment]{.comment-start author="John Smith" id="2" date="2019-12-0030T18:59:07Z"}[]{.comment-end id="2"}

### sample header 3

sample text [Nobody's comment]{.comment-start author="unknown" id="3" date="2019-12-0030T18:59:07Z"}[]{.comment-end id="3"}
```

If you convert the resulting markdown file to docx with pandoc, you will see your comments in the converted docx file.

Comment date is added automatically. If author is not defined at the beginning between round brackets, it is set to "unknown".

Conversion works even if HTML comments are split in multiple lines.
