---
layout: default
---
<h1 class="home-title">Dylan Piwko</h1>

<p class="lead">{{ site.degree }} · {{ site.graduation }}</p>

I'm an aerospace engineering student at the University of Michigan. I design and fly high-power rockets and the flight electronics inside them. I was a concept design intern at NASA Ames Research Center, and I've worked on machine learning for air traffic with an Embry-Riddle team.

<h2 id="projects">Projects</h2>

{% include project-list.html %}

<h2 id="contact">Contact</h2>

- Email: [{{ site.email }}](mailto:{{ site.email }})
- LinkedIn: [linkedin.com/in/dylan-piwko]({{ site.linkedin }})
- Printable portfolio: [PDF]({{ site.pdf | relative_url }})
