---
layout: distill
title: Getting Started - The OpenAI Python Library
description: an example of a distill-style blog post and main elements
tags: distill formatting
giscus_comments: true
date: 2024-02-15
featured: true

toc:
  - name: OpenAI Access and API Key
    # if a section has subsections, you can add them as follows:
    # subsections:
    #   - name: Example Child Subsection 1
    #   - name: Example Child Subsection 2
  - name: Citations
  - name: Footnotes
  - name: Code Blocks
  - name: Interactive Plots
  - name: Layouts
  - name: Other Typography?

# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
_styles: >
  .fake-img {
    background: #bbb;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 12px;
  }
  .fake-img p {
    font-family: monospace;
    color: white;
    text-align: left;
    margin: 12px 0;
    text-align: center;
    font-size: 16px;
  }
---

In this blog, we’ll focus on how to use API keys in a small **Python script**, and we’ll perform our first test with this OpenAI API.
OpenAI provides GPT-4 and ChatGPT as a service. This means users **cannot have direct access to the models code and cannot run the models on their own servers**.
However, OpenAI manages the deployment and running of its models, and users can call these models as long as they have an account and a **secret key**.

Before completing the following steps, make sure you are logged in on the [OpenAI](https://openai.com/) web page.

## OpenAI Access and API Key

OpenAI requires you to have an API key to use its services. This key has two purposes:
- It gives you the right to call the API methods.
- It links your API calls to your account for billing purposes.
You must have this key in order to call the OpenAI services from your application.
To obtain the key, navigate to the OpenAI platform page. In the upper-right corner,
click your account name and then “View API keys,” as shown below image.

When you are on the “API keys” page, click "Create new secret key" and make a copy of your key. This key is a long string of characters starting with ***sk-***.

> Keep this key safe and secure because it is directly linked to your account, and a stolen key could result in unwanted costs.

Once you have your key, the best practice is to export it as an environment variable. This will allow your application to access the key without writing it directly in your code. Here is how to do that.

**For Linux or Mac:**

{% highlight bash %}
# set environment variable OPENAI_API_KEY for current session
export OPENAI_API_KEY=sk-(...)
# check that environment variable was set
echo $OPENAI_API_KEY
{% endhighlight %}

**For Windows:**

{% highlight bash %}
# set environment variable OPENAI_API_KEY for current session
set OPENAI_API_KEY=sk-(...)
# check that environment variable was set
echo %OPENAI_API_KEY%
{% endhighlight %}

The preceding code snippets will set an environment variable and make your key available to other processes that are launched from the same shell session. For Linux
systems, it is also possible to add this code directly to your ``.bashrc file`. This will allow access to your environment variable in all your shell sessions. Of course, do not
include these command lines in the code you push to a public repository

Now that you have your key, it’s time to write your first “Hello World” program with the OpenAI API.

## "Hello World" OpenAI API

This section shows the first lines of code with the OpenAI Python library. We will start with a classic “Hello World” example to understand how OpenAI provides its
services.

Install the Python library with *pip*:

{% highlight bash %}
pip install --upgrade openai
{% endhighlight %}

Next, access the OpenAI API in Python

{% highlight python %}

import openai
# Call the openai ChatCompletion endpoint
response = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[{"role": "user", "content": "Hello World!"}],
)
# Extract the response
print(response["choices"][0]["message"]["content"])

{% endhighlight %}