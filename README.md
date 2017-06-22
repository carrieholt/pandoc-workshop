# Pandoc / R Markdown

See the example `.md` and `.Rmd` files.

Place any references you cite in the `.bib` files. These files are in BibTeX format. Follow the existing format when adding new references. Most reference managers and journal websites will export BibTeX formatted references.

Below are some detailed instructions on writing in Markdown. For the most part, just follow the format you already see in the document.

# A quick primer on our Git workflow

There are many collaboration models for working with Git. I suggest we work with as simple a model as possible, which I will describe here.

Once, you've set up Git and GitHub, you can clone (get a copy of) this repository with:

```
git clone URL-HERE
```

Once you've done this one, you don't have to do it again.

From now on, *before you start working*, switch into the repository folder and run:

```
git pull
```

This pulls down any changes that others have made to the files.

Now edit the files.

When you've done some small unit of work, run:

```
git add ms.md
```

This "stages" your work for committing.

Then run:

```
git commit -m "My changes"
```

Your commit message should be short (50 characters or less), start with a capital, and summarize what you did. You can also add a [more detailed commit message](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html). To do that, run:

```
git commit
```

And fill in the longer description.

Now your work is committed locally, but it's not on the server yet. To push it to the server, run:

```
git push
```

You can verify that your changes were pushed to the server by looking at this repository on GitHub.

Now repeat the process as necessary.

# Writing in Pandoc Markdown

[Markdown][] is an easy-to-read and easy-to-write syntax for writing in plain text format. 
It can be easily converted to a variety of output formats (e.g. `.docx`, `.rtf`, `.tex`, `.html`, `.pdf`). For that reason it's often referred to as a swiss army knife for writing.

[Pandoc][] is a more fully-featured version of Markdown and it likely fits our needs the best. It adds features like citations, math, and tables, which are standard in scientific papers.

If you browse the source for this page, you'll see that it's also written in Markdown.

## Benefits to using Markdown

There are many benefits to working in Markdown. For example:

1. You can use a non-proprietary plain text format.
2. The syntax is minimal compared to something like LaTeX. The syntax is designed to be easy to write and easy to read.
3. A Markdown file can be easily turned into a variety of formats such as `.docx`, `.rtf`, `.tex`, `.html`, `.pdf` all via a one line command.
4. Git: Because the file is plain text, it works well with version control systems like Git, which makes collaboration easier. 
Git also means we can use GitHub, which has some great tools for collaboration like the Issues page.
By using Git, multiple people can edit the same file at the same time and the changes can be merged after.
If there are merging conflicts, Git provides easy ways to resolve the conflict.
Also, by using Git we have an annotated history of all changes to our documents and who contributed what.

## Some examples of papers written with Markdown and GitHub

<https://github.com/NCEAS/pfx-commercial/blob/master/portfolio/text/ms.Rmd>
<https://github.com/datalimited/ensembles/blob/3a3d3e1cee248631b5477ebac0a8cb6b4b58fddd/text/ms.Rmd>
<https://github.com/seananderson/metafolio/blob/master/inst/ms/ms.md>
<https://github.com/NCEAS/pfx-commercial-salmon/tree/2ec7f67589a1d739a6f84157b9ef38ff8b5eb005/paper>
<https://github.com/ss3sim/ss3sim/blob/master/inst/ms/ss3sim-ms.md> (rendered PDF is [here](http://arxiv.org/abs/1312.6450))  
<https://github.com/karthikram/smb_git>  
<https://github.com/cboettig/ews-review>  
<https://github.com/weecology/data-sharing-paper>

## Markdown editors

Because Markdown is plain text, you can use any text editor you'd like to edit it. 
Most major editors also have Markdown packages available.
If you're looking for a zen-like Markdown-specific editor on a Mac, [Byword][], [MultiMarkdown Composer][], and [iA Writer][] are all great.
RStudio will work in a pinch.
You can also edit directly on GitHub if you don't want to set up Git on your computer.
I usually use Vim with the [Pandoc extension][vim-pandoc].
Another great Mac application is [Marked.app][], which auto-generates a preview of your document as you work, regardless of what you're using to edit and write text. 
It's pretty slick.

## Section headers

    # This is a heading
    ## This is a sub-heading
    ### This is a sub-sub-heading

The following also does the same thing, but for consistency, let's stick with the above.

    This is a heading
    =================

    This is a subheading
    --------------------

## Bold and italic

    *some words in italics*
    **some words in bold**

## Citations

    @smith2008 Translates to: Smith et al. (2008) ...
    [@smith2008] Translates to: (Smith et al. 2008) ...
    [@smith2008; @doe1999] Combines multiple citations in brackets
    [e.g. @smith2008] Translates to (e.g. Smith et al. 2008)

If you run into something more complicated, then [see these examples][pandoc-citations].

You also need to keep your references in some standard format. 
I suggest we use BibTeX.

Then on the last line of the paper you add

    # References

And when you build the document you point to your bibliography and `.csl` file. 
CSL stands for citation style language. 
It specifies the layout of the citations and references. 
For example, to create a PDF that's been passed through LaTeX:

    pandoc --bibliography=my-bib.bib --csl=icesjms.csl my-paper.md -o my-paper.pdf

Or to create a Word document:

    pandoc --bibliography=my-bib.bib --csl=icesjms.csl my-paper.md -o my-paper.docx

## Line breaks to make collaborating through Git easier

Markdown can accept hard-wrapped text (text where a hard return splits the lines at some character width).

For example, it will turn this:

    This is a hard-wrapped
    sentence. I have wrapped
    the lines myself.

into this:

    This is a hard-wrapped sentence. I have wrapped the lines myself.

when it's formatted.

There are different conventions on wrapping, but to work best with collaboration through Git, I suggest we hard wrap at sentences. 
For example:

    This is one sentence.
    This is another sentence.

This works well because version control systems like Git are inherently line-based. 
If we didn't use any hard wrapping then a single word change in a paragraph would cause the whole paragraph to be updated. 
This can create problems if multiple people edit the same paragraph and then commit. 
It can also make it hard to see what's changed. 
If we hard-wrapped everything at some character-width the editing one word could re-flow the whole paragraph and create many changes in Git.

## Math

You can embed LaTeX math directly. 
How it gets translated [depends on your output format][pandoc-math]. 
Everything should work if your output is PDF through LaTeX. 
If your output is, say a Word document, then some more complicated math may not translate well. 
You (we) can always get around that by translating to LaTeX first and then using something like `latex2rtf` to generate a Word document with math embedded as images.

[Markdown]: http://daringfireball.net/projects/markdown/
[Pandoc]: http://johnmacfarlane.net/pandoc/
[MultiMarkdown Composer]: http://multimarkdown.com/
[iA Writer]: http://www.iawriter.com/mac/
[Byword]: http://bywordapp.com/
[vim-pandoc]: https://github.com/vim-pandoc/vim-pandoc
[Marked.app]: http://markedapp.com/
[pandoc-citations]: http://johnmacfarlane.net/pandoc/README.html#citations
[pandoc-math]: http://johnmacfarlane.net/pandoc/README.html#math

