FROM ruby:2.6-alpine

COPY . /minikube/web-redis/rubyweb
WORKDIR /app

RUN bundle install

CMD ["ruby", "app.rb"]