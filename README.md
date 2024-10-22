# Gorunn Project Files Repository

This repository holds example project manifests for Gorunn, detailing the supported servers and their versions, as well as the structure of project manifests and env vars.

## Supported Servers and Versions

### PHP
- **Version:** `8.0 | 8.1 | 8.2 | 8.3`

### Node
- **Version:** `16 | 18 | 20`

### Python
- **Version:** `3.6 | 3.8 | 3.9 | 3.10 | 3.11 | 3.12`

## File Structure

Below is an example of a project file for a React project:

```yaml
git_repo: git@github.com:parapidcom/gorunn-example-react
type: node
version: "20"
endpoint: myreact.local.gorunn.io
env_vars: true
start_command: npm run dev
listen_port: 3000
build_commands:
  - npm i
```

### Breakdown of the parameters:
- **git_repo** -> URL to the project's git repository
- **type** -> php|node|python
- **version** -> one of the supported versions of the platform
- **endpoint** -> if provided, cli will create vhost on proxy ingress. endpoint must be in the form of `%s.local.gorunn.io`.
- **env_vars** -> true|false - will project have also environment variables | secrets. If true, cli will load it from `env/myreact.env` (if it does not exist, it will create new file from template)
- **start_command** -> This is command we start the server with
- **listen_port** -> port on which your local server will listen, so that proxy can forward to it as upstream
- **build commands** -> list all commands that are neccessary for project bootstrap. These are called with `gorunn build --app app_name` command.


⚠️ **Warning**: Filename must match the name of the project !


## Env files

Each project that utilizes `env_vars` can have its matchin env file in `env/` dir. If env file for project does not exist, and project has `env_vars` set to `true`, `gorunn parse` will generate new unencrypted file in `env/` dir and then it will encrypt it with `encryption_key` that was generated or provided during `gorunn init` process.


### Example
Lets say we want to have `myreact.env` with contents:

```bash
MYSQL_HOST=gorunn-mysql
DB_USERNAME=gorunn
DB_PASSWORD=password
```

1. save this in `env/myreact.env`
2. encrypt it with
```bash
gorunn projects env --encrypt --app myreact
```

This will create new file inside `env/` dir called `myreact.env.encrypted`. You can now include this file alongside project manifests and commit.
This way you can colaborate with other team members without sharing secrets through unsafe channels, just share **encryption key** safely.

⚠️ **Warning**: Do not push plain `env` files to the repo, always ignore them in `.gitignore`!
