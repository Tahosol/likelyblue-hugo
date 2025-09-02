---
title: "{{ replace .Name "-" " " | title }}"
description: "{{ .Name }}"
keywords: "{{replace .Name "-" ","}}"
cover: ../../images/{{ .Name }}/

date: {{ .Date }}
lastmod: {{ .Date }}

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
![](../../images/{{ .Name }}/)
