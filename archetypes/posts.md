---
title: '{{ replace .File.ContentBaseName "-" " " | title }}'
date: {{ .Date }}
lastmod: {{ .Date }}
slug: '/{{ .File.ContentBaseName | urlize }}/'
description: ''
image: ''
caption: ''
categories: []
tags: []
draft: true
---
