---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Building a commit-level dataset of real-world vulnerabilities"
authors: 
  - alexis
  - Robin David
  - Guénael Renault
date: 2022-04-304T17:29:27+01:00
doi: "10.1145/3508398.3511495"

# Schedule page publish date (NOT publication's date).
publishDate: 2022-03-24T17:29:27+01:00

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: "Proceedings of the Twelveth ACM Conference on Data and Application Security and Privacy"
publication_short: "*CODASPY'22*"

abstract: |
  While CVE have become a \emph{de facto} standard for publishing advisories
  on vulnerabilities, the state of current \gls{cve} databases is lackluster.
  Yet, \gls{cve} advisories are insufficient to bridge the gap with the
  vulnerability artifacts in the impacted program. Therefore, the community is
  lacking a public real-world vulnerabilities dataset providing such
  association.
  
  In this paper, we present a method restoring this missing link by analyzing
  the vulnerabilities from the \gls{aosp}, an aggregate of more than 1,800
  projects. It is the perfect target for building a representative dataset of
  vulnerabilities, as it covers the full spectrum that may be encountered in a
  modern system where a variety of low-level and higher-level components
  interact. More specifically, our main contribution is a dataset of more than
  1,900 vulnerabilities, associating generic metadata (e.g.~vulnerability type,
  impact level) with their respective patches at the commit granularity
  (e.g.~fix commit-id, affected files, source code language).
  
  Finally, we also augment this dataset by providing precompiled binaries for a
  subset of the vulnerabilities. These binaries open various data usage, both
  for binary only analysis and at the interface between source and binary. In
  addition of providing a common baseline benchmark, our dataset release
  supports the community for data-driven software security research.


# Summary. An optional shortened abstract.
summary: ""

tags: []
categories: []
featured: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_pdf:
url_code:
url_dataset: "https://github.com/quarkslab/aosp-dataset"
url_poster:
url_project:
url_slides:
url_source:
url_video:

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects: []

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
slides: ""
---
