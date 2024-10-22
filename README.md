# Gorunn Project Files Repository

This repository holds the project files for Gorunn, detailing the supported servers and their versions, as well as the structure of project files.

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
name: myreact
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
- **name** -> name of the project. Use no spaces or special characters here
- **type** -> php|node|python
- **version** -> one of the supported versions of the platform
- **endpoint** -> if defined, cli will create vhost on local proxy for it. endpoint must be in the form of %s.local.gorunn.io
- **env_vars** -> true|false - will project have also environment variables | secrets. If true, cli will load it from **~/gorunn/envs/myapp1.env** (if it does not exist, it will create new file from template)
- **start_command** -> This is command we start the server with
- **listen_port** -> port on which your local server will listen, so that proxy can forward to it as upstream
- **build commands** -> list all commands that are neccessary for project bootstrap. These are called with `gorunn build --app app_name` command.
