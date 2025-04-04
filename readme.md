# /htop Viewer – Flask App Hosted on GitHub Codespace

This project hosts a simple Flask web application that exposes a `/htop` endpoint, showing:

-  Your Full Name  
-  System Username  
-  Server Time in IST  
-  Live `top` command output (20 lines)

---

##  How to Run in Your Own Codespace

1. Fork this repository to your GitHub account.
2. Open it in a GitHub Codespace.
3. Run the Flask app using:
   ```bash
   python app.py

##  Developer Info

- **Name:** Krishnan Kaushik  
- **Environment:** GitHub Codespaces  
- **Language:** Python (Flask Framework)  
- **Port:** 5000 (make sure it's public in your Codespace settings)

---

##  Source Code

```python
from flask import Flask
import getpass
import subprocess
from datetime import datetime
import pytz

app = Flask(__name__)

@app.route('/htop')
def htop():
    flname = "Krishnan Kaushik"  
    user_name = getpass.getuser() 
    ist = datetime.now(pytz.timezone('Asia/Kolkata')).strftime('%Y-%m-%d %H:%M:%S')

    top_output = subprocess.getoutput("top -b -n 1 | head -20")

    return f"""
    <pre>
    Name: {flname}
    Username: {user_name}
    Server Time (IST): {ist}

    Top Output:
    {top_output}
    </pre>
    """

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000, debug=True)
