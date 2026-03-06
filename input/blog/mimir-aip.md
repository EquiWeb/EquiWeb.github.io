---
title: Mimir-AIP: Ontology, Data, and Agents
tags: [mimir-aip, ontology, data, agent]
template: dark
date: 2026-03-06
---

# Mimir-AIP: Ontology, Data, and Agents

Mimir-AIP is a toolkit for data aggregation, processing, and ontology-backed reasoning, available in both Python and Go. Originally the vision was to build a framework capable of ingesting data from various different sources, transforming through a series of data processing steps, and then having some set of steps to output and present the data such as visualisations etc. It was heavily inspired by [Palantir's](https://www.palantir.com/platforms/foundry/) product offering but catered more towards the needs of data analysts. Over time the project evolved to more heavily integrate with LLMs as a core component of the framework, it went from ingestion->processing->output to ingestion->processing->reasoning->output. Additionally, it became clear that Mimir needed to be a system running 24/7 to continuously ingest and process data. At the same time I was learning Go and decided a rewrite in Go would offer some advantages and allow the core architecture to be re-examined and improved. The Go version of Mimir-AIP is now the main focus of development, but the Python version is still available and serves as a reference implementation.

## Ontology: Data Representation and Aggregation
One of the key features and goals of Mimir-AIP was to allow ingestion from multiple independent data sources, and to be able to aggregate and represent that data in a unified way. To achieve this, Mimir-AIP has been heavily inspired by the Palantir approach of using an ontology to represent the symbolic relationships between different data entities. This offers a lot of advantages in terms of being able to easily query and reason about the data. Additionally the ontology allows for a lot of flexibility in terms of being able to easily ingest new sources of data and 'grow' the ontology as needed. 

## Scaling
Originally when I started working on the Go re-write I did not focus on scaling as a core requirement, but as the project evolved it became clear that in order to be able to continuously ingest and process data, Mimir-AIP needed to be designed with scalability in mind. As a result it has moved away from a single docker container running both backend and frontend, to a more distributed architecture with a single orchestrator, scalable backend workers, and a separate frontend. The workers are stateless and are created and destroyed as needed to handle the workload. Additionally for storage Mimir-AIP internally now uses an abstract storage layer, and swappable plugins which adapt that storage layers to different storage backends, this approach gives users more flexibility and choice over where and how the data is stored.

## Scope Creep: When to take a step back and re-build
When I first started working on Mimir-AIP, I had a clear vision of what I wanted to build and how I wanted to build it. However, as the project evolved and I started to integrate more features and functionality, it became clear that the original architecture was not well-suited to the new requirements. At this point I had a choice to either try and shoehorn the new features into the existing architecture, which over-time became increasingly difficult, OR to take a step back and document what the _ideal_ vision was, and then re-build the system from the ground up with the new requirements in mind.

I have now done this on two occasions, first was tht move from python framework approach to the go system, second was the move from a single docker container to a distributed architecture. Both times it was a difficult decision to make, as it meant throwing away a lot of work and starting from scratch, but in both cases it ultimately led to something that I am more happy with and proud of. It has let me add additional features and functionality that would have been difficult with the original architecture.

This is a fairly drastic approach, that would not be acceptable in the business world (although as AI adoption has exploded, I see more people embracing this approach), but ultimately this is a research project which is all about learning and experimentation, so I am not too concerned about the time lost in re-building, as long as it leads to a better end result. Ultimately, there is probably a middle ground here where when the scope creep starts to become unmanageable, identify the core components that are causing the issues, document the ideal vision for those components, and then re-build just those components rather than the entire system.

## Original Python Framework
See [Mimir-AIP Python](https://github.com/Mimir-AIP/Mimir-AIP).

## Go Rewrite
See [Mimir-AIP Go](https://github.com/Mimir-AIP/Mimir-AIP-Go).

Research covers scalable data pipelines, semantic enrichment, agent integrations.
