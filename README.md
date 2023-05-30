# Debugging a Flask application running on Docker

Build and run a Flask application that can be debugged with vscode.

Create a `.vscode` directory with the following `launch.json`:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Python: Remote Attach",
      "type": "python",
      "request": "attach",
      "connect": {
        "host": "localhost",
        "port": 5678
      },
      "pathMappings": [
        {
          "localRoot": "${workspaceFolder}",
          "remoteRoot": "."
        }
      ],
      "justMyCode": true
    }
  ]
}
```

```bash
docker build --target debug -t flask-random-number:debug .
```

```bash
docker run -p 5000:5000 -p 5678:5678 flask-random-number:debug
```

Visit <http://127.0.0.1:5000/"int"> for example <http://127.0.0.1:5000/5>

Now it is possible to set a `Breakpoint` in the desired line to start debugging with `F5`.

## Production

```bash
docker build --target prod -t flask-random-number:prod .
```

```bash
docker run -p 5000:5000 flask-random-number:prod
```
