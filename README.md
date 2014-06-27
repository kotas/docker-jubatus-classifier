# jubatus-classfier-docker

A Dockerfile for [Jubatus](http://jubat.us/) Classifier.

## Usage

Without any arguments, it runs in stand-alone mode using PA algorithm.

```
$ docker run -d -p 9199:9199 kotas/jubatus-classifier
```

And you can access to the Jubatus RPC via TCP port `9199`.

## Customize

If you want to pass a config file (.json), name it `jubatus.json` and put it into some directory, and mount the directory by `--volume` option.

```
$ touch /path/to/config/jubatus.json
$ docker run -d --volume /path/to/config:/opt/jubatus/etc -p 9199:9199 kotas/jubatus-classifier
```

## Save and load

By default, it uses `/opt/jubatus/data` as a directory for save and load command.

You can mount this directory to persist the data.

```
$ mkdir /path/to/data/
$ docker run -d --volume /path/to/data:/opt/jubatus/data -p 9199:9199 kotas/jubatus-classifier
```

## Options

You can pass any options to docker run which are passed to jubaclassifier command.

For example, to run jubaclassifier in [cluster mode using ZooKeeper](http://jubat.us/en/tutorial_distributed.html#join-jubatus-servers-to-cluster):

```
$ docker run -d -p 9180:9199 kotas/jubatus-classifier --name=shogun --zookeeper=localhost:2181
$ docker run -d -p 9181:9199 kotas/jubatus-classifier --name=shogun --zookeeper=localhost:2181
$ docker run -d -p 9182:9199 kotas/jubatus-classifier --name=shogun --zookeeper=localhost:2181
```
