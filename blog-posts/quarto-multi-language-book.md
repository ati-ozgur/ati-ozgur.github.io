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
I removed unimportant parts in the below quarto.yml file.
You could see original file [here](https://github.com/ati-ozgur/course-database/blob/main/_quarto.yml).
below [Index.qmd](https://github.com/ati-ozgur/course-database/blob/main/index.qmd) file contains two links for going to English or Turkish versions.


```yml
project:
  type: book
  output-dir: ./_site

book:
  chapters:
      - index.qmd
```



In the other two profiles, we render in two different directories using **output-dir** property.
Then using **navbar**, we could switch between the sites.

[quarto-tr.yml](https://github.com/ati-ozgur/course-database/blob/main/_quarto-tr.yml
)

```yml
project:
  output-dir: ./_site/tr
book:
  title: "Veritabanlarına Giriş"
  navbar:
    background: primary
    search: true
    right:
      - text: "English"
        href: ../en/index.html
      - text: "Türkçe"
        href: ../tr/index.html
```      

[quarto-en.yml](https://github.com/ati-ozgur/course-database/blob/main/_quarto-en.yml
)
```yml
project:
  output-dir: ./_site/en

book:
  title: "Introduction to databases"
  navbar:
    background: primary
    search: true
    right:
      - text: "English"
        href: ../en/index.html
      - text: "Türkçe"
        href: ../tr/index.html
```      

To be able to render all of the profiles, we render three times like below.

```bash
quarto render --to html --profile def
quarto render --to html --profile en
quarto render --to html --profile tr
``` 
In the github pages, above commands is repeated using following yml.


```yml
      - name: Render Quarto Project Profile Def
        uses: quarto-dev/quarto-actions/render@v2
        env:
          QUARTO_PROFILE: def
        with:
          to: html 
```

See [github workflow yaml](https://github.com/ati-ozgur/course-database/blob/main/.github/workflows/publish-github-pages.yml) file and [working site](https://ati-ozgur.github.io/course-database/).
