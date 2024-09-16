---
layout: post
title:  Dockerfile naming convention
date:   2024-09-16 00:00:00 +0000
categories: dockerfile
---

## Dockerfile naming convention

**Question**:

When naming a dockerfile for a bundle image (or any other purpose) should the file be named as `Dockerfile.bundle` or `bundle.Dockerfile`?

**Sources**:

- https://olm.operatorframework.io/docs/tasks/creating-operator-bundle/#bundle-images gives many examples for `bundle.Dockerfile`.
- https://stackoverflow.com/questions/26077543/how-to-name-dockerfiles#comment124463873_63995752 has a good point about `.Dockerfile` as an extension.
- From https://docs.docker.com/build/concepts/dockerfile/#filename:
  ```
  Some projects may need distinct Dockerfiles for specific purposes. A common convention is to name these <something>.Dockerfile
  ```

**Conclusion**:

`bundle.Dockerfile`
