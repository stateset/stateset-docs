---
description: Stateset leverages OpenAI's state-of-the-art GPT3 model.
---

# Stateset AI

Stateset powers chat, document generation, code execution and many other task's leveraging the most powerful language model in the world.&#x20;

Stateset's flagship Shopify app, Stateset ReSponse, is a very simple App that Responds to Gorgias Tickets using AI.

Gorgias, is a helpdesk designed for e-commerce stores that provides multichannel customer service from a single app.

Download and Install, link to Gorgias through the Admin Settings.

Here are the Gorgias Test Account credentials:

1. (Your Shopify Store)
2. Gorgias Subdomain: riggsandporter
3. Gorgias Username:
4. Gorgias API Key:
5. File Id: file-rqhXxX5fGNP3iRQe5CYigzYd

If you want to upload your own File it needs to be in JSONL format. For Example:

{"text" :"RiggsAndPorter clothing is made in the United States", "metadata": "riggs and porter is america's best clothing store"} {"text" :"RiggsAndPorter is located in Telluride, Nashville, and Austin", "metadata": "riggs and porter is america's best clothing store"}

If you want to upload or edit your own JSONL file here a gist of the JSONL for RiggsAndPorter:

[https://gist.github.com/domsteil/fda98a7bdd693f6e29d9b17f66bfa085](https://gist.github.com/domsteil/fda98a7bdd693f6e29d9b17f66bfa085)

Save the File in JSONL (riggsandporter.jsonl) format and upload it from the Admin Screen.

Once you have entered in the details click the Verify & Save Settings Button

Go back to the main page of the App by Clicking the Tickets Tab.

\*\*\*\*\*\*\*\*\*\*\*\*\* MAIN FUNCTIONALITY OF THE APP \*\*\*\*\*\*\*\*\*\*\*\*\*

1. Click into a ticket a by clicking Response.
2. Generate a Response.
3. Update the ticket.
4. In your Gorgias Platform, the Ticket is Updated.

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

### Stateset ReSponse AI APIs

**Chat**

{% swagger method="post" path="" baseUrl="https://stateset.io/api/ai/chat" summary="Chat" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="body" required="true" %}

{% endswagger-parameter %}
{% endswagger %}

**Code**

{% swagger method="post" path="" baseUrl="https://stateset.io/api/ai/code" summary="Code" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="body" required="true" %}

{% endswagger-parameter %}
{% endswagger %}

**Answer**

{% swagger method="post" path="" baseUrl="https://stateset.io/api/ai/answer" summary="Answer" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="body" required="true" %}

{% endswagger-parameter %}
{% endswagger %}

**File Upload**

{% swagger method="post" path="" baseUrl="https://stateset.io/api/ai/upload" summary="File Upload" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="body" required="true" %}

{% endswagger-parameter %}
{% endswagger %}

**Edit**

{% swagger method="post" path="" baseUrl="https://stateset.io/api/ai/edit" summary="Edit" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="body" required="true" %}

{% endswagger-parameter %}
{% endswagger %}

**Generate Contract**

{% swagger method="post" path="" baseUrl="https://stateset.io/api/ai/generate-contract" summary="Generate Contract" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="body" required="true" %}

{% endswagger-parameter %}
{% endswagger %}

**Generate Email**

{% swagger method="post" path="" baseUrl="https://stateset.io/api/ai/generate-email" summary="Generate Email" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="body" required="true" %}

{% endswagger-parameter %}
{% endswagger %}

**Translate**

{% swagger method="post" path="" baseUrl="https://stateset.io/api/ai/translate" summary="Translate" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="body" required="true" %}

{% endswagger-parameter %}
{% endswagger %}
