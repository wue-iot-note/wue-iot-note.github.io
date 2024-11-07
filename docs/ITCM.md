---
title: ITCM (Interoperable Train Control Messaging)
layout: default
---

# ITCM (Interoperable Train Control Messaging)
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Basic Message Packet Structure

```markdown
---------------------------------------------------------------
L2/L1   | IP     | TCP    | Class D | EMP    | CTC     | EMP
Headers | Header | Header | Header  | Header | Message | Footer
```