#  Python Web Proxy

This is a simple Python-based web proxy server that handles client requests and fetches content from the web. It demonstrates the use of socket programming and multi-threading.

## How to Run

```bash
python proxy.py
##index.html
<!DOCTYPE html>
<html>
<head>
    <title>Simple Web Proxy</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
</head>
<body>
    <h1>🔍 Simple Web Proxy</h1>
    <form action="/fetch" method="get">
        <input type="url" name="url" placeholder="Enter a website URL" required>
        <input type="submit" value="Fetch">
    </form>

    {% if content %}
    <hr>
    <div class="output">
        {{ content | safe }}
    </div>
    {% endif %}
</body>
</html>

## style.css
body {
    font-family: Arial, sans-serif;
    margin: 40px;
    background: #183543;
}
h1 {
    color: #d2cfcf;
}
form input[type=url] {
    width: 70%;
    padding: 10px;
    margin-right: 10px;
}
form input[type=submit] {
    padding: 10px 20px;
}
.output {
    background: #74a1f6;
    padding: 20px;
    border: 1px solid #ccc;
    max-height: 600px;
    overflow-y: scroll;
}

##python
from flask import Flask, request, render_template
import requests

app = Flask(__name__)

@app.route('/')
def index():
    return render_template("index.html", content=None)

@app.route('/fetch')
def fetch():
    url = request.args.get('url')
    try:
        headers = {"User-Agent": "Mozilla/5.0"}
        response = requests.get(url, headers=headers, timeout=5)
        content = response.text
    except Exception as e:
        content = f"<p style='color:red;'>Error fetching URL: {e}</p>"
    return render_template("index.html", content=content)

if __name__ == '__main__':
    app.run(debug=True)

Output
<img width="1787" height="745" alt="image" src="https://github.com/user-attachments/assets/73c43386-0dd0-4fab-b623-8663311130ef" />
<img width="2229" height="887" alt="image" src="https://github.com/user-attachments/assets/bf9c6e46-108e-41da-8cbc-75af4a0bebf4" />


