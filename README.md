# ansible-supervisor_task

A role for creating supervisor tasks.


## Actions

- Ensures that supervisor is installed (using `apt`)
- Creates a task in the supervisor conf directory.


## Usage:

```
  roles:
    - role: EDITD.supervisor_task
      name: webserver
      command: python -m SimpleHTTPServer
      directory: /opt/web
      user: ubuntu
      stopsignal: HUP
```

### Restarting tasks:

By default, the role will restart the task on each run, which you could skip like so:

```
  roles:
    - role: EDITD.supervisor_task
      name: webserver
      command: python -m SimpleHTTPServer
      directory: /opt/web
      user: ubuntu
      restart_task: no
```

### Signaling tasks:

Starting with supervisor 3.2.0, there is also the ability to send signals to tasks.
A good example where this might come in handy is signaling web servers, e.g. uwsgi,
to gracefully restart their workers. An example of how to do that would be:

```
  roles:
    - role: EDITD.supervisor_task
      name: webserver
      command: uwsgi
      directory: /opt/web
      user: ubuntu
      restart_task: no
      signal_task: HUP
```

## License

MIT
