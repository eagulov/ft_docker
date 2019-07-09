FROM ruby

RUN apt-get update -y \
	&& apt-get install -y \
	build-essential libpq-dev nodejs sqlite3

ONBUILD COPY app /opt/app
ONBUILD WORKDIR /opt/app
ONBUILD RUN bundle install && \
			rake db:migrate && \
			rake db:seed
