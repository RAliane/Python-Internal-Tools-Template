# PowerBI3 - Internal Tools Template

This is a template for setting up an internal Python-based tool, featuring both backend and frontend components, as well as an optional Nginx configuration. This project uses `FastAPI` for the backend, `Streamlit` for the frontend, and other useful Python packages.

## Project Structure

```
.
├── README.md
├── config
│   └── nginx.config
├── containerfile.yml
├── docker-compose.yml
├── main.py
├── pyproject.toml
├── run.sh
├── src
│   ├── backend
│   │   ├── Modules
│   │   │   ├── data
│   │   │   │   └── data.db
│   │   │   ├── logs
│   │   │   │   └── logs.db
│   │   │   ├── main
│   │   │   │   └── main.py
│   │   │   └── routes
│   │   │       └── routes.py
│   │   └── public
│   │       └── main.py
│   └── frontend
│       └── main.py
└── uv.lock
```

## Setup

### Prerequisites

Make sure you have the following installed:

* Python 3.8+
* UV (Python package manager) `pip install uv`
* Docker & Docker Compose (if using containers)
* Nginx (optional, if you plan to use the provided configuration)

---

### Install Dependencies (Local Python)

UV Package Manager will have all your dependencies preset and you just run:

```bash
uv sync
```

To add another library:

```bash
uv add requests
```

> **Note:** `uv.lock` is used for dependency management and should be updated if you modify any dependencies.

---

### Running the Application

#### Option 1: Locally (Python)

1. **Backend (FastAPI)**:

```bash
uv run fastapi dev
```

2. **Frontend (Streamlit)**:

```bash
uv run streamlit run src/frontend/main.py
```

3. **Using `run.sh`** (starts both backend & frontend):

```bash
./run.sh
```

---

#### Option 2: Using Docker

You can run the entire stack with Docker and Docker Compose.

1. **Build & start containers**:

```bash
docker-compose up --build
```

2. **Access services**:

* Backend (FastAPI): [http://localhost:8000](http://localhost:8000)
* Frontend (Streamlit): [http://localhost:8501](http://localhost:8501)
* Optional Nginx (proxy): [http://localhost](http://localhost)

3. **Stop containers**:

```bash
docker-compose down
```

> **Note:** Volumes in `docker-compose.yml` allow hot-reloading during development.

---

### Nginx Setup (Optional)

The `config/nginx.config` file is provided for setting up Nginx. Modify as needed:

```nginx
server {
    listen 80;
    server_name yourdomain.com;

    location / {
        proxy_pass http://localhost:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

---

### Editing for Your Setup

* **Main Application**: Update `main.py` in both `src/backend` and `src/frontend`.
* **Database**: Replace `data.db` and `logs.db` with your real files.
* **Dependencies**: Update `pyproject.toml` or use `uv add` as needed.

---

## Contributing

Feel free to fork this repo and make improvements. Submit pull requests if you'd like to contribute.

---

## License

This project is open-source and available under the [Apache 2.0 License](LICENSE).

---

If you want, I can also **update the project structure diagram** in the README to explicitly show backend, frontend, and container files grouped visually for clarity—it’ll look cleaner for someone browsing the repo. Do you want me to do that?
# PowerBI3 - Internal Tools Template

This is a template for setting up an internal Python-based tool, featuring both backend and frontend components, as well as an Nginx configuration. This project uses `FastAPI` for the backend, `Streamlit` for the frontend, and other useful Python packages.

## Project Structure

```

.
├── README.md
├── config
│   └── nginx.config
├── containerfile.yml
├── docker-compose.yml
├── main.py
├── pyproject.toml
├── run.sh
├── src
│   ├── backend
│   │   ├── Modules
│   │   │   ├── data
│   │   │   │   └── data.db
│   │   │   ├── logs
│   │   │   │   └── logs.db
│   │   │   ├── main
│   │   │   │   └── main.py
│   │   │   └── routes
│   │   │       └── routes.py
│   │   └── public
│   │       └── main.py
│   └── frontend
│       └── main.py
└── uv.lock

11 directories, 14 files

````

## Setup

### Prerequisites

Make sure you have the following installed:

- Python 3.8+  
- UV (Python package manager)  ```pip install uv```
- Nginx (if you plan to use the provided configuration)  

### Install Dependencies

UV Package Manager will have all your dependencies preset and you just run:

```bash
uv sync
````
and will install all your dependencies.

If you wanted to add another library, you'd run:
```
uv add requests
```
and your dependencies will be resolved automatically.

> **Note:** `uv.lock` is used for dependency management, and should be updated if you're modifying any dependencies.

### Running the Application

You can start the app using the `run.sh` script or run the backend and frontend manually.

1. **Backend (FastAPI)**:
   To run the backend server, use the following command to run your dev environement:

   ```bash
   uv run fastapi dev
   ```

2. **Frontend (Streamlit)**:
   To run the frontend with Streamlit, use the following command:

   ```bash
   uv run streamlit run src/frontend/main.py
   ```

3. **Using `run.sh`**:
   The `run.sh` script is a wrapper to start both the backend and frontend services. You can run it like this:

   ```bash
   ./run.sh
   ```

### Nginx Setup (Optional)

The `config/nginx.config` file is provided for setting up Nginx. Modify this file according to your specific setup.

> **Note:** Be sure to update the configuration if you want to use it with an Nginx reverse proxy.

```bash
# Example Nginx configuration file
# Edit this for your setup
server {
    listen 80;
    server_name yourdomain.com;

    location / {
        proxy_pass http://localhost:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

### Editing for Your Setup

* **Main Application**:
  Update `main.py` in both `src/backend` and `src/frontend` to fit your application's needs.

* **Database**:
  Replace `data.db` and `logs.db` with your actual data files.

* **Dependencies**:
  If you need to add any new Python dependencies, update the `pyproject.toml` file.

## Contributing

Feel free to fork this repo and make any improvements. Please submit pull requests if you'd like to contribute.

## License

This project is open-source and available under the [Apache 2.0 License](LICENSE).
