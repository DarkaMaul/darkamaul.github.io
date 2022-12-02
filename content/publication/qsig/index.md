---
title: "Towards Patch Detection using Binary Only Semantic Signatures"
authors:
- alexis
- Robin David
- Guénael Renault
date: "2022-11-09T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2022-11-09T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["3"]

# Publication name and optional abbreviated publication name.
publication: "*HAL*"
publication_short: "*HAL*"

abstract: "Detecting if a software is patched against a known 1-day vulnerability is crucial to assess a system exposure. Indeed, because of the patch propagation delay or discontinued support, recurrent security patches are insufficient to prevent these vulnerabilities. The Firmware Matching Problem (FMP) asks to check if a patch has been applied to a complete system. In this paper, we detail a generic strategy to solve it and implement it in QSig, an automated binary patch detection solution based on semantic signatures. To face the challenges raised by this problem, QSig automatically generates a semantic signature by extracting the difference between the vulnerable and fixed version of the binary. Built to streamline the patches' detection on filesystems, QSig uses a robust matching algorithm to scan target binaries. We demonstrate QSig versatility and our approach pertinence by conducting several experiments in different contexts: a cross-architecture matching on smartphone images (Pixel 4) to emphasize our semantic signatures, a Debian live image to highlight its efficiency, and against an hybrid solution to compare both techniques."

# Summary. An optional shortened abstract.
# summary: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis posuere tellus ac convallis placerat. Proin tincidunt magna sed ex sollicitudin condimentum.

# tags:
# - Source Themes
featured: false

links:
url_pdf: https://hal.inria.fr/hal-03845743/document
url_code: 'https://github.com/quarkslab/qsig'
# url_dataset: '#'
# url_poster: '#'
# url_project: ''
# url_slides: 'https://raw.githubusercontent.com/quarkslab/conf-presentations/master/GreHack2022/Quokka-achallande-2022.pdf'
# url_source: '#'
# url_video: 'https://static.sstic.org/videos2021/1080p/bgraph.mp4'

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
# image:
#   caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/pLCdAaMFLTE)'
#   focal_point: ""
#   preview_only: false

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
