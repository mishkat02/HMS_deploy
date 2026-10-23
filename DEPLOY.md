# Deploy: Hospital Management System -> PythonAnywhere (free)

1. Sign up (free "Beginner" account) at https://www.pythonanywhere.com. Your username becomes <username>.pythonanywhere.com.
2. Zip this folder (WITHOUT env/ or .venv/), then on PythonAnywhere: Files tab -> upload the zip to /home/<username>/
3. Open a Bash console (Consoles tab):
       cd ~ && unzip hospital.zip -d hospital      # adjust to your zip name
       mkvirtualenv hmsenv --python=python3.12      # use the Python version you'll pick in step 4
       pip install -r ~/hospital/requirements.txt
   (If the zip created a nested folder, make sure app.py sits directly in ~/hospital/)
4. Web tab -> "Add a new web app" -> Next -> "Manual configuration" -> choose Python 3.12 -> Next.
   - Source code:  /home/<username>/hospital
   - Virtualenv:   /home/<username>/.virtualenvs/hmsenv
   - Click the WSGI configuration file link, delete everything, paste:

         import sys
         path = '/home/<username>/hospital'
         if path not in sys.path:
             sys.path.insert(0, path)
         from app import app as application

   - (Optional) Static files: URL /static/  ->  Directory /home/<username>/hospital/static
5. Click the green "Reload" button, then open https://<username>.pythonanywhere.com
6. Log in with the admin already in your database (admin123 / 1234) and change it.
7. Keep it alive: free web apps expire if unused. Log in about once a month and press the "Run until ..." extend button on the Web tab.
8. Updating later: re-upload changed files (or `git pull`), press Reload.
