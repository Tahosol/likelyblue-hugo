---
title: "{{ replace .Name "-" " " | title }}"
description: "{{ .Name }}"
keywords: "{{replace .Name "-" ","}}"

date: {{ .Date }}
lastmod: {{ .Lastmod }}

math: false
mermaid: false

categories:
  -
tags:
  -
  -
---
{{ replace .Name "-" " " | title }}
<!--more-->
