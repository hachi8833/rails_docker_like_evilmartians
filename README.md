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
* [dip]([dip](https://github.com/bibendi/dip))
* Git: 2.24.0
    * Use [git-flow](https://danielkummer.github.io/git-flow-cheatsheet/index.ja_JP.html)

## Setup

1. Perform `gem install dip` to install dip.
2. Perform `git clone` to clone the repository.
3. Rename `yourapp_docker` in docker-compose.yml to your project name.
4. `docker-compose build` to build
5. `dip sh` to login the container.
   1. Perform `rails new .` with your preferential options.
   2. If needed, perform `bundle lock --add-platform x86-mingw32 x86-mswin32 x64-mingw32 java` to supress the warning.
   3. `rm -rf vendor` to remove vendor/ directory.
   4. `exit` to logoff from the container.
6. `git checkin` to commit.
7. `dip provision` to setup database connections and envs.
8. `git checkin` to commit the updated schema.
9. `dip minitest` to perfom the initial test.
1-. add `config.hosts << "localhost"` and `config.web_console.whitelisted_ips = '0.0.0.0/0'` to config/environments/development.rb
11. `git checkin` to commit the change.
12. `dip rails s` to start Rails.
13. Open `http://localhost:3000/` on your browser to show the welcome page.

