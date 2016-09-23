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

Or if you want to restart a uwsgi process gracefully you could do something like this:

```
roles:
    - role: EDITD.supervisor_task
      name: webserver
      command: uwsgi --ini /path/to/you/conf
      user: ubuntu
      restart_task: no
      restart_signal: HUP
      restart_pidfile: /path/to/pid/file/defined/in/conf
```

### Removing a task

To ensure that a task is not present, you can use `state: absent`

```
  roles:
    - role: EDITD.supervisor_task
      name: webserver
      state: absent
```

## License

MIT
