# Kappa architecture hands-on

## Getting started

1. Clone the repository (already done if you're working on a lab computer).

    Clone the repository to the desktop.

    ```bash
    cd ~/Desktop
    git clone https://github.com/IBCNServices/kappa-course.git
    ```

    The repository with the problem code is now in the `kappa-course` folder in your desktop.

2. Get the latest code from the repository

    ```bash
    cd ~/Desktop/kappa-course
    git pull origin master
    # Ensure the docker container can access the files.
    chmod -R o+rwx ~/Desktop/kappa-course
    ```

3. Start the Kafka broker.

    ```bash
    docker start kafka || docker run -d -p 2181:2181 -p 9092:9092 --env ADVERTISED_HOST=0.0.0.0 --env ADVERTISED_PORT=9092 --name kafka spotify/kafka
    ```

4. Start InfluxDB

    ```bash
    docker start influxdb || docker run -d -p 8086:8086 --name influxdb influxdb
    ```

5. Start Jupyter Notebook and mount the current directory as the "work" folder inside of the container.

    Run notebook and mount current directory as `work` inside of the container.

    ```bash
    cd ~/Desktop/kappa-course
    docker start -i notebook || docker run -it --net="host" -v "$PWD":/home/jovyan/work --name notebook jupyter/pyspark-notebook
    ```

    The notebook should show output similar to the following text.

    ```txt
    [I 09:03:49.276 NotebookApp] JupyterLab extension loaded from /opt/conda/lib/python3.7/site-packages/jupyterlab
    [I 09:03:49.277 NotebookApp] JupyterLab application directory is /opt/conda/share/jupyter/lab
    [I 09:03:49.278 NotebookApp] Serving notebooks from local directory: /home/jovyan
    [I 09:03:49.278 NotebookApp] The Jupyter Notebook is running at:
    [I 09:03:49.278 NotebookApp] http://(howard or 127.0.0.1):8888/?token=TOKEN
    [I 09:03:49.278 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
    [C 09:03:49.282 NotebookApp]

        To access the notebook, open this file in a browser:
            file:///home/jovyan/.local/share/jupyter/runtime/nbserver-7-open.html
        Or copy and paste one of these URLs:
            http://(howard or 127.0.0.1):8888/?token=TOKEN
    ```

    Open the http url of the command in your browser, using the `127.0.0.1` hostname. Don't forget to remove the brackets and the other hostname from the url.

6. In the Jupyter web ui, open the `introduction` notebook in the `work` folder and follow the instructions there.

## Appendix

### Reset environment and remove databases

```bash
docker stop kafka; docker rm kafka
docker stop influxdb; docker rm influxdb
docker stop notebook; docker rm notebook
```

## Authors

This repository is created by teaching staff of the Faculty of Engineering and Architecture at Ghent University.

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.
