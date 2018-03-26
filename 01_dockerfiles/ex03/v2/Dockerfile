FROM debian:latest

RUN apt-get -y update && \
	apt-get -y upgrade 
RUN apt-get -y install sudo \
					   vim \
					   build-essential \
					   zlib1g-dev \
					   libyaml-dev \
					   libssl-dev \
					   libgdbm-dev \
					   libre2-dev \
					   libreadline-dev \
					   libncurses5-dev \
					   libffi-dev \
					   curl \
					   openssh-server \
					   checkinstall \
					   libxml2-dev \
					   libxslt-dev \
					   libcurl4-openssl-dev \
					   libicu-dev \
					   logrotate \
					   rsync \
					   python-docutils \
					   pkg-config \
					   cmake \
					   libkrb5-dev \
					   git \
					   nginx
RUN apt-get remove ruby1.8
RUN apt-get -y install ruby-full
RUN gem install bundler --no-ri --no-rdoc
RUN rm -rf /usr/local/go
RUN curl --remote-name --progress https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz
RUN echo '1862f4c3d3907e59b04a757cfda0ea7aa9ef39274af99a784f5be843c80c6772  go1.8.3.linux-amd64.tar.gz' | shasum -a256 -c - && \
tar -C /usr/local -xzf go1.8.3.linux-amd64.tar.gz
RUN ln -sf /usr/local/go/bin/{go,godoc,gofmt} /usr/local/bin/
RUN rm go1.8.3.linux-amd64.tar.gz
RUN curl --location https://deb.nodesource.com/setup_8.x | sudo bash -
RUN apt-get install -y nodejs
RUN curl --silent --show-error https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get -y install yarn
RUN adduser --disabled-login --gecos 'vsyveniu' git
RUN apt-get install -y postgresql postgresql-client libpq-dev postgresql-contrib
RUN -u postgres psql -d template1 -c "CREATE USER git CREATEDB;" && \
	-u postgres psql -d template1 -c "CREATE EXTENSION IF NOT EXISTS pg_trgm;" && \
 	-u postgres psql -d template1 -c "CREATE DATABASE gitlabhq_production OWNER git;" && \
	-u git -H psql -d gitlabhq_production
RUN gitlabhq_production> \q
RUN apt-get install redis-server
RUN cd /home/git
RUN -u git -H git clone https://gitlab.com/gitlab-org/gitlab-ce.git -b 10-6-stable gitlab
RUN cd /home/git/gitlab && \
	-u git -H cp config/gitlab.yml.example config/gitlab.yml && \
	-u git -H editor config/gitlab.yml && \
	-u git -H cp config/secrets.yml.example config/secrets.yml && \
	-u git -H chmod 0600 config/secrets.yml
RUN chown -R git log/ && \
	chown -R git tmp/ && \
	chmod -R u+rwX,go-w log/ \
	chmod -R u+rwX tmp/ && \
	chmod -R u+rwX tmp/pids/ && \
	chmod -R u+rwX tmp/sockets/ 
RUN -u git -H mkdir public/uploads/
RUN chmod 0700 public/uploads && \
	chmod -R u+rwX builds/ &&\
	chmod -R u+rwX shared/artifacts/ && \
	chmod -R ug+rwX shared/pages/
RUN -u git -H cp config/unicorn.rb.example config/unicorn.rb && \		
    -u git -H cp config/initializers/rack_attack.rb.example config/initializers/rack_attack.rb && \
    -u git -H git config --global core.autocrlf input && \
    -u git -H git config --global gc.auto 0 && \
    -u git -H git config --global repack.writeBitmaps true && \
    -u git -H git config --global receive.advertisePushOptions true && \
    -u git -H cp config/resque.yml.example config/resque.yml && \
    -u git -H editor config/resque.yml
RUN -u git cp config/database.yml.postgresql config/database.yml && \
 	-u git -H chmod o-rwx config/database.yml
RUN -u git -H bundle install --deployment --without development test mysql aws kerberos
RUN -u git -H bundle exec rake gitlab:shell:install REDIS_URL=unix:/var/run/redis/redis.sock RAILS_ENV=production SKIP_STORAGE_VALIDATION=true
RUN -u git -H bundle exec rake "gitlab:workhorse:install[/home/git/gitlab-workhorse]" RAILS_ENV=production
RUN -u git -H bundle exec rake gitlab:setup RAILS_ENV=productio
RUN -u git -H bundle exec rake gitlab:setup RAILS_ENV=production GITLAB_ROOT_PASSWORD=root GITLAB_ROOT_EMAIL=somefellavs@gmail.com
RUN cp lib/support/init.d/gitlab /etc/init.d/gitlab
RUN update-rc.d gitlab defaults 21
RUN -u git -H bundle exec rake "gitlab:gitaly:install[/home/git/gitaly]" RAILS_ENV=production
RUN chmod 0700 /home/git/gitlab/tmp/sockets/private && \
	chown git /home/git/gitlab/tmp/sockets/private
RUN cp lib/support/logrotate/gitlab /etc/logrotate.d/gitlab
RUN -u git -H bundle exec rake gettext:compile RAILS_ENV=production
RUN -u git -H yarn install --production --pure-lockfile && \
	-u git -H bundle exec rake gitlab:assets:compile RAILS_ENV=production NODE_ENV=production
RUN service gitlab start
RUN cp lib/support/nginx/gitlab /etc/nginx/sites-available/gitlab && \
	ln -s /etc/nginx/sites-available/gitlab /etc/nginx/sites-enabled/gitlab
RUN nginx -t && service nginx restart







