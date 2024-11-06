---
title: Home
---

# DS219 -- HOMEWORK ASSIGNMENT

<div class="toc" markdown="1">
## Contents:

{% for lesson in site.pages %}
{% if lesson.nav == true %}- [{{ lesson.title }}]({{ lesson.url | relative_url }}){% endif %}
{% endfor %}
</div>

![DALL·E 2024-08-12 16 56 31 - A vibrant and engaging image for a 'LLM Workshop 101'  The scene shows a classroom or a workshop setting with diverse people engaging with technology](https://github.com/user-attachments/assets/4a53e73e-54c5-44f0-82ba-630f3e7a5351)


Are you curious to learn about Large Language Models (LLMs), but unsure how and where to begin? This workshop is designed with specifically you in mind. LLMs have emerged as powerful tools in natural language processing, yet their implementation poses challenges, particularly in managing computational resources effectively.

During this workshop, we will delve into the fundamentals of LLMs and guide you in selecting the appropriate open source models for your requirements. We will discuss the concept of self-hosted LLMs and introduce containerization technologies such as Kubernetes, Docker, and Podman. Through illustrative use-cases like RAG application, text generation or speech recognition, you will learn how to set up LLMs locally on your laptop and build container images for the models using Podman. We will also be exploring model serving and inference methods, including interaction with the model via a simple UI application. Moreover, the workshop will cover model evaluation techniques and introduce various metrics that can be utilized to effectively measure the performance and quality of model outputs.

Attendees will gain practical knowledge and skills to effectively harness the capabilities of LLMs in real-world applications. They will understand the challenges associated with managing computational resources and learn how to overcome them. By the end of the workshop, participants will be equipped with the tools to set up and deploy LLMs, evaluate model performance, and implement them in various natural language processing tasks.
 
> built using [Jekyll](https://jekyllrb.com/) and [GitHub Pages](https://pages.github.com/)
>
> images and content: cc-by-sa <a href="https://github.com/hemajv"></a> (get [source code]({{ site.repo }})).
>
> <a href="http://creativecommons.org/licenses/by-sa/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" alt="Creative Commons License" /></a>
