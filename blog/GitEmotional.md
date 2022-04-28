---
layout: default
title: GitEmotional
permalink: /GitEmotional/
---

In Winter 2019, I decided to participate in HackED 2019 at the University of Alberta, making this my first ever Hackathon. I didn't know much of what to expect going in, but I showed up and stumbled across some people and I knew, joining their team.

The team:

* [Frederic Sauve-Hoover](https://github.com/rsauvehoove)
* [Kevin de Haan](https://github.com/kdehaan)
* [Logan Yue](https://github.com/LoganYue)
* [Boris Fleysher](https://github.com/Struckdown)

We created an online app that can be run on any GitHub repository to return a line graph over time of the repository's "Sentimental" state. Using commit messages, it would evaluate the sentimental change at each point, and then create a line graph. We pulled data from Github using Github's API. We then used a sentiment analysis NLP tool for the actual analysis. For each commit meassage, we would analyze the commit message and give it a positive or negative score, with some words and modifiers having a stronger value than others. We would then add this to a cumulative sum, using that as the y value and the date as the x value. We then used JavaScript charts to build the graph itself.

Considering I had no background in building web apps or anything related to React or JavaScript, this was a bit tougher for me. I ended up focusing on the graphs and getting the charts to work, as well as just general bug fixes. We used [chartsjs](https://www.chartjs.org/), so I went through the tutorials as quickly as I could. Given my familiarity with other programming languages, I was able to work with javascript well enough to output the graphs within the timeboxed event while the other team members worked on the various other steps, such as building the react online app to actually display the app online and getting the Git data using their API.

[Repository Link to our work](https://github.com/rsauvehoover/git-emotional)

Unfortunately, I don't think our app works anymore, and the only screenshot is posted here on [Devpost](https://devpost.com/software/git-emotional)

