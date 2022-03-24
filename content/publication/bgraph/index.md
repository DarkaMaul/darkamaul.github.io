---
title: " Exploitation du graphe de dépendance d'AOSP à des fins de sécurité "
authors:
- alexis
- Robin David
- Guénael Renault
date: "2021-06-01T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2020-03-01T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: "*Symposium sur la sécurité des technologies de l'information*"
publication_short: "*SSTIC'21*"

abstract: Contrairement aux GNU autotools, le système de build Soong, développé par Google, se prête plus favorablement à l'analyse de l'interdépendance des cibles de compilations. Utilisées à des fins de sécurité, ces relations de dépendances permettent d'évaluer la propagation d'une vulnérabilités et les composants affectés à travers un graphe, appelé graphe de dépendance unifié. Appliqué à l'Android Open Source Project, la construction et l'exploitation de ce graphe permettent de savoir quelles sont les cibles issues d'un fichier. Ces travaux présentent les problématiques techniques liées au calcul de ce graphe et le potentiel offert par son exploitation. 

# Summary. An optional shortened abstract.
# summary: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis posuere tellus ac convallis placerat. Proin tincidunt magna sed ex sollicitudin condimentum.

# tags:
# - Source Themes
featured: false

links:
url_pdf: https://hal.inria.fr/hal-03329791/document
url_code: 'https://github.com/quarkslab/bgraph'
# url_dataset: '#'
# url_poster: '#'
# url_project: ''
url_slides: 'https://www.sstic.org/media/SSTIC2021/SSTIC-actes/bgraph/SSTIC2021-Slides-bgraph-challande_renault_david.pdf'
# url_source: '#'
url_video: 'https://static.sstic.org/videos2021/1080p/bgraph.mp4'

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
projects:
- bgraph

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
slides: ""
---
