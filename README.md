# UGAIN BDHO

## Getting started

Run kafka.

```bash
docker start kafka || docker run -p 2181:2181 -p 9092:9092 --env ADVERTISED_HOST=0.0.0.0 --env ADVERTISED_PORT=9092 --name kafka spotify/kafka
```

Run notebook and mount current directory as `work` inside of the container.

```bash
docker start notebook || docker run -it --rm --net="host" -v "$PWD":/home/jovyan/work jupyter/pyspark-notebook --name notebook
```

## Authors

This repository is created by teaching staff of the Faculty of Engineering and Architecture at Ghent University.

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.
