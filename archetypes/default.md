---
title: '{{ replace .File.ContentBaseName "-" " " | title }}'
date: {{ .Date }}
slug: '/{{ .File.ContentBaseName | urlize }}/'
description: ''
image: ''
caption: ''
categories:
tags:
---
