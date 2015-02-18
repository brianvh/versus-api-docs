---
title: Versus API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - url_params

search: true
---

# Introduction

This website documents the RESTful V2 endpoints for the Versus Multi-Game Tournaments API.

Due to the Multi-Game nature of the Versus API, all endpoints require identifying the Game, via its `:game_uuid`, in the URL path. In addition, all endpoints except the one for requesting a new session token (detailed below), require the currently active `token` as a parameter.

The `token` parameter can be provided as either a URL query parameter, for `GET` endpoints, or as one of the request body parameters for `POST` and `PUT` endpoints.
