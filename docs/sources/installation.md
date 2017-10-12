## Installation (Website)

Here are some requirements and guides to contributing to the Girl Develop It website code base. Be sure to review this when trying to install a local development environment! Be sure to reach out to us at [website@girldevelopit.com](mailto:website@girldevelopit.com) with questions.

There are two ways to install the website on your local machine. We reccomend you use our Vagrant environment. This is a pre-packaged, configured development environment that includes a virtual machine. These instructions will work on Windows, Mac, or Linux machines.

---

### How to Vagrant

<!-- To set up the Vagrant environment locally:

1. Install VirtualBox
2. Install Vagrant
3. clone the git repository
4. `$ vagrant up`
5. `$ vagrant ssh`
6. `$ cd /opt/gdi/development`
7. `$ bundle install`
8. `$ rake db:create db:migrate db:seed`
9. `$ bin/rails s`
10. Point your browser to `localhost:3000`
11. DEVELOP IT! \o/ -->

#### 0. Install Git (Windows only)
Git is a cross-platform tool that helps users collaborate on code projects. We use Git, combined with the site GitHub, to manage our website. Windows users will need to install Git on their machines. You can the latest version from [Git for Windows](https://git-for-windows.github.io/)

Vagrant cannot run properly inside Powershell, so powershell-based tools like [GitHub Desktop](https://desktop.github.com/) won't work for Windows users.

#### 1. Install VirtualBox
VirtualBox is a cross-platform virtualization application (see: [the VirtualBox manual](https://www.virtualbox.org/manual/ch01.html)). That means it can install multiple virtual machines at the same time, which is great for development. You can download the latest version on [the VirtualBox website](https://www.virtualbox.org/wiki/Downloads).

If you have an older version of VirtualBox on your machine, be sure to update it. Version 5.0.12 and below won't work with this setup.

#### 2. Install Vagrant
Vagrant is a wonderful tool to help you build complete development environments. Download the latest version on [the Vagrant website](https://www.vagrantup.com/downloads.html).

#### 3. Clone the gdi-website Git repository
Clone the Git repository into your local development folder: `git@github.com:girldevelopit/gdi-website.git`

#### 4. Start Vagrant
Depending on your machine, this could take a while.

```
$ vagrant up
$ vagrant ssh
```

#### 6. Install and initialize the development environment

Run the following:

```
$ cd /opt/gdi/development
$ bundle install
$ rake db:create db:migrate db:seed
$ bin/rails s
```

Again, this could take several minutes to run.

#### 7. View website
Test your connection in a browser: `localhost:3000`

---

##Manual Installation

If you prefer not to use Vagrant, you can manually install the site on your local machine. This instructions will only work for machines running Mac OS X or above.

### Required installations
* [homebrew](http://brew.sh/), a package manager for Mac OS X.
* [rvm](http://rvm.io/), a command-line tool to manage different versions of Ruby.
* ruby 2.1.7
* PostgreSQL 9.3.+
  * Install with homebrew using `brew install postgres` and follow the brew instructions for these with `brew update` and `brew doctor`.
  * **OR**
  * Using [Postgres.app for Mac OS X](http://www.postgresql.org/download/macosx/) (recommended).

**Note:** If you are upgrading from 9.2., please see instructions below for "Upgrading PostgreSQL from 9.2."

---

### Setting up your local dev environment

- Fork this repo into your personal Github account.
- Clone _your_ copy to your desktop, then navigate to that directory.
- Next, install all required gems:

```sh
bundle install
```

- If you run into an error `-bash: bundle: command not found`, install the `bundle` gem, then try again.
```sh
gem install bundle; bundle install
```

- Next, start postgres with command-line interface OR with PostgreSQL Mac OS X GUI. Make sure it is running before proceeding to next steps.

Finally, set up the database:

```sh
rake db:create db:migrate db:seed
```

This will build your database and populate it with some test data. If you are setting up a local development environment, ignore rake migration errors for now. Optionally instead of the `rake` command, you can simply run

```sh
createdb
```

- Meetup API key is set as an environment variable. To register a [new API key](https://secure.meetup.com/meetup_api/key/).

To run locally:
```
$ export MEETUP_API_KEY=[new key]
```

Check with
```
$ echo $MEETUP_API_KEY
```

- Add another remote:  
   `git remote add upstream git@github.com:girldevelopit/gdi-new-site.git`
- Now test your local dev environment by running `rails s` and visiting http://0.0.0.0:3000. You should now see a local copy of the live website! \o/

---

### Ubuntu installation instructions
* Install RVM [Website Instructions](http://rvm.io/rvm/install)
  * Install the pgp key for rvm
  ```sh
  gpg --keyserver hkp://keys.gnupg.net --recv-keys D39DC0E3
  ```
  * Install rvm, make sure to not run this as sudo, RVM should be installed on your user
  ```sh
  curl -sSL https://get.rvm.io | bash -s stable
  ```
  * Source the RVM scripts (the output from the install command has instructions for how to set this up permanently)
  ```sh
  source ~/.rvm/scripts/rvm
  ```
* Install Ruby
```sh
rvm install 2.1.7
```
* Create a new Gemset
```sh
rvm gemset use gdi-new-site --create
```
* Install some system prereqs
```sh
sudo apt-get install build-essential libpq-dev  imagemagick libmagickwand-dev nodejs
```
* Install and Configure Postgres [Website Instructions](http://www.postgresql.org/download/linux/ubuntu/)
  * Simple install (Try first, if it fails follow complex install)
  ```sh
  sudo apt-get install postgresql-9.3
  ```
  * Complex install
  **Note:** Change precise to match the name of your ubuntu distribution (12.04 = precise, 14.04 = trusty)

    ```sh
    echo "deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main" > /etc/apt/sources.list.d/pgdg.list
    wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | \
    sudo apt-key add -
    sudo apt-get update
    sudo apt-get install postgresql-9.3
    ```
  * Configure [Source](https://stackoverflow.com/questions/11092807/installing-postgresql-on-ubuntu-for-ruby-on-rails)
  **Note:** Change <username> to your ubuntu username

    ```sh
	  sudo su postgres -c psql
	  postgres=# CREATE ROLE <username> SUPERUSER LOGIN;
      postgres=# \q
	 ```
