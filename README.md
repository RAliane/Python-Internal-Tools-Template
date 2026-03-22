# PowerBI3 - Internal Tools Template

This is a template for setting up an internal Python-based tool, featuring both backend and frontend components, as well as an Nginx configuration. This project uses `FastAPI` for the backend, `Streamlit` for the frontend, and other useful Python packages.

## Project Structure

```

.
├── README.md           # Project overview
├── config
│   └── nginx.config    # Nginx configuration file
├── main.py             # Main entry point for the app
├── pyproject.toml      # Python dependencies and setup
├── run.sh              # Shell script to run the app
├── src
│   ├── backend
│   │   ├── data        # Directory containing data files
│   │   │   └── data.db # Example database file
│   │   ├── logs        # Directory for log files
│   │   │   └── logs.db # Example log file
│   │   └── main.py     # Backend main script
│   └── frontend
│       └── main.py     # Frontend main script (Streamlit)
└── uv.lock             # Lock file for project dependencies

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
   To run the backend server, use the following command:

   ```bash
   uv run fastapi
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
