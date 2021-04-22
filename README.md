# rails_docker_like_evilmartians
Sample repo for rails + docker + docker-compose + dip, with respect to Evilmartians' configs

## Assumed environment

* macOS: 11.2.3（Big Sur）
* [Docker for Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac)
    * Docker: 20.10.5
    * Docker-compose: 1.28.5
    * (Add Dockerhub account)
* Rails: 6.1.3.1
* Ruby: 3.0.1
* [dip]([dip](https://github.com/bibendi/dip)): 7.0.1
* Git: 2.31.1
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

