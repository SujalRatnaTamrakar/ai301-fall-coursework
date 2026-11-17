This term, through my AI 301 course at Georgia State University, I contributed to open source by opening a pull request in Open edX's assessment engine that removes a retired feature flag and its demo code. The work was chosen by a checker tool I built, which grades open-source issues against a rubric I wrote.

The tool's first picks taught me the real lesson. It approved two issues that already had pull requests implementing them, because my notes said "no linked PR" and I had never actually searched for one. I fixed the checker so that claim has to be verified with a real search, released the claim I had placed, and re-screened every candidate. The stricter checker rejected four more bad picks before it found the Open edX issue, where a maintainer had confirmed the code was dead and ready to remove.

My pull request is open as a draft and still needs my signed contributor agreement before the project can merge it. What I take into my job search is a habit worth more than the code: verify the evidence instead of asserting it, and let a failed first version make the second one better.

https://github.com/openedx/edx-ora2/pull/2483
#OpenSource #SoftwareEngineering #Python
