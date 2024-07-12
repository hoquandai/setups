FROM ruby:3.3.4-bullseye

RUN apt-get update -qq && \
    apt-get install --no-install-recommends -y build-essential npm

RUN gem install rails -v 7.1.3.4

WORKDIR /main

VOLUME /main

CMD ["bundle", "exec", "bash"]
