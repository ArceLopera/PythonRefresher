## When initialicing
pip install mkdocs mkdocs-material
mkdocs new .

## when deploying
cd .\PythonRefresher\
mkdocs build
git commit --allow-empty -m "Trigger rebuild"
git push
mkdocs gh-deploy --force

## Run local server
mkdocs serve
>> docker run --rm -it -p 8000:8000 -v "%cd%":/docs squidfunk/mkdocs-material