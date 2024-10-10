# Quarto multi language book

I needed to create a multi language book website.

I have used information from following posts to create my own solution.


- [Quarto issues: Multilingual websites / books #275](https://github.com/quarto-dev/quarto-cli/issues/275)

- [A multi-language (German/ English) Quarto website](https://quarto-dev.marioangst.com/en/blog/posts/multi-language-quarto/)

- [Multi-language Blog with Quarto - Guide](https://oooo12.ooo/blog/multilanguage-blog-with-quarto/)

I have used [quarto project profiles](https://quarto.org/docs/projects/profiles.html) and navigation bar for this purpose.

I have three profiles

- def (for default)
- tr (Turkish language version)
- en (English language version)

def profile is only used for main index.html page and redirection to English and Turkish main pages.
You can see the important parts of the quarto.yml below.
I removed unimportant parts in the below


```yml
project:
  type: book
  output-dir: ./_site

book:
  chapters:
      - index.qmd
```


