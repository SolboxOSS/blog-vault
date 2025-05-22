---
sidebar_position: 1
id: <% tp.file.title.toLowerCase().replace(/[^\w\s-]/g, '-').replace(/-+/g, '-').replace(/^-|-$/g, '').replace(/\s+/g, '-') %>
title: <% tp.file.title %>
slug: /<% tp.file.folder(true).split('/').map(p => p.replace(/[^\w\s-]/g, '').replace(/\s+/g, '-').toLowerCase()).join('/') %>/<% tp.file.title.toLowerCase().replace(/[^\w\s-]/g, '-').replace(/-+/g, '-').replace(/^-|-$/g, '').replace(/\s+/g, '-') %>
description: This is sample Post for writer
keywords:
  - rcloneview
  - howto
  - cloud
  - sync
  - rclone
tags:
  - RcloneView
  - howto
  - Cloud
  - Sync
date: <% tp.date.now("YYYY-MM-DD") %>
author: Jay
---
