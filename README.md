# LLM Consultant
A GPT-powered consultant on Python which use an [`openai`](https://github.com/openai/openai-python) package with the web chat widget which made on [Next.js](https://nextjs.org/).

## How to deploy

Firstly, clone the repository:
```
git clone https://github.com/roli2py/llm-consultant.git
```

Enter in the repository:
```
cd ./llm-consultant
```

Then, select the method which you want.

### Docker Compose (First method)

To deploy the project with Docker Compose, simply execute this command:
```
docker compose up -d
```

### Manually (Second method)

#### Databases

Firstly, we need the databases. One is MySQL/MariaDB and second is ChromaDB.

You must have the MySQL/MariaDB database before going further. Installing and configuring of RDB is not a part of this instruction.

Then, get the IP, port, login, password and database name.

After we got the data, we need to launch the ChromaDB server. To do this, we need to install the ChromaDB package from PyPI and start a server:
```
pip install chromadb
chroma run
```

The databases is started and now we can launch the project's components

#### Project's components

Firstly, we need to configure and launch API. To configure, we must edit `settings.toml` of the `data` folder in the root package:
```
cd ./llm-consultant-api/src/llm_consultant_api/data
vim settings.toml
```

After editing, return to the root of the package and start API:
```
cd ..
python3 main.py
```

Leave the terminal and start a new one.

Secondly, we need to launch the widget. To do this, we must go to the `llm-consultant-widget` folder and start the server with `npm`:
```
cd ./llm-consultant-widget
npm i
npm run build
npm run start
```

Thirdly, we need to configure `nginx`. You need a installed and configured `nginx` before going further. Installing and configuring of `nginx` is not a part of the instruction.

Then, replace the env vars in the templates with TODO, edit the config files and copy them to the config folder. For example, if your config folders is the `sites-available` and `sites-enabled` then TODO, edit the config files, copy them into `sites-available` and create the softlinks in `sites-enabled` to the config files:
```
TODO
cd ./proxy/templates
vim ./api.conf
vim ./widget.conf
cp * /etc/nginx/sites-available
ln -s /etc/nginx/sites-available/api.conf /etc/nginx/sites-enabled/api.conf
ln -s /etc/nginx/sites-available/widget.conf /etc/nginx/sites-enabled/widget.conf
```

Restart `nginx`:
```
nginx -s reload
```

If you need a support of HTTPS, then edit and execute the `init-letsencrypt.sh` script:
```
vim ./init-letsencrypt.sh
./init-letsencrypt.sh
```

The project is started!