# rails_docker_like_evilmartians
Sample repo for rails + docker + docker-compose + dip, with respect to Evilmartians' configs

## Assumed environment

* macOS: 10.15.1（Catalina）
* [Docker for Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac)
    * Docker: 19.03.4
    * Docker-compose: 1.24.1
    * (Add Dockerhub account)
* Rails: 6.0.1
* Ruby: 2.6.5
* Git: 2.24.0
    * Use [git-flow](https://danielkummer.github.io/git-flow-cheatsheet/index.ja_JP.html)

## Setup

1. Perform `git clone` to clone the repository.
2. Rename `yourapp_docker` in docker-compose.yml to your project name.
3. `docker-compose build` to build
4. `dip sh` to login the container.
  1. Perform `rails new .` with your preferential options.
  2. If needed, perform `bundle lock --add-platform x86-mingw32 x86-mswin32 x64-mingw32 java` to supress the warning.
  3. `rm -rf vendor` to remove vendor/ directory.
  4. `exit` to logoff from the container.
5. `git checkin` to commit.
6. `dip provision` to setup database connections and envs.
7. `git checkin` to commit the updated schema.
8. `dip minitest` to perfom the initial test.
9. add `config.hosts << "localhost"` and `config.web_console.whitelisted_ips = '0.0.0.0/0'` to config/environments/development.rb
10. `git checkin` to commit the change.
11. `dip rails s` to start Rails.
12. Open `http://localhost:3000/` on your browser to show the welcome page.

