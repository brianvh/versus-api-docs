---
title: Versus API Reference

toc_footers:
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - url_params
  - session

search: true
---

# Introduction

> The `token` parameter can be provided as either a URL query parameter, for `GET` endpoints, or as part of the JSON request body for `POST` and `PUT` endpoints.

This website documents the RESTful V2 endpoints for the Versus Multi-Game Tournaments API.

Due to the Multi-Game nature of the Versus API, all endpoints require identifying the Game, via its `:game_uuid`, in the URL path. In addition, all endpoints except _Request New Session Seed_, require the currently active `token` as a parameter.
