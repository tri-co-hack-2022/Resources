# ⚡FastAPI 

## Introduction 

This tutorial is a quick introduction to FastAPI, which is a simple Python web framework for creating REST APIs, static HTML pages, and many other web applications. Sebastián Ramírez, the creator of FastAPI has excellent [documentation](https://fastapi.tiangolo.com/) and [gitter](https://gitter.im/tiangolo/fastapi) forum. 

FastAPI, in many respects, is an updated version of Flask. It's built with the features and capabilities of Python3 in mind, particularly type hints for data validation.  It also embraces asynchronous functions and other features of modern web design.  

In the following sections, I'll share several use cases for FastAPI.  I am particularly fond of FastAPI as a general toolkit that can be used for building simple static HTML or serving advanced machine learning models.  It's minimal and simple but capable of growing as your project evolves and becomes more complex.   

## Setup 

To get started, open your terminal. You'll need to have Python version 3.6 or later installed on your machine. See [this text](https://assets.digitalocean.com/books/python/how-to-code-in-python.pdf) if you need help installing Python and [pip](https://pip.pypa.io/en/stable/installation/).

Next, create a virtual environment for your project.
- `python -m venv venv`
- `source ./venv/bin/activate`

Enter this command to install fastAPI and several common dependencies that you may need.  
`pip install fastapi uvicorn jinja2 python-multipart aiofiles` 

Now create a `main.py` file using the terminal or your preferred code editor such as VSCode. 

```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
async def root():
    return {"message": "Hello World"}
```

Save the file and now you can run the application with:  
`uvicorn main:app --reload`

In your browser, enter `localhost:8000` and you should see the response from your application. 

## REST APIs

Together with HTML, APIs form the "backbone" of the modern worldwide web.  APIs provide an easy way to request and send data between machines over a network.

Perhaps the simplest way to view an API request is to use the [`curl` command](https://www.keycdn.com/support/popular-curl-examples). Here's an example request that searches the the Library of Congress catalog for `Pinnipeds` (otherwise known as seals 🦭).
  
Enter `curl https://www.loc.gov/search/?q=Pinnipeds&fo=json` in the terminal or just paste the address into your browser.  You'll get machine-readable results for the search. 

A common way to handle requests in Python is the requests library.  

```python 
import requests 

data = requests.get('https://www.loc.gov/search/?q=pinnipeds&fo=json').json()
for result in data['results']:
    print(result['title'])
```

## Creating APIs

The first and best use of FastAPI is to create your API. You may have your own data that you want to serve to the web or perhaps a machine learning model.  You could receive text as input, for example, and return a json object with all of the named entities contained in the text.  

Here's what the code for such an application could look like.

```python
import spacy
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
async def process_text(text: str): 
    nlp = spacy.load("en_core_web_sm")
    doc = nlp(text)
    return [(ent.text, ent.label_) for ent in doc.ents] 
```

If you enter `http://localhost:8000/?text=I%20love%20Berlin` in your browser, you'll get back `Berlin GPE` meaning it found a place named Berlin in the text. 


## Static sites 

In addition to serving data, FastAPI can render HTML and serve it to the web.  I frequently use FastAPI to programmatically build static web pages from data.   

**seasons.csv**
```csv
page,content
summer, This is a page for summer.
winter, It's snowing!
spring, Where have all the flowers gone? Here they are! 
fall, All the leaves are brown and the sky is gray.
```

```python
import csv
from pathlib import Path
from fastapi import FastAPI, Request
from fastapi.responses import HTMLResponse


app = FastAPI()

# Load our season data
reader = csv.DictReader(open('seasons.csv'))
data = [d for d in reader]

@app.get("/")
def root(response_class=HTMLResponse): 
    links = """"""
    for page in data:
        links += f" <li><a href='./{page['page']}'>{page['page']}</a></li>"
    html_content = f"""
     <html>
        <head>
            <title>Seasons</title>
        </head>
        <body>
            <h1> These are my thoughts on the seasons</h1>
            <ul>
            {links}
            </ul>
        </body>
    </html>"""
    return HTMLResponse(content=html_content, status_code=200)


@app.get("/{season}")
def seasons(season: str, response_class=HTMLResponse): 
    page_data = [d for d in data if d['page'] == season][0]
    html_content = f"""
     <html>
        <head>
            <title>{ page_data['page'] }</title>
        </head>
        <body>
            <h4>{ page_data['page'] }</h4>
            <p>{ page_data['content'] }</p>
        </body>
    </html>
    """
    return HTMLResponse(content=html_content, status_code=200)


def build():
    #create the index page 
    page = root(Request)
    (Path.cwd() / 'site' / 'index.html').write_bytes(page.body)

    for season in data: 
        page = seasons(Request, season['page'])
        (Path.cwd() / 'site ' /f"{season['page']}.html").write_bytes(page.body)
build()
```

In the `site` folder, I'd now have all the files I'd need.  For an example of this approach in production see: https://github.com/HCDigitalScholarship/migration-encounters

> Note that it's much easier to use an HTML templating engine such as [Jinja](https://jinja.palletsprojects.com/en/3.0.x/) rather than the pure-Python example above.  

Static sites are easily deployed with services such as [GitHub Pages](https://pages.github.com/), [Netlify](https://www.netlify.com/) or [Fleek](https://fleek.co/). 

## Dynamic Web Applications 

The same approach used above can be used with an active server and running application.  
Here's a template that you can use to deploy a FastAPI application to Heroku: https://github.com/apjanco/fastapi_template
Here's an example project: https://github.com/HCDigitalScholarship/FastBridge


