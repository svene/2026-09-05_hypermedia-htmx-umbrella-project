# Instructions for AI

this file serves as working document for claude. it contains information and instructions so that the prompt on the commandline can refer to this file.
this document will be a living working document as work on this project progresses.
Claude should also maintain it's list of TODOs inside this file.

## Umbrella project's purpose
I want this project to become a place for documentation of the various variants of my hypermedia htmx applications.
The apps (variants) this umbrella docs project refers to. Some projects implement the same app in different variants, others just show a poc or hypermedia/htmx patterns:

### folders relative from the current one:
- ../../2025/2025-08-23_ssfe-patterns-jte-vc-htmx
- ../../2025/2025-08-23_ssfe-patterns-jte-htmx
- ../../2025/2025-08-23_ssfe-patterns-thymeleaf-htmx
- ../../2025/2025-12-21_ssfe-patterns-quarkus-qute-htmx
- ../../2025/2025-12-27_ssfe-patterns-hono-htmx
- ../../2025/2025-12-31-springboot-hono-poc
- ../2026-01-24_hda-dynapage-demo
- ../2026-03-07_springboot-graalvm-jsx-poc
- ../2026-03-09_hda-springboot-graalvm-jsx-demo
- ../2026-03-15_hda-quarkus-graalvm-jsx-demo

### additional notes:
- the date-prefixes of the folder names indicate when these projects were started and thus also reflect my learning experience.
- the timeline shows that I tried out various template engines to be used with a java webapplication
- 2025-08-23_ssfe-patterns-thymeleaf-htmx: only started, still needs to be implemented like the JTE variants
- - ../../2025/2025-12-27_ssfe-patterns-hono-htmx
- currently (September 2026) my preferred template engine is HONO/TS with it's html`` tagged template
- there are also folder ../2026-05-01_springboot-hono-docs and ../2026-05-02_ssfe-patterns-jte-vc-htmx-docs which I think I created to generate docs from the real code. In a later step these most likely can be extended to create code-docs for the variants.

### Open Items
- create a file History.md which includes the main differences between the variants
- create a file Variant-Comparison.md which includes the main differences between the variants. Analysis of the projects will be needed to do this.
