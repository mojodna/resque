Redis Keys
==========

Resque uses a number of Redis keys for housekeeping and task tracking. All keys
are prefixed with your configured Resque namespace (default: `resque`), e.g.
`resque:queues`.

Queues and Tasks
----------------

Queues and tasks are tracked in the following keys:

* `queues` - a Set of queue names
* `queue:<queue name>` - a List of JSON blobs describing a task

Failed tasks (and the reason for their failure):

* `failed` - a List of JSON blobs with error data

Workers
-------

Workers are tracked in the following keys:

* `workers` - a Set of worker ids, formatted as `<hostname>:<pid>:<queues>`,
  e.g. `pika.local:77277:*` for a worker running on `pika.local` and operating on
  all queues.
* `worker:<worker id>:started` - a String containing the date/time when the
  worker was started

Statistics
----------

A variety of statistics are tracked in the following keys:

* `stat:failed` - a String containing the total number of failed tasks
* `stat:processed` - a String containing the total number of tasks processed
* `stat:failed:<worker id>` - a String containing the number of failed tasks
  belonging to a particular worker
* `stat:processed:<worker id>` - a String containing the number of tasks
  processed by a particular worker

Worker-specific statics are cleared when the worker shuts down.
