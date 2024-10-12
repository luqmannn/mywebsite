---
title: Why Kubernetes is so difficult

date: 2024-10-13
type: page
categories: 
    - Kubernetes
tags:
    - Kubernetes
    - Cloud technology
    - Cloud native
---

### Introduction
This year I've decided to learn some of the key important technology in the cloud native world, which is Kubernetes. To make it easy for begineer to understand, essentially it is a system or platform to deploy an application (web/mobile/serverless) using declarative configuration inside a YAML file and orchestrate an application container. An application will be deploy by spinning up pods, a most basic unit in Kubernetes that can contain a single container or multiple container.

But to understand Kubernetes, one needs to learn and understand container. In the old days, to ship and test an application, developer need to install multiple package and dependency. Let's say web application, a developer need to install PHP interpreter, frameworks, database software and some Javascript library. One developer test their application and it works on their laptop. So they share their code to their team that have the same software stack installed on their laptop but it didn't works as expected or didn't run at all.

Do you see where the problem start where the team will argue between each other "**It works on my laptop**" and the other team member will argue back "**I've installed the exact same software as you with the same settings**". Instead of wasting their time with arguments, developers can use container to package their application to other people and operations team can deploy it without having to worry about dependency or compatability issues.

### Alien concept
Even for someone like me coming from infra background, I struggle a lot to understand and wrap my head around the the new concept that I've never heard before. Things like *Deployments*, *StatefulSets*, *Service*, *ConfigMaps*, *Secret*, *Persistent Volume Claims*, *Storage Class*, *Ingress*. There's no way around it unless I need to practice with question and exercise more frequent than everyone else that already familiar with this. But it's okay and I can handle this situation. It's just that my brain have been spinning around and I've been stress about it for some time because the exam will be held on the middle next month.

Let's see if I can pass the CKA exam

### CKA exam
This is practical hands-on exam that will test your skill in managing and operating Kubernetes cluster. Based on the information from [CKA page](https://training.linuxfoundation.org/certification/certified-kubernetes-administrator-cka/):
- This exam is an **online**, **proctored**, **performance-based** test that requires **solving multiple tasks from a command line running Kubernetes**.
- Candidates have **2 hours** to complete the tasks.
- Candidates who register for the (CKA) exam will have **2 attempts** (per exam registration) to an exam simulator, provided by [Killer.sh](https://killer.sh/)
- The exam is based on **Kubernetes v1.31**
- The CKA exam environment will be aligned with the most recent K8s minor version within approximately 4 to 8 weeks of the K8s release date

Some of the material that will be useful and I need to be aware of:
- [Candidate Handbook](https://training.linuxfoundation.org/go/candidate_handbook)
- [Exam Tips](https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad)
- [Curriculum Overview](https://github.com/cncf/curriculum/blob/master/CKA_Curriculum_v1.31.pdf)
- [FAQ](https://docs.linuxfoundation.org/tc-docs/certification/faq-cka-ckad)
- [Linux Foundation Agreement](https://docs.linuxfoundation.org/tc-docs/certification/lf-cert-agreement/)
- [Verify Certification](https://training.linuxfoundation.org/certification/verify/)