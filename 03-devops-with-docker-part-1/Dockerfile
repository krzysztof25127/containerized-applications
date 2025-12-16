# FROM ubuntu:22.04
# WORKDIR /mydir
# RUN apt-get update && apt-get install -y curl python3
# RUN curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o /usr/local/bin/yt-dlp
# RUN chmod a+x /usr/local/bin/yt-dlp
# ENTRYPOINT ["/usr/local/bin/yt-dlp"]
# # define a default argument
# CMD ["https://www.youtube.com/watch?v=Aa55RKWZxxI"]


# FROM ubuntu:22.04
# WORKDIR /usr/src/app

# COPY script.sh .

# RUN apt-get update
# RUN apt-get -y install curl
# RUN chmod +x script.sh
# ENTRYPOINT ["./script.sh"]

# FROM devopsdockeruh/simple-web-service:alpine

# CMD ["server"]

FROM ruby:3.1.0

EXPOSE 3000

WORKDIR /usr/src/app

RUN gem install bundler:2.3.3

COPY Gemfile* ./

RUN bundle install

COPY . .

RUN rails db:migrate RAILS_ENV=production

RUN rake assets:precompile

CMD ["rails", "s", "-e", "production"]